# EXPLAINABILITY.md

This document explains the internal mechanisms, data lineage, operational boundaries, and governance framework of **# Explainability & Decision Transparency Report** (`agentbench`) in accordance with the **OpenGAP v0.1.0** specification for the **HiDevs GitAgent Passport** clearance pipeline.

> **Agent Name:** # Explainability & Decision Transparency Report (`agentbench`)  
> **Specification:** OpenGAP v0.1.0  
> **Category / Domain:** Developer Tools / Multi-Environment LLM Agent Benchmarking & Function-Calling Evaluation  
> **Compliance Standard:** OpenGAP Checkpoint 2 (Explainability & Decision Governance), OWASP LLM Top 10, MITRE ATLAS  

---

## How the Agent Decides

### 1. Deterministic Multi-Stage Decision Pipeline
The agent operates via a strictly deterministic, 5-stage execution pipeline designed to evaluate model outputs across heterogeneous interactive sandbox environments.

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



### 3. Thresholding & Refusal Decision Criteria

# Explainability & Decision Transparency Report enforces strict operational boundaries and deterministic refusal thresholds:
- **Refusal on Policy Violation**: Requests violating boundary constraints halt with code `ERR_POLICY_VIOLATION`.
- **Refusal on Timeout**: Executions exceeding budget limits terminate with code `ERR_EXECUTION_TIMEOUT`.

### 4. Fallback Decision Mechanism

Continuous operational stability is maintained through layered fault recovery:
- **Model Fallback Cascade**: High-level reasoning and synthesis default to `gemini-2.0-flash` with automatic failover to `gpt-4o` and `claude-3-5-sonnet`.

### 5. Human-in-the-Loop Governance

Human operators retain sovereign authority over the multi-agent execution lifecycle:
- **Operational Review**: Sensitive actions require operator sign-off.
- **Audit Logging**: All decisions are recorded for auditability.

---

## The Data It Uses

# Explainability & Decision Transparency Report operates under strict principles of data minimization, environment isolation, and privacy protection.

### 1. Ingested Input Data

The framework processes only operational data necessary to perform its functions:
- **Input Directives**: Operational tasks and data payloads.

### 2. Configuration & Reference Data

- **Configuration Schemas**: Declarative system configuration files.

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

### 1. Deterministic Multi-Stage Decision Pipeline
The agent operates via a strictly deterministic, 5-stage execution pipeline designed to evaluate model outputs across heterogeneous interactive sandbox environments.

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

### 2. Mathematical Decision & Affinity Scoring
Task selection and trajectory evaluation rely on a standardized affinity and scoring formulation:

$$S_{\text{eval}}(t) = \alpha \cdot \mathbb{I}(\text{State}_t = \text{Goal}) + \beta \cdot \left(1 - \frac{\text{Steps}_t}{\text{MaxSteps}}\right) - \gamma \cdot \text{Penalty}_{\text{error}}$$

Where:
- $\alpha = 0.70$: Primary objective completion weight.
- $\beta = 0.20$: Trajectory efficiency and step economy coefficient.
- $\gamma = 0.10$: Syntactic or runtime execution error penalty.
- $\mathbb{I}(\cdot)$: Binary indicator function verifying exact state assertions.

Environment routing affinity across available task workers is calculated as:

$$A(e, k) = \frac{\exp(\mathbf{w}_e \cdot \mathbf{x}_k)}{\sum_{j=1}^{M} \exp(\mathbf{w}_j \cdot \mathbf{x}_k)}$$

Where $\mathbf{x}_k$ represents the embedding vector of task scenario $k$ and $\mathbf{w}_e$ denotes the capability weights of containerized worker $e$.

### 3. Thresholding & Refusal Decision Criteria
When inputs violate safety boundaries or task criteria, execution is refused with deterministic status codes:

