# Lecture 2 - Conditional Probability and Independence

## Review from Last Class

- Sample spaces (finite)
- Probability functions on discrete spaces
- Uniform probability spaces
- Multiplicative counting principle
- Permutations/combinations

## Repeated Experiments/Product of Sample Spaces

E.g. Flip a coin twice:

$$
\Omega_1 = \{H, T\}
$$

$$
\Omega = \{(H,H), (H,T), (T,H), (T,T)\} = \Omega_1 \times \Omega_1 = \Omega_1^2
$$

E.g. Flip a coin $n$ times:

$$
\Omega = \Omega_1 \times \dots \times \Omega_1 = \Omega_1^n \quad \text{all n-tuples with elements in } \{H, T\}
$$

E.g. Flip a coin and then pick a month at random:

$$
\Omega_1 = \{H, T\}, \quad \Omega_2 = \{Jan, Feb, Mar, Apr, May, Jun, Jul, Aug, Sep, Oct, Nov, Dec\}
$$

$$
\Omega = \Omega_1 \times \Omega_2 = \{(\omega_1, \omega_2), \omega_1 \in \Omega_1, \omega_2 \in \Omega_2\}
$$

Q: How many elements in $\Omega$? (Answer: 24)

## Product of Probability Spaces

If we have a probability function $P_1$ defined in $\Omega_1$ and a probability $P_2$ defined in $\Omega_2$ we can naturally define a probability $P$ in $\Omega_1 \times \Omega_2$ as:

$$
P(\{\omega_1, \omega_2\}) = P_1(\omega_1) P_2(\omega_2)
$$

E.g.
$$
P(\{H, Jul\}) = P(H) \times P(Jul) = \frac{1}{2} \times \frac{1}{12}
$$

This is how we model **independence**.

## Infinite (Countable) Sample Spaces

E.g. number of coin flips until first heads appears:

What is the right probability space for this experiment?
$$
\Omega = \{1, 2, 3, \dots\} = \mathbb{N}
$$

Sample space has to be infinite because no guarantee experiment will terminate in a finite number of steps!

If we assume that after $k$ flips all $k$-tuples are equally likely what should the probability $P(k)$ be?

$$
\{k = 1\} = \{H\} \Rightarrow P(1) = \frac{1}{2}
$$

$$
\{k = 2\} = \{T, H\} \Rightarrow P(2) = \frac{1}{4}
$$

$$
\vdots
$$

$$
\{k\} = \{\underbrace{T, \dots, T}_{k-1 \text{ times}}, H\} \Rightarrow P(k) = \frac{1}{2^k}
$$

Does this result in a proper probability function?

For infinite sample spaces need to change additivity rule to **countably additivity rule**:
$$
P\left(\bigcup_{k=1}^{\infty} A_k\right) = \sum_{k=1}^{\infty} P(A_k) \quad \text{provided they are disjoint } (A_k \cap A_l = \emptyset \; \forall k, l \in \mathbb{N}, k \neq l)
$$

Verification of $P(\Omega) = 1$:

$$
P(\Omega) = P(\{1, 2, 3, \dots\}) = P(1) + P(2) + P(3) + \dots = \sum_{k=1}^{\infty} \frac{1}{2^k} = 1
$$

(Used that for a geometric series: $1 + r + r^2 + \dots = \sum_{k=0}^{\infty} r^k = \frac{1}{1-r}$ if $0 \leq r < 1$)

By extension of the rule for finite sample spaces, the probability defined above is a proper probability function.

## Conditional Probability

**Example:** You roll a fair 6-faced die. Let $A$ be the event that the outcome is an odd number, $A = \{1, 3, 5\}$. Let $B$ be the event that the outcome is less than 4, $B = \{1, 2, 3\}$. What is the probability of $A$? What is the probability of $A$ given $B$?

$$
P(A) = \frac{|A|}{|S|} = \frac{|\{1,3,5\}|}{|S|} = \frac{3}{6} = \frac{1}{2}
$$

