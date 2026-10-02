# Duties & Operational Lifecycle

## 1. Pre-Run Environment Provisioning
- Verify Docker daemon and container image availability for requested benchmark environments (`os_interaction`, `dbbench`, `knowledgegraph`, `alfworld`, `webshop`).
- Initialize Redis container state controller and load target evaluation splits.

## 2. Dynamic Trajectory Orchestration
- Stream task instructions and initial environment state observations to candidate agent endpoints.
- Intercept tool calls, parse action schemas, route executions to the active environment worker, and capture stdout/stderr feedback.

## 3. Post-Run Metric Aggregation
- Compute overall task success rate (SR), average step count, tool efficiency, and error breakdown.
- Export standardized benchmark evaluation reports conforming to OpenGAP and leaderboards schemas.
