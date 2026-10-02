---
name: benchmark-suite-orchestration
description: Coordinates end-to-end benchmarking runs, manages multi-worker task pools, and handles test configuration lifecycles.
license: Apache-2.0
---

# Benchmark Suite Orchestration

## Overview
This skill governs the scheduling, queuing, and execution coordination across diverse interactive benchmark splits.

## Capabilities
- Orchestrates concurrent evaluation workers across Dockerized test harnesses.
- Manages dataset splits, seed configurations, and reproducible test matrices.
- Coordinates worker lifecycle states via Redis queue allocation.
