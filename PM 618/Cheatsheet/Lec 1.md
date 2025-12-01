# Lecture 1: Probability Basics Cheatsheet

## 1. Core Definitions & Context
* **Random Phenomena:** Events with non-deterministic outcomes (uncertainty).
    * *Causes:* Lack of full information (coin flip), intrinsic randomness (quantum mechanics), or measurement error.
    * *Examples:* Weather, stock prices, roll of a die.
* **Probability vs. Statistics:**
    * **Probability:** Models randomness. Given a known process, what data/observations will arise?
    * **Statistics:** The inverse problem. Given observations/data, infer properties of the underlying random process.
* **Sample Space ($\Omega$):** The set of *all* possible outcomes of an experiment.
    * *Example (Coin):* $\Omega = \{H, T\}$
    * *Example (Youtube Click):* $\Omega = \{YES, NO\}$
* **Event Space ($\mathcal{F}$):** The collection of all possible events (subsets of $\Omega$). It is closed under unions and intersections.

---

## 2. Set Theory Operations
Used to manipulate events within the Event Space.

| Operation | Notation | Definition |
| :--- | :--- | :--- |
| **Union** (OR) | $A \cup B$ | Elements in $A$, $B$, or both. |
| **Intersection** (AND) | $A \cap B$ | Elements common to both $A$ and $B$. |
| **Complement** (NOT) | $A^c$ or $\Omega \setminus A$ | Elements in $\Omega$ but not in $A$. |
| **Difference** | $A \setminus B$ | Elements in $A$ but not in $B$. |
| **Disjoint** | $A \cap B = \emptyset$ | Events share no common elements. |

### DeMorgan's Laws
Crucial for converting between intersections and unions of complements.
1.  $(A \cup B)^{c} = A^{c} \cap B^{c}$ (Not "A or B" $\equiv$ Not A **and** Not B)
2.  $(A \cap B)^{c} = A^{c} \cup B^{c}$ (Not "A and B" $\equiv$ Not A **or** Not B)

---

## 3. Probability Axioms & Properties
A probability function $P: \mathcal{Z} \rightarrow \mathbb{R}$ must satisfy these three axioms:

### The 3 Axioms
1.  **Non-Negativity:** $P(A) \ge 0$
2.  **Normalization:** $P(\Omega) = 1$ (Something in the sample space must happen).
3.  **Additivity (Disjoint):** If $A \cap B = \emptyset$, then $P(A \cup B) = P(A) + P(B)$.
    * *Generalized:* $P(\bigcup_{i=1}^{n}A_{i})=\sum_{i=1}^{n}P(A_{i})$ if pairwise disjoint.

### Derived Properties
Useful formulas derived from the axioms:
* $P(\emptyset) = 0$
* $P(A^c) = 1 - P(A)$
* $P(A \setminus B) = P(A) - P(A \cap B)$
* **Inclusion-Exclusion Principle:** $P(A \cup B) = P(A) + P(B) - P(A \cap B)$
* **Monotonicity:** If $B \subset A$, then $P(A \setminus B) = P(A) - P(B)$.

---

## 4. Calculating Probabilities

### Discrete Probability
For a sample space $\Omega = \{\omega_{1}, \dots, \omega_{n}\}$ where probabilities $p_i$ sum to 1:
$$
P(A) = \sum_{\omega_{i} \in A} p_{i}
$$

### Uniform Probability Spaces
When every outcome in a finite sample space is equally likely (e.g., fair dice, shuffled deck).
$$
P(A) = \frac{|A|}{|\Omega|} = \frac{\text{Number of outcomes in A}}{\text{Total number of outcomes in } \Omega}
$$

### Product Spaces (Repeated Experiments)
For combined experiments (e.g., flipping a coin $n$ times), the sample space is the Cartesian product.
* **Sample Space:** $\Omega = \Omega_1 \times \Omega_2$
* **Size:** $|\Omega| = |\Omega_1| \times |\Omega_2|$
* **Probability (Independence):** $P(\{\omega_1, \omega_2\}) = P_1(\omega_1) \times P_2(\omega_2)$

---

## 5. Combinatorics (Counting)
Used to determine $|A|$ and $|\Omega|$ in uniform probability problems.

### Multiplicative Principle
If experiment 1 has $n_1$ outcomes, and experiment 2 has $n_2$ outcomes, the sequence has $n_1 \times n_2$ outcomes.

### Permutations (Order Matters)
Arranging $k$ objects from a set of $n$ distinct objects.
$$
p(n,k) = \frac{n!}{(n-k)!}
$$
* *Note:* A full permutation of $n$ items is $n!$.

### Combinations (Order Does NOT Matter)
Choosing $k$ objects from a set of $n$ distinct objects.
$$
c(n,k) = \binom{n}{k} = \frac{n!}{(n-k)!k!}
$$
* *Key Relationship:* Permutations = Combinations $\times$ ordering of selected items ($k!$).

---

## 6. Infinite Sample Spaces
When the experiment may not terminate in a fixed number of steps (e.g., flip coin until Head).
* **Countable Sample Space:** $\Omega = \mathbb{N} = \{1, 2, 3, \dots\}$.
* **Countable Additivity:** Axiom 3 extends to infinite disjoint sequences:
    $$
    P(\bigcup_{k=1}^{\infty}A_{k}) = \sum_{k=1}^{\infty}P(A_{k})
    $$
* **Geometric Series Example:** Probability of first Head appearing at flip $k$: $P(k) = \frac{1}{2^k}$.
    * Verification: $\sum_{k=1}^{\infty} \frac{1}{2^k} = 1$.

### Finite vs. Infinite Sets
* **Finite:** Can correspond to $\{1, \dots, n\}$.
* **Countable:** Can correspond 1-to-1 with Natural Numbers $\mathbb{N}$ (e.g., Integers, Rationals $\mathbb{Q}$).
* **Uncountable:** Cannot be listed (e.g., Real numbers $\mathbb{R}$, Irrational numbers).

---

## 7. Classic Problem Case Studies

### De Méré’s Paradox
A historical gambling problem solved by probability.
1.  **Bet 1:** 4 rolls of a single die. Win if at least one '6' appears.
    * *Result:* Favorable ($P > 0.5$).
2.  **Bet 2:** 24 rolls of two dice. Win if at least one 'double 6' appears.
    * *De Méré's Intuition:* Thought it was favorable.
    * *Actual Math:* Unfavorable ($P < 0.5$). 25 rolls are required to make it favorable.

### Birthday Paradox
How many people ($n$) are needed for the probability of two people sharing a birthday to be $> 0.5$?
* **Method:** Calculate $P(\text{No Match})$ using the multiplicative principle and subtract from 1.
* **Result:** Surprisingly low number (around 23 people).