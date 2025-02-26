---
date: 2025-02-26
time: 18:00
author: 
title: "Towards Guaranteed Safe AI:\r A Framework for Ensuring Robust and Reliable AI Systems"
created-date: 2025-02-26
tags: 
paper: 
code: 
zks-type: lit
---
==draft mode via LM summary==


**General Summary:** The "Towards Guaranteed Safe AI" paper introduces a framework for creating AI systems with high-assurance quantitative safety guarantees, termed Guaranteed Safe (GS) AI. This approach uses a combination of a **world model**, a **safety specification**, and a **verifier** to ensure AI systems reliably avoid harmful behaviours. The paper argues for the necessity of this approach and its superiority over other AI safety methods that rely on empirical evaluations and informal arguments. It details the core components of GS AI, discusses the challenges in implementing them, and suggests potential solutions. The authors also provide examples of how GS AI can be applied to practical problems, such as autonomous vehicles and medical diagnosis. The paper emphasizes that creating safe AI systems is both a technical and a societal problem, while primarily focusing on the technical aspects.

---

## Description of result

The paper defines and introduces **Guaranteed Safe (GS) AI** as a family of approaches to AI safety, aiming to equip AI systems with high-assurance quantitative safety guarantees. This involves creating AI systems that reliably and robustly avoid harmful or dangerous behaviours. The core components of GS AI are:

- **World Model:** A mathematical description of how the AI system affects the outside world, handling both Bayesian and Knightian uncertainty.
- **Safety Specification:** A mathematical description of acceptable effects or behaviours for the AI system.
- **Verifier:** Provides an auditable proof certificate that the AI satisfies the safety specification relative to the world model.

The paper suggests that GS AI offers a more robust approach to AI safety compared to methods relying solely on empirical evaluations.

---

## How it compares to previous work

The GS AI approach is contrasted with existing AI safety practices that primarily rely on quality assurance (evaluations) to determine if an AI system is safe. The paper argues that these methods are insufficient for safety-critical applications because they do not provide rigorous, quantifiable safety guarantees. GS AI aims to provide a positive safety case with quantifiable guarantees, using empirical and theoretical arguments. It also differs from "AI boxing" methods, where the AI's ability to affect the world is limited by restricting interaction channels, while GS AI uses formal verification of the AI's output as the "gate".

---

## Main strategies used to obtain results

The paper uses the following strategies to define and support the GS AI framework:

- **Defining Core Components:** Clearly defines the three core components of GS AI: world model, safety specification, and verifier, detailing their roles and requirements.
- **Addressing Challenges:** Discusses the main challenges in creating each component, such as handling uncertainty in world models and formalizing safety specifications.
- **Suggesting Solutions:** Proposes potential solutions and research directions for overcoming these challenges, including using machine learning to generate world models and formal verification techniques.
- **Providing Examples:** Offers concrete examples of practical problems and how they can be solved using a GS AI approach, illustrating the application of the framework.
- **Comparing to Alternatives:** Contrasts GS AI with other AI safety methods, highlighting its advantages in providing high-assurance quantitative safety guarantees.
- **Mapping Approaches to Safety Levels:** Projects different approaches for building world models and creating safety specifications onto a spectrum based on how much safety they would grant if successfully implemented.