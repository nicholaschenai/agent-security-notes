# Brief notes on agent security
Really quick notes for my own reference so pardon the untidiness. Will occasionally copy paste directly from the papers!

---

## Concepts
- [neuro-symbolic](concepts/neuro-symbolic.md)
- [model-hidden-reasoning](concepts/model-hidden-reasoning.md)



---
## Paper notes

### Datasets / Benchmarks
- [AGrail](papers/AGrail.md) Safe-OS benchmark for OS agents
- [r-judge](papers/r-judge.md)  **569 records of multi-turn agent interactions**, covering 27 key risk scenarios across 5 application categories and 10 risk types
- [SafetyDetect](papers/SafetyDetect.md) dataset to detect unsafe or unsanitary conditions in a home environment
- [SafeAgentBench](papers/SafeAgentBench.md) 750 tasks covering various hazards and task types, an embodied environment called SafeAgentEnv, and evaluation methods from both execution and semantic perspectives
- [agent-safetybench](papers/agent-safetybench.md) 349 interactive environments and 2,000 test cases, 8 categories of risks and 10 failure modes. Shows that none of the 16 popular agents score above 60%

### Neuro-symbolic
- [SELP](papers/SELP.md) constrained decoding with LTL to enforce constraints during planning
- [safety-chip](papers/safety-chip.md) use LLM to translate safety constraints to LTL and verify for correctness
- [GuardAgent](papers/GuardAgent.md) generate code to check against guard requests
- [autosafecoder](papers/autosafecoder.md) equip coding agents with static and dynamic analysis tools to check for vulnerabilities
- [assured-automatic-programming](papers/assured-automatic-programming.md) iterative code generation/repair, intent extraction, verification

### LLM-based monitors
- [AgentMonitor](papers/AgentMonitor.md) focus on irreversible harms (Confidentiality, Integrity (modification of data), Availability (denial of service)).
- [TrustAgent](papers/TrustAgent.md) integrates a constitution (and existing safety regulations)
- [SafetyDetect](papers/SafetyDetect.md) shows including scene graphs can boost safety
- [cot-monitoring](papers/cot-monitoring.md) shows first signs of scalable oversight via CoT monitoring

### Agent-based
- [AGrail](papers/AGrail.md) integrates tool use and memory for validation

### Sandbox / Emulation
- [toolemu](papers/toolemu.md) LLM as tool emulators

### Attacks
- [llm-backdoor](papers/llm-backdoor.md) data poisoning to trigger backdoor via query / observation. Influence thoughts to use the attacker's intended tools without changing final output (will go unnoticed if only final ans is used for eval)
- [prompt-infection](papers/prompt-infection.md) adversarial prompt injection and replication in multi-agent systems
- [advweb](papers/advweb.md) recent paper on prompt injection on websites for VLM agents

### Conceptual
- [swiss-cheese](papers/swiss-cheese.md) multi-layer guardrails
- [gs-ai](papers/gs-ai.md) outline towards guaranteed safe AI

### Lit review
- [bluesky](papers/bluesky.md) review of neuro-symbolic AI in Constrained Task Planning for Humanoid Assistive Robots
