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
	\forall i\in [d], p_i=\text{Softmax}(x)_i=\frac{e^{x_i}}{\sum_{j=1}^de^{x_j}}.
\]
This means that \(\forall i\in [d] p_i\leq 0\) and \(\sum_i p_i=1\), i.e. (p_1,\dots,p_d) defines a proper discrete distribution.
The problem being that sometimes we are interested in an operation on \(x\in\mathbb{R}^d\) giving discrete variables: \(\forall i\in[d] p_i\in\{0,1\}\)

