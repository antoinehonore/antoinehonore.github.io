+++
categories = ["notes"]
author = "Antoine Honoré"
date = "2022-03-22"
description = "Gumbel softmax"
featured = "pic01.jpg"
featuredalt = ""
featuredpath = "date"
linktitle = ""
title = "Gumbel softmax"
slug = ""
type = "notes"
[params]
  math = true
+++

I usually understand the Gumbel-Softmax (GS) operation as a replacement for softmax which returns a one-hot encoded output instead of a proper discrete distribution.
In addition GS does that in way that is differentiable wrt to the input.

Just to recap: let \( x\in \mathbb{R}^d \) we have

\[
\begin{aligned}
	\forall i\in [d],\quad p_i=\text{Softmax}(x/\tau)_i=\frac{e^{x_i/\tau}}{\sum_{j=1}^de^{x_j/\tau}},
\end{aligned}
\]
where \(\tau>0\) is a temperature parameter.
This means that \(\forall i\in [d]\quad p_i\leq 0\) and \(\sum_i p_i=1\), i.e. \((p_1,\dots,p_d)\) defines a proper discrete distribution.
Here the issue is that sometimes, we are interested in an operation on \(x\in\mathbb{R}^d\) giving discrete variables: \(\forall i\in[d]\quad p_i\in\{0,1\}\), which is not the case here.

At first I thought that Gumbel-Softmax was a simple trick:
\[
\begin{aligned}
	y = z - p^{(cut)} + p,
\end{aligned}
\]
where \(z=\text{one_hot}(\arg\max p_i)\) is a non-differentiable discretization of \(p\), and \(p^{(cut)}\) is the vector \(p\) that does not propagate gradient wrt the input \(x\).
This means that the output is the discretization, and the gradient  with respect to the input is the gradient of the softmax operation with respect to its input.
Problem solved then, we have the operation we wanted.

# Gumbel-softmax also allows to sample
This is only part of the story. 
The Gumbel-softmax operation is a way to *sample* one-hot encoded vectors in \(d\) dimensions that are differentiable wrt to the weights of the discrete distributions.
Let's see how this is done.
Let \(\pi\in\Delta^{d-1}\) denote a discrete probability distribution. 
Let \(\forall i\in [d] g_i\sim \text{Gumbel}(0,1)\) i.i.d.

A sample \(z\in\{0,1\}^d\) defined as:
\[
	z = \text{one\_hot}(\arg\max_i [\log \pi_i +g_i]),
\]
is drawn from the discrete distribution \((\pi_1,\dots,\pi_d)\) and is differentiable wrt \pi.
Using a temperature softmax to replace the \(\arg\max\) operation leads to
\[
\forall i \in [d] p_i = \frac{e^{[\log\pi_i +g_i]/\tau}}{\sum_{j=1}^de^{[\log\pi_j +g_j]/\tau}}.
\]

# Why Gumbel(0,1) ?
One legit question here is why use a Gumbel(0,1) distribution to sample i.i.d. \((g_i)_{i=1}^d\) ? Why not use another distribution, e.g. the beloved Normal distribution ?

This is because \(g_i\sim\) Gumbel(0,1) i.i.d. ensures that the maximum element is preserved after adding the noise g_i. 

Let's see this in details.
Let \(M=\arg\max_i p_i\). 
Then we have that
\[
p_M = \Pr(x_M+g_M \text{ is the max } \forall i\in[d]).
\]

*Proof:*
Let \(\mathcal{P} = \Pr(x_M+g_M \text{ is the max } \forall i\in[d])\).
Let \(g_i\sim\) Gumbel(0,1) i.i.d.

\[
\begin{aligned}
	\mathcal{P} &= \int \Pr(\forall i\in[d] x_i+g_i<x_M + g_M)\Pr(g_M)dg_M\\
				&= \int \prod_{i\neq M} e^{-e^{g_M+x_M-x_i}}e^{-g_M}e^{-e^{-g_M}}dg_M\\
				&= \int \prod_i e^{-e^{g_M+x_M-x_i}}e^{-g_M}dg_M\\
				&= \int \prod_i e^{-e^{g_M}e^{-x_M}(\sum_i e^{x_i})}e^{-g_M}dg_M
\end{aligned}
\]

With a change of variable \(t=e^{-g_M}\), we have \(e^{-g_M}dg_M = -dt\), thus:

\[
\begin{aligned}
\mathcal{P} &= \int_0^\infty e^{-\frac{\sum_ie^{x_i}}{e^{x_M}}t}\\
&=\frac{e^{x_M}}{\sum_ie^{x_i}} = p_M
\end{aligned}
\]
which concludes the proof.

Therefore the Gumbel(0,1) distribution is required because we chose to approach the differentiable sampling problem using additive noise to the log-weights of the distributions we want to sample from. 
For this approach to work, the distribution of the noise must not modify the distribution of the maximum of the log-weights with additive noise. Gumbel(0,1) is a distribution with this property. For once, the Normal distribution is not.



# References

- It turns out this was discovered simultaneously by two groups: https://arxiv.org/abs/1611.00712 (they use the name "concrete distribution") and https://arxiv.org/abs/1611.01144

- A nice blog with the derivation in the last section: https://mukappalambda.github.io/readings/gumbel_softmax/#gumbel-reparameterization-trick

- The pytorch package is a good place to find a Python implementation: https://pytorch.org/docs/stable/generated/torch.nn.functional.gumbel_softmax.html 