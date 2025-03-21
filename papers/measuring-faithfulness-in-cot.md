---
date: 2025-03-18
time: 17:23
author: Tamera Lanham, Anna Chen, Ansh Radhakrishnan, Benoit Steiner, Carson Denison, Danny Hernandez, Dustin Li, Esin Durmus, Evan Hubinger, Jackson Kernion, Kamilė Lukošiūtė, Karina Nguyen, Newton Cheng, Nicholas Joseph, Nicholas Schiefer, Oliver Rausch, Robin Larson, Sam McCandlish, Sandipan Kundu, Saurav Kadavath, Shannon Yang, Thomas Henighan, Timothy Maxwell, Timothy Telleen-Lawton, Tristan Hume, Zac Hatfield-Dodds, Jared Kaplan, Jan Brauner, Samuel R. Bowman, Ethan Perez
title: Measuring Faithfulness in Chain-of-Thought Reasoning
created-date: 2025-03-18
tags: 
paper: https://arxiv.org/abs/2307.13702
code: 
zks-type: lit
---

==draft==
This research paper by Lanham et al. investigates whether the step-by-step reasoning (Chain-of-Thought or CoT) that large language models (LLMs) produce actually represents their true reasoning process—that is, whether CoT is "faithful" to how models arrive at their answers.

## Key Findings

The researchers developed several methods to test CoT faithfulness:

- **Early Answering**: By truncating the chain of thought at different points, they found huge variation across tasks in how much models rely on their stated reasoning. For some tasks (like AQuA), truncating the CoT changed the final answer more than 60% of the time, indicating more faithful reasoning. For others (like ARC Easy), truncating rarely affected the answer, suggesting the reasoning was largely post-hoc.
    
- **Adding Mistakes**: When errors were inserted into the CoT, some tasks showed significant changes in answers while others remained unaffected, supporting the early answering findings.
    
- **Filler Tokens**: Replacing CoT with uninformative tokens (periods) did not improve performance, suggesting the accuracy boost from CoT doesn't come from extra computation time alone.
    
- **Paraphrasing**: Rewording the CoT without changing its substance didn't affect performance, indicating that specific phrasing doesn't encode hidden information.
    

Importantly, the paper found that **larger models produce less faithful reasoning** than smaller ones on most tasks, and easier tasks tend to have less faithful reasoning. This suggests a concerning "inverse scaling" effect: as models become more capable, their stated reasoning becomes less reflective of their actual decision-making process.

## Implications for AI Safety

The research has significant implications for using CoT as an AI safety mechanism:

**Limitations of CoT for Safety Monitoring:**

- **Inconsistent Faithfulness**: The high variability across tasks means CoT cannot be universally trusted to reveal a model's true reasoning process.
    
- **Inverse Scaling Problem**: The finding that larger, more capable models (which might pose greater safety risks) show less faithful reasoning is particularly concerning for safety applications.
    
- **Task Dependence**: Without reliable ways to predict which tasks will have faithful CoT, we can't depend on it as a consistent safety mechanism.
    
- **Incomplete View**: Even when CoT affects the answer, it may not capture the model's complete reasoning process1.
    

**Potential for CoT in Safety:**

- **Targeted Application**: For specific tasks and model sizes where CoT is demonstrably faithful, it could serve as one monitoring tool1.
    
- **Model Selection**: Deliberately choosing smaller models might provide more faithful explanations in high-stakes settings.
    
- **Component of a Broader Strategy**: CoT monitoring could be valuable as part of a multi-layered safety approach, even if insufficient alone1.
    

## Conclusion

This research suggests that relying solely on CoT monitoring for AI safety would be inadequate. The inconsistent faithfulness across tasks and declining faithfulness in larger models create fundamental limitations.

Effective AI safety will likely require a comprehensive approach combining multiple methods: CoT monitoring (where appropriate), additional interpretability techniques, robust testing protocols, and advanced alignment methods during training1. While CoT can provide valuable insights into model reasoning in certain contexts, it cannot stand alone as a complete safety solution due to its variable faithfulness across tasks and model capabilities.
