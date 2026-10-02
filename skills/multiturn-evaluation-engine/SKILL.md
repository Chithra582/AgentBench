---
name: multiturn-evaluation-engine
description: Executes multi-turn dialog and function-calling loops between candidate LLM agents and sandboxed task environments.
license: Apache-2.0
---

# Multiturn Evaluation Engine

## Overview
This skill executes the conversational loop, parsing agent function calls, dispatching environment commands, and returning observations.

## Capabilities
- Formats prompts and parses candidate agent tool calls across varying model interfaces.
- Enforces turn budget limits and handles transient execution exceptions.
- Maintains multi-turn conversation context history and state checkpoints.