$$
P(A | B) = \frac{|A \cap B|}{|B|} = \frac{2}{3}
$$

We can write:
$$
P(A | B) = \frac{|A \cap B|}{|B|} = \frac{\frac{|A \cap B|}{|S|}}{\frac{|B|}{|S|}} = \frac{P(A \cap B)}{P(B)}
$$

### Definition

If $A$ and $B$ are events, and $P(B) > 0$ the conditional probability of $A$ given $B$ is defined as:

$$
P(A | B) = \frac{P(A \cap B)}{P(B)}
$$

- Fraction of the probability $B$ also in the event $A$
- Tells us how to update probability in the presence of new information

**Example:**
- What is the probability that two cards drawn at random from a deck of playing cards will both be aces?
$$
\frac{\binom{4}{2}}{\binom{52}{2}} = \frac{4 \times 3}{52 \times 51}
$$

- What is the probability that two cards drawn at random from a deck of playing cards will both be aces if after dealing the first card it is an Ace?
$$
\frac{3}{51}
$$

## Bayes Rule

From the definition we get the properties:

**Multiplication rule:**
$$
P(A \cap B) = P(A | B) P(B)
$$

**Bayes rule:**
$$
P(B | A) = \frac{P(A | B) P(B)}{P(A)} \quad \text{(if } P(A) > 0\text{)}
$$

### 

Example: There are approximately 2.6 physicians per 1,000 people in the US (from world public health data by country)

Probability of choosing a physician if randomly choose a US inhabitant = $\frac{2.6}{1000} = 0.0026$

- $A = \{\text{Being a Physician in the US}\} = \{\text{Physician}\}$
- $B = \{\text{Being a Woman in the US}\} = \{\text{Woman}\}$
- $P(\text{Physician}) = \frac{2.6}{1000}$
- $P(\text{Woman}) = 0.508$ (From US Census)
- $P(\text{Woman} | \text{Physician}) = 0.36$ (From Labor statistics)

$$
P(\text{Physician} | \text{Woman}) = \frac{P(\text{Woman} | \text{Physician})P(\text{Physician})}{P(\text{Woman})} = \frac{2.6}{1000} \times \frac{0.36}{0.508} = \frac{1.6}{1000}
$$

## Some Special Cases

- $A$ and $B$ disjoint $\Rightarrow P(A | B) = P(B | A) = 0$
- $B \subset A \Rightarrow P(A | B) = 1$
- $A \subset B \Rightarrow P(A | B) = \frac{P(A)}{P(B)}$

## Conditional Probability is a Probability Function

For fixed $C$ with $P(C) > 0$ the conditional probability $P_C(\cdot) = P(\cdot | C)$ is a probability function:

1. $P_C(A) = P(A | C) \geq 0$
2. $P_C(\Omega) = P(\Omega | C) = 1$
3. $P_C(A \cup B) = P_C(A) + P_C(B)$ if $A \cap B = \emptyset$

## Law of Total Probability

If the sample space can be partitioned as $\Omega = \bigcup_{i=1}^{n} A_i$, with $A_1, \dots, A_n$ disjoint, then:

$$
P(B) = \sum_{i=1}^{n} P(B | A_i) P(A_i)
$$

(holds even for a countable partition)

In particular, for any event $A$, the sample space can be partitioned as $\Omega = A \cup A^c$:

$$
P(B) = P(B | A)P(A) + P(B | A^c)P(A^c)
$$

### Law oftotal probability example

The probability of infection from a certain virus upon exposure is 10% for children age < 13, 5% for ages 13-60, and 15% for ages 60+. What is the probability that a random individual is infected upon exposure in a population where $P(\text{Age} < 13) = 0.2$, $P(13 \leq \text{Age} \leq 60) = 0.6$, $P(\text{Age} > 60) = 0.2$?

Let $I$ denote the event of infection:

$$
P(I) = P(I | \text{Age} < 13)P(\text{Age} < 13) + P(I | 13 \leq \text{Age} \leq 60)P(13 \leq \text{Age} \leq 60) + P(I | \text{Age} > 60)P(\text{Age} > 60)
$$

