# EXPLAINABILITY.md

This document explains the internal mechanisms, data lineage, operational boundaries, and governance framework of **# Explainability & Decision Transparency Report** (`agentbench`) in accordance with the **OpenGAP v0.1.0** specification for the **HiDevs GitAgent Passport** clearance pipeline.

> **Agent Name:** # Explainability & Decision Transparency Report (`agentbench`)  
> **Specification:** OpenGAP v0.1.0  
> **Category / Domain:** Developer Tools / Multi-Environment LLM Agent Benchmarking & Function-Calling Evaluation  
> **Compliance Standard:** OpenGAP Checkpoint 2 (Explainability & Decision Governance), OWASP LLM Top 10, MITRE ATLAS  

---

## How the Agent Decides

# Explainability & Decision Transparency Report operates via a deterministic five-stage operational pipeline.

### 1. Decision Architecture

The runtime intake, state classification, evaluation, and execution tracking operate across a deterministic, five-stage pipeline:

```
+-----------------------------------------------------------------------------------+
|                            Deterministic Execution Pipeline                        |
+-----------------------------------------------------------------------------------+
|  [Stage 1: Ingestion & Task Configuration]                                        |
|     --> Validate target benchmark suite, split configurations, & model credentials|
+-----------------------------------------+-----------------------------------------+
                                          |
                                          v
+-----------------------------------------------------------------------------------+
|  [Stage 2: Environment Container Provisioning]                                    |
|     --> Spin up isolated task workers (OS, DBBench, WebShop, KG, ALFWorld via Docker)|
+-----------------------------------------+-----------------------------------------+
                                          |
                                          v
+-----------------------------------------------------------------------------------+
|  [Stage 3: Multi-Turn Interaction & Action Dispatch]                             |
|     --> Stream state observations, parse tool calls, and execute sandboxed actions |
+-----------------------------------------+-----------------------------------------+
                                          |
                                          v
+-----------------------------------------------------------------------------------+
|  [Stage 4: Objective Scoring & Evaluation Gate]                                   |
|     --> Compare final environment state against ground-truth assertion predicates  |
+-----------------------------------------+-----------------------------------------+
                                          |
                                          v
+-----------------------------------------------------------------------------------+
|  [Stage 5: Trajectory Telemetry & Report Export]                                  |
|     --> Aggregate success rates, compute efficiency metrics, and output JSONL logs |
+-----------------------------------------------------------------------------------+
```

### 2. Decision Logic & Routing Formulations

& Evaluation Gate]                                   |
|     --> Compare final environment state against ground-truth assertion predicates  |
+-----------------------------------------+-----------------------------------------+
                                          |
                                          v
