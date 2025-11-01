---
layout: post
title: "Literature Review"
date: 2025-10-31 21:00:00 +0800
tags: [new]
---
As the advancement of additive manufacturing enables multiscale and lattice material structure fabri-
cation, precise control of material properties becomes achievable through the design and discovery of
novel and specialized metamaterial structures. Compared to bulk natural materials, metamaterials can
offer superior properties such as high specific modulus and strength Zheng et al. [2014], Bauer et al.
[2016], as well as unusual mechanical parameters, including negative Poisson’s ratio Lakes [1987],
Bertoldi et al. [2010], stiffness Lakes et al. [2001], Hewage et al. [2016], and compressibility Nicolaou
and Motter [2012]. While forwardly predicting the underlying properties for a given structure can
usually be easily achieved by solving the partial differential equations (PDEs) using numerical
approaches such as finite element (FE) analysis, to fully unlock the potential in practical applications,
designing metamaterial structures to meet certain properties or engineering requirements is needed,
but it still remains a challenge as an ill-posed inverse problem.

### Generation strategies
Conventional gradient-based topology optimization Sigmund and Maute [2013], Wang et al. [2014]
are prevalently used to address this problem, being especially efficient for high-dimensional design
problems with a smooth objective function. Its applications, however, can be hindered by reliance
on iterations of time-consuming discretization method and instability for non-convex objective
functions introduced by the complex material structure. To circumvent these problems, evolutional
strategies Beyer and Schwefel [2002], Deng et al. [2022], typically boosted by a deep learning
surrogate model for fast evaluation, provides a strong alternative with global exploration capability,
but it still relies on a large number of forward processes through iterations and is prone to converge
prematurely.

In recent years, deep generative frameworks have emerged as powerful solutions due to their superior capa
bility of modeling complex mapping relations. Methods such as conditional Generative Adverserial
Network (cGAN) Goodfellow et al. [2020], Li et al. [2018], Yang et al. [2021], flow-based models Dinh
et al. [2014, 2016], Kingma and Dhariwal [2018], Papamakarios et al. [2021], Guan et al. [2021], and
conditional Variational Auto Encoder (cVAE) Kingma and Welling [2013], Ma et al. [2019] are proved
to succeed in metamaterial design tasks by providing single-shot generation of various structures.
These methods holds different advantages and therefore are alternative solutions for different tasks.
For example, Flow-based models transform a simple gaussian distribution into a more complex
conditional distribution through invertible functions that are easy to compute the Jacobian determinant.
They excel in uncertainty quantification by providing explicit density estimates of generated samples,
and the invertible framework endows them with flexibility in fine-tuning and manipulating the results. The
generation ability of VAE stems from learning a lower-dimensional latent representation of observed
data and then sampling output in the latent space; VAE offers more stable convergence, well-structured
latent distribution, and can provide posterior estimation through the encoder, but it usually exhibits
compromised generation quality. GAN generally outperforms the other two in terms of generation
quality, as the generator is trained in competition with a discriminator; however, they face crucial
issues such as mode collapse (i.e., degraded diversity of output samples) and instability during
optimization due to their adversarial objective.
Later, Diffusion-based models, e.g., Diffusion Denoising diffusion probabilistic models (DDPMs) Ho
et al. [2020] and variants Song and Ermon [2019], Song et al. [2020], emerge as more robust generation
strategies. They involve a forward process that gradually corrupts the data sample into noise and
a reverse denoising process, during which the properties of structure can be infused as condition,
to reconstruct the sample. Compared to previous baselines, they showcase impressive generation
capabilities, including high-level sample details, generalization to unseen data, and broad coverage
of sample space. In addition, the relatively simple structure and stable objective function guarantee
their robustness as the dataset and model capacity scaling up. As the current State-of-the-Art deep
generative framework, their application has extended to a broader scope, such as 3D modeling Poole
et al. [2022], Liu et al. [2023], protein design Watson et al. [2023], trajectory planning Janner et al.
[2022], and medical imaging Chung and Ye [2022].

