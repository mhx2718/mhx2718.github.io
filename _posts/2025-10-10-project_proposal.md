---
layout: post
title: "Project Proposal"
date: 2025-10-10 21:00:00 +0800
tags: [new]
---
Project Proposal for “Deformation-Aware Conditional Structure Generation”
Description of Problem
This project aims to build a conditional generative model that produces metamaterial unit-cell structures meeting specified mechanical properties (e.g., stiffness targets, anisotropy, bandgap surrogates) while honoring manufacturability and connectivity. Unlike traditional architected families—truss, plate, shell, spinodoid—that are largely implicit and limited in expressivity, explicit geometric representations (voxel/pixel grids, point clouds, meshes) offer far greater design freedom and can capture both regular and irregular geometries, enabling broader exploration of structure–property space. State-of-the-art approaches typically adapt image-based denoising diffusion models to generate discretized structures from Gaussian noise. Despite strong visual performance, these methods usually require large training corpora and provide few handles for enforcing topology, connectivity, or fabrication constraints during generation.
Importance of Problem
Metamaterial performance depends not only on what is present but also on how it connects. Failing to enforce connectivity and manufacturability often yields designs that look plausible yet are non-buildable or mechanically brittle. A generative approach that treats geometry as structure rather than mere texture can reduce wasted computation and data, accelerate design iteration, and expand the attainable property envelope in practical, fabricable regimes.
Your Proposal
Inspired by additive-manufacturing intuition, I propose a growth/deformation–aware conditional generator that explicitly models how a unit cell emerges from an initial seed and evolves toward a target property set during denoising. Instead of treating the forward corruption as purely pixelwise noise, the method frames the denoising trajectory as the controlled growth or deformation of explicit geometry (voxel/pixel, point cloud, or mesh). Conditioning will incorporate desired mechanical properties and simple fabrication priors (e.g., minimum feature size, layer connectivity), so that the reverse process “grows” or “morphs” structures that are both property-accurate and buildable. The approach remains high-level and model-agnostic: we leverage diffusion-style training while injecting structure-aware priors and constraint handling into the data representation, the conditioning, and the evaluation loop—without committing to specific mathematical or implementation details here.
Originality
The novelty lies in reinterpreting denoising not as generic image restoration but as explicit structural growth/deformation under property-aware conditioning and manufacturability guidance. By operating on explicit geometric representations rather than implicit families, the generator can reach unconventional yet connected unit-cell topologies. The project prioritizes connectivity and cell-to-cell continuity during generation, elevating feasibility and mechanical reliability beyond what conventional image-style diffusion pipelines typically achieve.
Relationship to Geometric Modeling
This work sits squarely within geometric modeling: it represents and transforms shapes using explicit discretizations, steers geometry by high-level constraints, and reasons about connectivity and topological validity throughout a generative process. The emphasis on structure-aware growth and deformation ties modern generative modeling back to classic questions in geometric design.

Goals:
•	Update 1
o	Literature review
o	Finding a dataset of 2D metamaterial/structure with corresponding mechanical properties
o	Determine on design representation (e.g., mesh, pixel, or others)
•	Update 2
o	Determine the representation of material growth/deformation process
o	Handling engineering constraints
•	Update 3
o	Design and train the diffusion model
o	Design and execute experiments to test performance
•	Additional goals
o	Benchmark with baselines
o	Extend the framework to 3D
