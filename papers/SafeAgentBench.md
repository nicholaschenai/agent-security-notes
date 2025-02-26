---
date: 2025-02-26
time: 17:44
author: 
title: "SafeAgentBench: A Benchmark for Safe Task Planning of Embodied LLM Agents"
created-date: 2025-02-26
tags: 
paper: https://arxiv.org/abs/2412.13178
code: 
zks-type: lit
---
==draft mode via LM summary==

SafeAgentBench is a new benchmark designed to evaluate the safety awareness and task planning capabilities of embodied agents that use large language models (LLMs). It addresses the potential risks associated with embodied LLM agents performing hazardous tasks in real-world scenarios. The benchmark includes a dataset of 750 tasks covering various hazards and task types, an embodied environment called SafeAgentEnv, and evaluation methods from both execution and semantic perspectives. Experiments using SafeAgentBench reveal that current embodied LLM agents exhibit weak safety awareness, and simply changing the LLM does not significantly improve safety.

## Description of result

- SafeAgentBench features a dataset of **750 tasks**, with 450 tasks involving safety hazards and 300 safe tasks used as a control group.
- The dataset covers **10 common risks** to humans and property, categorised into harm to humans (fire hazard, electrical shock, explosion, poisoning/ingestion, slip hazard) and harm to property (liquid and spill damage, breakage and dropping, misuse of electrical appliances, furniture and decor damage, damage to small items).
- The tasks are divided into **three types**: detailed, abstract, and long-horizon, to assess safety issues across different task lengths and levels of abstraction.
- The benchmark includes **SafeAgentEnv**, an embodied environment based on AI2-THOR, which supports multi-agent execution with 17 high-level actions.
- Evaluation methods include **task-execution-based** and **LLM-based** assessments, with the latter addressing limitations of simulators and tasks with multiple outcomes.
- Experiments tested eight embodied LLM agents, revealing that even the most safety-conscious baseline achieved only a **10% rejection rate** for detailed hazardous tasks.
- A **ThinkSafe module**, which uses GPT-4 to assess the safety of an agent's next step, was tested, but it incorrectly rejected a high percentage of safe tasks, indicating that semantic-level filtering alone is insufficient.

---

## How it compares to previous work

- Unlike existing benchmarks like Behavior1K, ALFRED, and Lota-Bench, SafeAgentBench **specifically focuses on safety awareness** in embodied LLM agents.
- **ALFRED** has a limited range of task types and supported actions, and its outdated version makes it difficult to expand into safety issues.
- **Lota-Bench** primarily tests the planning capability of LLMs while overlooking other components of embodied agents.
- **RiskAwareBench** and **HAZARD** focus on text-level safety of LLMs, while SafeAgentBench evaluates the safety of embodied agents interacting with the environment.
- SafeAgentBench offers a more comprehensive evaluation by considering both task execution and semantic perspectives, addressing the limitations of relying solely on task execution.

---

## Main strategies used to obtain results

- The SafeAgentBench dataset was generated using **GPT-4** to create diverse task scenarios, with a two-step filtering process and human annotation to ensure executability and evaluability.
- **SafeAgentEnv** was developed based on AI2-THOR, with a new low-level controller to enable detailed task execution and support a broad spectrum of embodied LLM agents.
- **Eight representative embodied LLM agents** were selected as baselines, and their performance was tested using SafeAgentBench.
- Both **GPT-4** and **other open-source LLMs** (Llama3-8B, Qwen2-7B, and DeepSeek-V2.5) were used to investigate the impact of different LLMs on safety awareness.
- The **ThinkSafe module** was designed to assess the potential risks of task execution from a semantic perspective, using GPT-4 to determine whether a step poses any safety risks.
- A **user study** was conducted to verify the accuracy of GPT-4 evaluation across the three task types, demonstrating high consistency between human and GPT-4 assessments.