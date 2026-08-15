# Data and Tasks in Deep Neural Networks (DNNs)

This lecture introduces the **types of data and machine learning tasks** where Deep Neural Networks can be used.

### 1. Multi-Class Classification — MNIST Example

The first example is the **MNIST handwritten digit dataset**.

* Each image contains a handwritten digit from **0 to 9**.
* Each image has a size of **28 × 28 pixels**.
* Therefore, there are:

$$28 \times 28 = 784$$

pixel values.

The image matrix can be **flattened** into a single input vector:

$$x \in \mathbb{R}^{784}$$

Before feeding the image into the neural network, pixel values can be **normalized**, for example from their original range to **0–1**.

The output ($y$) can belong to one of **10 classes**:

$$y \in \{0, 1, 2, \dots, 9\}$$

This is called a **multi-class classification problem**.

The correct output can be represented using **one-hot encoding**. For example, if the image represents digit 0:

$$y = [1, 0, 0, 0, 0, 0, 0, 0, 0, 0]$$

The neural network predicts a probability distribution over all 10 classes, which can later be compared with the true distribution.

---

### 2. Binary Classification

The second type of problem is **binary classification**.

Example:

> Given a patient's medical information, predict whether the patient has liver disease or not.

Here, the output has only two possible classes:

$$y \in \{0, 1\}$$

For example:

* $0 \rightarrow$ No disease
* $1 \rightarrow$ Disease

Binary classification is essentially a special case of multi-class classification where:

$$k = 2$$

---

### 3. Regression

The third type of problem is **regression**.

Example:

> Given information about a locality or house, predict its price.

The output is not selected from a fixed set of classes. Instead, it can be any appropriate real number:

$$y \in \mathbb{R}$$

For example:

$$y = \text{₹}24,00,000$$

So, unlike classification, regression predicts a **continuous numerical value**.

---

## Main Difference Between the Three Tasks

| Task | Output |
| :--- | :--- |
| **Multi-Class Classification** | One out of $k$ possible classes |
| **Binary Classification** | One out of 2 classes |
| **Regression** | A continuous numerical value |

### Examples

* **Multi-class classification:** Identify whether an image is 0, 1, 2, ..., 9.
* **Binary classification:** Predict disease or no disease.
* **Regression:** Predict house price.

---

## Key Takeaway

According to the lecture, these three problem types:

1. **Regression**
2. **Binary Classification**
3. **Multi-Class Classification**

cover a large portion of real-world Machine Learning and Deep Learning applications.

The upcoming lectures will focus on understanding **how to design Deep Neural Networks for each of these three types of tasks**.

### One-line summary:

> **The lecture explains how different types of input data can be represented numerically and how Deep Neural Networks can solve three major types of problems: multi-class classification, binary classification, and regression.**