$$
= 0.1 \times 0.2 + 0.05 \times 0.6 + 0.15 \times 0.2 = 0.08
$$

## Medical Testing Example

A diagnostic test has 99% sensitivity and 98% specificity. 

If the population prevalence of the disease is 3%, what is the probability that an individual who tests positive is affected with the disease?

- $\text{Sensitivity} = P(\text{Test+} | \text{Affected}) = 0.99 $

- $ \text{Specificity} = P(\text{Test-} | \text{Not Affected}) = 1 - P(\text{Test+} | \text{Not Affected}) $
- $ (P(\text{Test+} | \text{Not Affected}) = 1 - \text{Specificity} = 0.02) $
- $ \text{Prevalence} = P(\text{Affected}) = 0.03 $



- $ P(\text{Affected} | \text{Test+}) = ? $
- $ P(\text{Test+}) = P(\text{Test+} | \text{Affected}) P (\text{Affected}) + P(\text{Test+} | \text{Not Affected}) P (\text{Not Affected}) $
- $ = 0.99 \times 0.03 + 0.02 \times 0.97 = 0.0297 + 0.0194 = 0.0491 $
- $ P(\text{Affected} | \text{Test+}) = \frac{P(\text{Test+} | \text{Affected})P(\text{Affected})}{P(\text{Test+})} = \frac{0.0297}{0.0491} = 0.605 $

## Monty Hall Problem

You're on a game show, and you're given the choice of three doors:
- Behind one door is a car
- Behind the others, goats

You pick a door, say No. 1, and the host, who knows what's behind the doors, opens another door, say No. 3, which has a goat.

He then says to you, "Do you want to switch to door No. 2 or keep prize behind door No. 1?"

**Should you switch?** `Answer: Yes! Switching gives you 2/3 probability of winning`

<img src="Lecture 2.assets/Screenshot 2025-11-28 at 12.13.51 AM-4317647-4317647-4317648.png" alt="Screenshot 2025-11-28 at 12.13.51 AM" style="zoom:50%;" />

## Independence

Two events $A$ and $B$ are **independent** iff (if and only if):
$$
P(A \cap B) = P(A)P(B)
$$

**E.g. fair coin tossed twice:**

$$
P(HH) = P(HT) = P(TH) = P(TT) = \frac{1}{4}
$$

$$
P(\{H \text{ in first toss}\}) = P(HH) + P(HT) = \frac{1}{4} + \frac{1}{4} = \frac{1}{2}
$$

$$
P(\{H \text{ in second toss}\}) = P(HH) + P(TH) = \frac{1}{4} + \frac{1}{4} = \frac{1}{2}
$$

$$
P(\{H \text{ in first toss}\} \cap \{H \text{ in second toss}\}) = P(\{H \text{ in first toss}\})P(\{H \text{ in second toss}\})
$$

The events $\{H \text{ in first toss}\}$ and $\{H \text{ in second toss}\}$ are independent.

(in fact any first toss outcome is independent of any second toss outcome)

Independence between $A$ and $B$ is equivalent to:

1. $P(A | B) = P(A)$
2. $P(B | A) = P(B)$
3. $A$ and $B^c$ are independent (or $A^c$ and $B$ are independent, or $A^c$ and $B^c$ are independent)

## Independence of Multiple Events

$A_1, \dots, A_n$ are independent iff:
$$
P(A_1 \cap A_2 \cap \dots \cap A_n) = P(A_1)P(A_2) \dots P(A_n)
$$

And also the equation above holds replacing any number of the $A_i$s by their complements ($2^n$ equations!)

**Pairwise independence does not imply independence!!**

**Example:** Two tosses of a fair coin

- $A = \{H \text{ in first toss}\}$
- $B = \{H \text{ in second toss}\}$
- $C = \{\text{two tosses are equal}\}$

`These are pairwise independent but not mutually independent`
