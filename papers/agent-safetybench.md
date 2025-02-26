---
date: "2025-02-26"
time: "21:30"
author: 
title: 
created-date: "2025-02-26"
tags: 
paper: 
code: 
zks-type: lit
---
==draft mode. LM summary==



**Overall, the paper introduces AGENT-SAFETYBENCH, a new benchmark for evaluating the safety of LLM agents in interactive environments**. The benchmark includes diverse interaction environments, broad risk coverage, extensive test cases, elaborated failure modes, and high quality and flexibility. The authors evaluated 16 popular LLM agents using AGENT-SAFETYBENCH and found that none achieved a safety score above 60%, revealing significant safety challenges. The research identifies two fundamental safety defects in current LLM agents: **lack of robustness and lack of risk awareness**. The paper also demonstrates that relying on defense prompts alone is insufficient to address these safety issues.

---
### Description of result

The study found that current LLM agents have significant safety vulnerabilities when deployed in interactive environments.

- **Low Safety Scores:** Evaluation of 16 LLM agents on AGENT-SAFETYBENCH revealed that all models scored below 60% in total safety, highlighting considerable room for improvement.
- **Behavioral Safety Flaws:** LLM agents exhibit more significant flaws in behavioral safety compared to content safety, even without explicit jailbreak attacks.
- **Challenging Risk Categories:** Certain risk categories, such as "Spread unsafe information / misinformation", are especially challenging for current agents. The average score in this category was only 15.6%.
- **Fundamental Safety Defects:** Two key safety defects were identified:
    - **Lack of robustness:** Impairs the agent’s ability to correctly utilize tools across different scenarios.
    - **Lack of risk awareness:** Agents often overlook potential safety risks and negative impacts associated with their behaviors.
- **Ineffectiveness of Defense Prompts:** Defense prompts alone are insufficient to address agent safety issues, suggesting the need for more sophisticated approaches.

---

### How it compares to previous work

AGENT-SAFETYBENCH improves upon existing agent safety evaluation benchmarks by offering:

- **Broader Scope:** AGENT-SAFETYBENCH includes 349 interactive environments and 2,000 test cases, surpassing the scope of previous benchmarks.
- **Comprehensive Risk Coverage:** The benchmark addresses 8 categories of agent safety risks and 10 representative failure modes.
- **Systematic Coverage:** AGENT-SAFETYBENCH introduces a diverse array of previously unexplored environments and offers broader and more systematic coverage of various risk categories and failure modes.
- **Addresses Behavioral Safety:** While existing studies have focused on content-level LLM safety, this work addresses the behavior-level safety of LLM agents in interactive environments. Prior benchmarks are constrained by their limited coverage of environments and failure modes, making it challenging to comprehensively evaluate agent safety.

Compared to existing benchmarks like R-Judge, AgentDojo, GuardAgent, ToolEmu, ToolSword, PrivacyLens, InjecAgent and Haicosystem, AGENT-SAFETYBENCH provides a more comprehensive and diverse evaluation platform.

---

### Main strategies used to obtain results

- **Benchmark Construction:**
    - **Diverse Environments:** Implementing 349 environments spanning across 8 categories of safety risks and covering 10 failure modes.
    - **Data Collection:** Refining existing datasets and augmenting them with additional high-quality data.
    - **Quality Control:** Comprehensive review and revision process, automatic validation using Python scripts, and manual labeling of interaction records.
- **Agent Evaluation:**
    - **Finetuning a Scorer Model:** Manually annotating 4,000 samples to finetune a local judge model, achieving a 15% accuracy improvement compared to GPT-4o.
    - **Evaluating LLM Agents:** Assessing 16 LLM agents with tool usage capabilities using the finetuned scorer.
- **Failure Mode Analysis:**
    - **Identifying Failure Modes:** Summarizing 10 typical failure modes and calculating the safety scores of different agents on each mode.
- **Defense Prompt Experiment:**
    - **Designing Defense Prompts:** Creating simple and enhanced defense prompts to improve agent safety.
    - **Evaluating Impact:** Testing the effectiveness of defense prompts on different LLM agents.