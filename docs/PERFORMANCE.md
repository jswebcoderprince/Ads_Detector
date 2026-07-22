# Performance

## Overview

This document describes the performance characteristics, expectations, and optimization strategies for Ads Detector, covering the CSV Processor, Scan Queue, Website Scanner, Detection Engine, Database Layer, Dashboard, and Export System. Given that the platform's core operation — browser-automation-based website scanning — is inherently resource-intensive, performance considerations are central to the system's usability at scale.

## Purpose

The purpose of this document is to:

- Define expected performance characteristics for each stage of the core workflow.
- Identify the primary performance bottlenecks in the system and how they are mitigated.
- Establish guidelines for scaling scan throughput without degrading reliability.
- Support informed decisions around concurrency, resource allocation, and database performance tuning.

## Detailed Explanation

### Performance by Workflow Stage

**CSV Upload and Validation**
- CSV parsing and validation should complete in well under a second for typical files (hundreds to low thousands of rows), since this stage involves only file parsing and lightweight validation logic, not network I/O.
- Very large CSV files (tens of thousands of rows) should be processed using streaming/chunked parsing rather than loading the entire file into memory at once.

**Domain Processing**
- Domain normalization and duplicate removal are CPU-bound, in-memory operations and should scale linearly with input size without introducing significant latency.

**Scan Queue**
- Queue population and ordering are lightweight operations; the primary performance consideration here is ensuring the queue does not become a bottleneck when large batches of domains are submitted simultaneously.

**Website Scanner**
- This is the most resource-intensive and highest-latency stage of the pipeline, since each scan involves launching or reusing a Playwright browser instance, navigating to a live website, and waiting for network activity to settle.
- Typical per-domain scan time will vary significantly based on target site responsiveness, but the system must enforce a configurable timeout (`SCANNER_TIMEOUT_SECONDS`) to bound worst-case latency per domain.
- Overall scan throughput is governed primarily by `SCANNER_MAX_CONCURRENT_SCANS`; increasing this value improves throughput but increases memory and CPU consumption proportionally.

**Detection Engine**
- Rule-based pattern matching against captured scan data is CPU-bound but fast relative to the scanning stage itself, since it operates on already-captured data rather than performing additional network requests.

**Confidence Scoring**
- Scoring computation is lightweight and should not introduce meaningful latency relative to detection.

**Database Storage**
- Because SQLite is used, write performance is generally strong for the expected single-instance, moderate-concurrency usage pattern, but write throughput can degrade under high concurrent write load due to SQLite's file-level locking behavior.

**Dashboard**
- Dashboard responsiveness at scale depends on proper pagination, indexing, and avoidance of loading the entire result set into the browser/UI layer at once.

**Export**
- Export generation time scales with the size of the filtered result set; large exports should stream data to the output file rather than buffering the entire result set in memory.

## Functional Requirements

- The Scanner Engine must enforce a configurable per-domain timeout to prevent a single unresponsive site from blocking the scan queue indefinitely.
- The Dashboard must implement pagination or virtualized rendering once result counts exceed a reasonable single-page threshold (e.g., a few hundred rows).
- Export operations must not block the user interface; long-running exports should be handled asynchronously with a completion notification.
- Database queries supporting the Dashboard and Filtering System must be indexed appropriately to avoid full table scans on large datasets.

## Technical Considerations

- SQLite's single-writer model means that concurrent scan result writes should be batched or queued at the application level to avoid lock contention during high-throughput scanning periods.
- Playwright browser instances consume significant memory per concurrent instance; concurrency limits must be tuned based on available host memory, not just CPU core count.
- Detection rule matching performance should be periodically profiled as the ruleset grows, since a large number of rules evaluated naively (rather than through efficient pattern indexing) could become a bottleneck over time.
- Database indexes should be defined on frequently filtered columns (domain, confidence score, tags, star status) to keep Dashboard and Filtering System queries performant, consistent with `DATABASE_DESIGN.md`.

## Workflow / Process

```
Performance Baseline Established for Each Pipeline Stage
              ↓
Load Testing Performed with Representative Domain Batches
              ↓
Bottlenecks Identified (Scanner Concurrency, DB Writes, Dashboard Rendering)
              ↓
Targeted Optimization Applied (Indexing, Concurrency Tuning, Pagination)
              ↓
Performance Re-Measured Against Baseline
              ↓
Acceptable Thresholds Documented and Monitored Going Forward
```

## Error Handling

- Performance degradation (e.g., scan timeouts increasing, dashboard load times increasing) must be logged and surfaced through the logging strategy defined in `LOGGING.md`, not silently tolerated.
- If the Scanner Engine's concurrency limit is exceeded due to a configuration error, the system must queue excess scan requests rather than attempting to exceed configured resource limits, which could destabilize the host system.
- Slow database queries should be logged with execution time so that performance regressions can be identified before they impact users.

## Security Considerations

- Uncontrolled scan concurrency could be exploited to exhaust host resources; concurrency limits must be enforced server-side and not solely relied upon as a client-configurable setting.
- Export operations on very large filtered result sets must be rate-limited or queued to prevent a single user action from degrading performance for other operations.

## Future Improvements

- Introduce a caching layer for frequently accessed Dashboard queries (e.g., aggregate technology counts) to reduce repeated database load.
- Explore a distributed or worker-pool-based scanning architecture if scan volume grows beyond what a single-host concurrency model can support.
- Add automated performance regression testing as part of the CI pipeline, benchmarking key operations against defined thresholds.
- Evaluate migrating from SQLite to a client-server database (e.g., PostgreSQL) if concurrent write throughput becomes a limiting factor, as noted in `KNOWN_LIMITATIONS.md`.

## Summary

Performance in Ads Detector is shaped primarily by the resource-intensive nature of browser-automation-based scanning. This document establishes expected performance characteristics at each workflow stage, identifies key bottlenecks — particularly scanner concurrency and SQLite write contention — and outlines the mitigations and monitoring practices needed to keep the platform responsive and reliable as scan volume and dataset size grow.
