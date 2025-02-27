---
date: 2025-01-16
time: 17:24
author: 
title: "SELP: Generating Safe and Efficient Task Plans for Robot Agents with\r Large Language Models"
created-date: 2025-01-16
tags: 
paper: https://arxiv.org/abs/2409.19471
code: 
zks-type: lit
---
==TODO: still in draft==
## Description of result
This paper presents **SELP**, a novel approach for generating safe and efficient task plans for robot agents using large language models (LLMs). The authors demonstrate SELP's effectiveness in **drone navigation** and **tabletop manipulation tasks**, showing significant improvements in **safety rate** and **plan efficiency** compared to state-of-the-art LLM planners. For drone navigation, SELP achieves a 10.8% improvement in safety rate and a 19.8% improvement in plan efficiency. In tabletop manipulation tasks, SELP achieves a 20.4% improvement in safety rate.

---
## How it compares to previous work
SELP addresses the limitations of existing LLM planners, which struggle to maintain safety and efficiency as task complexity increases, particularly in long-horizon tasks with multiple constraints. While previous approaches like Safety-Chip use LTL automata to monitor action sequences, SELP employs constrained decoding to directly modify the LLM's probability distribution, effectively pruning unsafe actions during plan generation. Furthermore, SELP leverages domain-specific fine-tuning to optimize the LLM for both efficiency and safety, addressing the potential conflict between these objectives.

---
## Main strategies used to obtain results
SELP incorporates three key strategies to achieve its results:

- **Equivalence Voting:** This mechanism ensures consistency and confidence in the LTL specifications generated from natural language commands. It involves generating multiple LTL formulas, grouping equivalent ones, and selecting the majority group as the final specification.
- **Constrained Decoding:** This technique utilizes the generated LTL formula to enforce the autoregressive inference of plans, ensuring their conformity to the specified constraints. It translates the LTL specification into a Büchi automaton that monitors the plan generation process and masks inconsistent tokens, forcing the LLM to resample until a safe plan is produced.
- **Domain-Specific Fine-Tuning:** SELP fine-tunes the LLM with safe and efficient plans specific to the task domain (e.g., drone navigation, tabletop manipulation). This customization enhances the LLM's ability to generate plans that are both safe and efficient within the given domain.

These three strategies work in conjunction to enable SELP to generate safe and efficient plans for robot agents, effectively handling complex and long-horizon tasks with multiple constraints.

---

**Why researchers made their decisions:**

- Used LLMs for LTL specification generation because:
	- Natural language commands need formal translation
	- LTL provides a rigorous way to specify temporal constraints
	- Multiple LTL formulas with voting increases reliability
- Implemented constrained decoding because:
	- Integrates safety constraints directly into the probability distribution n thus generation process
	- Previous works (Safety Chip) reprompts LM if action is unsafe, which is not efficient
- Added domain-specific fine-tuning because:
	- Helps LLMs be more efficient planners on top of safety constraints
	- Reasoning ability to solve temporal constraints learned is transferrable

## Ideas

- Method seems quite general and could be evaluated on more domains or more complex scenarios
- Might benefit from hierarchical planning
- Could add adversarial testing to see how robust the method is (could have errors in NL to LTL translation via LLM)