---
layout: post
title: "Project Proposal"
date: 2025-10-10 21:00:00 +0800
tags: [new]
---
Project Proposal for "Deformation-Aware Mechanical Structure Generation"

This project aims to build a conditional generative model that produces metamaterial unit-cell structures meeting specified mechanical properties (e.g., stiffness targets, anisotropy, bandgap surrogates) while reserving manufacturability and connectivity. Unlike traditional architected families—truss, plate, shell, spinodoid—that are largely implicit and limited in expressivity, explicit geometric representations (e.g., voxel/pixel grids, point clouds, meshes) offer greater design freedom and can capture both regular and irregular geometries, enabling broader exploration of structure–property space. State-of-the-art approaches typically adapt image-based denoising diffusion models to generate discretized structures from Gaussian noise. Despite strong visual performance, these methods usually require large training corpora and hardly handle topology, connectivity, or fabrication constraints during generation.

Metamaterial performance depends not only on what is present but also on how it connects. Denoising diffusion probabilistic models (DDPMs) were originally developed for 2D image synthesis; this design is counterintuitive for mechanical structures, which are more naturally described by simpler, often binary patterns and require explicit topological constraints during generation. Failing to enforce connectivity and manufacturability often yields designs that look plausible yet are non-buildable or mechanically brittle. A generative approach that treats geometry as structure rather than mere texture therefore has the potential to reduce data and computation overhead. Inspired by additive-manufacturing intuition, I propose a deformation–aware mechanical structure generator that explicitly models how a unit cell emerges from an initial shape and evolves toward a structure displaying target properties during denoising. Instead of treating the forward corruption as purely pixelwise noise, the method is expected to frame the denoising trajectory as the controlled growth or deformation of explicit geometry (voxel/pixel, point cloud, or mesh). Conditioning will incorporate desired mechanical properties, volume fabrication priors, so that the reverse process “grows” or “morphs” structures that are both property-accurate and buildable.

The novelty lies in reinterpreting denoising not as generic image restoration but as explicit structural deformation under property-aware conditioning and manufacturability guidance. By operating on explicit geometric representations and deformations, the generator is expected to learn from the data more efficiently, facilitating the enforcement of feasibility constraints beyond what conventional image-style diffusion pipelines typically achieve. Finally, by observing the evolving process, a certain level of interpretability is expected to be obtained.

# Goals

- **Update 1**
  - Literature review
  - Finding a dataset of 2D metamaterial/structure with corresponding mechanical properties
  - Determine design representation (e.g., mesh, pixel, or others)

- **Update 2**
  - Determine the representation of material growth/deformation process
  - Handling engineering constraints

- **Update 3**
  - Design and train the diffusion model
  - Design and execute experiments to test performance

- **Additional goals**
  - Benchmark with baselines
  - Extend the framework to 3D
