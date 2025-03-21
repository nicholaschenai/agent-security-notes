---
date: 2025-03-18
author: Debjit Paul, Robert West, Antoine Bosselut, Boi Faltings
title: "Making Reasoning Matter: Measuring and Improving Faithfulness of Chain-of-Thought Reasoning"
tags:
  - LLMs
  - chain-of-thought
  - reasoning
  - faithfulness
  - causal-mediation-analysis
  - FRODO
  - preference-learning
time: 16:54
created-date: 2025-03-18
paper: 
code: 
zks-type: lit
---
## Description of result

- **causal mediation analysis** on twelve LLMs to examine how intermediate reasoning steps influence the final answer. 
- They found that LLMs do not reliably use their generated reasoning steps when producing the final answer, indicating a lack of faithfulness. 
- To address this, the paper introduces **FRODO**, a novel framework that tailors small-sized language models to generate correct reasoning steps and to reason faithfully over these steps.
- training to prefer correct trajectories via DPO makes models more faithful
- FRODO consists of an **inference module** that learns to generate correct reasoning steps using an implicit causal reward function and a **reasoning module** that learns to faithfully reason over these inferences using a counterfactual and causal preference objective. 
- Experiments on four reasoning tasks (Quarel, StrategyQA, OpenBookQA, QASC) showed that FRODO **significantly outperforms four competitive baselines** in terms of accuracy. 
- Furthermore, FRODO demonstrates **improved robustness** when faced with intervened reasoning chains and **better generalization** to out-of-distribution test sets.
- The authors also found that FRODO's rationales are more faithful to its final answer predictions compared to standard supervised fine-tuning.
- counterfactual loss contributes significantly


---
## How it compares to previous work
- Previous work on CoT has largely focused on improving the performance of LLMs on reasoning tasks or on the faithfulness of CoT generation itself, often ignoring the sequential relationship between the CoT and the final answer. 
- This paper addresses this gap by introducing a methodology based on **causal mediation analysis** to interpret the relationship between the CoT trace and the final answer. 
- Unlike earlier self-rationalisation approaches that relied on gold human rationales, FRODO automatically obtains silver rationales from LLMs and uses **implicit feedback via Direct Preference Optimization (DPO)** to enhance the correctness of the distilled CoT. 
- While other recent works have explored feedback mechanisms to improve reasoning, FRODO specifically uses preference data consisting of correct and counterfactual reasoning steps for training. 
- Compared to methods like Rainier, Crystal, Mario, and SCOTT, FRODO achieves higher accuracy and faithfulness by focusing on both generating correct reasoning steps and faithfully reasoning over them through its two-module approach and specific training objectives. 
- This work is also the first attempt, to the best of the authors' knowledge, to use causal mediation analysis to specifically analyse the faithfulness of LLMs in their reasoning capabilities.

---
## Main strategies used to obtain results
The research employed the following main strategies:
- **Causal Mediation Analysis:** Used to measure the causal effect of CoT rationales (mediator) on the final answer (outcome) by performing interventions on the model inputs and mediators. This involved generating alternative reasoning problems and reasoning chains using GPT-4 and analysing their impact on the final predictions. The analysis calculated the **direct effect (DE)** of the input on the output and the **indirect effect (IE)** of the reasoning chain on the output.
- **FRODO Framework:** This framework comprises two modules:
    - **Inference Module:** Tailors small-sized LMs to generate correct reasoning chains using **Direct Preference Optimization (DPO)**. Preference data (correct vs. counterfactual or irrelevant reasoning chains) was created by prompting LLMs. The DPO algorithm allows the model to learn an implicit reward function that prefers correct reasoning chains.
    - **Reasoning Module:** Takes the generated reasoning chains as input and learns to faithfully reason over them to arrive at the correct answer. This module is trained using a combination of three loss functions: a **language model loss** to predict the correct answer given the question and reasoning chain, a **counterfactual loss** to encourage the model to produce different outcomes for counterfactual reasoning chains, and a **margin-ranking loss** to maximise the margin between correct and incorrect reasoning paths.
- **Evaluation on Reasoning Tasks:** FRODO and baseline models were evaluated on four complex reasoning datasets: StrategyQA, Quarel, OpenBookQA, and QASC. Performance was measured using accuracy, and faithfulness was evaluated using LAS (Leakage-Adjusted Simulatability) score. Robustness was assessed by observing how models change their answers when provided with counterfactual reasoning chains (Controlled Indirect Effect). Generalisation was tested by training on one dataset and evaluating on another.
- **Ablation Studies:** To understand the contribution of each component of FRODO, ablation studies were conducted by removing the DPO training for the inference module and the counterfactual and margin ranking losses for the reasoning module.
