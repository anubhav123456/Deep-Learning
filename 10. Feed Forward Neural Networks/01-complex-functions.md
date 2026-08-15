# Lecture Summary: Why Do We Need Complex Functions?

This lecture introduces the main motivation for moving from simple models—like the MP Neuron, Perceptron, and Sigmoid Neuron—toward **Feedforward Neural Networks**.

---

### 1. Quick Recap

So far, the course has covered:
* **MP Neuron**
* **Perceptron**
* **Sigmoid Neuron**
* Classification and limited regression
* Loss functions such as **Squared Error** and **Cross-Entropy**
* Optimization progressing from brute-force search to **Gradient Descent**
* Evaluation metrics such as **RMSE**

#### The Major Limitation
Despite their improvements, these simple models **cannot handle non-linearly separable data**.

---

### 2. The New Goal: Build More Powerful Functions

The central question for Feedforward Neural Networks is:

> **How can we construct complex, flexible functions that can model intricate relationships in real-world data?**

The lecture emphasizes two mathematical constraints for these functions:
1. **Continuous**
2. **Differentiable**

Because training relies on **Gradient Descent**, every component function within the model must allow differentiation so gradients can be calculated and propagated.

---

### 3. Practical Example: The Smartphone Preference Problem

Consider a dataset with two features:
* **Screen Size**
* **Cost**

Suppose a customer only likes phones that satisfy *both* conditions:
* **Screen size:** Between $3.5$ and $4.5$ inches
* **Price:** Between ₹$8,000$ and ₹$12,000$
* **Desired region (inside box):** Output $= 1$
* **Undesired region (outside box):** Output $= 0$

#### Why Simple Models Fail
You **cannot draw a single straight line** to separate the desired phones from all surrounding undesired phones. This dataset is fundamentally **non-linearly separable**.

---

### 4. What Kind of Function Do We Need?

Conceptually, we need a function that outputs $1$ inside a bounded interval and $0$ everywhere else:

$$\text{Output: } 0 \longrightarrow \text{gradually rises to } 1 \longrightarrow \text{gradually falls to } 0$$

Smooth, continuous curves (rather than step functions with sharp edges) are essential so that the function remains differentiable for Gradient Descent.

---

### 5. Why Can't a Single Sigmoid Neuron Solve This?

A sigmoid neuron has parameters $w_1, w_2,$ and $b$. Adjusting these parameters rotates or shifts the decision boundary surface.

However, a sigmoid function inherently produces a **monotonically increasing or decreasing S-shaped curve** ($\sigma(z)$). It can only create a single transition from low to high:

$$\text{Sigmoid Profile: } 0 \longrightarrow 1 \quad \text{or} \quad 1 \longrightarrow 0$$

It **cannot** independently rise, peak, and fall again ($0 \to 1 \to 0$) to isolate a closed middle region. Therefore, a single sigmoid neuron lacks sufficient representation power.

---

### The Core Idea

Simple models can only represent simple, linearly separable relationships:

$$\boxed{\text{Complex Non-Linear Data} \implies \text{Requires Higher Representation Power} \implies \text{Feedforward Neural Networks}}$$

By stacking and combining simpler functions (neurons) across multiple layers, neural networks can approximate arbitrarily complex non-linear decision boundaries.

---

### In One Sentence

> **The purpose of neural networks is to increase the representation power of our models so they can learn complex, non-linear relationships that a single perceptron or sigmoid neuron cannot represent.**