# Model Hidden Reasoning

## Intro
This part is about detecting and mitigating hidden reasoning in NN models (e.g. LLMs). We also investigate related topics like CoT faithfulness and to what extent it can be used for the goal above

## Detecting CoT faithfulness from activations
- [hardness-of-faithful-cot](../papers/hardness-of-faithful-cot.md) collect dataset of activations and faithfulness (cant find the dataset itself but pipeline available in code). identified "faithfulness vectors" within the model's attention heads through probing analysis, then edited specific attention heads by translating along these vectors during inference. Negative result (no significant improvement)
- [RepE](../papers/RepE.md) studies from representation level, use PCA to identify faithfulness directions in latent space

## Papers
- [cot-monitoring](../papers/cot-monitoring.md) shows first signs of scalable oversight via CoT monitoring, and also real world obfuscated CoT, especially when trained on CoT monitor outputs. Suggests **not** to apply CoT pressure
- [FRODO](../papers/FRODO.md) training to prefer correct trajectories via DPO makes models more faithful, counterfactual loss contributes significantly
- [step-by-step-implicit](../papers/step-by-step-implicit.md)
- [chainscope](../papers/chainscope.md) Models can produce unfaithful CoT even in natural, non-adversarial contexts
- [measuring-faithfulness-in-cot](../papers/measuring-faithfulness-in-cot.md) several techniques to test CoT faithfulness. Larger models produce less faithful reasoning than smaller ones!