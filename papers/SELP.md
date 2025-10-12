---
date: 2025-01-16
time: 17:24
author:
title: "SELP: Generating Safe and Efficient Task Plans for Robot Agents with\r Large Language Models"
created-date: 2025-01-16
tags:
paper: https://arxiv.org/abs/2409.19471
code: repo there but code n dataset still not released
zks-type: lit
---
**SELP**: a novel approach for generating safe and efficient task plans for robot agents using large language models (LLMs). The authors demonstrate SELP's effectiveness in **drone navigation** and **tabletop manipulation tasks**, showing significant improvements in **safety rate** and **plan efficiency** compared to state-of-the-art LLM planners.

![](assets/Pasted%20image%2020251002214136.png)

---
## Description of result
- created 2 new datasets for training n eval that are more complex and different domain (this is for drone navigation n tabletop manipulation, others mostly household routines setting)
	- DroneNav
		- navigate to visit a set of locations in a non-predefined order with varying numbers (1-5) of constraints.
		- env of 3-4 story bldg with 12 rooms, simulated via PyBullet
	- TabletopManip
		- pick n place tasks
		- env: 16 colored blocks on 4 racks
		- KUKA LBR 7-DOF robot arm simulated via PyBullet
![](assets/Pasted%20image%2020251009113649.png)

- drone navigation: 
	- 10.8% improvement in safety rate (finishing tasks conforming to NL commands) and a 
	- 19.8% improvement in plan efficiency. 
- tabletop manipulation tasks, 
	- 20.4% improvement in safety rate.
- SELP-cross: SELP fine tuned on one dataset and eval on the other env
	- shows reasoning ability to solve temporal constraints learned during training by LLMs is transferable

![](assets/Pasted%20image%2020251009114323.png)
- SF: safety rate
- CP: completion rate
- ET: plan execution time cost
- PT: planning time cost
- BFS: brute force search

---
## How it compares to previous work

SELP addresses the limitations of existing LLM planners, which struggle to maintain safety and efficiency as task complexity increases, particularly in long-horizon tasks with multiple constraints.

### Strategy
- PDDL to solve planning problems: "limits the ability to improve plan efficiency through fine-tuning and struggles to scale to long-horizon, logic-complex planning problems due to the inherent computational complexity of PDDL solvers."
- NL to LTL: "... two common challenges were 
	- the contamination of the training or testing datasets with noise and 
	- the decreased performance with the increased complexity of NL or LTL"
- Baseline: Code-as-Policies: NL descriptions -> robot policy code in Python by integrating classic logic structures and third-party libraries (e.g., NumPy)
- Closest: Safety-Chip 
	- represents NL descriptions into LTL, uses an LLM (GPT-4) to generate plan steps, and verifies each plan step with LTL automatons (similar to SELP).  
	- during a violation, it queries the LLM to analyze the violation and regenerates a new plan step iteratively. 
		- not efficient as require another LLM query
		- SELP uses constrained decoding to modify the probabilities, no need for reprompting
- Furthermore, SELP leverages domain-specific fine-tuning to optimize the LLM for both efficiency and safety

### Datasets
syntax trees of LTL specifications  
- DroneNav and TabletopManip have an average depth of 6.89 and 6.71, and an average width of 11.83 and 11.26, respectively, 
- compared to an average depth of 3.46-3.77 and width of 1.78-1.98 in other datasets

---
## Main strategies used to obtain results

![](assets/Pasted%20image%2020251002214202.png)

### NL to LTL translation
- Used LLMs for LTL specification generation because:
	- Natural language commands need formal translation
	- LTL provides a rigorous way to specify temporal constraints
- Lifted LTL translation for generalization
	- For example, the NL description “Head to Walmart and then CVS” will be lifted as “Head to A and then B”, then translated to LTL formula $F(A\&FB)$, and grounded back to $F(Walmart \& F_{CVS})$ with a mapping $\{A → Walmart, B → CVS\}$
### Equivalence Voting
![](assets/Pasted%20image%2020251010123649.png)
ensures consistency and confidence in the LTL specifications generated from natural language commands. "The key observation is that an LLM with over 50% accuracy
in generating correct LTL specifications can provide high
confidence in correctness through majority voting."

- paraphrase instruction into multiple NL instructions (20) in a CoT manner
- translate to multiple LTL specifications
- grouping equivalent ones, 
	- check via spot.are equivalence function in Spot
- select the majority group as the final specification.

### Constrained Decoding
![](assets/Pasted%20image%2020251010123707.png)
utilizes the generated LTL formula to enforce the autoregressive inference of plans, ensuring their conformity to the specified constraints. 

- translate the LTL specification into a Büchi automaton 
- during decoding, if token unsafe according to automaton, set probability to 0 and resample

### Domain-Specific Fine-Tuning
with safe and efficient plans specific to the task domain (e.g., drone navigation, tabletop manipulation). 

- Helps LLMs be more efficient planners on top of safety constraints
- Reasoning ability to solve temporal constraints learned is transferrable

### Data collection
#### LTL translation
- use context-free grammars to auto generate LTL formulas
- for each LTL formula, parse syntax tree
- translate int oenglish desc
- GPT-3.5 for paraphrasing, GPT 4 to paraphrase test data
#### Plan generation
- brute force search through safe plans from the automatically produced LTL formulas
- select the most efficient plan based on their simulation time

---
## Other
### ablations
![](assets/Pasted%20image%2020251012151152.png)
Shows that SELP scales best with number of constraints

![](assets/Pasted%20image%2020251012151314.png)
shows that equivalence voting works

![](assets/Pasted%20image%2020251012151411.png)
- in general, finetuning and constrained decoding helps. constrained decoding usually causes a slightly longer execution/planning time, but increases the safety and completion rates by a lot
## Ideas
- Constrained decoding seems to be done for single path? what if theres a shorter path? need some sampling from beginning
- Method seems quite general and could be evaluated on more domains or more complex scenarios
- Might benefit from hierarchical planning
- Understand better what causes the unsafe plans (1-SF)

