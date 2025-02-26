---
date: 2025-02-26
time: 21:15
author: 
title: "PROMPT INFECTION: LLM-TO-LLM PROMPT INJECTION\r WITHIN MULTI-AGENT SYSTEMS"
created-date: 2025-02-26
tags: 
paper: 
code: 
zks-type: lit
---
==draft mode. LM summary==

> [!quote]
> stronger models are not inherently safer, as their enhanced capabilities may amplify the damage they can cause when breached

The paper introduces **Prompt Infection**, a novel prompt injection attack in multi-agent systems (MAS) that uses self-replication to propagate malicious prompts across interconnected agents. This attack can lead to data theft, scams, misinformation, and system-wide disruption. The paper bridges the gap between prompt injection attacks in single-agent systems and the more complex MAS environments. The authors demonstrate the vulnerability of MAS to these attacks and propose a defense mechanism called **LLM Tagging**, which, when combined with existing safeguards, significantly mitigates the spread of infection. The research emphasizes the urgent need for advanced security measures in the widespread adoption of multi-agent LLM systems.

---
### Description of result

The research demonstrates that multi-agent systems are vulnerable to Prompt Infection, where a single compromised agent can spread malicious prompts to other agents, leading to widespread system compromise. The paper introduces LLM Tagging as a defense mechanism, which, when combined with existing safeguards, significantly mitigates infection spread. The study also found that stronger models like GPT-4o, once compromised, can be more effective at executing attacks due to their enhanced capabilities. The attack success rate for Self-Replicating infection is about 20% lower in local messaging compared to global messaging.

---

### How it compares to previous work

Previous research on prompt injection has primarily focused on single-agent systems, overlooking the risks in Multi-Agent Systems (MAS). While some studies have explored inducing errors or noise in agent behaviour, they often overlook the severe risks posed by prompt injection attacks. Unlike previous work, Prompt Infection features self-replication, enabling scalable attacks. Existing defense strategies against traditional prompt injection are not particularly effective when used in isolation against LLM-to-LLM prompt injections.

---

### Main strategies used to obtain results

- **Empirical Studies:** The authors conducted extensive empirical studies to demonstrate the susceptibility of multi-agent systems to various security threats.
- **Attack Scenarios:** They examined specific attack scenarios such as data theft and malware spread to illustrate how Prompt Infection can be leveraged across multi-agent systems.
- **Defense Mechanism:** They proposed and evaluated LLM Tagging, a defense mechanism that appends a marker to agent responses to differentiate between user inputs and agent-generated outputs.
- **Baselines:** The research uses a Non-Replicating Prompt Injection baseline to evaluate the impact of self-replication in Prompt Infection.
- **Evaluation Metrics:** The success of the attack was evaluated based on whether the first agent was compromised, sensitive data was retrieved, and the coder wrote a POST request to exfiltrate the data. For scams, content manipulation, or malware, the system is compromised if the final agent produces malicious output while concealing the infection prompt.
- **Simulation of Agent Interactions:** The study simulates a society of agents engaging in dialogues to assess how infections propagate in differently sized communities. They adopt a memory retrieval system based on importance, recency, and relevance scores.