---
date: 2025-02-26
time: 17:40
author: 
title: "Autosafecoder: A multi-agent framework for securing llm code generation through static analysis and fuzz testing"
created-date: 2025-02-26
tags: 
paper: 
code: 
zks-type: lit
---
==draft mode via LM summary==


## Description of result

AutoSafeCoder is a multi-agent framework that enhances code generation security through static and dynamic analysis. The system integrates three agents:

- **Coding Agent:** Generates and repairs code using a few-shot learning approach. It refines code based on feedback from other agents.
- **Static Analyser Agent:** Detects security vulnerabilities through static analysis, using the MITRE CWE database. It provides feedback to the Coding Agent for remediation.
- **Fuzzing Agent:** Generates diverse inputs for dynamic testing to identify runtime crashes and errors. It uses type-aware mutation to produce fuzzing inputs and reports issues to the Coding Agent.

The process involves iterative feedback loops between these agents, ensuring continuous improvement of code security. The Static Analyser Agent provides feedback until the code is deemed secure or after four communication rounds, and the fuzzing mutation loop runs for 150 iterations. Experiments demonstrate a 13% reduction in vulnerabilities compared to baseline LLMs.

---

## How it compares to previous work

Previous multi-agent code generation systems have primarily focused on the functionality of the generated code, often overlooking critical security aspects. While tools like VUDDY, MVP, and Movery identify vulnerable code clones, they generally overlook vulnerability repair. AutoSafeCoder differentiates itself by integrating static and dynamic analysis to ensure both functional correctness and security. Unlike VulRepair and AIBUGHUNTER, AutoSafeCoder incorporates dynamic execution-based techniques to assess the generated code's vulnerability. This comprehensive approach addresses both the identification and repair of vulnerabilities, maintaining high functionality while enhancing security.

---

## Main strategies used to obtain results

AutoSafeCoder employs several key strategies to achieve its results:

- **Multi-Agent Collaboration:** Utilising a system of three agents that communicate and provide feedback to each other iteratively to refine code.
- **Static and Dynamic Analysis Integration:** Combining static analysis to identify early coding flaws with dynamic analysis to detect runtime issues.
- **Few-Shot and In-Context Learning:** Applying these techniques within the LLM framework to enable agents to effectively identify vulnerabilities in a continuous feedback loop.
- **Type-Aware Mutation:** Using a mutation strategy based on the data type of each parameter to generate valid and effective fuzzing inputs.
- **Iterative Feedback Loops:** Allowing the Coding Agent to modify code based on feedback from the Static Analyser and Fuzzing Agents until vulnerabilities are resolved or a limit is reached.