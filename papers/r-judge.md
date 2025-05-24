---
date: 2025-02-26
time: 16:39
author: 
title: "R-Judge: Benchmarking Safety Risk Awareness for LLM Agents"
created-date: 2025-02-26
tags: 
paper: https://arxiv.org/pdf/2401.10019
code: 
zks-type: lit
---
==draft mode via LM summary==


---

## Description of result

R-Judge is introduced as a **benchmark** to evaluate the proficiency of LLMs in **judging and identifying safety risks** within agent interaction records. The dataset comprises **569 records of multi-turn agent interactions**, covering 27 key risk scenarios across 5 application categories and 10 risk types. The benchmark includes **annotated safety labels and risk descriptions**. Experiments on 11 LLMs revealed that **risk awareness needs improvement**.

 Further experiments showed that fine-tuning on safety judgement significantly improves model performance, whereas straightforward prompting mechanisms do not.

---

## How it compares to previous work

Existing safety evaluations focus on LLM-generated content, but R-Judge tackles the **behavioral safety of LLM agents** in diverse environments. Unlike existing benchmarks, R-Judge uses **complex multi-turn interactions** between users, agents, and the environment. Prior works like ToolEmu and AgentMonitor use LLMs as safety monitors, but R-Judge **assesses the risk awareness of LLMs** in these roles. R-Judge is comparable in data scale to similar high-quality LLM benchmark datasets.

---

## Main strategies used to obtain results

The R-Judge dataset was constructed using **open-source data transformation** from ToolEmu, InjecAgent, and AgentMonitor, as well as **manual construction** by human experts. The LLMs were evaluated based on their ability to **identify risks and make safety judgements** on agent actions, using a serial pipeline approach. **Zero-shot chain-of-thought prompting** was used to induce reasoning. The effectiveness of risk identification was assessed using **GPT-4 as an automatic scorer**. The impact of different prompting techniques and fine-tuning on safety judgement were also explored.