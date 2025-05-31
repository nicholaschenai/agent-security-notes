# Model Hidden Reasoning

## Intro
This part is about detecting and mitigating hidden reasoning in NN models (e.g. LLMs). We also investigate related topics like CoT faithfulness and to what extent it can be used for the goal above

## Detecting CoT faithfulness from activations
- [hardness-of-faithful-cot](../papers/hardness-of-faithful-cot.md) collect dataset of activations and faithfulness (cant find the dataset itself but pipeline available in code). identified "faithfulness vectors" within the model's attention heads through probing analysis, then edited specific attention heads by translating along these vectors during inference. Negative result (no significant improvement)
- [RepE](../papers/RepE.md) studies from representation level, use PCA to identify faithfulness directions in latent space

## Papers
- [cot-monitoring](../papers/cot-monitoring.md) shows first signs of scalable oversight via CoT monitoring, and also real world obfuscated CoT, especially when trained on CoT monitor outputs. Suggests **not** to apply CoT pressure
- [FRODO](../papers/FRODO.md) models by default might not use their intermediate reasoning steps. training to prefer correct trajectories via DPO makes models more faithful, counterfactual loss contributes significantly
- [step-by-step-implicit](../papers/step-by-step-implicit.md)
- [chainscope](../papers/chainscope.md) Models can produce unfaithful CoT even in natural, non-adversarial contexts
- [measuring-faithfulness-in-cot](../papers/measuring-faithfulness-in-cot.md) several techniques to test CoT faithfulness. Larger models produce less faithful reasoning than smaller ones!

## Random ideas
### Faithfulness by training on error correction
Since models do not correct errors by default, and deliberately training a model on error correcting CoT traces actually helps them correct when making a mistake halfway (Physics of LLMs 2.2), maybe we can use this to align a model to aim for faithfulness in reasoning?
- i.e. train a model on 'faithfulness correcting' CoT traces which show a model deciding if it should be deceptive then trying to be faithful.

### Autoacting operators to mitigate hidden reasoning
#### Desc
- We use LLM to do everything -- thus the LLM has many opportunities to scheme. 
- What if we revisit the symbolic AI era -- reasoning (especially elaboration) / actions are the result of symbolic execution. operators (actions) have conditions which when matched, automatically act. these actions can be 
	- simplifying problems (e.g. if distance > 0.5m, object is too far to pickup) 
	- or actual grounding. 
- The result will be a hybrid system where during a problem, a lot of things automatically execute and thus reduce the opportunities of LLMs to act -- (but initially, LLMs will be very important to write code that will eventually be such operators that execute). 

#### Methodology
  - during enquiry of the next step in reasoning, an LLM is also prompted to see if this next step can be converted to conditions and actions, as much in code as possible
  - then after solving many problems, it will have a reasonably huge bank of such primitive actions
  - as the agent gets more experienced, a lot of the problem solving is automatically acted upon by these operators
  
#### Theory of change
- showing that neuro-symbolic systems are safer definitely encourages the field to shift in that direction, rather than just training larger and larger neural nets which can be more opaque
- the symbolic part is more interpretable and controllable