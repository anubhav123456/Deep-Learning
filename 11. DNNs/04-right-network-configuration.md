# Neural Network Configuration & Hyperparameter Tuning

This lecture continues the discussion on **classification** and explains an important practical question:

> **If we know how a neural network works, how do we decide its architecture?**

For example:

* How many hidden layers?
* How many neurons in each layer?
* What learning rate should we use?
* Which optimization algorithm should we use?

The answer is: **Hyperparameter Tuning**.

---

### 1. Focus remains on Classification

The instructor decides to complete the entire story for **classification** first:

1. Model / Neural Network
2. Output layer $\rightarrow$ **Softmax**
3. Loss Function
4. Learning Algorithm

Regression will be discussed in the next chapter.

Also, **binary classification is treated as a special case of multiclass classification**.

If:

$$k = 2$$

then we simply have two classes.

---

### 2. Real-world data can have complex non-linearity

Suppose we have two input features:

$$x_1, x_2$$

and we want to predict an output ($y$).

Sometimes the classes may be separated by a simple linear boundary, but real-world data can have highly complex patterns such as:

* Circular boundaries
* Inner region belonging to one class and outer region to another
* Irregular shapes
* Highly complex nonlinear relationships

A **Deep Neural Network** can learn and approximate these nonlinear relationships.

---

### 3. The main problem: How do we choose the network architecture?

We know that neural networks can model complex functions.

But we don't automatically know:

> **What exact neural network architecture is best for our problem?**

For example, should we use:

#### Network A

* 1 hidden layer
* Few neurons

#### Network B

* 2 hidden layers
* Different number of neurons

#### Network C

* 3 hidden layers
* More neurons

#### Network D

* Same number of neurons in every layer

There can be many possible configurations.

---

### 4. High-dimensional data makes visualization impossible

With 2 or 3 input features, we can visualize the data and get some intuition about its structure.

But real-world datasets often have:

$$1,000,\ 10,000,\ \text{or even millions of features}$$

In such high-dimensional spaces, we cannot visualize the data and say:

> "This data has this particular type of non-linearity, so I should use exactly this neural network."

Therefore, in practice, we need to **experiment with different architectures**.

---

### 5. Try multiple neural network configurations

The practical approach is:

#### Step 1: Create different network architectures

For example:

$$\text{Model 1: 1 hidden layer}$$

$$\text{Model 2: 2 hidden layers}$$

$$\text{Model 3: More neurons}$$

$$\text{Model 4: Different neuron distribution}$$

#### Step 2: Train all these models

#### Step 3: Calculate their loss

For example:

| Model | Loss |
| :--- | :---: |
| Model 1 | 0.45 |
| Model 2 | 0.32 |
| Model 3 | **0.18** |
| Model 4 | 0.29 |

If Model 3 performs best according to the relevant evaluation criteria, it may be the most suitable choice.

This overall process of choosing and testing different configurations is called: **Hyperparameter Tuning**.

---

### 6. What are Hyperparameters?

Hyperparameters are settings that we choose **before or during the training setup**, rather than values automatically learned as model weights.

Important hyperparameters include:

#### Architecture-related

* Number of hidden layers
* Number of neurons in each layer

#### Training-related

* Learning rate ($\eta$)
* Batch size
* Number of epochs

#### Optimization-related

* Gradient Descent
* Adam
* AdaGrad
* Other optimization algorithms

Different combinations can produce very different results.

---

### 7. This is a major part of an ML/DL Engineer's job

The instructor emphasizes that a significant part of practical deep learning involves:

> **Trying sensible configurations, evaluating them, and finding what works best.**

An ML/DL engineer generally does not invent a completely new neural network every day.

Instead, they often:

1. Understand the problem.
2. Prepare the data.
3. Choose candidate models.
4. Select architectures.
5. Tune hyperparameters.
6. Train multiple experiments.
7. Compare performance.
8. Improve the model.

---

### 8. Hyperparameter tuning is not random brute force

The goal is **not** to try millions of random neural networks.

That would be:

* Computationally expensive
* Time-consuming
* Inefficient

Instead, engineers use:

* Experience
* Intuition
* Previous research
* Best practices
* Systematic experimentation

Over time, you develop a better sense of which configurations are worth trying.

---

## The Complete Practical Flow

The main idea of this lecture can be represented as:

$$\text{Dataset}$$

$$\downarrow$$

$$\text{Choose multiple Neural Network architectures}$$

$$\downarrow$$

$$\text{Choose hyperparameters}$$

$$\downarrow$$

$$\text{Train Models}$$

$$\downarrow$$

$$\text{Calculate Loss / Evaluate Performance}$$

$$\downarrow$$

$$\text{Compare Models}$$

$$\downarrow$$

$$\text{Select the Best Configuration}$$

---

## Key Takeaway

> **There is no universal formula that tells us the perfect number of layers or neurons for every problem.**

In practice, we build several reasonable configurations and use **hyperparameter tuning** to find a configuration that performs well.