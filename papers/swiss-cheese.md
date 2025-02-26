---
date: 2025-02-26
time: 17:56
author: 
title: "Swiss Cheese Model for AI Safety: A Taxonomy\r and Reference Architecture for Multi-Layered \rGuardrails of Foundation Model Based Agents"
created-date: 2025-02-26
tags: 
paper: 
code: 
zks-type: lit
---
==draft mode via LM summary==


- **FM-based agents** are autonomous systems that perceive context, reason, plan, and execute workflows by interacting with FMs, external tools, knowledge bases, and other agents to achieve goals.
- **Runtime guardrails** are mechanisms integrated into an agent’s architecture to safeguard its behaviour during runtime, preventing undesirable or unsafe behaviours.
- **Multi-layered guardrails** are essential to manage the autonomy and non-deterministic nature of FM-agents. These are inspired by the Swiss Cheese Model, where multiple layers of protection are implemented, each with its weaknesses (holes), but collectively providing a robust defence against failures.
- A **taxonomy** categorises runtime guardrails based on quality attributes and design options. Quality attributes include accuracy, efficiency, privacy, security, safety, fairness, compliance, generalisability, customisability, adaptability, traceability, portability, interoperability, and interpretability. Design options encompass actions, targets, scope, rules, autonomy, modalities, and underlying techniques.
- A **reference architecture** for multi-layered runtime guardrails includes dimensions for quality attributes, pipelines (prompts, intermediate results, final results), and agent artifacts (goals, plans, tools).
- **AgentOps infrastructure** is used for continuous monitoring and logging.

---

## Description of result

The paper introduces a taxonomy and reference architecture for multi-layered runtime guardrails in FM-based agents. The taxonomy categorises guardrails based on quality attributes (e.g., privacy, security) and design options (e.g., actions, targets). The reference architecture, inspired by the Swiss Cheese Model, proposes multi-layered guardrails that address specific quality attributes, pipeline stages, and agent artifacts. This architecture aims to enhance AI safety by providing a structured approach to designing and implementing robust runtime safeguards.

---

## How it compares to previous work

Existing guardrail approaches primarily address functional correctness, often overlooking quality attributes such as customisability and interpretability. These approaches mainly focus on single-layered guardrails applied to specific agent artifacts, which are insufficient for managing the autonomy and non-deterministic nature of FM-agents. This paper addresses these limitations by providing a comprehensive taxonomy and reference architecture for multi-layered runtime guardrails, offering concrete guidance for AI-safety-by-design from a software architecture perspective. It builds upon initial efforts in runtime guardrails, such as NeMo Guardrails and OpenAI’s Moderation API, by providing a more comprehensive and structured approach.

---

## Main strategies used to obtain results

The results were obtained through a systematic literature review (SLR) following the Petticrew and Roberts approach. The research questions (RQs) were formulated to capture diverse aspects of multi-layered runtime guardrails. An automated keyword-based search was executed across multiple scientific databases, followed by a study filtering process. Data extraction and quality assessment were conducted on the selected studies to develop the taxonomy and reference architecture. The findings from 32 high-quality selected studies were synthesized through an iterative clustering and validation process.