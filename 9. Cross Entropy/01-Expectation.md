# Introduction to Expectation

This lecture begins the journey toward understanding Cross-Entropy Loss.

The instructor explains that the upcoming concepts will be studied in this order:

$$\boxed{\text{Expectation} \longrightarrow \text{Information Content} \longrightarrow \text{Entropy} \longrightarrow \text{Cross-Entropy}}$$

The final goal is to use Cross-Entropy as a way to measure the difference between:

$$\text{True Distribution } (y) \quad \text{and} \quad \text{Predicted Distribution } (\hat{y})$$

---

### 1. What Is Expectation?

The lecture explains expectation intuitively as the average value you expect to receive, considering all possible outcomes and their probabilities.

> **Key Idea:** Multiply each possible outcome's value by its probability, then sum everything together.

---

### 2. Example: Betting on Four Teams

Suppose there are four teams: $A, B, C, D$. The random variable $X$ represents the winning team with the following probability distribution:

| Team | Probability |
| :--- | :---: |
| **A** | $0.4$ |
| **B** | $0.2$ |
| **C** | $0.1$ |
| **D** | $0.3$ |

Now suppose your profit or loss depends on which team wins:

| Winning Team | Profit / Loss |
| :--- | :---: |
| **A** | ₹10,000 |
| **B** | ₹2,000 |
| **C** | -₹8,000 |
| **D** | ₹5,000 |

*Note: Team C gives a negative value, representing a financial loss.*

---

### 3. Calculating Expected Profit

To calculate the expected profit, multiply every profit by the probability of that outcome:

$$\mathbb{E}[\text{Profit}] = (0.4)(10000) + (0.2)(2000) + (0.1)(-8000) + (0.3)(5000)$$

Calculating this step-by-step:

$$= 4000 + 400 - 800 + 1500$$

$$\boxed{\mathbb{E}[\text{Profit}] = \text{₹}5100}$$

This does not necessarily mean that you will earn exactly ₹5,100 in a single bet. Instead, it represents the long-run average outcome over many similar trials, assuming the underlying probabilities are accurate.

---

### 4. General Formula for Expectation

Suppose a random variable $X$ can take several values. For every possible value $x$:

1. Find its probability: $P(X=x)$
2. Find the quantity/value associated with that outcome: $G(x)$

Then the expectation is defined as:

$$\boxed{\mathbb{E}[G(X)] = \sum_x P(X=x)G(x)}$$

In simple words:

$$\boxed{\text{Expectation} = \sum (\text{Probability of outcome}) \times (\text{Value associated with outcome})}$$

---

### 5. Important Concept: Functions of Random Variables

The value associated with an outcome does not have to be the raw random variable itself.

For example:

$$X = \text{Winning Team } \in \{A, B, C, D\}$$

We cannot directly average categorical letters like $A, B, C,$ and $D$. Instead, we map each outcome to a quantitative scalar using a function $G(X) = \text{Profit}$:

* $G(A) = 10000$
* $G(B) = 2000$
* $G(C) = -8000$
* $G(D) = 5000$

Then we calculate the expected value of this function, $\mathbb{E}[G(X)]$.

---

### Main Takeaway

> **Expectation is a probability-weighted average of a quantity across all possible outcomes.**

$$\boxed{\mathbb{E}[G(X)] = \sum_x P(X=x)G(x)}$$

This concept serves as the core foundation because the subsequent concepts—**Information Content**, **Entropy**, and **Cross-Entropy**—are all built directly on expectations:

$$\boxed{\text{Probability Distribution} \longrightarrow \text{Expectation} \longrightarrow \text{Information Content} \longrightarrow \text{Entropy} \longrightarrow \text{Cross-Entropy Loss}}$$