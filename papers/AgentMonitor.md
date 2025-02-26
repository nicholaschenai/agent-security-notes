---
date: 2025-02-26
time: 17:03
author: 
title: "TESTING LANGUAGE MODEL\r AGENTS SAFELY IN THE WILD"
created-date: 2025-02-26
tags: 
paper: 
code: 
zks-type: lit
---
==draft mode via LM summary==

## Description of result

The paper introduces **AgentMonitor**, a framework for safe, open-world testing of Language Model Agents (LMAs). It uses a language model-based monitor to audit agent actions, enforce safety boundaries, and prevent potentially irreversible harm. The effectiveness of AgentMonitor was evaluated on a dataset of AutoGPT outputs, achieving an F1 score of 89.4% in identifying unsafe or off-task behaviours. The framework uses parameters such as "Previous Context", "Prompt Context" and others to improve the monitor's ability to identify unsafe actions.

---

## How it compares to previous work

Existing methods for evaluating LMAs often use constructed sandbox environments to ensure safety. AgentMonitor differs by focusing on enabling safe evaluation in real-world environments, similar to the approach taken by ChemCrow, but with a general-purpose safety monitor that can be adapted to specific tests. Unlike some approaches, it aims to minimize human oversight and intervention. The use of model-based supervision contributes to the literature on scalable oversight.

---

## Main strategies used to obtain results

The study used several strategies to achieve its results:

- **Dataset Creation:** Assembling a dataset of potentially unsafe agent responses from AutoGPT outputs, supplemented with manually authored unsafe and off-task outputs.
- **Threat Model Definition:** Grounding the safety framework using the OWASP "Top 10 for LLM" to address concerns like prompt injection and excessive agency.
- **AgentMonitor Design:** Constructing a monitor based on a language model (gpt-3.5-turbo-16k) that intervenes before potentially harmful actions are executed, using various parameters to specify behaviour.
- **Ablation Studies:** Systematically removing individual model parameters to assess their impact on the monitor's performance, using F1 score as the primary metric.
- **Performance Evaluation:** Measuring the monitor's ability to flag unsafe or off-task outputs using precision, recall, and F1 score.
- Works with both prompted and deterministic (human written code) whitelists