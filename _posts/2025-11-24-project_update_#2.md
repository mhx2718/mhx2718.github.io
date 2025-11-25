---
layout: post
title: "Project Update #2"
date: 2025-11-24 21:00:00 +0800
tags: [new]
---
Since Update 1, I replaced the SDF-diffusion idea with a deformation-aware, flow-based model that better matches the constraints and periodicity of unit cells. More specifically, I work on the periodic cell and learn a velocity field whose flow transports a fixed, connected template mask into the final design. I switched to a flow-based framework over diffusion based on a paper by Lipman et al. 2023 [1]. This paper explores employing flow matching between noise and data, following paths defined by Optimal Transport (OT) displacement interpolation. I deemed this work as a reference for methodology because by regarding the material as a distribution, the generation of data from noise can be emulated by moving the original distribution to the target. Based on the paper, training a flow-based model can also provide faster training and sampling. 

The field is parameterized by a stream function $\psi$ in the Fourier domain, so the velocity
$v=\nabla^\perp\psi=(\partial_y\psi,-\partial_x\psi)$ is inherently incompressible $(\nabla\cdot v=0)$ and periodic.
We expand
$$
  \psi(x)=\sum_{k\in\mathcal K}\widehat\psi(k)\,e^{i2\pi k\cdot x},
  \mathcal K=\{\,k\in\mathbb Z^2:\ \|k\|_\infty\le K_{\max}\,\},
$$
which controls smoothness and sets a minimum feature scale via $\lambda_{\min}\approx 1/K_{\max}$.
Connectivity is preserved by design: the template $E_0\subset\mathbb T^2$ contains two wrap-around
bands (one per lattice direction) with specified topology, and then performs diffeomorphic transport by solving
$\dot\Phi_t(x)=v(\Phi_t(x),t),\ \Phi_0=\mathrm{Id}$ to keeps this topology intact.

Training uses flow matching with an OT-based target: for each sample I can solve for the OT path between the template and the design (this process may take some time), $\tilde T$. Along the straight path $x_t=(1-t)y+t\,\tilde T(y)$ the reference velocity is
$v^\*(x_t)=\tilde T(y)-y$. I regress the model velocity $v_\theta$ to the divergence-free projection of $v^\*$ via
$$
  \min_\theta\ \mathbb E\big\|\,v_\theta(x_t,t)-\Pi_{\mathrm{div}=0}[v^{\*}(x_t)]\,\big\|^2.
$$
At sampling time, I plan to integrate the learned field with an area-preserving scheme so that
$\det D\Phi_t\equiv 1$ and the volume fraction $|\Phi_t^{-1}(E_0)|=|E_0|$ is conserved up to discretization.

For data, I switched to the dataset provided in the paper by Liu et al. 2025 [2]. This paper uses a signed distance function (SDF) representation coupled with a denoising diffusion model to generate metamaterial structures conditioned on a target nonlinear stress-strain response. Based on my best knowledge, this is the only dataset available for pixel structure representation using an asymmetric field, whereas most of the work generates structures by sampling a quarter of the mask and fabricating the whole unit cell lattice by mirroring in both vertical and horizontal directions to ensure periodicity. Adding on that they considered various nonlinear responses to account for large deformation, buckling, and frictional contact, I believe this is a dataset of high quality to test my model upon.

Looking ahead to completion, I will need to first finalize the deformation encoding—specifying the band limit, regularization strategy, specifying the sampling process to keep the template at the target volume fraction, and then train the conditional flow-matching model on the new dataset. This change in methodology and data makes the original plan for Update 3 less certain, due to the heavier data preprocessing and more complex model configuration required. If the process proceeds smoothly, evaluation will focus on response matching and manufacturability checks, including periodicity, volume fraction, connectivity, and minimum feature thickness. The tentative goal for Update 3 is to deliver the trained model together with the corresponding evaluation results.

### References
[1] Yaron Lipman, Ricky T. Q. Chen, Heli Ben-Hamu, Maximilian Nickel, and Matthew Le. Flow
matching for generative modeling. In The Eleventh International Conference on Learning Repre-
sentations, 2023.

[2] Qibang Liu, Seid Koric, Diab Abueidda, Hadi Meidani, and Philippe Geubelle. Toward signed
distance function based metamaterial design: Neural operator transformer for forward prediction
and diffusion model for inverse design. Computer Methods in Applied Mechanics and Engineering,
446:118316, 2025.
