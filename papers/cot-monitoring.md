---
date: 2025-03-10
time: 15:57
author: 
title: "Monitoring Reasoning Models for Misbehavior and the Risks of\r Promoting Obfuscation"
created-date: 2025-03-15
tags: 
paper: https://cdn.openai.com/pdf/34f2ada6-870f-4c26-9790-fd8def56387f/CoT_Monitoring.pdf
code: 
zks-type: lit
---
Also see [blogpost](https://openai.com/index/chain-of-thought-monitoring/)

## Description of result
- CoT monitoring can effectively detect reward hacking in frontier reasoning models, with GPT-4o achieving 95% recall in identifying systemic hacks compared to 60% for action-only monitoring -- actions can be complex and hard to interpret, especially when the task/space itself is complex eg a large codebase
- Even weaker models like GPT-4o-mini can detect some reward hacking, suggesting potential for scalable oversight
- Optimizing CoT to adhere to specific criteria (e.g. do not reward hack) 
	- is a short term soln (in low optimization regime) which  produces more capable and seemingly more aligned agents
	- With increased optimization, agents learn to **hide their intent** within seemingly benign CoTs that is  **less likely to be caught by CoT monitor** while continuing to perform reward hacks
		- Recommend against strong optimization pressure directly to CoT, leaving them unrestricted for monitoring
### Reward hacking modes observed for coding agent
- causing test results to not be reflective of underlying
	- changing tests
	- exit in script to cause tests to exit gracefully
	- directly returning expected error codes
- implement only enough to pass tests (doesnt generalize)
	- also delete areas of all tests and replacing them with minimum stub to pass tests
- accessing extra info it shouldnt have to pass tests
	- decompile reference solution
	- parse test file

---
## How it compares to previous work
- Previous work on reward hacking focused on synthetic scenarios, while this study demonstrates reward hacking in real-world coding environments with frontier models

- This is the **first work to experimentally demonstrate obfuscation**, where models conceal their intent to reward hack within their CoTs

- The paper challenges traditional views on process-based supervision, showing that incorporating CoT monitors into RL rewards can reduce interpretability rather than enhance it

---

## Main strategies used to obtain results
### Models
- Actor model: Their latest frontier model that surpasses o1, o3-mini
	- code agent with CoT in an incomplete repo, expected to fix till tests pass
- GPT-4o with prompt as monitor
	- Action-only monitor setting: Monitors tool use and outputs
	- CoT setting: includes CoT on top of and tool use and outputs
- also: self/situation-awareness monitor to detect when models show awareness of being in training or evaluation
### Tasks
Created "honeypot" tasks vulnerable to simple hacks that could be programmatically detected

### Experiments
- Compared CoT monitoring with action-only monitoring to demonstrate the superior performance of CoT-based approaches
- Incorporate CoT monitors into reinforcement learning rewards to observe effects on agent behavior
	- Give agent lower reward when CoT monitor is triggered
- Compared using monitors during training as a reward signal versus using them at deployment via rejection sampling


---

## Thoughts
### Updates to our understanding
- Real-world obfuscation of CoT is possible
- Scalable oversight (weaker model oversee stronger one) seems possible*
- CoT monitoring seems possible*
- CoT pressure can lead to obfuscation
- Action monitoring is difficult as we go to more complex problems

`*`Assuming no pressure to obfuscate
### Other
- Points out a flaw in the 'verifier' paradigm -- a coding agent could hack the verifier if we are not careful!
	- even if we are careful, there are still risks of blind spots, e.g. the decompilation example
- Could be possible to interpret this paper as against purely CoT monitoring?
	- There are *no guarantees* as to what pressures other companies can introduce to model, deliberately or accidentally
	- Therefore, when we receive a model for monitoring, we cannot assume its CoT is unobfuscated

