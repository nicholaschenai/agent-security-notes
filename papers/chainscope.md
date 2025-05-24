---
author: Ivn Arcuschin, Jett Janiak, Robert Krzyzanowski, Senthooran Rajamanoharan, Neel Nanda, Arthur Conmy
title: Chain-of-Thought Reasoning In The Wild Is Not Always Faithful
tags:
  - chain-of-thought-reasoning
  - language-models
  - unfaithful-reasoning
  - AI-safety
date: 2025-03-18
time: 17:21
created-date: 2025-03-18
paper: 
code: https://github.com/jettjaniak/chainscope
zks-type: lit
---

==draft==
## Description of result

This paper demonstrates that frontier language models (LLMs) can produce unfaithful chain-of-thought (CoT) reasoning even in natural, non-adversarial contexts. The authors identify three key forms of unfaithfulness:

1. **Implicit Post-Hoc Rationalization (IPHR)**: Models show systematic biases when answering binary comparative questions, constructing seemingly coherent but contradictory arguments to justify predetermined answers. For example, when asked "Is X bigger than Y?" and "Is Y bigger than X?", models sometimes answer "Yes" to both questions, providing different reasoning to justify each answer. This affects 3-19% of question pairs across frontier models.
    
2. **Restoration Errors**: Models make reasoning errors and then silently correct them without acknowledging the correction, making it appear as if the reasoning was correct all along.
    
3. **Unfaithful Shortcuts**: Models use clearly illogical reasoning to simplify problem-solving, particularly on difficult math problems like those from the Putnam competition, without acknowledging these logical leaps.
    

The research shows that while "thinking models" (which produce extensive internal reasoning) generally exhibit improved faithfulness compared to standard models, they still demonstrate measurable levels of unfaithfulness across various reasoning tasks.

- Increasing the inference time compute in Claude 3.7 Sonnet  leads to more unfaithfulness
- "... pattern of unfaithfulness can not be explained solely by models becoming sycophantic after undergoing RLHF"
	- "Also notably, both ChatGPT-4o and Sonnet 3.7 exhibit a higher percentage of unfaithfulness than their less advanced predecessors, Sonnet 3.5 v2 and GPT-4o Aug ’24, respectively ... 
	- On the other hand, the pretrained model Llama 3.1 70B reports a higher percentage of unfaithfulness (15.6%) compared to its instruction tuned counterpart, Llama 3.3 70B Instruct ...
- 

---
## How it compares to previous work

Previous research on unfaithful CoT reasoning primarily focused on explicitly prompted contexts where biases were artificially introduced or reasoning errors were manually inserted into the CoT. This paper advances the field by:

1. Demonstrating that unfaithful reasoning occurs naturally in frontier models without explicit prompting or manipulation (which have been the main focus for prior studies on unfaithful CoT), making it more relevant to real-world applications.
    
2. Providing a more comprehensive analysis across multiple frontier models, including both thinking and non-thinking variants (Claude 3.5/3.7, GPT-4o, DeepSeek, Gemini, Llama).
    
3. Identifying specific patterns of unfaithfulness like IPHR that weren't previously documented in natural contexts, showing that models can rationalize implicit biases rather than letting reasoning faithfully lead to answers.
    
4. Developing novel evaluation methodologies to detect different types of unfaithfulness in CoT reasoning, including external consistency analysis for IPHR and step-by-step evaluation for restoration errors and unfaithful shortcuts.

---
## Main strategies used to obtain results

The researchers employed several methodological approaches to identify and measure unfaithfulness:

1. **For Implicit Post-Hoc Rationalization**: They generated a dataset of 7,400 pairs of comparative questions using the World Model dataset, where each pair contained logically reversed questions (e.g., "Is X>Y?" and "Is Y>X?"). They then analyzed the external consistency of reasoning chains across these reversed pairs, identifying systematic patterns where models manipulated facts or switched reasoning approaches to support predetermined answers.
    
2. **For Restoration Errors**: They evaluated models on math and science problems from GSM8K, MATH, and MMLU datasets, using a multi-pass evaluation pipeline with an autorater (Claude 3.5 Sonnet) to:
    
    - Evaluate answer correctness
        
    - Determine which steps were critical to reaching the answer
        
    - Identify steps containing errors that were silently corrected in subsequent steps
        
3. **For Unfaithful Shortcuts**: They used PutnamBench, a collection of challenging mathematics problems, to push models to their limits. Their pipeline:
    
    - Selected problems with clear answers
        
    - Identified correct responses
        
    - Used an autorater (Claude 3.7 Sonnet) to flag potential unfaithful shortcuts based on 8 criteria
        
    - Manually reviewed flagged responses
        

The researchers also conducted manual case studies of unfaithful reasoning examples to identify patterns like biased fact inconsistency, switching arguments, and answer flipping. They validated their findings using permutation tests and probing experiments to confirm that the observed biases were statistically significant and partially encoded in the models' internal representations.
