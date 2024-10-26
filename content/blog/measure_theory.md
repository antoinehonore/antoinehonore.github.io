+++
categories = ["notes"]
author = "Antoine Honoré"
date = "2022-03-22"
description = "Probability and Random Processes"
featured = "pic01.jpg"
featuredalt = ""
featuredpath = "date"
linktitle = ""
title = "First steps in measure theory"
slug = ""
type = "notes"
[params]
  math = true
+++

*The primary focus of my PhD did not turn out as theoretical as I would have hoped, and I never found time to dig very far into measure theory books. Keeping notes of the concepts I read about in this blog post will hopefully help me dedicate time to this. It might also help some interested readers in their journey through measure theory !*

# Real analysis

## lim sup of sum of arbitrary real sequences

Let \((x_n)_{n\in\mathbb{N}}\) and  $(y_n)\_{n\in\mathbb{N}}$ two series in $[-\infty, +\infty]$.
Then,

\begin{equation}
\begin{align}
&\forall\, n\in\mathbb{N},\,\forall t>n, \quad x_t \leq \sup_{t>n}(x_n) \, \text{and}\, y_t \leq \sup_{t>n}(y_t).\\
\text{Therefore } &\forall n\in\mathbb{N},\,\forall\, t>n, \quad x_t + y_t \leq \sup_{t>n}(x_n) +  \sup_{t>n}(y_t)\\
\text{therefore } &\forall n\in\mathbb{N},\,\forall t>n, \quad x_t + y_t \leq \inf_n\sup_{t>n}(x_n) +  \inf_n\sup_{t>n}(y_t)\\
\text{therefore } &\forall\, n\in\mathbb{N}, \quad  \sup_{t>n}(x_t + y_t) \leq \inf_n\sup_{t>n}(x_n) +  \inf_n\sup_{t>n}(y_t)\\
\text{therefore } &\inf_n\sup_{t>n}(x_t + y_t) \leq \inf_n\sup_{t>n}(x_n) +  \inf_n\sup_{t>n}(y_t)\\
\text{i.e. } &\lim\sup (x_n + y_n) \leq \lim\sup (x_n) +  \lim\sup (y_n)
\end{align}
\end{equation}

## lim sup of sum of one arbitrary and one converging real sequences
Suppose that $\lim y_n = a<\infty$.
$\lim\sup(x_n)$ can be understood as the supremum of all the limits of converging sub-sequences of $(x_n)_{n\in\mathbb{N}}$.
Let $L$ denote the set of the limits of the converging sub-sequences of $x_n$.

Then, the set of the limits of all the converging sub-sequences of $x_n + y_n$ is 
\begin{equation} L+a=\{t+a\,|\,t\in L\}.\end{equation}

Then we have:

\begin{equation}
\lim\sup (x_n + y_n) = \sup (L+a) = \sup (L) + a = \lim\sup(x_n) + \lim y_n
\end{equation}


# Measure Theory
## Probability density function of a random variable

Let $K=\mathbb{R}$ or $\mathbb{C}$ (assume $K=\mathbb{R}$). ? K could be any field (corps commutatif)?

Let $E\subseteq K$. Let $(E,\,\mathcal{B},\,\lambda)$ the Lebesgue (Borel) measure space.

Let $\Omega$ a set. Let $\Sigma$ be a $\sigma$-algebra on $\Omega$. Let $\mathbb{P}:\,\Sigma\,\rightarrow\,[0,1]$ be a measurable function such that $\mathbb{P}(\Omega)=1$ (+ some other assumptions that I skipped).

Let $(\Omega,\,\Sigma,\,\mathbb{P})$ be a probability space.

### Continuous Random Variable

Let $X:\,\Omega\,\rightarrow\,E$ be a measurable function. The measurable functions defined in a probability space are called random variables.

#### Probability Distribution

The probability distribution of the random variable $X$ is the measurable function: 

\begin{equation}p_{X}:\,\Sigma\,\rightarrow\,[0,1], \end{equation}

defined wrt to $\mathbb{P}$, that assigns a probability to every possible element of the $\sigma$-algebra such that: 

\begin{equation} \forall S\,\in\,\mathcal{B},\,p_{X}(S)=\mathbb{P}(X \in S)=\mathbb{P}(\{\omega \in \Omega\,|\,X( \omega ) \in S\}). \end{equation} 

The probability distribution of the random variable $X$ is a measure on $E$, that was "pushed-forward" by $X$, from the measure $\mathbb{P}$ on $\Omega$.

#### Density Function

A density function of $X$ is the Radon-Nykodym derivative of $p_X$ wrt to $\lambda$. Let us assume that 

\begin{equation} \forall S\,\in\,\mathcal{B},\,\lambda (S)=0\,\implies\,p_{X}(S)=0, \end{equation} i.e. $p_{X}$ is absolutely continuous wrt $\lambda$, also noted $p_{X} << \lambda$. 

Then we have that: $\exists ! \lambda-a.e\, f:\Omega\rightarrow [0,+\infty[$ such that,

\begin{equation}  \forall A\subseteq \Omega,\,p_{X}(A)=\int_{A} f d\mu \end{equation} 

### Discrete Random Variables
Let us now assume that the initial measure space is defined with (1) a finite $\sigma$-algebra $\mathcal{B}$ (i.e. containing singleton sets of $B$ and their unions) and (2) the counting measure $\mu:S\mapsto |S|$ on $\mathcal{B}$.
A random variable $X:\Omega\rightarrow E$ is discrete iif $E$ is countable.
if X is a discrete random variable the probability distribution of X is the push forward measure $f_X$ defined as:

\begin{equation} \forall x\in V f_X(x)=\mathbb{P}(X=x) = \mathbb{P}(\{\omega\in\Omega|X(\omega)=x\}). \end{equation}

Supposing that the Radon-Nykodym derivative of $p_X$ wrt to the counting measure exists
