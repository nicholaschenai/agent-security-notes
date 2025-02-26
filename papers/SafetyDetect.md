---
date: 2025-02-26
time: 17:38
author: 
title: "“Don’t forget to put the milk back!”\r Dataset for Enabling Embodied Agents to Detect Anomalous Situations"
created-date: 2025-02-26
tags: 
paper: https://arxiv.org/pdf/2404.08827
code: 
zks-type: lit
---
==draft mode via LM summary==

The **SafetyDetect dataset** is designed to **evaluate the ability of embodied AI agents to detect unsafe or unsanitary conditions in a home environment**. The dataset contains 1000 anomalous home scenes with unsafe or unsanitary situations. The dataset uses the VirtualHome simulator. Using large language models (LLMs) with a **scene graph** to represent the scene and the relationships between objects is key to the approach. The **SafetyDetect dataset** is aimed at enabling researchers to create embodied agents that can detect unsafe or unsanitary conditions in the home. The agent must discover any potential anomalies and report them to the user without explicit instructions. Object relations from the scene graph are classified as normal, dangerous, unsanitary, or dangerous for children, with the most promising approach utilizing GPT-4. Real-world experiments were conducted on a ClearPath TurtleBot, generating a scene graph from visuals of the real-world scene, with minimal performance loss.

## Description of result

The SafetyDetect dataset enables embodied AI agents to detect anomalies by:

- **Identifying unsafe or unsanitary conditions**: Agents must identify hazards like spills, tripping hazards, or exposed refrigerated foods.
- **Considering user preferences**: Agents should only report anomalies relevant to the user's context, such as the presence of children.
- **Utilizing scene graphs**: Representing the environment as a graph of objects and their relationships helps LLMs reason about the scene.
- **Employing LLMs**: Large language models provide the knowledge needed to classify object relations as normal, unsafe, unsanitary, or dangerous for children.
- **Achieving high detection rates**: The best methods can correctly identify over 90% of anomalous scenarios.

---

## How it compares to previous work

The SafetyDetect dataset distinguishes itself from previous work through:

- **Focus on household anomaly detection**: Unlike other datasets that concentrate on tasks like navigation, instruction following, or cleaning up clutter, SafetyDetect specifically addresses the detection of unsafe or unsanitary conditions.
- **Unique use case**: The dataset is designed for detecting unsafe or unsanitary conditions, which is a unique focus compared to other datasets. Prior approaches would need significant modification to work on SafetyDetect.
- **Emphasis on LLMs and scene graphs**: SafetyDetect leverages recent advances in LLMs and scene graphs for scene understanding, differentiating it from methods that rely on hard-coded rules or knowledge graphs.
- **Anomaly diversity**: The dataset includes a wide range of diverse and unrelated anomalies, making it more challenging than tasks with precise goals.

---

## Main strategies used to obtain results

The primary strategies employed to achieve high anomaly detection rates include:

- **Scene graph utilization**: Representing the scene as a graph of objects and their relationships provides crucial context to the LLM.
- **Classification approach**: Classifying object relations as normal, unsafe, unsanitary, or dangerous for children improves performance compared to directly detecting anomalous relationships.
- **Chain-of-thought prompting**: Providing the LLM with example anomalies, classifications, and explanations enhances its reasoning abilities.
- **Leveraging LLMs**: Using LLMs like GPT-4 provides diverse knowledge about home environments and potential hazards.
- **Sim-to-real transfer**: Validating the approach in real-world scenarios using a ClearPath TurtleBot demonstrates the practicality of the SafetyDetect dataset and methods.