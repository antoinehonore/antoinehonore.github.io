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

I usually understand the Gumbel softmax (GS) operation as a replacement for softmax, differentiable, and that given an arbitrary input in \(d\) dimensions, yields a one-hot encoded vector, instead of an arbitrary discrete distribution.
Just to recap: let \( x\in \mathbb{R}^d \) we have

\[
\begin{aligned}
	\forall i\in [d], p_i=\text{Softmax}(x/\tau)_i=\frac{e^{x_i/\tau}}{\sum_{j=1}^de^{x_j/\tau}},
\end{aligned}
\]
where \(/\tau>0\) is a temperature parameter.
This means that \(\forall i\in [d] p_i\leq 0\) and \(\sum_i p_i=1\), i.e. \((p_1,\dots,p_d)\) defines a proper discrete distribution.
The problem being that sometimes we are interested in an operation on \(x\in\mathbb{R}^d\) giving discrete variables: \(\forall i\in[d] p_i\in\{0,1\}\).

At first I thought that Gumbel-Softmax was a simple trick:

\[
\begin{aligned}
	y = z - p^{(cut)} + p,
\end{aligned}
\]
where \(z=\text{one\_hot}(\arg\max p_i)\) is a non-differentiable discretization of \(p\), and \(p^{(cut)}\) is the vector \(p\) that does not propagate gradient wrt the input \(x\).
This means that the output is the discretization, and the gradient  with respect to the input is the gradient of the softmax operation with respect to its input.
Problem solved then, we have the operation we wanted.

This is only part of the story. 
The Gumbel-softmax operation is a way to *sample* one-hot encoded vectors in \(d\) dimensions that are differentiable wrt to the weights of the discrete distributions.

Let \(\pi\in\Delta^{d-1}\) denote a discrete probability distribution. 
Let \(\forall i\in [d] g_i\) sampled from the Gumbel(0,1) distribution.

A sample \(z\in\{0,1\}^d\) defined as:
\[
	z = \text{one\_hot}(\arg\max_i [\log \pi_i +g_i]),
\]

is drawn from the discrete distribution \((\pi_1,\dots,\pi_d)\) and is differentiable wrt \pi.
Using a temperature softmax to replace the \(\arg\max\) operation leads to

\[
\forall i \in [d] p_i = \frac{e^{[\log\pi_i +g_i]/\tau}}{\sum_{j=1}^de^{[\log\pi_j +g_j]/\tau}}
\]