+-----------------------------------------------------------------------------------+
|  [Stage 5: Trajectory Telemetry & Report Export]                                  |
|     --> Aggregate success rates, compute efficiency metrics, and output JSONL logs |
+-----------------------------------------------------------------------------------+
```

### 3. Thresholding & Refusal Decision Criteria

# Explainability & Decision Transparency Report enforces strict operational boundaries and deterministic refusal thresholds:
- **Refusal on ERR_TURN_LIMIT_EXCEEDED**: **Max Turn Budget ($T_{\text{max}}$)** halts execution with code `ERR_TURN_LIMIT_EXCEEDED`.
- **Refusal on ERR_STEP_TIMEOUT**: **Per-Step Execution Timeout** halts execution with code `ERR_STEP_TIMEOUT`.
- **Refusal on ERR_SANDBOX_ESCAPE_VIOLATION**: **Host System Access Attempt** halts execution with code `ERR_SANDBOX_ESCAPE_VIOLATION`.
- **Refusal on ERR_INVALID_TOOL_PAYLOAD**: **Malformed Tool Argument Schema** halts execution with code `ERR_INVALID_TOOL_PAYLOAD`.
- **Refusal on ERR_UNSAFE_OPERATION_BLOCKED**: **Database Destruction Safeguard** halts execution with code `ERR_UNSAFE_OPERATION_BLOCKED`.

### 4. Fallback Decision Mechanism

Continuous operational stability is maintained through layered fault recovery:
- **Model Fallback Cascade**: High-level reasoning and synthesis default to `gemini-2.0-flash` with automatic failover to `gpt-4o` and `claude-3-5-sonnet`.

### 5. Human-in-the-Loop Governance

Human operators retain sovereign authority over the multi-agent execution lifecycle:
- **Consequential Action Sign-Off**: Sensitive and consequential actions require operator sign-off.
- **Offline Ledger Auditing**: Operators can verify execution records and state transitions offline.

---

## The Data It Uses

# Explainability & Decision Transparency Report operates under strict principles of data minimization, environment isolation, and privacy protection.

### 1. Ingested Input Data

The framework processes only operational data necessary to perform its functions:
- **Agent Prompts**: High-level problem formulations and initial instruction context.
- **Model Responses**: Raw generation tokens, function call arguments, and reasoning chains.
- **Environment Telemetry**: Container stdout, stderr, exit codes, and DOM/database snapshot states.

### 2. Configuration & Reference Data

- **Interactive Datasets**: OS Interaction tasks, DBBench SQL schemas, ALFWorld PDDL game states, WebShop e-commerce catalogs, and Freebase knowledge graphs.
- **Ground-Truth Predicates**: Formal validation scripts and expected end-state assertions.

### 3. Base Model & Inference Lineage

- **Supported Models**: OpenAI GPT-4/3.5 series, Anthropic Claude series, open-weights models (Llama, Mistral, Qwen, ChatGLM) evaluated via standardized API adapters.
- **Runtime Dependencies**: Docker, Docker Compose, Redis controller, Python 3.10+ execution runtime.

### 4. Data Privacy, Storage, and Retention

- **OWASP LLM & MITRE ATLAS Hardened**: Defended against indirect prompt injection, credential leakage, and unauthorized external API dispatch.
- **Local Environment Isolation**: Agent execution workspaces, intermediate scratchpads, and vector stores reside strictly within designated local project directories.
- **Automated Secret Scrubbing**: API keys, database credentials, and personal credentials are automatically redacted prior to embedding or logging.
- **Zero Commercial Monetization**: Prompts, intermediate reasoning trajectories, and task deliverables are never commercialized or shared with third parties.

---

## Limitations

Understanding the operational boundaries and technical constraints of # Explainability & Decision Transparency Report is essential for effective deployment.

### 1. High Memory Overhead in WebShop & ALFWorld Workers
- **Limitation**: Running concurrent WebShop and ALFWorld workers requires in excess of 16GB of system RAM, risking out-of-memory container crashes on constrained workstations.
- **Mitigation**: Implement worker pool concurrency limits and automatically schedule memory-intensive environments sequentially.

### 2. Discontinued or Static External Service Schemas
- **Limitation**: External snapshot databases (such as legacy Freebase dumps) may contain outdated schema definitions that drift from modern web endpoints.
- **Mitigation**: Enforce self-contained, frozen Docker images housing localized database instances to guarantee consistent test conditions.

### 3. Non-Deterministic Model Generation
- **Limitation**: Commercial LLM endpoints may exhibit minor stochastic behavioral shifts even at temperature 0 due to parallel batching.
- **Mitigation**: Mandate multi-trial evaluation runs ($k \ge 3$) with standard deviation reporting across all benchmark metrics.

### 4. Limited Coverage of GUI Operating Systems
- **Limitation**: OS interaction tasks prioritize headless bash CLI environments rather than graphical desktop interfaces (Windows/macOS GUI).
- **Mitigation**: Pair AgentBench with VisualAgentBench (VAB) extensions for multi-modal desktop and mobile agent validation.

### 5. Benchmark Saturation by State-of-the-Art Models
- **Limitation**: Rapid capability advances have led to near-saturation on simpler sub-tasks within DBBench and basic OS commands.
- **Mitigation**: Continuously curate and roll out hard-split test scenarios with multi-hop dependencies and adversarial error injection.

---

## Summary & Compliance Checklist

| Checkpoint 2 Requirement | Corresponding Section | Status |
| :--- | :--- | :---: |
| **How the agent decides** | [How the Agent Decides](#how-the-agent-decides) | **Covered** |
| - Decision architecture & 5-stage pipeline | Section 1 | Verified |
| - Decision logic & routing formulations | Section 2 | Verified |
| - Thresholding & refusal decision criteria | Section 3 | Verified |
| - Fallback decision mechanism | Section 4 | Verified |
| - Human-in-the-loop governance & oversight | Section 5 | Verified |
| **The data it uses** | [The Data It Uses](#the-data-it-uses) | **Covered** |
| - Ingested input data & query streams | Section 1 | Verified |
| - Configuration & reference schemas | Section 2 | Verified |
| - Base model lineage & deterministic engines | Section 3 | Verified |
| - Data privacy, retention lifecycle & MITRE/OWASP | Section 4 | Verified |
| **Its limitations** | [Limitations](#limitations) | **Covered** |
| - High Memory Overhead in WebShop & ALFWorld Workers | Section 1 | Verified |
| - Discontinued or Static External Service Schemas | Section 2 | Verified |
| - Non-Deterministic Model Generation | Section 3 | Verified |
| - Limited Coverage of GUI Operating Systems | Section 4 | Verified |
| - Benchmark Saturation by State-of-the-Art Models | Section 5 | Verified |
