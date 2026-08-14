# Information Content

This lecture introduces **Information Content (IC)**, which is the next concept in the journey toward understanding Entropy and eventually Cross-Entropy Loss.

$$\boxed{\text{Expectation} \longrightarrow \text{Information Content} \longrightarrow \text{Entropy} \longrightarrow \text{Cross-Entropy}}$$

---

### 1. What Is Information Content?

The basic intuition is:

> **The more surprising an event is, the more information we gain when we learn that it happened.**

* **Example 1: Sun rises in the East**  
  Suppose someone tells you: *"Today, the sun rose in the East."*  
  This gives you almost no new information because it is a certain event ($P \approx 1$).
  $$\boxed{\text{High Probability} \implies \text{Low Surprise} \implies \text{Low Information}}$$

* **Example 2: A rare storm**  
  Suppose someone tells you: *"There will be a storm today."*  
  If storms are very rare in your area, this event has a low probability. Learning that it happened gives you much more information.
  $$\boxed{\text{Low Probability} \implies \text{High Surprise} \implies \text{High Information}}$$

---

### 2. First Requirement for Information Content

Information content must be a function of probability: $IC = f(P)$.

Since $P \downarrow \implies IC \uparrow$, the function should inversely scale with probability:

$$IC \propto \frac{1}{P}$$

---

### 3. Second Requirement: Independent Events

Suppose there are two independent events:
* **Event $X$:** Team B wins a match.
* **Event $Y$:** The AC in a room is ON.

Learning both pieces of information should equal the sum of their individual information contents:

$$IC(X, Y) = IC(X) + IC(Y)$$

Since the events are independent, their joint probability is:

$$P(X, Y) = P(X) \cdot P(Y)$$

Therefore, our function must satisfy:

$$f(a \cdot b) = f(a) + f(b)$$

---

### 4. Why Do We Use Logarithms?

The logarithm naturally converts multiplication into addition:

$$\log(a \cdot b) = \log(a) + \log(b)$$

To ensure rare events have higher information content, we apply the logarithm to the reciprocal of probability:

$$IC(X=A) = \log\left(\frac{1}{P(X=A)}\right) = -\log(P(X=A))$$

In information theory, base $2$ is standard (measuring information in bits):

$$\boxed{IC(X=A) = -\log_2(P(X=A))}$$

---

### 5. Numerical Examples

* **Case 1: Certain Event ($P=1$)**
  $$IC(X) = -\log_2(1) = 0 \text{ bits}$$
  $$\boxed{\text{A certain event gives 0 bits of new information.}}$$

* **Case 2: Fair Coin Flip ($P=0.5$)**
  $$IC(X) = -\log_2(0.5) = 1 \text{ bit}$$

* **Case 3: Rare Event ($P=0.125 = \frac{1}{8}$)**
  $$IC(X) = -\log_2\left(\frac{1}{8}\right) = 3 \text{ bits}$$

#### Summary Table

| Probability of Event | Information Content |
| :--- | ---: |
| **1.0** | $0$ bits |
| **0.5** | $1$ bit |
| **0.25** | $2$ bits |
| **0.125** | $3$ bits |

---

### Summary: The Two Pillars of the Formula

$$\boxed{IC(x) = -\log_2(P(x))}$$

1. **Surprise (Inversely proportional):** Lower probability events yield higher information ($P(x)\downarrow \implies IC(x)\uparrow$).
2. **Additivity (Logarithmic property):** Ensures $IC(X,Y) = IC(X) + IC(Y)$ when $P(X,Y) = P(X)P(Y)$.

---

### Main Takeaway

$$\boxed{\text{Information Content of an event} = -\log_2(\text{Probability of that event})}$$

Combining **Expectation** with **Information Content** leads directly to **Entropy**:

$$\boxed{\text{Entropy} = \text{Expected Information Content}}$$

*This directly sets up the mathematical foundation for Cross-Entropy Loss in classification models.*