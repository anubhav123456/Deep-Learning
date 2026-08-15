# Entropy = Expected Information Content

This lecture combines all the concepts learned so far and uses them to define **Entropy**.

$$\boxed{\text{Random Variable} \longrightarrow \text{Probability Distribution} \longrightarrow \text{Information Content} \longrightarrow \text{Expectation} \longrightarrow \text{Entropy}}$$

---

### 1. Quick Recap of Previous Concepts

#### Random Variable
Suppose $X$ represents the winning team in a tournament:

$$X \in \{A, B, C, D\}$$

The random variable can take one of these possible values.

#### Probability Distribution
A distribution assigns a probability to every possible value of the random variable:

$$P(X=A), \quad P(X=B), \quad P(X=C), \quad P(X=D)$$

All probabilities must sum to $1$:

$$\sum_i P(X=i) = 1$$

#### Information Content
The information content ($IC$) of an event is:

$$IC(X=i) = -\log_2 P(X=i)$$

$$\boxed{\text{Rare Event} \implies \text{More Surprise} \implies \text{More Information}}$$

* **High probability:** Low information content
* **Low probability:** High information content

#### Expectation
Expectation is a **probability-weighted average**. If every outcome $i$ has an associated quantity $G(i)$, then:

$$\mathbb{E}[G(X)] = \sum_i P(X=i) G(i)$$

---

### 2. What Is Entropy?

Instead of associating profit or gain with every outcome, we associate its **information content**:

$$\text{Value associated with outcome } i = -\log_2 P(X=i)$$

To find the **average information content**, we calculate its expectation:

$$H(X) = \mathbb{E}[IC(X)] = \sum_i P(X=i) \times IC(X=i)$$

Substituting the formula for information content:

$$H(X) = \sum_i P(X=i) \left[-\log_2 P(X=i)\right]$$

Factoring out the negative sign gives the standard formula for **Entropy**:

$$\boxed{H(X) = -\sum_i P(X=i) \log_2 P(X=i)}$$

---

### 3. The Most Important Definition

$$\boxed{\text{Entropy = Expected Information Content}}$$

> **Entropy tells us the average amount of information (or surprise) we expect to gain when observing the outcome of a random variable.**

For our four-team example:

$$H(X) = -\sum_{i \in \{A,B,C,D\}} P(X=i) \log_2 P(X=i)$$

---

### Intuition: Measuring Uncertainty

* **Situation 1: One outcome is almost certain ($P = [0.99, 0.01]$)**  
  There is very little uncertainty because we almost know what will happen. Therefore, **Entropy is low**.

* **Situation 2: Outcomes are equally likely ($P = [0.5, 0.5]$)**  
  There is maximum uncertainty because we genuinely cannot predict the outcome. Therefore, **Entropy is higher**.

$$\boxed{\text{Higher Uncertainty} \implies \text{Higher Entropy}}$$

---

### Main Takeaway

> **Entropy is not the information content of a single specific event. It is the weighted average (expected) information content across all possible outcomes.**

$$\boxed{H(X) = -\sum_i P(X=i) \log_2 P(X=i)}$$

*The next concept will connect entropy to transmission efficiency and coding theory—specifically, the minimum average number of bits required to encode a message.*