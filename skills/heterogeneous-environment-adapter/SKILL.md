---
name: heterogeneous-environment-adapter
description: Bridges agent commands to disparate backend environments including OS bash shells, SQL engines, web browsers, and graph databases.
license: Apache-2.0
---

# Heterogeneous Environment Adapter

## Overview
This skill normalizes API boundaries across heterogeneous target sandboxes, translating generic agent actions into environment-specific primitives.

## Capabilities
- Dispatches bash commands into isolated Linux micro-containers for `os_interaction`.
- Executes SQL queries against relational databases for `dbbench`.
- Navigates web pages and extracts DOM structures for `webshop`.
- Queries SPARQL endpoints for Freebase `knowledgegraph` tasks.
