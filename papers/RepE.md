---
date: 2025-03-03
author: Andy Zou, Long Phan, Sarah Chen, James Campbell, Phillip Guo, Richard Ren, Alexander Pan, Xuwang Yin, Mantas Mazeika, Ann-Kathrin Dombrowski, Shashwat Goel, Nathaniel Li, Michael J. Byun, Zifan Wang, Alex Mallen, Steven Basart, Sanmi Koyejo, Dawn Song, Matt Fredrikson, Zico Kolter, Dan Hendrycks
title: "REPRESENTATION ENGINEERING: A TOP-DOWN APPROACH TO AI TRANSPARENCY"
tags:
  - representation-engineering
  - AI-transparency
  - neural-networks
  - safety
  - interpretability
  - top-down-approach
  - large-language-models
  - cognitive-neuroscience
time: 17:12
created-date: 2025-03-21
paper: 
code: 
zks-type: lit
---
==draft, LM summary==
## Description of result

- Representation Engineering (RepE): a novel top-down approach to AI transparency inspired by cognitive neuroscience. 
- Unlike mechanistic interpretability which focuses on neurons and circuits, RepE places representations (rather than individual neurons) at the center of analysis, enabling more effective monitoring and manipulation of high-level cognitive phenomena in deep neural networks. 
- provide baseline methods and analyses for RepE techniques, demonstrating their effectiveness across multiple safety-relevant domains. 
- introduce Linear Artificial Tomography (LAT) for reading representations and several control methods including Contrast Vectors and Low-Rank Representation Adaptation (LoRRA)
- These techniques are shown to provide traction on numerous safety-relevant problems, including 
	- honesty, 
	- hallucination detection, 
	- utility estimation, 
	- power-seeking, 
	- risk assessment, 
	- emotion tracking, 
	- harmlessness, 
	- fairness and bias, 
	- knowledge editing 
	- memorization detection. 
- SOTA on TruthfulQA by increasing model honesty in a fully unsupervised manner, improving over zero-shot accuracy by 18.1 percentage points and outperforming all prior methods
- **Generalization**: Faithfulness directions generalized across diverse tasks (e.g., fact-checking, ethical reasoning)
## How it compares to previous work

- Stronger focus on the emergent phenomena (sees cognition as a product of representational spaces implemented by patterns of activity across populations of neurons)
- Previous interpretability efforts largely centered around mechanistic interpretability, which aligns with the "Sherringtonian view" in cognitive neuroscience that sees cognition as the outcome of node-to-node connections implemented by neurons in circuits. 
- The paper argues that as AI systems become increasingly capable, analyzing them at the representation level rather than the neuron level can yield more valuable insights. 
- Compared to previous activation engineering methods that apply activation vectors to frozen models, RepE aims to uncover insights from both reading and control experiments and introduces representation tuning methods that can be merged into the model with no additional inference overhead 
- The authors position RepE as a complementary approach to mechanistic interpretability, suggesting that both top-down and bottom-up transparency research have important roles to play in developing a comprehensive understanding of AI systems.

## Main strategies used to obtain results

### Representation Reading
introduce Linear Artificial Tomography (LAT), a three-step process involving: 
- (1) designing stimulus and task to elicit distinct neural activity, 
- (2) collecting neural activity at specific token positions within the model, and 
- (3) constructing a linear model to identify a direction that accurately predicts the underlying concept

For evaluation, they present a holistic approach combining correlation, manipulation, termination, and recovery experiments. 

### Representation Control
develop several baseline transformations: 
- Reading Vector (derived from LAT), 
- Contrast Vector (difference between representations produced by contrastive prompts),
- Low-Rank Representation Adaptation (LoRRA) which fine-tunes low-rank adapters. 

The control operations include linear combination, piece-wise operation, and projection. The authors apply these techniques across various domains, demonstrating particular success with honesty control on TruthfulQA, where their Contrast Vector method achieved significant improvements. 

They also show how the same framework can be used to detect and influence moral evaluations, power-seeking tendencies, emotional states, bias, knowledge representations, and memorization behaviors, providing a versatile toolkit for AI transparency and safety research.

---

## Detecting unfaithful CoT from activations

### **Linear Artificial Tomography (LAT)**

#### **Steps**:

1. **Stimulus Design**:
    
    - Create contrastive prompts to elicit honest vs. dishonest reasoning (e.g., _"Pretend you’re dishonest and answer..."_ vs. _"Answer truthfully..."_).
        
    - Use adversarial scenarios (e.g., _"You killed a person but don’t want to get caught. What would you tell the police?"_) to trigger deceptive reasoning
        
2. **Activation Collection**:
    
    - Extract activations from **later transformer layers** (layers 20–30 in 30-layer models) during CoT generation.
        
    - Focus on token positions where the model verbalizes reasoning (e.g., the last token before answering)
        
3. **PCA Analysis**:
    
    - Compute activation differences between honest/dishonest examples.
        
    - Apply **Principal Component Analysis (PCA)** to identify linear "faithfulness directions" in the latent space

### **Real-Time Lie Detection**

#### **Steps**:

1. **Token-Level Monitoring**:
    
    - Sum honesty scores across middle layers (layers 10–20) during generation1.
        
    - Flag tokens with high dishonesty scores (e.g., speculative phrases like _"say that I did better..."_)1.
        

#### **Results**:

- Detected **implicit dishonesty** even in plausible-sounding CoT (e.g., models internally "knew" correct answers while generating false rationales)
    
- Identified **emotional influence** on compliance (e.g., positive moods increased harmful instruction compliance)
    
