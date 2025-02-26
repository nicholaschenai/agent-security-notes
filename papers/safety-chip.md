---
date: 2025-02-26
time: 17:31
author: 
title: "Plug in the safety chip: Enforcing constraints for LLM-driven robot agents"
created-date: 2025-02-26
tags: 
paper: 
code: 
zks-type: lit
---
==draft mode via LM summary==

The study introduces a "safety chip" module designed to enhance the safety of robot agents driven by Large Language Models (LLMs). This module focuses on teaching robots the "don'ts" by enforcing safety constraints, which is crucial for practical usage and meeting safety standards like ISO 61508. The safety chip incorporates a queryable safety constraint module based on linear temporal logic (LTL) that enables natural language (NL) to temporal constraints encoding, safety violation reasoning and explaining, and unsafe action pruning. Experimental results in VirtualHome and on a real robot demonstrate the system's adherence to safety constraints and its scalability with complex constraints.

## Description of result

The "safety chip" is a hybrid system that represents safety constraints using Linear Temporal Logic (LTL), which can be verified for correctness. It translates English instructions describing safety constraints into LTL constraints, which are then verified by experts. This system includes a translator for NL to LTL, a query system for explaining safety violations, and a constraint monitor for validating and pruning actions. The safety chip monitors the LLM agent's actions, masks unsafe actions, and uses reprompting to guide the agent toward safe actions. The system was tested in the VirtualHome environment and on a physical robot, demonstrating its ability to maintain a high safety rate, even with complex constraints.

---

## How it compares to previous work

- **Addresses limitations of LLMs:** LLMs have limitations in consistently adhering to safety standards and scaling up with complex constraints. The safety chip overcomes these challenges by using a formal language (LTL) for safety constraints.
- **Combines strengths of different paradigms:** The method combines the generality and expressiveness of natural language with the rigorousness of formal language.
- **Draws inspiration from runtime monitoring frameworks:** The approach to safety violation identification and constraint enforcement is inspired by runtime monitoring frameworks reliant on temporal logic specifications.
- **Utilizes reprompting:** The system uses reprompting to enable LLM-based agents to plan and avoid violating safety constraints.
- **Compared to other methods:** The "safety chip" significantly outperformed baselines, such as Base Model with NL Constraints and Code as Policies, in terms of safety rate, especially under a larger number of constraints.

---

## Main strategies used to obtain results

- **NL to LTL Translation:** Uses a modular framework to translate natural language constraints into LTL formulas. This translation relies on in-context learning and does not require fine-tuning.
- **Constraint Verification:** Relies on human experts to verify the correctness of the LTL formulas.
- **Action Pruning:** Enforces safety constraints by tracking the truth value of each proposition and pruning unsafe actions.
- **Reprompting with LLMs:** Uses a query system to provide feedback to the LLM agent regarding reasons for violation. This involves prompting the query system to reason over explanations for validation results and feeding the output to the LLM agent.
- **Experimental Evaluation:** Conducted experiments in VirtualHome and on a real robot to evaluate the system's performance. These experiments compared the safety chip to baseline methods in terms of success rate and safety rate.
