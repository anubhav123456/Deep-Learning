# Output Layer and Softmax Function

This lecture explains **how to choose the output function of a neural network** based on the type of problem.

### 1. Two main types of ML tasks

#### **Classification**

Example: Given an image, predict whether it belongs to one of **4 classes**.

The output should be a **probability distribution**:

$$\hat{y} = [\hat{y}_1, \hat{y}_2, \hat{y}_3, \hat{y}_4]$$

Requirements:

* Every probability must be **$\ge 0$**
* All probabilities must **sum to 1**

For example:

$$[0.1, 0.2, 0.6, 0.1]$$

Here, the model thinks Class 3 has a 60% probability.

---

#### **Regression**

Example: Given movie features, predict:

* IMDb rating
* Critics rating
* Rotten Tomatoes rating
* Box office collection

These outputs are real numbers:

$$\hat{y} \in \mathbb{R}^k$$

Regression does **not** require the outputs to sum to 1.

---

### 2. What happens before the output layer?

The neural network performs its normal computations until the final layer:

$$a_3 = W_3 h_2 + b_3$$

The values in $a_3$ can be **any real numbers**, including negative values.

For example:

$$a_3 = [3, 4, 10, 3]$$

or:

$$a_3 = [7, -2, 4, 1]$$

These values are often called **logits**.

---

### 3. Why can't we simply divide by the sum?

Suppose:

$$[3, 4, 10, 3]$$

You might try:

$$\left[ \frac{3}{20}, \frac{4}{20}, \frac{10}{20}, \frac{3}{20} \right]$$

This works because:

* All values are positive.
* The total becomes 1.

But consider:

$$[7, -2, 4, 1]$$

If we divide each value by the sum:

$$7 + (-2) + 4 + 1 = 10$$

we get:

$$[0.7, -0.2, 0.4, 0.1]$$

The sum is still 1, but **$-0.2$ is negative**.

A negative probability is impossible.

So simple normalization does not work for neural network outputs.

---

### 4. The solution: Softmax

We need a function that:

1. Converts every value into a positive number.
2. Makes all final outputs sum to 1.

The key observation is:

$$e^x > 0$$

for **every value of $x$**, even when $x$ is negative.

For example:

$$e^{-2} > 0$$

Therefore, we first apply exponentiation and then normalize.

The softmax formula for class $i$ is:

$$\hat{y}_i = \frac{e^{a_i}}{\sum_{j=1}^{k} e^{a_j}}$$

For 4 classes:

$$\hat{y}_1 = \frac{e^{a_1}}{e^{a_1} + e^{a_2} + e^{a_3} + e^{a_4}}$$

and similarly for the other classes.

---

### 5. Complete neural network flow for classification

The process looks like:

$$\text{Input} \rightarrow \text{Hidden Layers} \rightarrow a_3 = W_3 h_2 + b_3 \rightarrow \text{Softmax} \rightarrow \hat{y}$$

Where:

$$a_3$$

contains arbitrary real values, and:

$$\hat{y} = \text{Softmax}(a_3)$$

is a valid probability distribution.

---

## The main takeaway

| Problem | Output Type | Output Function |
| :--- | :--- | :--- |
| **Multi-class Classification** | Probabilities | **Softmax** |
| **Regression** | Real numbers | Depends on the regression setup |

### Softmax guarantees:

$$\hat{y}_i > 0$$

and

$$\sum_i \hat{y}_i = 1$$

So, for a multi-class classification problem, the neural network produces **logits** in the final layer, and then **Softmax converts those logits into probabilities**.

### In one line:

> **Logits $\rightarrow$ Softmax $\rightarrow$ Probability distribution $\rightarrow$ Choose the class with the highest probability**

The next logical topic after this lecture is **what output function should be used for regression problems**, followed by **how to calculate the loss between the true output and predicted output**.