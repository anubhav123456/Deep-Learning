# Integration of Cross-Entropy into Machine Learning

This lecture explains how cross-entropy loss fits back into the standard machine learning training algorithm.

---

### 1. We Now Have a New Loss Function

Previously, the sigmoid neuron may have used squared error loss. Now, for binary classification, we use **Binary Cross-Entropy Loss**:

$$\mathcal{L} = -\left[ y \log(\hat{y}) + (1 - y) \log(1 - \hat{y}) \right]$$

Where:
* $y \in \{0, 1\}$ = True label
* $\hat{y} \in (0, 1)$ = Predicted probability from the sigmoid neuron

---

### 2. The Overall Learning Pipeline Remains Unchanged

Suppose the dataset contains training examples:

$$(x_1, y_1), (x_2, y_2), \dots, (x_N, y_N)$$

For every input:

$$x_i \longrightarrow \text{Sigmoid Model} \longrightarrow \hat{y}_i$$

So you get:
* **True outputs:** $(y_1, y_2, \dots, y_N)$
* **Predicted outputs:** $(\hat{y}_1, \hat{y}_2, \dots, \hat{y}_N)$

Then calculate the total loss across all training examples.

#### Pipeline Flow
$$\text{Data} \longrightarrow \text{Model} \longrightarrow \hat{y} \longrightarrow \text{Loss} \longrightarrow \text{Gradient} \longrightarrow \text{Update Weights}$$

---

### 3. Gradient Descent Still Works the Same Way

The basic parameter update rule does not change:

$$w \leftarrow w - \eta \frac{\partial \mathcal{L}}{\partial w}$$

$$b \leftarrow b - \eta \frac{\partial \mathcal{L}}{\partial b}$$

The only difference is:
* **Earlier:** Derivatives were calculated using **Squared Error Loss**.
* **Now:** Derivatives are calculated using **Binary Cross-Entropy Loss**.

The overall optimization algorithm remains Gradient Descent; only the loss function—and therefore its gradient—changes.

---

### Summary of the Training Steps

1. Take input vector $x$.
2. Pass it through the sigmoid neuron to get prediction $\hat{y} = \sigma(w^T x + b)$.
3. Compare true label $y$ and predicted output $\hat{y}$ using Cross-Entropy Loss.
4. Compute the gradient:
   $$\frac{\partial \mathcal{L}}{\partial w} \quad \text{and} \quad \frac{\partial \mathcal{L}}{\partial b}$$
5. Update weights and bias using the learning rate $\eta$.
6. Repeat for multiple epochs/iterations.

*The next lecture derives how to calculate the gradient of the new cross-entropy loss with respect to the model parameters ($w$ and $b$).*

---

### In One Sentence

> **Cross-entropy replaces squared error as the loss function, but the overall gradient descent learning process remains the same—we just need to derive a new gradient for the new loss function.**