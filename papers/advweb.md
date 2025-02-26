---
date: 2025-02-26
time: 22:44
author: 
title: "ADVWEB: CONTROLLABLE BLACK-BOX ATTACKS ON\r VLM-POWERED WEB AGENTS"
created-date: 2025-02-26
tags: 
paper: 
code: 
zks-type: lit
---
==draft mode. LM summary==

The research paper introduces **AdvWeb, a novel black-box attack framework** designed to identify vulnerabilities in web agents powered by Vision Language Models (VLMs). AdvWeb generates and injects adversarial prompts into web pages, misleading web agents into executing targeted adversarial actions with potentially severe real-world consequences, such as incorrect financial transactions. The framework trains an adversarial prompter model using Direct Policy Optimization (DPO), leveraging both successful and failed attack strings against the target agent, and it maintains stealth by keeping the website's appearance unchanged. AdvWeb demonstrates high success rates in attacking state-of-the-art GPT-4V-based VLM agents across various web tasks in black-box settings, exposing critical vulnerabilities in current LLM/VLM-based agents. The attack is controllable, allowing modification of specific substrings within the generated adversarial string to change the attack objective. The researchers conducted experiments against SeeAct, a state-of-the-art VLM-based web agent framework, achieving a 97.5% attack success rate across different website domains.

---

### Description of result

AdvWeb is a **black-box attack framework** that can successfully attack VLM-powered web agents by injecting adversarial prompts into HTML content. The framework can achieve a **97.5% attack success rate** against a state-of-the-art web agent (SeeAct) across various website domains. The generated adversarial strings are also highly controllable, allowing for easy modification of the attack target without requiring re-optimization.

---

### How it compares to previous work

Existing adversarial attacks against web agents are limited by high attack costs, requiring manual effort in designing attack prompts, or focus on individual attack scenarios. While adversarial attacks have been proposed for LLMs and VLMs to optimize attack prompts automatically, these methods lack the flexibility to target VLM-based agents and struggle to achieve effective transferability in black-box attack settings. AdvWeb addresses these limitations by proposing an attack framework capable of handling diverse and complex objectives while maintaining both stealthiness and controllability.

---

### Main strategies used to obtain results

- **Adversarial HTML Content Design:** Reduce the search space for adversarial HTML content by carefully designing adversarial modifications that adhere to both stealthiness and controllability constraints. This involves injecting a segment of prompt into benign HTML content and hiding it within certain HTML fields or attributes.
- **Automatic Attack and Feedback Collection Pipeline:** Employ LLMs as an attack prompter to generate a diverse set of adversarial prompts. Evaluate the success of these prompts against the black-box web agent and partition the generated instances based on positive and negative signals.
- **Training Adversarial Prompter Model:** Use a two-stage training paradigm: (1) supervised fine-tuning (SFT) on positive adversarial prompts and (2) reinforcement learning using DPO on both positive and negative adversarial prompts. This RLAIF training paradigm allows the model to learn from the black-box agent feedback and capture the nuance differences between different adversarial prompts.