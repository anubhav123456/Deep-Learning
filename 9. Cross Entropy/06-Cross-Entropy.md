# Why Cross-Entropy Becomes the Loss Function

This lecture connects everything learned so far—probability distributions, entropy, cross-entropy, and KL divergence—back to the sigmoid neuron and binary classification.

---

### 1. Binary Classification Setup

Suppose we give the model an image and want to classify it as **Text** or **No Text**.

For this particular image, we already know the correct answer: it contains text. Therefore, the true distribution is:

$$y = [1, 0]$$

| Class | True Probability |
| :--- | :---: |
| **Text** | $1$ |
| **No Text** | $0$ |

All probability mass is concentrated on the correct class.

---

### 2. Model Prediction Using Sigmoid

The image is passed through a sigmoid neuron. Suppose the sigmoid output is $0.7$. This means:

$$P(\text{Text}) = 0.7 \implies P(\text{No Text}) = 1 - 0.7 = 0.3$$

So the predicted distribution is:

$$\hat{y} = [0.7, 0.3]$$

Our goal is to adjust the model so that $\hat{y}$ becomes as close as possible to $y$.

---

### 3. Earlier: Squared Error Loss

Previously, we could measure the difference using squared error:

$$\sum_i (y_i - \hat{y}_i)^2$$

However, $y$ and $\hat{y}$ are not just ordinary vectors—they are **probability distributions**. Therefore, instead of squared error, we use a measure grounded in probability theory: **KL Divergence**.

---

### 4. KL Divergence Formulation

Recall that:

$$D_{\text{KL}}(y \parallel \hat{y}) = H(y, \hat{y}) - H(y)$$

Where:
* **Cross-Entropy:** $H(y, \hat{y}) = -\sum_i y_i \log \hat{y}_i$
* **Entropy:** $H(y) = -\sum_i y_i \log y_i$

Therefore:

$$D_{\text{KL}}(y \parallel \hat{y}) = -\sum_i y_i \log \hat{y}_i - H(y)$$

The ultimate goal during training is:

$$\boxed{\min_{w, b} D_{\text{KL}}(y \parallel \hat{y})}$$

We want to minimize the difference between the true distribution and the predicted distribution by changing the model parameters ($w = \text{weights}$, $b = \text{bias}$).

---

### 5. The Most Important Insight

Look carefully at the two components of KL Divergence:

$$D_{\text{KL}}(y \parallel \hat{y}) = \underbrace{-\sum_i y_i \log \hat{y}_i}_{\text{depends on } w, b} - \underbrace{H(y)}_{\text{constant}}$$

* The predicted probabilities ($\hat{y}_i$) depend on the model parameters ($w$ and $b$).
* The true labels ($y_i$) are fixed in the training data and do not depend on $w$ and $b$.

Therefore, the target label entropy $H(y)$ is a **constant** during optimization. 

Adding or subtracting a constant does not change where a minimum occurs:

$$\min_{w, b} [f(w, b) - C] \equiv \min_{w, b} f(w, b)$$

*(For example, $\min_x x^2$ and $\min_x (x^2 + 3)$ both reach their minimum at $x = 0$.)*

Consequently:

$$\boxed{\min_{w, b} D_{\text{KL}}(y \parallel \hat{y}) \equiv \min_{w, b} H(y, \hat{y})}$$

---

### 6. Therefore, We Use Cross-Entropy Loss

The final loss function simplifies directly to Cross-Entropy:

$$\boxed{\mathcal{L} = -\sum_i y_i \log \hat{y}_i}$$

---

### 7. Applying It to This Example

* **True distribution:** $y = [1, 0]$
* **Predicted distribution:** $\hat{y} = [0.7, 0.3]$

$$\mathcal{L} = -1 \log(0.7) - 0 \log(0.3) = -\log(0.7)$$

The second term disappears because $y_2 = 0$.

More generally, for any one-hot encoded label:

$$\boxed{\mathcal{L} = -\log(\hat{y}_c)}$$

where $c$ is the true target class.

---

### 8. Intuition: What Does the Loss Do?

Suppose the correct answer is **Text**:

* **Model 1 (Very confident & correct):** $P(\text{Text}) = 0.99 \implies \mathcal{L} = -\log(0.99) \approx 0$ ✅ *(Very small loss)*
* **Model 2 (Somewhat confident):** $P(\text{Text}) = 0.70 \implies \mathcal{L} = -\log(0.70) \approx 0.35$ *(Moderate loss)*
* **Model 3 (Wrong & confident):** $P(\text{Text}) = 0.01 \implies \mathcal{L} = -\log(0.01) \approx 4.60$ ❌ *(Very large loss)*

Cross-entropy heavily penalizes the model when it assigns a low probability to the correct answer.

---

### Final Big Picture

$$\text{Classification}$$
$$\Downarrow$$
$$\text{True label } (y) \text{ and Model output } (\hat{y}) \text{ represented as Probability Distributions}$$
$$\Downarrow$$
$$\text{Measure difference using KL Divergence: } D_{\text{KL}}(y \parallel \hat{y}) = H(y, \hat{y}) - H(y)$$
$$\Downarrow$$
$$\text{Since } H(y) \text{ is constant: } \boxed{\min D_{\text{KL}}(y \parallel \hat{y}) \equiv \min H(y, \hat{y})}$$
$$\Downarrow$$
$$\boxed{\text{Cross-Entropy Loss: } \mathcal{L} = -\log(\text{probability assigned to true class})}$$

---

### One-Line Takeaway

> **During training, Cross-Entropy Loss pushes the model to assign a probability close to $1$ to the correct class and close to $0$ to all incorrect classes.**