| Threshold Parameter | Value | Decision / Refusal Action | Error Code |
| :--- | :--- | :--- | :--- |
| **Max Turn Budget ($T_{\text{max}}$)** | $\ge 30$ turns | Terminate session immediately as exhausted | `ERR_TURN_LIMIT_EXCEEDED` |
| **Per-Step Execution Timeout** | $> 120$ seconds | Terminate active sandbox sub-process | `ERR_STEP_TIMEOUT` |
| **Host System Access Attempt** | Regex match on host mount | Block command and quarantine worker container | `ERR_SANDBOX_ESCAPE_VIOLATION` |
| **Malformed Tool Argument Schema** | Schema mismatch | Return structured feedback to agent | `ERR_INVALID_TOOL_PAYLOAD` |
| **Database Destruction Safeguard** | `DROP DATABASE`, `SHUTDOWN` | Intercept and reject execution | `ERR_UNSAFE_OPERATION_BLOCKED` |

### 4. Multi-Tier Fallback Mechanisms & Human-in-the-Loop Governance
1. **Tier 1 (Automated Retry)**: Transient network disconnections to LLM inference endpoints undergo 3 exponential backoff attempts (1s, 2s, 4s).
2. **Tier 2 (Environment Reset)**: If an environment worker crashes or encounters an unrecoverable state, the worker container is killed and restarted from its pristine base snapshot.
3. **Tier 3 (Human-in-the-Loop Interruption)**: In ambiguous benchmark discrepancies or potential container security alerts, execution halts and alerts are dispatched to the administrative console.

---

## The Data It Uses

### 1. Ingestion Data & Input Types
- **Agent Prompts**: High-level problem formulations and initial instruction context.
- **Model Responses**: Raw generation tokens, function call arguments, and reasoning chains.
- **Environment Telemetry**: Container stdout, stderr, exit codes, and DOM/database snapshot states.

### 2. Reference Benchmarks & Knowledge Bases
- **Interactive Datasets**: OS Interaction tasks, DBBench SQL schemas, ALFWorld PDDL game states, WebShop e-commerce catalogs, and Freebase knowledge graphs.
- **Ground-Truth Predicates**: Formal validation scripts and expected end-state assertions.

### 3. Model Lineage & System Architecture
- **Supported Models**: OpenAI GPT-4/3.5 series, Anthropic Claude series, open-weights models (Llama, Mistral, Qwen, ChatGLM) evaluated via standardized API adapters.
- **Runtime Dependencies**: Docker, Docker Compose, Redis controller, Python 3.10+ execution runtime.

### 4. Data Privacy, Governance & Retention
- **Ephemeral Sandbox Policy**: All sandbox container data, created files, and modified records are destroyed upon test teardown.
- **Zero Host Leakage**: Network interfaces inside task containers operate on bridge subnets isolated from corporate intranets.
- **Retention Period**: Trajectory interaction logs are stored locally for up to 30 days for reproducible research audits before archival.

---

## Limitations

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
| - Deterministic Multi-Stage Decision Pipeline
The agent operates via a strictly deterministic, 5-stage execution pipeline designed to evaluate model outputs across heterogeneous interactive sandbox environments.

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

### 2. Mathematical Decision & Affinity Scoring
Task selection and trajectory evaluation rely on a standardized affinity and scoring formulation:

$$S_{\text{eval}}(t) = \alpha \cdot \mathbb{I}(\text{State}_t = \text{Goal}) + \beta \cdot \left(1 - \frac{\text{Steps}_t}{\text{MaxSteps}}\right) - \gamma \cdot \text{Penalty}_{\text{error}}$$

Where:
- $\alpha = 0.70$: Primary objective completion weight.
- $\beta = 0.20$: Trajectory efficiency and step economy coefficient.
- $\gamma = 0.10$: Syntactic or runtime execution error penalty.
- $\mathbb{I}(\cdot)$: Binary indicator function verifying exact state assertions.

Environment routing affinity across available task workers is calculated as:

