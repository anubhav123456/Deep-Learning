# Entropy and the Average Number of Bits

This lecture gives a very important practical interpretation of entropy:

$$\boxed{\text{Entropy = Average number of bits required to transmit information}}$$

It connects probability, information content, binary encoding, and entropy.

---

### 1. Recap: Entropy Formula

Previously, entropy was defined as the expected information content:

$$\boxed{H(X) = -\sum_i p_i \log_2 p_i}$$

where $p_i = P(X=i)$.

The lecturer now explains why this formula also represents the average number of bits needed to transmit messages.

---

### 2. Equal Probability Messages

Suppose you have 4 possible messages: $A, B, C, D$.

To transmit 4 different messages digitally, we need:

$$\log_2(4) = 2 \text{ bits}$$

For example:

| Message | Binary Code |
| :--- | :---: |
| **A** | `00` |
| **B** | `01` |
| **C** | `10` |
| **D** | `11` |

Every message requires 2 bits.

#### Why does information content also equal 2?
If all four messages are equally likely ($P(A) = P(B) = P(C) = P(D) = \frac{1}{4}$), the information content of any message is:

$$IC = -\log_2\left(\frac{1}{4}\right) = 2 \text{ bits}$$

Therefore:

$$\boxed{\text{Information Content} = \text{Number of bits required}}$$

for an equally likely message.

---

### 3. Example with 8 Messages

If there are 8 equally likely messages ($A, B, C, D, E, F, G, H$), we need:

$$\log_2(8) = 3 \text{ bits}$$

to represent each message (`000`, `001`, `010`, $\dots$, `111`).

Each message has probability $\frac{1}{8}$, and its information content is:

$$-\log_2\left(\frac{1}{8}\right) = 3 \text{ bits}$$

Again:

$$\boxed{\text{Number of bits} = \text{Information Content}}$$

---

### 4. What If Some Messages Are More Frequent?

This is the most important part of the lecture.

Suppose the message probabilities are:

| Message | Probability | Information Content / Bits |
| :--- | :---: | ---: |
| **A** | $1/2$ | $1$ bit |
| **B** | $1/4$ | $2$ bits |
| **C** | $1/8$ | $3$ bits |
| **D** | $1/8$ | $3$ bits |

The general formula is:

$$\boxed{\text{Bits for a message} = -\log_2(P(\text{message}))}$$

So:

$$\boxed{\text{More frequent message} \implies \text{Fewer bits}}$$

$$\boxed{\text{Rare message} \implies \text{More bits}}$$

---

### 5. Calculating the Average Number of Bits

Now we calculate the expected number of bits:

$$\mathbb{E}[\text{Bits}] = \frac{1}{2}(1) + \frac{1}{4}(2) + \frac{1}{8}(3) + \frac{1}{8}(3)$$

$$= 0.5 + 0.5 + 0.375 + 0.375 = \boxed{1.75 \text{ bits}}$$

Compare this with the uniform approach, where we used 2 bits for every message. By using the probability distribution intelligently:

$$\boxed{2 \text{ bits} \longrightarrow 1.75 \text{ bits on average}}$$

We save bits on average.

---

### 6. Connection to Entropy

The average number of bits is calculated as:

$$\sum_i p_i \left(-\log_2 p_i\right) = -\sum_i p_i \log_2 p_i$$

This is **exactly** the formula for entropy:

$$\boxed{H(X) = -\sum_i p_i \log_2 p_i}$$

Therefore:

$$\boxed{\text{Entropy of } X = \text{Expected Information Content} = \text{Average bits required to encode } X}$$

---

### The Core Intuition

Suppose you are sending messages continuously. If you know some messages occur frequently, it makes sense to give them shorter representations:

* **Very common message** $\rightarrow$ Short binary code
* **Rare message** $\rightarrow$ Longer binary code

Because common messages occur more often, using fewer bits for them reduces overall communication cost (the foundation of efficient encoding like **Huffman Coding**).

---

### Complete Connection So Far

$$\boxed{\text{Probability of Event} \longrightarrow \text{Information Content: } IC(x) = -\log_2 P(x)}$$

$$\Downarrow$$

$$\boxed{\text{Expected Information Content} \longrightarrow \text{Entropy: } H(X) = -\sum_i P(X=i) \log_2 P(X=i)}$$

$$\Downarrow$$

$$\boxed{H(X) = \text{Average number of bits needed to represent/transmit } X}$$

---

### Main Takeaway

> **Entropy measures the average uncertainty or information in a random variable. From a communication perspective, it tells us the average number of bits needed to efficiently encode outcomes according to their probabilities.**

*The next and final step in this sequence is **Cross-Entropy**, where the course will move from measuring the information within one distribution to measuring the difference between a **true distribution** and a **predicted distribution**.*