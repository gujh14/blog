---
title: "PhysChem: Deep Molecular Representation Learning via Fusing Physical and Chemical Information"
date: "2022-07-29"
draft: false
math: true
categories:
- Research - Technical
tags:
- Multi-task
- Model fusion
- Chemical conformation
- Molecular property
image: physchem_1.png
---
NeurIPS Poster, '21,  
<https://arxiv.org/abs/2112.04624>

# Summary
- Used physicist network (PhysNet) and chemist network (ChemNet) simultaneously, and each network shares information to solve individual tasks.
- PhysNet: Neural physical engine. Mimics molecular dynamics to predict conformation.
- ChemNet: Message passing network for chemical & biomedical property prediction.
- Molecule without 3D conformation can be inferred during test time.

## Preliminaries
- Molecular representation learning:  
    Embedding molecules into latent space for downstream tasks.
    
- Neural Physical Engines  
    Neural networks are capable of learning annotated potentials and forces in particle systems.  
    HamNet proposed a neural physical engine that operated on a generalized space, where positions and momentums of atoms were defined as high-dimensional vectors.
    
- Multi-task learning  
    Sharing representations for different but related tasks.
    
- Model fusion  
    Merging different models on identical tasks to improve performance.

## Notation
Graph $\mathcal{M} = (\mathcal{V}, \mathcal{E}, n, m, \mathbf{X}^v, \mathbf{X}^e)$  
- $\mathcal{V}$: set of $n$ atoms  
- $\mathcal{E}$: set of $m$ chemical bonds  
- $\mathbf{X}^v \in \mathbb{R}^{n \times d_v} = (x^v_1, ..., x^v_n)^\top$: matrix of atomic features  
- $\mathbf{X}^e \in \mathbb{R}^{m \times d_e} = (x^e_1, ..., x^e_m)^\top$: matrix of bond features

## Model
![Image 1](physchem_1.png)
Figure 1. PhysChem Architecture

- Initializer
    - Input: atomic features, bond features (from RDKit)
    - Layer: fully connected layers
    - Output:
    - bond states, atom states for ChemNet  