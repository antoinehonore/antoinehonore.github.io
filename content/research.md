+++
title = "Research"
date = "2024-10-26"
aliases = ["about-me"]
[ author ]
  name = "Antoine"
+++

# About me
I am currently a postdoc at the division of information science and engineering of KTH Royal Institute of Technology in Stockholm, Sweden. I work in the research group of [Prof. Ming Xiao](https://www.kth.se/profile/mingx/), in collaboration with [Prof. Volker Lauschke](https://ki.se/en/people/volker-lauschke) at the department of [Physiology and Pharmacology](https://ki.se/en/fyfa/personalized-medicine-and-drug-development) at Karolinska Institutet. I work as an associated researcher with the [neonatal transfusion network](https://neonataltransfusionnetwork.com).

My interest in research is the design of prediction models contributing to more reliable and trustworthy predictions in clinical contexts. This encompasses the design, implementation and training of deep architectures working from different data modalities, possibly integrating multiple ones. I am also interested in enabling health informatics research with information systems integrating various sources of data generated in hospital contexts.

My main project focuses on the development of graph-based prediction models to quantify the impact of genetic variants of drug transporter proteins. This project is part of an effort toward personalized medicine, ultimately aiming at a fast and reliable identification of suitable chemotherapeutic treatments for cancer patients based on their genetic profile.

I obtained my PhD under the supervision of [Assoc. Prof. Saikat Chatterjee](https://www.kth.se/profile/sach/), in a collaborative project with [Prof. Eric Herlenius](https://ki.se/personer/eric-herlenius) at the [department of Women's and Children's Health](ki.se/en/kbh/department-of-womens-and-childrens-health) at Karolinska Institutet. My thesis is available [online](https://kth.diva-portal.org/smash/record.jsf?pid=diva2%3A1762032).

# Projects

## On-going

### Variant effect predictions
2023 - 2025

## Neored
2023 - 

## ITNet
Title: ITNet: Irregular Timeseries Data Fusion with Attention Mechanisms

Abstract: 

Timeseries regression from multimodal data is a difficult task when modalities have missing data or different sampling frequencies. Current approaches such as feature fusion often rely on interpolation and might result in either too simplistic or  overly computationally expensive algorithms. We propose ITNet, an end-to-end trainable multihead causal cross-attention model adapted for irregularly sampled multimodal timeseries data. We show the performances of the model on synthetic data from 2d linear state-space models with a varying number of modalities, varying data missingness and varying signal-to-measurement-noise ratio (SMNR). We compare with Kalman filters exploiting either one or all available modalities. Provided a sufficient number of modalities and high enough SMNR, ITNet outperforms the closed form Kalman Filter. Importantly, our model achieves these results without assuming knowledge of the state transition matrix. This is of particular importance towards the use of ITNet for practical cases.

[[paper (submitted to FUSION 2025)]()], [[code](https://github.com/antoinehonore/itnet)]'

## Finished
### Neonatal sepsis detection
2018 - 2023
- 

### DANSE: Data-driven Non-linear State Estimation of Model-free Process in Unsupervised Bayesian Setup 

Title: 

Abstract: 

We propose DANSE – a data-driven non-linear state estimation method. DANSE provides a closed-form posterior of the state of a model-free process, given linear measurements of the state in a Bayesian setup, like the celebrated Kalman filter (KF). Non-linear dynamics of the state are captured by data-driven recurrent neural networks (RNNs). The training of DANSE combines maximum-likelihood and gradient-descent in an unsupervised framework, i.e. only measurement data and no process data are required. Using simulated linear and non-linear process models, we demonstrate that DANSE - without knowledge of the process model - provides competitive performance against model-based approaches such as KF, unscented KF (UKF), extended KF (EKF), and a hybrid approach such as KalmanNet.
Authors: Anubhab Ghosh, Antoine Honore, Saikat Chatterjee

[[paper](https://ieeexplore.ieee.org/document/10289946)], [[code](https://github.com/anubhabghosh/danse)]

# Manuscripts
Unpublished works

## Convolution based Variational Bayes for Factorial HMM

Abstract: 

We propose a method to scale factorial Hidden Markov Models (HMMs) to long and complex time series.
Factorial HMMs are suited for time series modeling tasks because of the distributed structure of their latent space.
We use a continuous state space relaxation of a factorial HMM and propose a convolution-based variational distribution that can be learned with a gradient-based variational expectation-maximization (EM) algorithm.
The number of trainable parameters in our model is independent of the length of the input data.
Our model can accommodate different kinds of emission distributions, simple to complex, such as Gaussian and conditional normalizing flows (CNFs). 
The proposed model is evaluated for synthetic and real world data modeling and generation.

[[manuscript](https://openreview.net/forum?id=aSTsODJ3On)], [[code](https://github.com/antoinehonore/factorialHMM)]