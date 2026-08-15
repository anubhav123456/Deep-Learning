# Universal Approximation Theorem 
# How Neural Networks Approximate Any Function

This lecture provides an intuitive proof of the **Universal Approximation Theorem (UAT)**.

> **Central Question:** How can a collection of simple sigmoid neurons approximate an arbitrarily complex, non-linear function?

---

### 1. The Core Objective

Suppose there is an unknown target function $y = f(x)$ representing a complex real-world relationship:

Instead of manually deriving an intricate equation for $f(x)$, we construct an approximating function $\hat{y} = \hat{f}(x)$ using a neural network.

The Universal Approximation Theorem guarantees that a neural network can approximate any continuous function to arbitrary accuracy given enough neurons.

---

### 2. Strategy: Decomposing a Function into Towers

Instead of trying to fit a complex curve in a single step:

$$\text{Complex Function} \longrightarrow \text{Decompose into step functions / rectangular towers}$$

Each rectangular tower:
* Has a specific height (amplitude)
* Exists only within a narrow interval $[x_1, x_2]$
* Outputs $0$ everywhere outside that interval

We can express the continuous curve as a linear combination of these localized basis functions:

$$\hat{f}(x) = \sum_{i=1}^{N} f_i(x) = f_1(x) + f_2(x) + \dots + f_N(x)$$

$$\boxed{\text{More & Thinner Towers} \implies \text{Finer Granularity} \implies \text{Higher Approximation Precision}}$$

---

### 3. How Sigmoid Neurons Construct a "Tower"

A standard sigmoid activation function $\sigma(z) = \frac{1}{1 + e^{-z}}$ transitions smoothly from $0$ to $1$. 

By increasing the weight parameter $w \to \infty$, the sigmoid curve becomes extremely steep, acting like a sharp **step function**:

$$\sigma(wx + b) \approx H(x - x_0)$$

Now, subtracting two appropriately shifted steep sigmoids isolates a bounded region:

$$\text{Tower}(x) = \sigma(w_1 x + b_1) - \sigma(w_2 x + b_2)$$

#### Evaluation across regions:
* **Region 1 ($x < x_1$):** Both sigmoids output $0 \implies 0 - 0 = 0$
* **Region 2 ($x_1 \le x \le x_2$):** First sigmoid is $1$, second is $0 \implies 1 - 0 = 1$
* **Region 3 ($x > x_2$):** Both sigmoids output $1 \implies 1 - 1 = 0$

$$\boxed{\text{Sigmoid}_1 - \text{Sigmoid}_2 \approx \text{Tower Function}}$$

---

### 4. Neural Network Architecture for One Tower

A two-layer sub-network takes input $x$ into two parallel sigmoid neurons:

The output node calculates the linear combination with weights $+1$ and $-1$:

$$\text{Output} = (+1)\sigma(w_1 x + b_1) + (-1)\sigma(w_2 x + b_2)$$

---

### 5. Multi-Tower Network Architecture

To approximate the complete function, we stack multiple tower units in parallel across a single hidden layer and aggregate their outputs:

$$\hat{f}(x) = \sum_{k=1}^{M} c_k \left[ \sigma(w_{k,1} x + b_{k,1}) - \sigma(w_{k,2} x + b_{k,2}) \right]$$

By tuning the parameters ($w, b,$ and output weight $c$), we precisely control:
* **Location:** Where each tower starts and ends
* **Width:** The interval range $[x_1, x_2]$
* **Height:** The amplitude scaling factor $c_k$

---

### 6. The Complete UAT Proof Flow

$$\text{Unknown Target } y = f(x)$$
$$\Downarrow$$
$$\text{Decompose into } N \text{ Rectangular Towers}$$
$$\Downarrow$$
$$\text{Construct Each Tower using Pair of Sigmoids: } \sigma(w_1 x + b_1) - \sigma(w_2 x + b_2)$$
$$\Downarrow$$
$$\boxed{\text{Combine Towers in Hidden Layer} \implies \text{Universal Function Approximation}}$$

---

### Main Takeaway

> **You do not need to manually invent complex mathematical formulas for real-world tasks. By pairing sigmoid neurons with steep weights, a neural network creates step-like "towers." Combining many such towers allows a single-hidden-layer network to approximate any continuous function to arbitrary precision.**