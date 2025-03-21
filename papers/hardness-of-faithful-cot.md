---
author: Dan Ley, Sree Harsha Tanneru, Chirag Agarwal, Himabindu Lakkaraju
title: On the Hardness of Faithful Chain-of-Thought Reasoning in Large Language Models
tags:
  - chain-of-thought
  - faithfulness
  - large-language-models
  - reasoning
date: 2025-03-18
time: 17:12
created-date: 2025-03-18
paper: https://openreview.net/forum?id=1OyE9IK0kx
code: in supplemental info
zks-type: lit
---
==draft==


## Description of result

- This research investigates the challenge of eliciting faithful Chain-of-Thought (CoT) reasoning from Large Language Models (LLMs). 
- The study explores three common approaches to improve faithfulness: 
	- in-context learning, 
	- fine-tuning, 
	- activation editing. 
- Despite implementing novel strategies within each approach, the researchers found limited success in consistently enhancing the faithfulness of CoT reasoning across diverse datasets and LLMs. 
- The results reveal a trade-off between accuracy and faithfulness, with more accurate LLMs (like GPT-4) often demonstrating lower faithfulness in their reasoning processes. 
- While some strategies showed marginal improvements in controlled scenarios, these gains failed to generalize well across different reasoning tasks and benchmarks. 
- The study concludes that eliciting faithful reasoning from LLMs is **inherently difficult**, suggesting that **current techniques are insufficient** for addressing this complex challenge.

---
## How it compares to previous work

- This work builds upon previous research that identified the problem of unfaithful CoT reasoning in LLMs. 
- While prior studies like Turpin et al. and Lanham et al. [measuring-faithfulness-in-cot](measuring-faithfulness-in-cot.md) focused on measuring and demonstrating the lack of faithfulness in LLM-generated explanations, this research takes the next step by systematically exploring potential solutions. 
- Unlike previous works that aimed to improve CoT quality in terms of human understanding or knowledge alignment, this study specifically targets faithfulness - ensuring that explanations accurately reflect the model's internal reasoning process. 
- The authors note that while activation editing, fine-tuning, and in-context learning have been successfully applied to other LLM challenges (like reducing biases and hallucinations), their application to improving CoT faithfulness represents a novel contribution to the field.

---
## Main strategies used to obtain results

The researchers employed three distinct approaches to improve CoT faithfulness: ICL, SFT and activation editing

### ICL
**In-context learning strategies**: They developed various sampling techniques (Deterministic Uniform, Deterministic Faithful, Stochastic Uniform, and Stochastic Faithful) to select examples of faithful reasoning to include in prompts during inference. These strategies were tested with different LLMs (GPT-4, GPT-3.5-Turbo, and LLAMA-3-8b-Instruct) across multiple reasoning datasets.

### SFT
**Fine-tuning strategies**: Using Parameter-Efficient Fine-Tuning (PEFT) and Low-Rank Adaptation (LoRA), they fine-tuned models on datasets containing examples of faithful reasoning, selected through similar sampling strategies as used in the in-context learning approach.

### Activation editing
identified "faithfulness vectors" within the model's attention heads through probing analysis, then edited specific attention heads by translating along these vectors during inference.



The technique involves two key steps:

1. **Probing Analysis**: First, the researchers identify "faithfulness vectors" within the model's attention heads through probing analysis. They create a dataset of questions with corresponding intermediate activations at all layers and attention heads in the LLM. For each attention head and layer, they train a logistic regression classifier to predict the faithfulness of reasoning generated for each question. This allows them to identify which attention heads encode more information about faithful CoT reasoning.
    
2. **Activation Editing**: Once the faithfulness vectors are identified, they edit specific attention heads by translating along these identified vectors during inference. The parameters of the linear probe classifier indicate the direction in which faithful and unfaithful reasoning are maximally separable. The researchers translate in this direction using the formula:
    
$$
\text{Attention}(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V + \alpha \cdot \frac{\theta_{hl}}{\sigma_{hl}}
$$

Where:

- $\theta_{hl}$ represents the learned parameters from the linear probe at layer $l$ and attention head $h$
    
- $\sigma_{hl}$ is a scaling factor representing the standard deviation of projections of activations in the direction of $\theta_{hl}$
    
- $\alpha$ is a hyperparameter to control the strength of intervention
    

#### Implementation Details

To avoid causing out-of-distribution inputs for subsequent layers, the researchers do not translate the activations of all attention heads. Instead, they focus on the top-K heads ranked by the faithfulness metric, thereby intervening on the LLM's behavior in a minimally invasive manner.

#### Results of the Technique

Despite its theoretical promise, the activation editing approach showed limited success in improving the faithfulness of CoT reasoning. The researchers found that:

1. Intervening on attention heads led to a drop in accuracy with only marginal gains in faithfulness.
    
2. There was no significant improvement in both accuracy and faithfulness compared to zero-shot CoT performance.
    
3. The identified faithful attention heads, optimal intervention strength, and optimal number of intervened heads were not consistent across different datasets, highlighting the lack of generalization of this strategy.
    
4. The results demonstrated a trade-off between accuracy and faithfulness, where the configuration that produced the most faithful reasoning was not the same as the one that produced the most accurate reasoning.
    

This technique represents an innovative approach to improving CoT faithfulness, but the results underscore the inherent difficulty in eliciting faithful reasoning from LLMs through activation editing alone.



### Evaluation
The effectiveness of these strategies was evaluated using faithfulness metrics from Lanham et al., particularly the "early answering" metric, which measures whether truncating a CoT explanation causes the model to change its final response. The researchers conducted extensive experiments across three benchmark datasets: AQUA (algebraic word problems), LOGIQA (deductive reasoning), and TRUTHFULQA (factuality-based questions).