$$A(e, k) = \frac{\exp(\mathbf{w}_e \cdot \mathbf{x}_k)}{\sum_{j=1}^{M} \exp(\mathbf{w}_j \cdot \mathbf{x}_k)}$$

Where $\mathbf{x}_k$ represents the embedding vector of task scenario $k$ and $\mathbf{w}_e$ denotes the capability weights of containerized worker $e$.

### 3. Thresholding & Refusal Decision Criteria
When inputs violate safety boundaries or task criteria, execution is refused with deterministic status codes:

| Threshold Parameter | Value | Decision / Refusal Action | Error Code |
| :--- | :--- | :--- | :--- |
| **Max Turn Budget ($T_{\text{max}}$)** | $\ge 30$ turns | Terminate session immediately as exhausted | `ERR_TURN_LIMIT_EXCEEDED` |
| **Per-Step Execution Timeout** | $> 120$ seconds | Terminate active sandbox sub-process | `ERR_STEP_TIMEOUT` |
| **Host System Access Attempt** | Regex match on host mount | Block command and quarantine worker container | `ERR_SANDBOX_ESCAPE_VIOLATION` |
| **Malformed Tool Argument Schema** | Schema mismatch | Return structured feedback to agent | `ERR_INVALID_TOOL_PAYLOAD` |
| **Database Destruction Safeguard** | `DROP DATABASE`, `SHUTDOWN` | Intercept and reject execution | `ERR_UNSAFE_OPERATION_BLOCKED` |

### 4. Multi-Tier Fallback Mechanisms & Human-in-the-Loop Governance
1. **Tier 1 (Automated Retry)**: Transient network disconnections to LLM inference endpoints undergo 3 exponential backoff attempts (1s, 2s, 4s).
2. **Tier 2 (Environment Reset)**: If an environment worker crashes or encounters an unrecoverable state, the worker container is killed and restarted from its pristine base snapshot.
3. **Tier 3 (Human-in-the-Loop Interruption)**: In ambiguous benchmark discrepancies or potential container security alerts, execution halts and alerts are dispatched to the administrative console.

---

## The Data It Uses

### 1. Ingestion Data & Input Types
- **Agent Prompts**: High-level problem formulations and initial instruction context.
- **Model Responses**: Raw generation tokens, function call arguments, and reasoning chains.
- **Environment Telemetry**: Container stdout, stderr, exit codes, and DOM/database snapshot states.

### 2. Reference Benchmarks & Knowledge Bases
- **Interactive Datasets**: OS Interaction tasks, DBBench SQL schemas, ALFWorld PDDL game states, WebShop e-commerce catalogs, and Freebase knowledge graphs.
- **Ground-Truth Predicates**: Formal validation scripts and expected end-state assertions.

### 3. Model Lineage & System Architecture
- **Supported Models**: OpenAI GPT-4/3.5 series, Anthropic Claude series, open-weights models (Llama, Mistral, Qwen, ChatGLM) evaluated via standardized API adapters.
- **Runtime Dependencies**: Docker, Docker Compose, Redis controller, Python 3.10+ execution runtime.

### 4. Data Privacy, Governance & Retention
- **Ephemeral Sandbox Policy**: All sandbox container data, created files, and modified records are destroyed upon test teardown.
- **Zero Host Leakage**: Network interfaces inside task containers operate on bridge subnets isolated from corporate intranets.
- **Retention Period**: Trajectory interaction logs are stored locally for up to 30 days for reproducible research audits before archival.

---

## Limitations

### 1. High Memory Overhead in WebShop & ALFWorld Workers | Section 1 | Verified |
| - Discontinued or Static External Service Schemas | Section 2 | Verified |
| - Non-Deterministic Model Generation | Section 3 | Verified |
| - Limited Coverage of GUI Operating Systems | Section 4 | Verified |
| - Benchmark Saturation by State-of-the-Art Models | Section 5 | Verified |