### Exploring structure representation
The design representation of metamaterial’s cellular structure under deep generative frameworks can
be divided into two class: implicit and explicit. Implicit geometry representations of metamaterial
are majorly parameterizations for regularized unit cell structures such as truss, plate, shell, and
spinodal lattice. Truss usually displays excellent mechanical properties, especially high stiffness- or
strength-to-density ratios Zheng et al. [2014], Meza et al. [2014]. However, the composition of beam 
in truss lattice induces compliant deformation mode in both stretching and bending, which
account for its poor scaling of stiffness and strength with relative density.
Plate-based metamaterials showcase superior mass-specific stiffness than truss and the their
elastically-isotropic response can reach the theoretical limit of Young’s modulus, defined by the
Hashin-Shtrikman bound Hashin and Shtrikman [1963], Berger et al. [2017]. However, both structures
suffer from stress concentration at the junction of members, which induces premature failure, and
therefore renders undesirable recoverability. Shell lattices, including triply periodic minimal surfaces
(TPMSs), address the stress concentration and recoverability issue by providing smooth inner-cell
and cell-to-cell connection, and can still reach high stiffness due to its unique doubly curved surface
geometry, realizing better energy absorption capabilities compared to truss structures. However
since shell architectures follow the periodicity of symmetric unit cells (so as truss and plate), their
mechanical properties are highly susceptible to manufacturing imperfections and defects (surface
roughness and waveness) which can be unavoidably introduced in massive-scale fabrication.
Spinodal metamaterials were explored as a non-periodic architectures which showcase robustness to
manufacturing uncertainties Hsieh et al. [2019]. The structure is designed to emulate the structure
patterns observed during spinodal phase separation in solid solution metals and polymer blends Hodge
et al. [2007], Lee and Mohraz [2010]. This type of material structure is proven to have excellent
energy absorption, resilience, and near-optimal scaling of specific stiffness Guell Izard et al. [2019],
Portela et al. [2020]. These implicit architecture representations are usually mutually exclusive
in design tasks, i.e., design frameworks that output a certain type of implicit geometry can only
generate designs under this category without significantly altering the setup. To overcome this
limitation in both sample and property space, explicit geometric representations, such as voxel/pixel
grids, point clouds, and meshes, offer greater design freedom and can capture both regular and
irregular geometries for a broader range of mechanical properties. Despite providing more geometry
details and degree of freedom, explicit representation generally increases modeling complexity as
the dimensionality of design space elevates, which can be intractable to learn and data-intensive,
therefore works are done in compromise between computational complexity and performance.

### Recent work on explicit-form structure generation
Most of the studies in inverse designing voxel-based metamaterials are confined to a limited design space:
either 2D pixels (image) Bastek and Kochmann [2023], Wang et al. [2024] or low-resolution 3D
structures Yang and Buehler [2023]. Vlassis et al. firstly applies denoising diffusion probabilistic
model to learn the nonlinear mapping between pixelized microstructure and quantitative properties
on the mechanical-MINIST dataset. Also, by concatenating the output of the diffusion model with a
pretrained CNN that predicts the functional behavior of the structure, they achieve a faster primary
ranking of the generated design without FEM. Bastek et al. integrate the 2D structural image with
an independent time dimension describing the deformation during the mechanical test to guide the
learning of the corresponding discretized stress–strain response. Also, by creating a data set using
Gaussian random field on a higher 96 × 96 grid, they further expand the study to more complex
mechanical behavior, such as frictional contact and buckling. Yang et al. applied a transformer-based
GAN to predict complete 3D mechanical fields from input 2D field images and reconstruct composite
geometry; however, it is tested only under an 8 × 8 grid design space. Though there are a few
studies extending to high-dimensional voxel representation, they mainly focus on linear material
properties Yang et al. [2024], Zheng et al. [2025]. Yang et al. trained a conditional diffusion model on
3D voxel dataset and realize fast generation of delicate microstructures with the bulk modulus, shear
modulus, and Poisson’s ratio as the optimization objectives.
There exist other interesting works that utilize the generative capability of diffusion-based frameworks
for voxel-based metamaterial design. A data augmentation technique applying on limited training
space boosted the performance of the diffusion model on 3D metamaterial optimization Zheng et al.
[2025]. It managed to overcome the data scarcity issue and expand the original 200 representations to
5 000 entries. Adding an implicit topology representation of the structure derived from persistent
homology (PH) to the generative model, Du et al. [2026] proposed a method that facilitates the generation
of a diversity of metamaterial unit structures with richer shapes and properties. Under this framework
the design generation can be based on topology, properties, or both, therefore enhances the exploration
of the solution space.

