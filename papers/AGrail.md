---
date: 2025-02-26
time: 17:09
author: 
title: "AGrail: A Lifelong Agent Guardrail with Effective and Adaptive Safety Detection"
created-date: 2025-02-26
tags: 
paper: https://arxiv.org/abs/2502.11448
code: 
zks-type: lit
---
==draft mode via LM summary==



## Description of result

AGrail is a framework designed to improve the safety of LLM agents by addressing task-specific and systemic risks. The framework features:

- **Adaptive Safety Check Generation:** AGrail dynamically generates safety checks based on universal safety criteria and can incorporate task-specific trusted contexts.
- **Effective Safety Check Optimisation:** The framework iteratively refines safety checks to identify the most effective checks for each agent action using two cooperative LLMs.
- **Tool Compatibility & Flexibility:** AGrail can use internal reasoning and invoke customised auxiliary tools to enhance the checking process.
- **Safe-OS benchmark:** A high-quality, comprehensive dataset designed to evaluate the robustness of online OS agents.

---

## How it compares to previous work

- Existing guardrail approaches often overlook modalities beyond natural language outputs, such as Python code or Linux commands.
- GuardAgent relies on manually specified trusted contexts, which limits its ability to adapt to dynamic downstream tasks. AGrail overcomes this through adaptive safety check generation.
- Conseca generates adaptive safety policies, but its reliance on manually specified trusted contexts may lead to misinterpretations of user intent and task requirements. AGrail optimises safety checks to balance robustness and utility.
- Unlike GuardAgent, which uses memory for knowledge-enabled reasoning, AGrail optimises memory collaboratively via test-time adaptation and storing effective safety checks.
- Existing benchmarks primarily rely on LLM-generated data, which may not fully reflect real-world scenarios. AGrail includes the Safe-OS benchmark, which focuses on real-world agent outputs to ensure realistic and adaptive evaluation.

---

## Main strategies used to obtain results

- **Adaptive Safety Check Generation:** Universal safety criteria are applied across various agents, with support for manually designed safety criteria to enhance task-specific effectiveness.
- **Test-Time Adaptation (TTA):** AGrail employs two LLMs (Analyzer and Executor) in an iterative refinement process to ensure effective and adaptive agent actions.
    - The **Analyzer** retrieves stored safety checks and modifies them based on agent usage principles and safety criteria.
    - The **Executor** evaluates safety checks, invokes external tools for validation, and updates the memory module.
- **Memory Module:** Agent actions, safety categories, and generated safety checks are stored, with a step-back prompting technique used to convert agent actions into natural language and tool command language for enhanced generalization and retrieval accuracy.
- **Experimental Evaluation:** AGrail's performance is evaluated on datasets like Mind2Web-SC, EICU-AC, AdvWeb, and EIA, as well as the Safe-OS benchmark, focusing on real-world agent outputs. Evaluation metrics include accuracy, precision, recall, F1-score, and agreement metrics to assess the quality of safety evaluations.