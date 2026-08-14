# Binary Cross-Entropy Loss with a Sigmoid Neuron

This lecture takes the general cross-entropy formula and simplifies it specifically for a binary classification problem using a sigmoid neuron.

The final result is the famous **Binary Cross-Entropy Loss**:

$$\boxed{\mathcal{L} = -\left[y \log(\hat{y}) + (1 - y) \log(1 - \hat{y})\right]}$$

Let's understand how we get there step-by-step.

---

### 1. The Binary Classification Problem

We have an image, and the task is to predict:
* $0 \longrightarrow \text{No Text}$
* $1 \longrightarrow \text{Text}$

Suppose the image actually contains text, so $y = 1$.

The sigmoid neuron processes the image and outputs $\hat{y} = 0.7$. Since sigmoid outputs a value between $0$ and $1$, we interpret it as:

$$P(\text{Text}) = 0.7 \implies P(\text{No Text}) = 1 - 0.7 = 0.3$$

---

### 2. Constructing Probability Distributions

* **True Label ($y = 1$):** Represented as the distribution $[0, 1]$

| Class | True Probability |
| :--- | :---: |
| **No Text ($0$)** | $0$ |
| **Text ($1$)** | $1$ |

* **Predicted Label ($\hat{y} = 0.7$):** Represented as $[1 - \hat{y},\ \hat{y}] = [0.3, 0.7]$

Now we compare:
* **True distribution:** $[0, 1]$
* **Predicted distribution:** $[0.3, 0.7]$

---

### 3. Applying Cross-Entropy

The general cross-entropy formula across classes is:

$$\mathcal{L} = -\sum_i y_i \log(\hat{y}_i)$$

For a binary classification task (Class $0$ and Class $1$):

$$\mathcal{L} = -\left[ y_0 \log(\hat{y}_0) + y_1 \log(\hat{y}_1) \right]$$

Substituting $\hat{y}_1 = \hat{y}$ and $\hat{y}_0 = 1 - \hat{y}$:

$$\mathcal{L} = -\left[ (1 - y) \log(1 - \hat{y}) + y \log(\hat{y}) \right]$$

---

### 4. Case 1: True Label is 1 ($y = 1$)

The true distribution is $[0, 1]$. Substituting $y_0 = 0$ and $y_1 = 1$:

$$\mathcal{L} = -\left[ 0 \cdot \log(1 - \hat{y}) + 1 \cdot \log(\hat{y}) \right]$$

$$\boxed{\mathcal{L} = -\log(\hat{y})}$$

* **Example:** If $\hat{y} = 0.7$, then $\mathcal{L} = -\log(0.7)$. The closer $\hat{y}$ is pushed toward $1$, the smaller the loss becomes.

---

### 5. Case 2: True Label is 0 ($y = 0$)

Suppose the image does not contain text ($y = 0$).

If the sigmoid predicts $\hat{y} = 0.2$, this means $P(\text{Text}) = 0.2$ and $P(\text{No Text}) = 0.8$.

The true distribution is $[1, 0]$. Substituting $y_0 = 1$ and $y_1 = 0$:

$$\mathcal{L} = -\left[ 1 \cdot \log(1 - \hat{y}) + 0 \cdot \log(\hat{y}) \right]$$

$$\boxed{\mathcal{L} = -\log(1 - \hat{y})}$$

* **Example:** $\mathcal{L} = -\log(1 - 0.2) = -\log(0.8)$.

---

### 6. Combining the Cases

So far, the loss acts as a piecewise function:

$$\mathcal{L} = \begin{cases} -\log(\hat{y}), & \text{if } y = 1 \\ -\log(1 - \hat{y}), & \text{if } y = 0 \end{cases}$$

To avoid piecewise `if-else` branching during optimization/backpropagation, we combine both cases into a single smooth mathematical formulation:

$$\boxed{\mathcal{L} = -\left[ y \log(\hat{y}) + (1 - y) \log(1 - \hat{y}) \right]}$$

---

### 7. Why Does This Unified Formula Work?

* **When $y = 1$:**  
  $$\mathcal{L} = -\left[ 1 \log(\hat{y}) + 0 \log(1 - \hat{y}) \right] \implies \boxed{\mathcal{L} = -\log(\hat{y})}$$

* **When $y = 0$:**  
  $$\mathcal{L} = -\left[ 0 \log(\hat{y}) + 1 \log(1 - \hat{y}) \right] \implies \boxed{\mathcal{L} = -\log(1 - \hat{y})}$$

---

### 8. Intuition: What Does the Loss Do?

Cross-entropy always measures:

$$\boxed{-\log(\text{probability assigned to the correct class})}$$

* **Model is correct and confident ($y=1, \hat{y}=0.99$):**  
  $\mathcal{L} = -\log(0.99) \approx 0$ ✅ *(Very small loss)*

* **Model is uncertain ($y=1, \hat{y}=0.50$):**  
  $\mathcal{L} = -\log(0.50) \approx 0.69$ *(Moderate loss)*

* **Model is confidently wrong ($y=1, \hat{y}=0.01$):**  
  $\mathcal{L} = -\log(0.01) \approx 4.60$ ❌ *(Very large penalty)*

> **Binary Cross-Entropy severely penalizes models that make wrong predictions with high confidence.**

---

### Main Takeaway

$$\boxed{\mathcal{L} = -\left[ y \log(\hat{y}) + (1 - y) \log(1 - \hat{y}) \right]}$$

Where:
* $y \in \{0, 1\}$ = Ground truth label
* $\hat{y} \in (0, 1)$ = Sigmoid model prediction

This single unified equation automatically simplifies to $-\log(\hat{y})$ when $y=1$ and $-\log(1-\hat{y})$ when $y=0$.