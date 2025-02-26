---
date: 2025-02-26
time: 16:57
author: 
title: "IDENTIFYING THE RISKS OF LM AGENTS \rWITH AN LM-EMULATED SANDBOX"
created-date: 2025-02-26
tags: 
paper: 
code: 
zks-type: lit
---
==draft mode via LM summary==

## Description of result

ToolEmu uses **LLMs to emulate tool executions**, create virtual sandboxes, and automatically evaluate the safety and helpfulness of LM agents, particularly in scenarios with underspecified user instructions. It includes components such as emulators, safety evaluators, and helpfulness evaluators, and has been validated to identify real failures.

---

## How it compares to previous work

- Existing benchmarks primarily focus on assessing the capabilities of LM agents in specific domains like code execution or web environments.
- Unlike previous evaluations with statically established sandboxes, ToolEmu's LM-emulation framework facilitates a broader and more expandable evaluation scope across tools and test scenarios. Many of the assessed tools are either absent from existing benchmarks or challenging to assess in real-world settings with previous standard practices.

---

## Main strategies used to obtain results

- **LM Emulation**: ToolEmu leverages the ability of LMs, specifically GPT-4, to emulate tool executions based on tool specifications, thus creating an automated virtual sandbox.
- **Automatic Evaluation**: It designs LM-based safety and helpfulness evaluators to identify potential risks and measure their severities based on the LM agent's trajectory. The safety evaluator identifies failure cases and assesses safety scores, while the helpfulness evaluator assesses how effectively LM agents fulfill user instructions without causing risks.
- **Benchmark Curation**: ToolEmu curates an evaluation benchmark with diverse tools, test cases, and risk types. The initial set of tool specifications and test cases are generated using GPT-4, followed by human filtering and modifications.