---
date: 2025-03-02
time: 06:59
author: 
title: Do LLMs Really Think Step-by-step In Implicit Reasoning?
created-date: 2025-03-02
tags: 
paper: https://arxiv.org/abs/2411.15862
code: 
zks-type: lit
---
==draft==

### Summary of the Paper

The paper "Do LLMs Really Think Step-by-step In Implicit Reasoning?" investigates whether Large Language Models (LLMs) truly perform step-by-step reasoning in implicit Chain-of-Thought (CoT) as they do in explicit CoT. **Implicit CoT seeks to bypass the slower inference speeds and higher computational costs of explicit CoT by leveraging the model’s inherent reasoning capabilities without generating intermediate tokens**. The study probes the information of intermediate steps from the model’s hidden states when it is either trained or prompted to perform implicit CoT.

The key findings of the study are:

- **When prompted, LLMs hardly think about intermediate steps, suggesting they may just rely on experience rather than strict step-by-step reasoning**.
- **When trained, LLMs do calculate intermediate steps**.
- **The effect of using implicit CoT is susceptible to the format of the problem, reaffirming the current deficiency of implicit CoT**.
- **Implicit CoT can indeed simulate the behaviors of explicit CoT to some extent, but it cannot substitute explicit CoT, because its rationale is quite different and its efficacy in solving practical problems is still far from satisfactory**.

The authors used multi-step arithmetic problems to examine the implicit reasoning processes of LLMs, using a linear classifier to probe intermediate results from the hidden states of the models. They tested a generic model (Qwen2.5-72B-Instruct) and a model specifically trained for implicit CoT (a Mistral model). The problems were modified by reversing the order of equations and scaling the values to test the robustness of implicit CoT. The study highlights that while implicit CoT offers efficiency, its reliability and stability are questionable, and **explicit CoT remains essential for enhancing LLMs' ability on complex tasks**. The paper suggests that when users ask LLMs to give direct answers, they should be aware that the model may not have undergone a real reasoning process.

---

## Description of result

- When prompted to perform implicit Chain-of-Thought (CoT), Large Language Models (LLMs) hardly calculate intermediate results, especially with more steps, suggesting reliance on experience rather than step-by-step reasoning.
- When trained to perform implicit CoT, LLMs do calculate intermediate steps. The curve of each step starts to rise right after the curve of the previous step reaches a level, which is consistent with a natural CoT process.
- The efficacy of implicit CoT degrades severely with slight modifications to the problem format, whether the model is prompted or trained, suggesting it is faster but less reliable. Reversing the order of equations makes the model unable to calculate the intermediate results at all.

---

## How it compares to previous work

- Previous research has focused on knowledge-based problems to examine whether LLMs can recall their parametric knowledge during implicit reasoning, instead of investigating problems with more steps such as arithmetic.
- Some previous studies envisioned implicit reasoning as a substitute for explicit reasoning. This paper argues that implicit reasoning cannot be on par with explicit reasoning methods because it may not follow a step-by-step process in all problems.

---

## Main strategies used to obtain results

- The study uses multi-step arithmetic problems with only addition and subtraction to present the reasoning steps clearly.
- It leverages two models: Qwen2.5-72B-Instruct, a powerful generic model, and a special Mistral model trained by Internalizing CoT step by step.
- The models are prompted to give the answer directly without outputting steps.
- The hidden states associated with the final token of the given problem statement across layers are investigated.
- A simple linear classifier is employed to probe those intermediate results.

---

How CoT monitoring breaks down

The source provided focuses on the mechanics of implicit Chain-of-Thought (CoT) and does not directly address the broader questions of monitoring goals and beliefs, or potential breakdowns of CoT, ways to maintain its properties, or how to leverage it effectively. However, the paper's findings on the differences between explicit and implicit CoT, and the limitations of implicit CoT, offer insights that are relevant to your query.

Here's how the paper's findings relate to your questions:

- **Why Chain-of-Thought monitoring might break down:** The paper demonstrates that when LLMs are prompted to perform implicit CoT, they may not actually engage in step-by-step reasoning. Instead, they might rely on experience or pattern-matching to guess the answer. This suggests that **monitoring the "chain of thought" in implicit CoT could be misleading because there might not be a coherent chain of reasoning to monitor**. The model's internal processes may not reflect a logical progression towards the solution.
- **What can we do to keep this property?** The study indicates that training LLMs to internalise CoT step by step can lead to actual step-by-step reasoning. Therefore, **ensuring that LLMs are properly trained to perform genuine reasoning** is crucial for reliable CoT monitoring. However, the paper also shows that even with trained models, the efficacy of implicit CoT can be fragile and susceptible to changes in problem format. Thus, **explicit CoT may be more reliable**.
- **How can we leverage this property effectively?** Given the limitations of implicit CoT, **relying on explicit CoT**—where the model explicitly outputs the intermediate reasoning steps—may be a more effective way to understand the goals and beliefs of models/agents. Explicit CoT provides a clear chain of reasoning that can be monitored and analysed. The paper suggests that **explicit CoT remains essential for enhancing LLMs' ability on complex tasks**.

In summary, while the paper does not directly discuss monitoring goals and beliefs, it provides a cautionary tale about the reliability of implicit CoT and suggests that explicit CoT may be a more trustworthy approach for understanding the reasoning processes of LLMs.