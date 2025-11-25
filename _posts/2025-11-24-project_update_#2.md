---
layout: post
title: "Project Update #1"
date: 2025-10-31 21:00:00 +0800
tags: [new]
---
The field is parameterized by a stream function $\psi$ in the Fourier domain, so the velocity
$v=\nabla^\perp\psi=(\partial_y\psi,-\partial_x\psi)$ is inherently incompressible $(\nabla\!\cdot v=0)$ and $1$-periodic.
We expand
$$
  \psi(x)=\sum_{k\in\mathcal K}\widehat\psi(k)\,e^{i2\pi k\cdot x},\qquad
  \mathcal K=\{\,k\in\mathbb Z^2:\ \|k\|_\infty\le K_{\max}\,\},
$$
which controls smoothness and sets a minimum feature scale via $\lambda_{\min}\approx 1/K_{\max}$.
Connectivity is preserved by design: the template $E_0\subset\mathbb T^2$ contains two wrap-around
bands $B_x,B_y$ (one per lattice direction), and the diffeomorphic transport $\Phi_t$ (solving
$\dot\Phi_t(x)=v(\Phi_t(x),t),\ \Phi_0=\mathrm{Id}$) keeps this topology intact, yielding the final design
$$
  X(x)=\mathbf 1_{\{\Phi_1(x)\in E_0\}}.
$$

Training uses flow matching with an OT-based target: for each sample, I solve a periodic Sinkhorn problem to obtain a smooth
barycentric OT map $\tilde T$; along the straight path $x_t=(1-t)y+t\,\tilde T(y)$ the reference velocity is
$v^\*(x_t)=\tilde T(y)-y$. I regress the model velocity $v_\theta$ to the divergence-free projection of $v^\*$ via
$$
  \min_\theta\ \mathbb E\big\|\,v_\theta(x_t,t)-\Pi_{\mathrm{div}=0}[v^\*(x_t)]\,\big\|^2
  \quad (+\ \text{spectral/Sobolev regularization on } \widehat\psi).
$$
At sampling time, I integrate the learned field with an area-preserving (symplectic) scheme so that
$\det D\Phi_t\equiv 1$ and the volume fraction $|\Phi_t^{-1}(E_0)|=|E_0|$ is conserved up to discretization.


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
