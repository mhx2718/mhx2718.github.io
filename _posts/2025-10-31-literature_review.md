---
layout: post
title: "Literature Review"
date: 2025-10-31 21:00:00 +0800
tags: [new]
---
# Literature Review
As the advancement of additive manufacturing enables multiscale and lattice material structure fabri-
cation, precise control of material properties becomes achievable through the design and discovery of
novel and specialized metamaterial structures. Compared to bulk natural materials, metamaterials can
offer superior properties such as high specific modulus and strength Zheng et al. [2014], Bauer et al.
[2016], as well as unusual mechanical parameters, including negative Poisson’s ratioLakes [1987],
Bertoldi et al. [2010], stiffness Lakes et al. [2001], Hewage et al. [2016], and compressibilityNicolaou
and Motter [2012]. While forwardly predicting the underlying properties for a given structure can
usually be easily achieved by solving the partial differential equations (PDEs) using numerical
approaches such as finite element (FE) analysis, to fully unlock the potential in practical applications,
designing metamaterial structures to meet certain properties or engineering requirements is needed,
but it still remains a challenge as being an ill-posed inverse problem.

# Generation strategies
Conventional gradient-based topology optimizationSigmund and Maute [2013], Wang et al. [2014]
are prevalently used to address this problem, being especially efficient for high dimension design
problems with smooth objective function. Its applications, however, can be hindered by reliance
on iterations of time-consuming discretization method and instability for non-convex objective
functions introduced by the complex material structure. To circumvent these problems, evolutional
strategiesBeyer and Schwefel [2002], Deng et al. [2022], typically boosted by a deep learning
surrogate model for fast evaluation, provide a strong alternative with global exploration capability,
but it still relies on a large number of forward process through iterations and is prone to converge
prematurely.

In recent years, deep generative frameworks emerge as powerful solutions due to their superior capa
bility of modeling complex mapping relations. Methods such as conditional Generative Adverserial
Network (cGAN)Goodfellow et al. [2020], Li et al. [2018], Yang et al. [2021], flow-based modelsDinh
et al. [2014, 2016], Kingma and Dhariwal [2018], Papamakarios et al. [2021], Guan et al. [2021], and
conditional Variational Auto Encoder (cVAE)Kingma and Welling [2013], Ma et al. [2019] are proved
to succeed in metamaterial design tasks by providing single-shot generation of various structures.
These methods holds different advantages and therefore are alternative solutions for different tasks.
For example, Flow-based models transform a simple gaussian distribution into a more complex
conditional distribution through invertible functions that are easy to compute Jacobian determinant.
They excel in uncertainty quantification as providing explicit density estimate of generated samples,
and the invertible framework endows them flexibility in fine-tuning and manipulating the results. The
generation ability of VAE stems from learning a lower-dimension latent representation of observed
data and then samples output in the latent space; VAE offers more stable convergence, well-structured
latent distribution, and can provide posterior estimation through encoder, but it usually exhibits
compromised generation quality. GAN generally outperforms the other two in terms of generation

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

# References
- Jan-Hendrik Bastek and Dennis M Kochmann. Inverse design of nonlinear mechanical metamaterials via video denoising diffusion models. Nature Machine Intelligence, 5(12):1466–1475, 2023.
- Jens Bauer, Almut Schroer, Ruth Schwaiger, and Oliver Kraft. Approaching theoretical strength in glassy carbon nanolattices. Nature materials, 15(4):438–443, 2016.
- JB Berger, HNG Wadley, and RM McMeeking. Mechanical metamaterials at the theoretical limit of
isotropic elastic stiffness. Nature, 543(7646):533–537, 2017.
- Katia Bertoldi, Pedro M Reis, Stephen Willshaw, and Tom Mullin. Negative poisson’s ratio behavior induced by an elastic instability. Advanced materials, 22(3):361–366, 2010.
- Hans-Georg Beyer and Hans-Paul Schwefel. Evolution strategies–a comprehensive introduction. Natural computing, 1:3–52, 2002.
- Hyungjin Chung and Jong Chul Ye. Score-based diffusion models for accelerated mri. Medical image analysis, 80:102479, 2022.
- Bolei Deng, Ahmad Zareei, Xiaoxiao Ding, James C Weaver, Chris H Rycroft, and Katia Bertoldi. Inverse design of mechanical metamaterials with target nonlinear response via a neural accelerated evolution strategy. Advanced Materials, 34(41):2206238, 2022.
- Laurent Dinh, David Krueger, and Yoshua Bengio. Nice: Non-linear independent components estimation. arXiv preprint arXiv:1410.8516, 2014.
- Laurent Dinh, Jascha Sohl-Dickstein, and Samy Bengio. Density estimation using real nvp. arXiv preprint arXiv:1605.08803, 2016.
- Liang Du, Jiangbei Hu, Shengfa Wang, Yu Jiang, Na Lei, Ying He, and Zhongxuan Luo. Topo-genmeta: Generative design of metamaterials based on diffusion model with attention to topology. Computer-Aided Design, 190:103977, 2026. ISSN 0010-4485. doi: https://doi.org/10.1016/j.cad.2025.103977. URL https://www.sciencedirect.com/science/article/pii/S0010448525001381.
- Ian Goodfellow, Jean Pouget-Abadie, Mehdi Mirza, Bing Xu, David Warde-Farley, Sherjil Ozair, Aaron Courville, and Yoshua Bengio. Generative adversarial networks. Communications of the ACM, 63(11):139–144, 2020.
- Kelly M Guan, Timothy I Anderson, Patrice Creux, and Anthony R Kovscek. Reconstructing porous media using generative flow networks. Computers & Geosciences, 156:104905, 2021.
- Anna Guell Izard, Jens Bauer, Cameron Crook, Vladyslav Turlo, and Lorenzo Valdevit. Ultrahigh energy absorption multifunctional spinodal nanoarchitectures. Small, 15(45):1903834, 2019.
