# Flow Matching: A Gentle Introduction

Flow Matching is a framework for training generative models by directly learning a **vector field** that transports a simple distribution (e.g., Gaussian) to a complex data distribution.

---

## 1. Motivation

In generative modeling, we want to sample from a target distribution $p_0(x)$ (e.g., images, molecules). A common strategy is:

- Start from a simple distribution $p_1(x)$ (e.g., Gaussian)
- Gradually transform it into $p_0(x)$

Flow Matching provides a **continuous-time perspective** of this transformation.

---

## 2. The Core Idea

We define a time-dependent path of distributions:

$$
p_t(x), \quad t \in [0,1]
$$

such that:
- $p_1(x)$ is simple (noise)
- $p_0(x)$ is the data distribution

We then learn a vector field:

$$
v_t(x)
$$

that satisfies the **continuity equation**:

$$
\partial_t p_t(x) + \nabla \cdot (p_t(x) v_t(x)) = 0
$$

👉 This ensures that particles flowing along $v_t$ follow the correct distribution evolution.

---

## 3. Flow Matching Objective

Instead of solving the PDE directly, Flow Matching trains $v_t(x)$ via regression.

We sample:
- $x_0 \sim p_0$
- $x_1 \sim p_1$
- interpolate to get $x_t$

Then define a **target velocity field** $u_t(x)$, and train:

$$
\mathcal{L} = \mathbb{E} \| v_t(x_t) - u_t(x_t) \|^2
$$

👉 This is simple, stable, and avoids score estimation.

---

## 4. Connection to Diffusion Models

Diffusion models also define a path $p_t(x)$, but:

- They learn the **score function**:
  $$
  \nabla_x \log p_t(x)
  $$

- And simulate a **stochastic process** (SDE)

---

### Key Difference

| | Flow Matching | Diffusion Models |
|:---|:---|:---|
| Object learned | Velocity field $v_t(x)$ | Score $\nabla \log p_t(x)$ |
| Dynamics | Deterministic (ODE) | Stochastic (SDE) |
| Training | Regression | Score matching |

---

## 5. Unifying View

Both methods describe **transport of probability**:

- Diffusion: stochastic transport  
- Flow Matching: deterministic transport  

In fact, under certain conditions, diffusion models can be rewritten as ODEs, leading to:

👉 **Probability Flow ODE**

This shows that:
> Flow Matching and Diffusion are two views of the same underlying dynamics.

---

## 6. Why Flow Matching?

- Simpler objective (no score estimation)
- Often faster sampling (ODE)
- More flexible path design

---

## 7. Takeaway

Flow Matching reframes generative modeling as:

> Learning a vector field that transports probability mass from noise to data.

This provides a clean, physically grounded alternative to diffusion models.
