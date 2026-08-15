# Cross-Entropy and KL Divergence

This lecture explains how to measure the difference between a **true probability distribution** ($y$) and an **estimated/predicted probability distribution** ($\hat{y}$).

$$\boxed{\text{Entropy} \longrightarrow \text{Cross-Entropy} \longrightarrow \text{KL Divergence}}$$

---

### 1. The Setup: True vs. Estimated Distribution

Suppose a random variable $X$ represents a message that can be $\{A, B, C, D\}$.

* **True Distribution ($y$):** The actual underlying probabilities of the messages.
  $$y = [y_1, y_2, y_3, y_4] \quad \text{where } P(X=A) = y_1, P(X=B) = y_2, \dots$$

* **Estimated Distribution ($\hat{y}$):** The probabilities predicted or estimated by a model.
  $$\hat{y} = [\hat{y}_1, \hat{y}_2, \hat{y}_3, \hat{y}_4]$$

---

### 2. If We Knew the True Distribution (Entropy)

If we knew the actual probabilities, the minimum average number of bits required to encode messages is given by **Entropy**:

$$\boxed{H(y) = -\sum_i y_i \log_2 y_i}$$

This represents the **optimal expected cost** (ideal code length per message).

---

### 3. What If We Only Know an Estimated Distribution? (Cross-Entropy)

Suppose we construct our encoding scheme using our estimate $\hat{y}$. The code length assigned to message $i$ will be:

$$-\log_2 \hat{y}_i \text{ bits}$$

However, messages actually occur according to the **true distribution** $y$. Therefore, the expected number of bits we actually end up using is:

$$\boxed{H(y, \hat{y}) = -\sum_i y_i \log_2 \hat{y}_i}$$

This quantity is called **Cross-Entropy**.

---

### 4. Extra Cost & KL Divergence

Comparing the two costs:

* **Ideal cost (Entropy):** $H(y) = -\sum_i y_i \log_2 y_i$
* **Actual cost with estimated code (Cross-Entropy):** $H(y, \hat{y}) = -\sum_i y_i \log_2 \hat{y}_i$

The difference between them represents the **extra penalty/cost** incurred by using an incorrect distribution:

$$\text{Extra bits} = H(y, \hat{y}) - H(y)$$

This excess cost is called **Kullback–Leibler (KL) Divergence**:

$$\boxed{D_{\text{KL}}(y \parallel \hat{y}) = H(y, \hat{y}) - H(y)}$$

Expanding the formula:

$$D_{\text{KL}}(y \parallel \hat{y}) = -\sum_i y_i \log_2 \hat{y}_i - \left( -\sum_i y_i \log_2 y_i \right)$$

$$\boxed{D_{\text{KL}}(y \parallel \hat{y}) = \sum_i y_i \log_2 \left(\frac{y_i}{\hat{y}_i}\right)}$$

---

### 5. Intuition Behind KL Divergence

KL Divergence measures **how much extra information or encoding overhead is incurred** due to using $\hat{y}$ instead of $y$:

* **If $\hat{y} = y$:** $D_{\text{KL}}(y \parallel \hat{y}) = 0$ (Zero extra cost; perfect prediction).
* **If $\hat{y}$ differs from $y$:** $D_{\text{KL}}(y \parallel \hat{y}) > 0$ (Cost increases as the distributions diverge).

---

### 6. Why Cross-Entropy Matters for Machine Learning

In a classification task:
* **True label ($y$):** $[0, 1]$ (e.g., One-Hot vector for Text)
* **Model prediction ($\hat{y}$):** $[0.3, 0.7]$

Rearranging the fundamental relationship:

$$\boxed{H(y, \hat{y}) = H(y) + D_{\text{KL}}(y \parallel \hat{y})}$$

Since the true label distribution $y$ is fixed and non-trainable, its entropy **$H(y)$ is a constant**.

Therefore:

$$\min_{\theta} D_{\text{KL}}(y \parallel \hat{y}) \equiv \min_{\theta} H(y, \hat{y})$$

> **Minimizing Cross-Entropy directly minimizes KL Divergence**, forcing the model's predicted distribution $\hat{y}$ closer to the true distribution $y$. This makes Cross-Entropy the natural loss function for training classification models.

---

### Complete Flow of the Concept

$$\text{Probability Distribution}$$
$$\Downarrow$$
$$\text{Information Content: } IC(x) = -\log_2 P(x)$$
$$\Downarrow$$
$$\text{Entropy: } H(y) = -\sum_i y_i \log_2 y_i$$
$$\Downarrow$$
$$\text{Cross-Entropy: } H(y, \hat{y}) = -\sum_i y_i \log_2 \hat{y}_i$$
$$\Downarrow$$
$$\text{KL Divergence: } D_{\text{KL}}(y \parallel \hat{y}) = H(y, \hat{y}) - H(y)$$
$$\Downarrow$$
$$\boxed{\text{Minimize Cross-Entropy Loss} \implies \text{Align Predicted Distribution } \hat{y} \text{ with True Distribution } y}$$

---

### Main Takeaway

> **Entropy is the optimal average encoding cost when the true distribution is known. Cross-entropy is the actual average cost incurred when encoding based on an estimated distribution. Their difference is KL Divergence. Because the true label entropy is constant, minimizing Cross-Entropy Loss during training is mathematically equivalent to minimizing the KL Divergence between prediction and ground truth.**