Despite the manifested strong visual performance in handling complex and diverse structure-property
relations, to effectively implement diffusion-model-based frameworks for microstructure inverse
design still require large training corpora and hardly handle topology, inner-cell connectivity, or fabri-
cation constraints during generation. It is important to notice that metamaterial performance depends
not only on what is present but also on how it connects. Diffusion-based models were originally
developed for 2D image synthesis; this design is counterintuitive for mechanical structures, which
are more naturally described by simpler, often binary patterns and require explicit topological and
geometric constraints during generation. Failing to enforce these connectivity and manufacturability
often yields designs that look plausible yet are non-buildable or mechanically brittle. A generative
approach that treats samples as structure rather than mere texture, therefore has the potential to reduce
data and computation overhead.



### References
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
- Anna Guell Izard, Jens Bauer, Cameron Crook, Vladyslav Turlo, and Lorenzo Valdevit. Ultrahigh
energy absorption multifunctional spinodal nanoarchitectures. Small, 15(45):1903834, 2019.
- Zvi Hashin and Shmuel Shtrikman. A variational approach to the theory of the elastic behaviour of
multiphase materials. Journal of the Mechanics and Physics of Solids, 11(2):127–140, 1963.
- Trishan AM Hewage, Kim L Alderson, Andrew Alderson, and Fabrizio Scarpa. Double-negative
mechanical metamaterials displaying simultaneous negative stiffness and negative poisson’s ratio
properties. Advanced Materials, 28(46):10323–10332, 2016.
- Jonathan Ho, Ajay Jain, and Pieter Abbeel. Denoising diffusion probabilistic models. Advances in
neural information processing systems, 33:6840–6851, 2020.
- AM Hodge, J Biener, JR Hayes, PM Bythrow, CA Volkert, and AV Hamza. Scaling equation for
yield strength of nanoporous open-cell foams. Acta Materialia, 55(4):1343–1349, 2007.
- Meng-Ting Hsieh, Bianca Endo, Yunfei Zhang, Jens Bauer, and Lorenzo Valdevit. The mechanical
response of cellular materials with spinodal topologies. Journal of the Mechanics and Physics of
Solids, 125:401–419, 2019.
- Michael Janner, Yilun Du, Joshua B Tenenbaum, and Sergey Levine. Planning with diffusion for
flexible behavior synthesis. arXiv preprint arXiv:2205.09991, 2022.
- Diederik P Kingma and Max Welling. Auto-encoding variational bayes. arXiv preprint
arXiv:1312.6114, 2013.
- Durk P Kingma and Prafulla Dhariwal. Glow: Generative flow with invertible 1x1 convolutions.
Advances in neural information processing systems, 31, 2018.
Roderic Lakes. Foam structures with a negative poisson’s ratio. Science, 235(4792):1038–1040,
1987.
- Roderic S Lakes, T Lee, A Bersie, and Yun-Che Wang. Extreme damping in composite materials
with negative-stiffness inclusions. Nature, 410(6828):565–567, 2001.
- Matthew N Lee and Ali Mohraz. Bicontinuous macroporous materials from bijel templates. Adv.
Mater, 22(43):4836–4841, 2010.
- Xiaolin Li, Zijiang Yang, L Catherine Brinson, Alok Choudhary, Ankit Agrawal, and Wei Chen.
A deep adversarial learning methodology for designing microstructural material systems. In
International Design Engineering Technical Conferences and Computers and Information in
Engineering Conference, volume 51760, page V02BT03A008. American Society of Mechanical
Engineers, 2018.
- Zhen Liu, Yao Feng, Michael J Black, Derek Nowrouzezahrai, Liam Paull, and Weiyang Liu.
Meshdiffusion: Score-based generative 3d mesh modeling. arXiv preprint arXiv:2303.08133,
2023.
- Wei Ma, Feng Cheng, Yihao Xu, Qinlong Wen, and Yongmin Liu. Probabilistic representation and
inverse design of metamaterials based on a deep generative model with semi-supervised learning
strategy. Advanced Materials, 31(35):1901111, 2019.
- Lucas R Meza, Satyajit Das, and Julia R Greer. Strong, lightweight, and recoverable three-dimensional
ceramic nanolattices. Science, 345(6202):1322–1326, 2014.
- Zachary G Nicolaou and Adilson E Motter. Mechanical metamaterials with negative compressibility
transitions. Nature materials, 11(7):608–613, 2012.
- George Papamakarios, Eric Nalisnick, Danilo Jimenez Rezende, Shakir Mohamed, and Balaji
Lakshminarayanan. Normalizing flows for probabilistic modeling and inference. Journal of
Machine Learning Research, 22(57):1–64, 2021.
- Ben Poole, Ajay Jain, Jonathan T Barron, and Ben Mildenhall. Dreamfusion: Text-to-3d using 2d
diffusion. arXiv preprint arXiv:2209.14988, 2022.
- Carlos M Portela, A Vidyasagar, Sebastian Krödel, Tamara Weissenbach, Daryl W Yee, Julia R Greer,
and Dennis M Kochmann. Extreme mechanical resilience of self-assembled nanolabyrinthine
materials. Proceedings of the National Academy of Sciences, 117(11):5686–5693, 2020.
- Ole Sigmund and Kurt Maute. Topology optimization approaches: A comparative review. Structural
and multidisciplinary optimization, 48(6):1031–1055, 2013.
- Yang Song and Stefano Ermon. Generative modeling by estimating gradients of the data distribution.
Advances in neural information processing systems, 32, 2019.
- Yang Song, Jascha Sohl-Dickstein, Diederik P Kingma, Abhishek Kumar, Stefano Ermon, and Ben
Poole. Score-based generative modeling through stochastic differential equations. arXiv preprint
arXiv:2011.13456, 2020.
- Fengwen Wang, Ole Sigmund, and Jakob Søndergaard Jensen. Design of materials with prescribed
nonlinear properties. Journal of the Mechanics and Physics of Solids, 69:156–174, 2014.
- Haoyu Wang, Zongliang Du, Fuyong Feng, Zhong Kang, Shan Tang, and Xu Guo. Diffmat: Data-
driven inverse design of energy-absorbing metamaterials using diffusion model. Computer Methods
in Applied Mechanics and Engineering, 432:117440, 2024.
- Joseph L Watson, David Juergens, Nathaniel R Bennett, Brian L Trippe, Jason Yim, Helen E Eisenach,
Woody Ahern, Andrew J Borst, Robert J Ragotte, Lukas F Milles, et al. De novo design of protein
structure and function with rfdiffusion. Nature, 620(7976):1089–1100, 2023.
- Yanyan Yang, Lili Wang, Xiaoya Zhai, Kai Chen, Wenming Wu, Yunkai Zhao, Ligang Liu, and
Xiao-Ming Fu. Guided diffusion for fast inverse design of density-based mechanical metamaterials.
arXiv preprint arXiv:2401.13570, 2024.
- Zhenze Yang and Markus J Buehler. Fill in the blank: transferrable deep learning approaches to
recover missing physical field information. Advanced Materials, 35(23):2301449, 2023.
- Zhenze Yang, Chi-Hua Yu, and Markus J Buehler. Deep learning model to predict complex stress
and strain fields in hierarchical composites. Science Advances, 7(15):eabd7416, 2021.
- Xiaoyang Zheng, Junichiro Shiomi, and Takayuki Yamada. Optimizing metamaterial inverse design
with 3d conditional diffusion model and data augmentation. Advanced Materials Technologies,
page 2500293, 2025.
- Xiaoyu Zheng, Howon Lee, Todd H Weisgraber, Maxim Shusteff, Joshua DeOtte, Eric B Duoss,
Joshua D Kuntz, Monika M Biener, Qi Ge, Julie A Jackson, et al. Ultralight, ultrastiff mechanical
metamaterials. Science, 344(6190):1373–1377, 2014.
