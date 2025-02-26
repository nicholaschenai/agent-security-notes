---
date: 2025-02-26
time: 17:17
author: 
title: "TrustAgent: Towards Safe and Trustworthy LLM-based Agents"
created-date: 2025-02-26
tags: 
paper: 
code: 
zks-type: lit
---
==draft mode via LM summary==


## Description of result

The TrustAgent framework enhances the safety and helpfulness of LLM-based agents by using an Agent Constitution and a pipeline of three safety strategies: **pre-planning, in-planning, and post-planning**. It has been shown to improve agent performance across various domains, ensuring actions are not only correct but also safely sequenced.

---

## How it compares to previous work

Previous work on trustworthy LLM-based agents has primarily focused on observation, identifying, and assessing risks. TrustAgent builds upon these approaches by introducing a comprehensive framework that proactively improves safety through an Agent Constitution and a pipeline of strategies. Unlike AI constitutions that focus on verbal harm, the Agent Constitution places significant emphasis on the safety of actions and tool utilization.

---

## Main strategies used to obtain results

- **Agent Constitution**: Establishes a legal basis for governing LLM-based agents, guiding their behavior in accordance with fundamental principles.
- **Pre-planning Strategy**: Integrates safety knowledge into the agent's model before any actions are planned, using regulation learning and hindsight learning.
- **In-planning Strategy**: Enhances safety during plan generation by using prompting methods to guide the language model toward generating safe and appropriate content.
- **Post-planning Strategy**: Ensures safety by inspecting the generated plan against the Agent Constitution after generation but before execution, using a safety inspector agent.
