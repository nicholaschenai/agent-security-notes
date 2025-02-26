---
date: 2025-02-26
time: 16:39
author: 
title: 
created-date: 2025-02-26
tags: 
paper: https://arxiv.org/abs/2406.09187
code: 
zks-type: lit
---
==draft mode==
## Description of result

GuardAgent is introduced as the first LLM agent framework designed to safeguard other LLM agents. It operates by **assessing whether the inputs and outputs of a target LLM agent comply with a set of predefined guard requests**, such as safety rules or privacy policies. GuardAgent generates an action plan and converts it into executable code to enforce these guardrails. GuardAgent was evaluated on two novel benchmarks: EICU-AC (for healthcare agent access control) and Mind2Web-SC (for web agent safety control). The experiments showed high guarding accuracy, 98.7% on EICU-AC and 90.0% on Mind2Web-SC, demonstrating its effectiveness.

---

## How it compares to previous work

Existing guardrails for LLMs focus on moderating textual inputs and outputs, which are inadequate for LLM agents that have diverse output modalities and specific guard requests. Task-specific guardrails are hardwired into LLM agents, lacking generalizability across different agents and guard requests. In contrast, **GuardAgent provides a generalizable framework** that uses an LLM agent to safeguard other LLM agents. It generates guardrails by code generation and execution, increasing reliability compared to natural language-based guardrails. Unlike traditional guardrails that require training, GuardAgent employs in-context learning, allowing direct utilization of off-the-shelf LLMs.

---
## Main strategies used to obtain results
- Input: guard requests, specification of target agent and its inputs and outputs

- Plans with few shot demonstrations retrieved from memory (and context like specifications)

- Generate guardrail code based demonstrations and a list of callable functions

- Code executed to determine if target agent inputs and outputs satisfy the guard requests

