---
date: 2025-02-26
time: 17:54
author: 
title: "BlueSky: How to Raise a Robot — A Case for Neuro-Symbolic AI \rin Constrained Task Planning for Humanoid Assistive Robots"
created-date: 2025-02-26
tags: 
paper: 
code: 
zks-type: lit
---
==draft mode via LM summary==


## Description of result

The paper "BlueSky: How to Raise a Robot — A Case for Neuro-Symbolic AI in Constrained Task Planning for Humanoid Assistive Robots" explores methods to ensure robots respect constraints related to safety, security, privacy and social norms when planning tasks, particularly in assistive scenarios. It analyses symbolic, neural, and hybrid neuro-symbolic approaches to robot task planning, highlighting their trade-offs. The paper proposes using LLMs as knowledge bases and planners, and it suggests a roadmap for future research to integrate neural and symbolic AI for constrained robot task planning.

---

## How it compares to previous work

- **Classical symbolic approaches** are strong in guaranteeing constraint satisfaction but struggle with the task universality required for humanoid robots due to the high overhead in manual specification of constraints.
- **Neural planning** offers scalability and adaptability through learning but has difficulty ensuring that safety, security, and privacy constraints are met.
- **Machine learning-based access control** has been proposed, but current systems have error margins.
- **LLMs** represent a recent advancement, showing promise due to their ability to process and generate both signal- and symbol-based input and output. They can also infer social norms from their training data, reducing the need for explicit encoding. However, LLMs may produce inconsistent or incorrect plans compared to standard symbolic planning.
- **Neuro-symbolic AI** is presented as a way to combine the advantages of both symbolic and neural methods, offering a path to task-universal planning with guaranteed constraint satisfaction.

---

## Main strategies used to obtain results

- **Analysis of symbolic planning:** Examining how symbolic planners use search algorithms to find action sequences that transform the robot's state to achieve a goal, incorporating constraints as preconditions for actions.
- **Analysis of neural planning:** Assessing deep-learned neural planners and their ability to scale to complex deployments, alongside deep-learning based access control.
- **Evaluation of LLMs:** Testing the capabilities of LLMs like ChatGPT as constraint-observing neural planners by formulating task-planning problems in natural language and evaluating the generated plans.
- **Proposal of neuro-symbolic hybrid methods:** Advocating for combining neural planning and neural constraints for versatility with symbolic constraints for critical policies.
- **Description of neuro-symbolic integration levels:** Using Kautz's classification to differentiate between types of neuro-symbolic integration, from loosely coupled systems to those with deep symbolic reasoning within the neural engine.
