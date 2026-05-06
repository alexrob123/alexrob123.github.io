---
title: "PRJD"
collection: reports
date: 2026-04-27
permalink: /reports/2026-PRJD/
description: "Precision and Recall for Joint Distribution"
tags:
  - research
---

**Table of content**
- [Introduction](#introduction)
- [Precision Recall for Joint Distributions](#precision-recall-for-joint-distributions)
- [Experiments](#experiments)
- [Proofs and derivations](#proofs-and-derivations)
		- [PRJD](#prjd)
		- [Upper bound](#upper-bound)


# Introduction

We investigate the limit of evaluation metrics when it comes to evaluating conditional generative models.

We first want to investigate a brute-force adaptation of current methods to joint distributions. 


# Precision Recall for Joint Distributions

We propose to extend Precision and Recall as defines in Sajjadi-2018 to joint distributions.

$$
\alpha_\lambda(P_{XY}, Q_{XY}) =
\mathbb E_Y \bigg[ \alpha_\lambda(P_{X|Y}, \, Q_{X|Y}) \bigg]
$$


Furthermore

$$
\alpha_\lambda(P_{XY}, Q_{XY}) 
\le
\alpha_\lambda(P_{X}, Q_{X}) 
$$

# Experiments



# Proofs and derivations


### PRJD

$$
\begin{aligned}
\alpha_\lambda(P_{XY}, Q_{XY}) 
& = \int \int \min \bigg( \lambda \, p(x,y),\, q(x,y) \bigg) \ dxdy \\
& = \int \int \min \bigg( \lambda \, p(x|y) \, p(y), \, q(x|y) \, q(y) \bigg) \ dxdy 
\qquad \text{(Bayes theorem)}
\\
& = \int \int \min \bigg( \lambda \, p(x|y) \, p(y), \, q(x|y) \, p(y) \bigg) \ dxdy
\qquad \text{(assuming $P_Y = Q_Y$)}
\\
& = \int p(y) \int \min \bigg( \lambda \, p(x|y), \, q(x|y) \bigg) \ dx \ dy \\
& = \mathbb E_Y \bigg[ \int \min \bigg( \lambda \, p(x|Y), \, q(x|Y) \bigg) \ dx \ \bigg] \\
& = \mathbb E_Y \bigg[ \alpha_\lambda(P_{X|Y}, \, Q_{X|Y}) \bigg] \\
\end{aligned}
$$

### Upper bound
$$
\begin{aligned}
	\alpha_\lambda(P_{XY}, Q_{XY}) 
	& = 
	\int \int \min \bigg( \lambda \, p(x,y),\, q(x,y) \bigg) \ dxdy 
	\\ & = 
	\int \int \min \bigg( \lambda \, p(y|x) \, p(x), \, q(y|x) \, q(x) \bigg) \ dxdy
	\qquad \text{(Bayes theorem)}
	\\ & \le 
	\int \min \bigg( \int \lambda \, p(y|x) \, p(x) \ dy \, , \int \, q(y|x) \, q(x) \ dy \bigg) \ dx
	\qquad \text{(subadditivy under integration)}
	\\ & =
	\int \min \bigg( \lambda \, p(x) , \, q(x) \bigg) \ dx
	\\ & = 
	\alpha_\lambda(P_{X}, Q_{X}) 
\end{aligned}
$$