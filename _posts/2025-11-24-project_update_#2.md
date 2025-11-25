---
layout: post
title: "Project Update #1"
date: 2025-10-31 21:00:00 +0800
tags: [new]
---
Since the proposal, I completed a literature review on generative methods for mechanical metamateri-
als and refined the problem framing accordingly. The review explores the structural representation
for metamaterials and contrasts topology optimization and evolutionary strategies with generative
models, including conditional GANs, VAEs, flow-based approaches, and diffusion models. It supports
a constraint-aware, diffusion-oriented pipeline on pixel-based structural design, when the target is a
nonlinear stress–strain response.

For data, I have selected a pixel-based 2D metamaterial dataset given by Bastek and Kochmann [2023].
This dataset pairs each unit-cell design with full-field mechanical responses evaluated over multiple
strain steps up to 20% compressive strain. This dataset is large-scale and crafted to capture complex
nonlinear effects such as contact and post-buckling. It aligns with my proposal’s requirements and
allows me to focus on model design and evaluation rather than data generation.
Given the dataset’s structure, I treat the structural representation as signed distance field (SDF) pixels
so that given a random topology as the initial “noise”, the diffusion model is scheduled to reconstruct
it toward a feasible structure guided by a target stress–strain curve. Specifically, I assume to employ
a transport/flow-matching formulation in SDF space that predicts a velocity field moving an initial
random field toward a manufacturable topology; this route can intuitively accommodate smoothness
and minimum-thickness priors. This is because, first, the smoothness can be controlled by adding a
regularization term for the curvature of the SDF interface; the minimum thickness constraint can be
guaranteed by comparing local distance to a user-defined minimum thickness; I did not think of a
good way to control the connectivity, but it will be interesting to further investigate it. I will start
with this SDF transport strategy and may consider other options if there are technical challenges.

My proposal listed three intermediate goals for this stage: completing the literature review, selecting a
dataset with paired 2D structures and mechanical responses, and determining a design representation.
The literature review is complete. The dataset has been chosen with a clear rationale based on scale,
format, and coverage of complex effects. The representation is also determined: SDF pixels with
continuous representations for constraint handling and smoothing.

### Plan for Completion
The overall objective remains unchanged: given a target stress–strain curve, generate a 2D pixelated
unit cell matching the target stress–strain response. Looking ahead to the next milestone, I will deter-
mine the representation of material growth/deformation during generation and integrate engineering
constraints. Concretely, I will formalize how the model encodes deformation-aware evolution across
denoising steps, preferably through a velocity field in SDF space that “moves” geometry toward
feasible designs, in parallel with feasibility and manufacturability requirements.

This is Update 1. I am on schedule relative to the proposal: the literature review is complete, the
dataset is selected, and a pixel-first representation is established with a clear path for constraint-
aware refinement. Update 2 will concentrate on formalizing deformation-aware representation
and integrating engineering constraints; Update 3 will deliver the trained diffusion system and the
experimental evaluation.

### References
- Jan-Hendrik Bastek and Dennis M Kochmann. Inverse design of nonlinear mechanical metamaterials via video denoising diffusion models. Nature Machine Intelligence, 5(12):1466–1475, 2023.
