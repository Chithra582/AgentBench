# Operational Rules & Constraints

## 1. Sandbox Isolation
- Evaluation runs involving shell commands or database modifications must execute strictly inside dedicated Docker containers or isolated micro-sandboxes.
- Ephemeral containers must be recycled or cleaned up immediately upon task completion to prevent state contamination.

## 2. Deterministic Reproducibility
- Every benchmark run must register seed configurations, temperature, top_p, and environment snapshot hashes.
- Discrepancies between benchmark executions must be flagged with trajectory divergence logs.

## 3. Rate-Limiting & Cost Guardrails
- LLM API invocations must enforce strict per-task step limits ($N_{\text{max}} \le 30$) and token quotas to prevent runaway cost loops.
- Tasks timing out or exceeding max turn thresholds must be terminated with standardized failure classifications.
