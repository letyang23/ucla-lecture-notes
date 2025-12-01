# Lecture 1

### Probability basics

- Random phenomena are all around us: outcome of a coin flip, weather patterns, stock market, getting disease
- Random means non-deterministic, i.e. phenomena where there is an associated uncertainty about the outcome; we cannot predict perfectly (next day weather, roll of a die, price of Apple stock) 
- Inability to predict perfectly could be due to lack of full information (e.g. flipping coin) or intrinsic (quantum mechanics) 
- Error in measurements: anything we measure has uncertainty associated with it
- Randomness does not imply complete lack of pattern (e.g. a multiple coin toss will have about half heads and half tails), meteorologists can assess (and quantify!) whether the chance of rain is high or low

- Probability is the branch of mathematics that allows us to model randomness and studies properties of random phenomena
- Probability has application in computer science, machine learning, artificial intelligence, finance, statistics
- Probability allows as to model observations/data arising from phenomena/processes that are or can be modeled as random 
- Statistics can be thought of as providing solutions to the inverse problem of probability: given observations/data infer properties about the underlying random phenomenon/process that generated the data
- Probability can be defined formally (at different levels of mathematical rigor) or can be treated more intuitively

## Sample space

*Definition:* the set of all possible outcomes of an experiment of interest

*Examples:*

*   Single coin tossing: $\Omega = \{H, T\}$
*   Month of birth of a randomly chosen person: $Omega = \{Jan, Feb, Mar, Apr, May, Jun, Jul, Aug, Sep, Oct, Nov, Dec\}$
*   Whether a Youtube video will be clicked when presented to a potential viewer $Omega = \{YES, NO\}$

## Event space

Event Space: all possible events (collection of outcomes) we will consider.

For discrete sample spaces event space is typically all possible subsets of $\Omega$

*   Example: single coin toss
    -   Sample space: $\Omega = \{H, T\}$
    -   Event space: $\mathcal{F} = \{\emptyset, \{T\}, \{H\}, \{H, T\}\}$

*   Example: birth month of a randomly chosen person
    -   $\Omega = \{Jan, Feb, Mar, Apr, May, Jun, Jul, Aug, Sep, Oct, Nov, Dec\}$
    -   $\mathcal{F} = \{\emptyset, \{Jan\}, \dots, \{Dec\}, \{Jan, Feb\}, \dots, \{Jan, \dots, Dec\}\}$

*   Q: how many elements in $\mathcal{F}$?
    *   If your sample space $\Omega$ has **$n$** elements (outcomes), then the event space $\mathcal{F}$ contains **$2^n$** elements.


We require that union of events and intersection of events are also events:

$$
A, B \in \mathcal{F} \implies A \cup B \text{ and } A \cap B \in \mathcal{F}
$$

$\mathcal{F}$ is closed under unions and intersections

E.g. $A = \text{First semester} = \{\text{Jan}, \text{Feb}, \text{Mar}, \text{Apr}, \text{May}, \text{Jun}\}$

$B = \{\text{May}, \text{Jun}, \text{July}\}$

$A \text{ or } B = A \cup B = \{\text{Jan}, \text{Feb}, \text{Mar}, \text{Apr}, \text{May}, \text{Jun}, \text{Jul}\}$

$A \text{ and } B = A \cap B = \{\text{May}, \text{Jun}\}$

## Complements

$$
\text{not } A = A^{c} = \{Jul, Aug, Sep, Oct, Nov, Dec\}
$$

$$
A \setminus B = A - B = \{Jan, Feb, Mar\}
$$

$$
A^{c} = \Omega \setminus A = \Omega - A
$$

$\mathcal{Z}$ is closed under union, intersection, and set difference

**Venn Diagrams:**

<img src="Lecture 1.assets/Screenshot 2025-11-28 at 12.17.24 AM-4317851.png" alt="Screenshot 2025-11-28 at 12.17.24 AM" style="zoom:50%;" />

## Disjoint events

$$
A \text{ and } B = \emptyset \quad \text{i.e., no elements in common}
$$

E.g. 
* $A = \text{First semester} = \{Jan, Feb, Mar, Apr, May, Jun\}$
* $B = \text{Second semester} = \{Jul, Aug, Sep, Oct, Nov, Dec\}$

## DeMorgan's Laws

$$
(A \cup B)^{c} = A^{c} \cap B^{c}
$$

$$
(A \cap B)^{c} = A^{c} \cup B^{c}
$$

**Example:** Let $J$ be the event "John is guilty" and $M$ the event "Mary is guilty.”

* $(J \cap M)^{c} = \text{Not true that both John and Mary are guilty}$
* $J^{c} \cup M^{c} = \text{Either John or Mary are not guilty}$
* $(J \cup M)^{c} = \text{Not true that either John or Mary (or both) are guilty}$
* $J^{c} \cap M^{c} = \text{Neither John nor Mary are guilty}$

(prove DeMorgan's Laws to practice with set operations)

## Probability functions

A probability function is a 'set function' that assigns a real number to each event in $\mathcal{Z}$:

$$
P : \mathcal{Z} \rightarrow \mathbb{R} \text{ such that:}
$$

1. 
$$
P(A) \ge 0
$$

2.
$$
P(\Omega) = 1
$$

3. 
$$
P(A \cup B) = P(A) + P(B) \text{ if } A \cap B = \emptyset \quad (\text{i.e. additive on disjoint sets})
$$

The probability reflects the chances an event occurs, 0 being impossible and 1 being certain

#### **Example: Fair coin**

$$
P(\{H\}) = P(\{T\}) = \frac{1}{2} \quad (\text{we will simplify notation as } P(H) = P(T))
$$

$$
P(\emptyset) = 0
$$

$$
P(\{H,T\}) = P(\Omega) = 1
$$

#### **Example: birth month of a randomly chosen person**

$$
P(Jan) = P(Feb) = \dots = P(Dec) = \frac{1}{12}
$$

Or perhaps a more reasonable assignment of probabilities would be proportional to the number of days in each month:

$$
P(Jan) = \frac{31}{365}, P(Feb) = \frac{28}{365}, \dots
$$

(This shows that it is us, the users who assign probabilities; probabilities are not 'laws of nature')

---

Any probability in a discrete sample space can be constructed like in the previous examples:

$$
\Omega = \{\omega_{1}, \omega_{2}, \dots, \omega_{n}\}
$$

$$
p_{1} + p_{2} + \dots + p_{n} = 1, \quad p_{1} \ge 0, p_{2} \ge 0, \dots p_{n} \ge 0
$$

$$
P(A) = \sum_{w_{i} \in A} p_{i}, \quad \forall A \subset \Omega
$$

is a probability function.

Exercise: show this

---

Property 3 holds for any number of disjoint events:

$$
P(A \cup B \cup C) = P(A) + P(B) + P(C), \quad \text{if } A \cap B = \emptyset, A \cap C = \emptyset, B \cap C = \emptyset
$$

E.g. the sets:
* $A = \{\text{First Trimester}\} = \{Jan, Feb, Mar\}$
* $B = \{\text{Second Trimester}\} = \{Apr, May, Jun\}$
* $C = \{Nov\}$

Are pairwise disjoint

$$
P(A \cup B \cup C) = P(\{Jan, Feb, Mar, Apr, May, Jun, Nov\}) = \frac{7}{12}
$$

$$
P(A) = P(B) = \frac{3}{12}, \quad P(C) = \frac{1}{12}
$$

In general:
$$
P(A_{1}\cup...\cup A_{n})=P\left(\bigcup_{i=1}^{n}A_{i}\right)=\sum_{i=1}^{n}P(A_{i})
$$
Provided the events are pairwise disjoint:
$$
A_{k}\cup A_{l}=\emptyset,\forall k,l\in\{1...n\},k\ne l
$$

## Derived properties

If $A, B \in \mathcal{Z}$

$$
P(\emptyset) = 0
$$

$$
0 \le P(A) \le 1
$$

$$
P(A^{c}) = 1 - P(A)
$$

$$
P(A - B) = P(A) - P(A \cap B)
$$

$$
B \subset A \Rightarrow P(A - B) = P(A) - P(B)
$$

$$
P(A \cup B) = P(A) + P(B) - P(A \cap B)
$$

(Good practice exercise to show these)

## Repeated experiments/Product of sample spaces

E.g. Flip a coin twice:

$$
\Omega = \{(H,H), (H,T), (T,H), (T,T)\} = \{H,T\} \times \{H,T\} = \{H,T\}^{2}
$$

E.g. Flip a coin $n$ times:

$$
\Omega = \{H,T\}^{n} \quad \text{all } n\text{-tuples with elements in } H,T
$$

E.g. Flip a coin and then pick a month at random:

$$
\Omega_{1} = \{H,T\}, \quad \Omega_{2} = \{Jan, Feb, Mar, \dots, Dec\}
$$

$$
\Omega = \Omega_{1} \times \Omega_{2} = \{(\omega_{1}, \omega_{2}), \omega_{1} \in \Omega_{1}, \omega_{2} \in \Omega_{2}\}
$$

Q: How many elements in $\Omega$?

## Repeated experiments/Product of sample spaces

If we have a probability function $P_{1}$ defined in $\Omega_{1}$ and a probability $P_{2}$ defined in $\Omega_{2}$ we can naturally defined a probability $P$ in $\Omega^{1} \times \Omega^{2}$ as:

$$
P(\{\omega^{1}, \omega^{2}\}) = P_{1}(\omega^{1}) P_{2}(\omega^{2})
$$

E.g.

$$
P(\{H, Jul\}) = P(H) \times P(Jul) = \frac{1}{2} \times \frac{1}{12}
$$

(This is how we model independence, which will cover next week)

## Uniform probability spaces

In many applications it makes sense to assign the same probability to all elements of a finite sample space

E.g. two coin flip:
$$
\Omega = \{(H,H), (H,T), (T,H), (T,T)\} = \{H,T\} \times \{H,T\}
$$
$$
P(H,H) = P(H,T) = P(T,H) = P(T,T) = \frac{1}{4}
$$

In general, a uniform probability space with $|\Omega|=n$, has:
$$
P(\omega) = \frac{1}{n} \quad \forall \omega \in \Omega
$$
And the probability of an event is the number of elements in the event divided by the total number of elements in the sample space:
$$
P(A) = \frac{|A|}{|\Omega|}
$$

E.g. Pick a single card from a well shuffled standard 52-card deck:
$$
P(\text{Ace}) = \frac{4}{52}
$$

$$
P(\text{diamond suit}) = P(\Diamond) = \frac{13}{52} = \frac{1}{4}
$$

## Multiplicative counting principle

Many problems in probability theory require that we count the number of ways that a particular event can occur. This kind of counting falls under the area of mathematics called combinatorics.

**The Multiplicative counting principle (MP).**

Suppose that we perform $r$ experiments such that the $k^{\text{th}}$ experiment has $n_{k}$ possible outcomes, for $k=1,2, \dots, r$. Then there are a total of:

$$
n_{1} \times n_{2} \times n_{3} \times \dots \times n_{r}
$$

possible outcomes for the sequence of $r$ experiments.

Example 1: Need to choose a password for an online account. Password must consist of two lowercase letters (a to z) followed by one capital letter (A to Z) followed by four digits (0,1, \dots, 9).

Example 2: How many subsets does a set with $n$ elements have?

## Permutations

How many five-card hands are possible from a standard fifty-two card deck? (if order matters)

$$
52 \times 51 \times 50 \times 49 \times 48 = \frac{52!}{47!} = 311,875,200 \text{ by the MP}
$$

In general, a $k\text{-permutation}$ of $n$ distinct objects is a way to arrange $k$ objects out of the $n$ in a row (order matters).

The number of $k\text{-permutations}$, $p(n,k)$, is given by:
$$
p(n,k) = \frac{n!}{(n-k)!}
$$

$n\text{-permutations}$ are often refer to as just permutations. There are:
$$
\frac{n!}{(n-n)!} = n! \text{ permutations}
$$

## Combinations

How many five-card hands are possible from a standard fifty-two card deck? (if order does not matter)

$$
52 \times 51 \times 50 \times 49 \times 48 = \frac{52!}{47!} \quad \text{ordered arrangements}
$$

Each arrangement was counted $5!$ times so the number of unordered arrangements is:
$$
\frac{52!}{47!5!} = 2,598,960
$$

In general, a $k\text{-combination}$ of $n$ distinct objects is a way to arrange $k$ objects out of the $n$ when order does not matter.

The number of $k\text{-combinations}$, $c(n,k)$, is given by:
$$
c(n,k) = \frac{n!}{(n-k)!k!} = \binom{n}{k}
$$

$$
p(n,k) = c(n,k) \times k!
$$

## Card problem

Suppose we deal a 5-card hand from a regular 52-card deck. Which is larger, P(One king) or P(Two hearts)?

$$
P(\text{One king}) = \frac{\binom{4}{1} \times \binom{48}{4}}{\binom{52}{5}}
$$

$$
P(\text{Two hearts}) = \frac{\binom{13}{2} \times \binom{39}{3}}{\binom{52}{5}}
$$

```r
4 * choose (48, 4) / choose (52, 5)
## [1] 0.2994736
choose(13, 2) * choose (39, 3) / choose (52, 5)
## [1] 0.2742797
```

## De Mere's problem

* Dice game that played an important role in the historical development of probability.
* Chevalier de Méré had been betting that, in four rolls of a die, at least one six would turn up.
* He was winning consistently and, to get more people to play, he changed the game to bet that, in 24 rolls of two dice, a pair of sixes would turn up.
* De Méré lost with 24 and felt that 25 rolls were necessary to make the game favorable.
* Was De Méré right?

## Simulating De Mere's problem

Single die roll in R:

```r
sample (1:6, size = 1, replace = TRUE)
[1] 2
```

Four rolls of one die

```R
sample (1:6, size = 4, replace = TRUE)
[1] 1 2 4 3
```

## Simulating De Mere's problem

Checking if a six came up

```r
any(sample(1:6, size = 4, replace = TRUE) == 6)
## [1] FALSE
```

Full simulation:

```R
nreps = 1000
set.seed (2021)
results = numeric(0)
for (i in 1:nreps) results[i] = any (sample(1:6, size = 4, replace = TRUE) == 6)
mean(results)

## [1] 0.507
```

## De Mere's problem

Questions:

1. Based on this simulation result, do you think the bet's favorable?

2. Derive/compute the actual probability (hint: use that all outcomes of the four rolls of a die are equally likely)

3. Simulate the second scheme (24 rolls of two dice). What can you say about the favorability of the bet?

4. Derive/compute the actual probability. How about for 25 rolls of two dice?

## Birthday 'paradox'

How many people $n$ do we need to have in a room to make it a favorable bet (probability of success greater than $1/2$) that two people in the room will have the same birthday?

Assume all 365 b-days are equally likely.

1. Perform a simulation in R to answer this question (hint: use the base R function 'duplicate' to check that whether there are matching b-days)

2. Compute the probability by mathematical derivation and plot the probability as a function of $n$. (Hint: use the multiplication principle to count)

## Infinite (countable) sample spaces

E.g. flip a coin until first heads appears:

What is the right probability space for this experiment?

$$
\Omega = \{1, 2, 3, \dots \} = \mathbb{N}
$$
Sample space has to be infinite because no guarantee experiment will terminate in a finite number of steps!

If we assume that after $k$ flips all $k\text{-tuples}$ are equally likely what should the probability $P(k)$ be?

$$
k=1=\{H\} \Rightarrow P(1) = \frac{1}{2}
$$

$$
k=2=\{T,H\} \Rightarrow P(2) = \frac{1}{4}
$$

$$
\vdots
$$

$$
k = \{\underbrace{T, \dots, T}_{\text{k-1 times}}, H\} \Rightarrow P(k) = \frac{1}{2^{k}}
$$

Does this result in a probability function?

## Infinite (countable) sample spaces

For infinite sample spaces need to change additivity rule to countably additivity rule:

2'.
$$
P\left(\bigcup_{k=1}^{\infty}A_{k}\right) = \sum_{k=1}^{\infty}P(A_{k}) \quad \text{provided they are disjoint } (A_{k} \cap A_{l} = \emptyset \quad \forall k,l \in \mathbb{N}, k \ne l)
$$

$$
\Omega = \{H,T\}^{\infty} \quad \text{all infinite sequences with elements in } \{H, T\}
$$

Verification of $P(\Omega)=1$:
$$
P(\Omega) = P(\{1,2,3, \dots\}) = P(1) + P(2) + P(3) + \dots = \sum_{k=1}^{\infty}\frac{1}{2^{k}} = 1
$$

(Used that for a geometric series:
$$
1 + r + r^{2} + \dots = \sum_{k=0}^{\infty}r^{k} = \frac{1}{1-r} \quad \text{if } 0 \le r < 1
$$
)

Q: What's the probability that it'll take an even number of tosses until the first heads?

## Finite and countable sets: a mathematical aside

A set is finite if its elements can be put in one-to-one correspondence with with:
$$
\{1,2,\dots,n\} \quad \text{for some } n \in \mathbb{N}
$$
E.g., the set of students in the classroom, the set of inhabitants in the world, the set of stars in the Milky Way.

A set is countable if its elements can be put in one-to-one correspondence with with the natural numbers:
$$
\mathbb{N}=\{1,2,3,\dots\}
$$
E.g. The set of natural numbers, the set of odd numbers $(n \rightarrow 2n+1)$, the set of even numbers $(n \rightarrow 2n)$, the set of primes, the set of rational numbers ($\mathbb{Q}$)$\textbf{!!}$

Examples of infinite non-countable sets:
$$
\mathbb{R}, \quad \text{the set of irrational numbers } \mathbb{R}-\mathbb{Q}, \quad \mathbb{R}^{2}
$$



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

### Law of total probability example

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


# Lecture 3 - Discrete Random Variables

## Review from Last Class

- Countable sample spaces (e.g. flipping a coin until first head, $\Omega = \{1, 2, \dots\} = \mathbb{N}$)
- Conditional Probability: $P(A | B) = \frac{P(A \cap B)}{P(B)}$
- Law of total probability: $P(B) = P(B | A_1)P(A_1) + \dots + P(B | A_n)P(A_n)$ for a (disjoint) partition $\Omega = A_1 \cup \dots \cup A_n$
- Bayes theorem: $P(A | B) = \frac{P(B | A)P(A)}{P(B)}$
- Independence: $P(A \cap B) = P(A)P(B)$ (or more intuitively $P(A | B) = P(A)$)
- For $n > 2$ events independence requires satisfying $2^n$ equations

**Q: Is disjoint the same as independent?** No! Disjoint events cannot both occur, while independent events don't affect each other's probabilities.

## Discrete Random Variables

A discrete random variable is a function $X : \Omega \rightarrow \mathbb{R}$ that takes a finite or countable number of values $x_1, x_2, \dots$

E.g. The number in the upper face of the rolled die, the sum of two dice

**Notation:**
- $\{\omega : X(\omega) = x\} = \{X = x\}$
- $P(\{X = x\}) = P(X = x)$

## Probability Mass Function (pmf)

The pmf of a discrete random variable taking values $x_1, x_2, \dots$ is the function:

$$
p : \mathbb{R} \rightarrow [0, 1]
$$

$$
p(x) = P(X = x) \quad \text{(Sometimes also denoted } p_X(x) \text{ or } f_X(x)\text{)}
$$

If $X$ takes on the values $x_1, x_2, \dots$ then:
- $p(x_i) > 0$, and $p(x_1) + p(x_2) + \dots = 1$
- $p(x) = 0$ for all other $x$

**E.g. Fair coin flip:**
$$
X = \begin{cases} 1 & \text{Heads} \\ 0 & \text{Tails} \end{cases}
$$

$$
p(1) = \frac{1}{2}, \quad p(0) = \frac{1}{2}, \quad p(0.5) = p(\pi) = 0
$$

## Cumulative Distribution Function (cdf)

The cdf of a discrete random variable taking values $x_1, x_2, \dots$ is the function:

$$
F : \mathbb{R} \rightarrow [0, 1] \quad \text{(sometimes denoted } F_X\text{)}
$$

$$
F(x) = P(X \leq x) \quad \forall x \in \mathbb{R}
$$

If $X$ takes on the values $x_1, x_2, \dots$ then:

$$
F(x) = \sum_{x_i \leq x} p(x_i)
$$

**E.g. Fair coin flip:**
$$
X = \begin{cases} 1 & \text{Heads} \\ 0 & \text{Tails} \end{cases}
$$

$$
F(x) = \begin{cases} 0 & x < 0 \\ \frac{1}{2} & 0 \leq x < 1 \\ 1 & x \geq 1 \end{cases}
$$

Both the pmf and the cdf completely characterize all the **probabilistic** information about a random variable (two random variables can have the same pmf and cdf and be different).

## Properties of the Cumulative Distribution Function

- $F(x)$ is increasing: $x_1 \leq x_2 \Rightarrow F(x_1) \leq F(x_2)$
- $0 \leq F(x) \leq 1$, $\lim_{x \to -\infty} F(x) = 0$, $\lim_{x \to +\infty} F(x) = 1$
- $F$ is right continuous: $\lim_{\epsilon \downarrow 0} F(x + \epsilon) = F(x)$

<img src="Lecture 3.assets/Screenshot 2025-11-28 at 12.21.53 AM.png" alt="Screenshot 2025-11-28 at 12.21.53 AM" style="zoom:50%;" />

## Bernoulli Distribution

A random variable has a **Bernoulli distribution**

$$
f_X(1) = p, \quad (0 \leq p \leq 1)
$$

$$
f_X(0) = 1 - p
$$

$$
X \sim Bern(p) \quad \text{or} \quad X \sim Bernoulli(p)
$$

- Models experiments with only two possible outcomes
- E.g. coin toss (H vs. T), die comes up six (yes vs. no)
- A random variable with a Bernoulli distribution is called a **Bernoulli trial**

## Binomial Distribution

$n$ independent Bernoulli trials (e.g. flipping a coin $n$ times): $X_1, \dots, X_n \sim Bernoulli(p)$

$X = X_1 + \dots + X_n$ counts the number of successes in $n$ trials

$$
X \sim Bin(n, p) \quad \text{or} \quad X \sim Binomial(n, p)
$$

$$
f_X(k) = P(X = k) = \binom{n}{k} p^k (1-p)^{n-k} \quad k = 0, 1, \dots, n
$$

- Models the number of successes in $n$ trials
- For $n = 1$ the Binomial distribution is the Bernoulli distribution

### Example: Side Effects

Suppose it is known that 5% of adults who take a certain medication experience negative side effects. What is the probability that more than $k$ patients in a random sample of 100 will experience negative side effects?

$$
P(X > 1 \text{ patients experience side effects}) = ?
$$
$$
P(X > 5 \text{ patients experience side effects}) = ?
$$
$$
P(X > 15 \text{ patients experience side effects}) = ?
$$

### Binomial Distribution in R

pmf, cdf, and Random generation of a binomial random variable

```r
# pmf
dbinom(3, size=10, prob=0.3)
## [1] 0.2668279

# cdf
pbinom(3, size=10, prob=0.3)
## [1] 0.6496107

# Random generation
rbinom(n=1, size=10, prob=0.3)
## [1] 2

rbinom(n=3, size=10, prob=0.3)
## [1] 0 1 3
```

### Side Effects Example (continued)

$$
P(X > 1) = 1 - P(X \leq 1) = 1 - F_X(1)
$$

```r
1 - pbinom(1, size = 100, prob = 0.05)
## [1] 0.9629188

pbinom(1, size = 100, prob = 0.05, lower.tail = FALSE)
## [1] 0.9629188

pbinom(5, size = 100, prob = 0.05, lower.tail = FALSE)
## [1] 0.3840009

pbinom(15, size = 100, prob = 0.05, lower.tail = FALSE)
## [1] 3.705408e-05
```

### Binomial distribution pmf

```r
par(mar=c(6,8,5,1))

plot(0:5, dbinom(0:5, size=5, prob=0.4), col='red4', type='p', pch=16, cex=1.3, xlab='x', ylab='p(x)', cex.lab=2, cex.axis=2)
```

<img src="Lecture 3.assets/Screenshot 2025-11-28 at 12.24.33 AM.png" alt="Screenshot 2025-11-28 at 12.24.33 AM" style="zoom:50%;" />

### Binomial distribution cdf

```R
par(mar=c(6,8,5,1))

plot(stepfun(0:5, c(0, pbinom(0:5, size=5, prob=0.4))), pch = 1, lwd=2, col='steelblue', xlab='x', ylab='F(x)', cex.lab=2, cex.axis=2, main='', verticals = F)
```

<img src="Lecture 3.assets/Screenshot 2025-11-28 at 12.25.34 AM.png" alt="Screenshot 2025-11-28 at 12.25.34 AM" style="zoom:50%;" />

### Simulating a binomial 3 different ways

**Generating $n$ Bernoulli trials**

```R
Bernoulli_trials_1 = sample(0:1, 10, replace = TRUE, prob=c(0.3, 0.7))
Bernoulli_trials_1

## [1] 1 1 0 1 1 0 1 0 1 0

sum(Bernoulli_trials_1)

## [1] 6
```
**Generating $n$ Bernoulli trials using rbinom()**

```R
Bernoulli_trials_2 = rbinom(10, size = 1, prob=0.3)
Bernoulli_trials_2

## [1] 0 1 0 0 0 0 0 0 0 0

sum(Bernoulli_trials_2)

## [1] 1
```

**Directly sampling from the binomial** 

```R
rbinom(1, size=10, prob=0.3) 

## [1] 5
```

## Geometric Distribution

A discrete random variable $X$ has a **geometric distribution** with parameter $p$, where $0 < p \leq 1$, if its probability mass function is given by:

$$
p_X(k) = P(X = k) = (1-p)^{k-1} p \quad k = 1, 2, \dots
$$

$$
X \sim Geo(p) \quad \text{or} \quad X \sim Geometric(p)
$$

Models the (discrete) waiting time until an event happens. E.g. number of trials till first heads.

### Example: Concert Ticket

You and a friend want to go to a concert, but there's only one ticket left. The salesperson decides to toss a coin until heads appears. In each toss heads appears with probability $p$, where $0 < p < 1$, independent of each of the previous tosses. If the number of tosses needed is odd, your friend is allowed to buy the ticket; otherwise you can buy it. Would you agree to this arrangement?

### Geometric Memoryless Property

$$
P(X > n + k | X > k) = P(X > n)
$$

The probability it'll take $n$ additional trials if the first $k$ are failures is the same as the probability it'll take $n$ trials at the beginning of the experiment.

### Geometric Distribution in R

pmf, cdf, and Random generation of a binomial random variable

**Warning:** The definition of the geometric in R is the number of **failures before the first success**, i.e. $X - 1$.

```r
dgeom(x=5, prob = 0.1)
## [1] 0.059049

pgeom(10, prob= 0.1)
## [1] 0.6861894

rgeom(n=1, prob= 0.1)
## [1] 0

rgeom(n=3, prob= 0.1)
## [1] 4 3 4
```

#### Geometric distribution pmf

```R
par(mar=c(6,8,5,1))
plot(0:50, dgeom(0:50, prob=0.1), col='red4', type='p', pch=16, cex=1, xlab='x', ylab='p(x)', cex.lab=2, cex.axis=2
```

<img src="Lecture 3.assets/Screenshot 2025-11-28 at 12.33.25 AM.png" alt="Screenshot 2025-11-28 at 12.33.25 AM" style="zoom:50%;" />

#### Geometric distribution cdf

```R
par(mar=c(6,8,5,1))
plot(stepfun(0:50, c(0, pgeom(0:50, prob=0.1))), pch = 1, lwd=2, col='steelblue', xlab='x', ylab='F(x)', cex.lab=2, cex.axis=2, m
```

<img src="Lecture 3.assets/Screenshot 2025-11-28 at 12.33.09 AM.png" alt="Screenshot 2025-11-28 at 12.33.09 AM" style="zoom:50%;" />


# Lecture 4 - Continuous Random Variables

## Review from Last Class

- Discrete random variables:
  - Take finite or countable values
  - Completely characterized by their pmf or cdf

- **Bernoulli:** $X = \begin{cases} 1 & \text{Heads} \\ 0 & \text{Tails} \end{cases}$

- **Binomial:** number of successes in $n$ independent Bernoulli trials with identical probability of success $p$
  - $X \sim Binomial(n, p)$, $x \in \{0, 1, \dots, n\}$

- **Geometric distribution:** number of trials until first success in repeated Bernoulli experiments with identical probability of success $p$
  - $X \sim Geometric(p)$, $x \in \{1, 2, \dots\}$

## Continuous Random Variables

A continuous random variable is a function $X : \Omega \rightarrow \mathbb{R}$ that takes on uncountable infinite values and such that for $a \leq b$:

$$
P(a \leq X \leq b) = \int_a^b f_X(x) \, dx
$$

for some function $f_X(x) \geq 0$,  $\forall x \in \mathbb{R}$ and $\int_{-\infty}^{+\infty} f_X(t) \, dt = 1$

$f_X : \mathbb{R} \rightarrow \mathbb{R}$ is called the **probability density function** (or density function) of the random variable $X$.

<img src="Lecture 4.assets/Screenshot 2025-11-28 at 12.35.57 AM.png" alt="Screenshot 2025-11-28 at 12.35.57 AM" style="zoom:50%;" />

## Probability Density Function

- More generally, if $S \subset \mathbb{R}$: $P(X \in S) = \int_S f_X(x) \, dx$

**Properties of the pdf:**

- $P(-\infty < X < +\infty) = \int_{-\infty}^{\infty} f_X(t) \, dt = 1$

- $F_X(x) = P(X \leq x) = \int_{-\infty}^{x} f_X(t) \, dt$

- $f_X(x) = \frac{d}{dx} F_X(x) = F_X'(x)$ (Fundamental theorem of calculus)

- $P(x - \frac{\epsilon}{2} < X < x + \frac{\epsilon}{2}) = \int_{x-\frac{\epsilon}{2}}^{x+\frac{\epsilon}{2}} f_X(t) \, dt \approx \epsilon f_X(x)$

- $f_X(x) = \lim_{\epsilon \to 0} \frac{P(x - \frac{\epsilon}{2} < X < x + \frac{\epsilon}{2})}{\epsilon}$, i.e. represents the density of probability 'mass' at point $x$

- For a continuous random variable $X$, $P(X = x) = 0$

## Fundamental Theorem of Calculus

**Part I:** Let $f$ be a continuous real-valued function defined on a closed interval $[a, b]$. Let $F$ be the function defined, for all $x$ in $[a, b]$, by:
$$
F(x) = \int_a^x f(t) \, dt
$$

Then $F$ is uniformly continuous on $[a, b]$ and differentiable on the open interval $(a, b)$, and:

$$
F'(x) = f(x)
$$

for all $x$ in $(a, b)$.

**Part II:** Let $f$ be a real-valued function on a closed interval $[a, b]$ and $F$ antiderivative of $f$ in $(a, b)$:

$$
F'(x) = f(x)
$$

If $f$ is (Riemann) integrable on $[a, b]$ then:

$$
\int_a^b f(x) \, dx = F(b) - F(a)
$$

## Example

Let a continuous random variable $X$ be given that takes values in $[0, 1]$, and whose distribution function is given by:

$$
F(x) = \begin{cases} 0 & \text{if } x < 0 \\ 2x^2 - x^4 & \text{if } 0 \leq x \leq 1 \\ 1 & \text{if } x \geq 1 \end{cases}
$$

<img src="Lecture 4.assets/Screenshot 2025-11-28 at 12.37.47 AM.png" alt="Screenshot 2025-11-28 at 12.37.47 AM" style="zoom:50%;" />

1. Compute $P(\frac{1}{4} \leq X \leq \frac{3}{4})$
2. What is the probability density function of $X$?
3. Compute $P(\frac{1}{4} \leq X \leq \frac{1}{2} \text{ or } X > \frac{3}{4})$

## Uniform Distribution, $X \sim U[a, b]$

$$
f(x) = \begin{cases} \frac{1}{b-a} & \text{if } x \in [a, b] \\ 0 & \text{otherwise} \end{cases}
$$

$$
F(x) = \begin{cases} 0 & \text{if } x < a \\ \frac{x-a}{b-a} & \text{if } a \leq x < b \\ 1 & \text{if } x \geq b \end{cases}
$$

<img src="Lecture 4.assets/Screenshot 2025-11-28 at 12.38.22 AM.png" alt="Screenshot 2025-11-28 at 12.38.22 AM" style="zoom:50%;" />

## Exponential Distribution, $X \sim Exp(\lambda)$

$$
f(x) = \begin{cases} \lambda e^{-\lambda x} & \text{if } x \geq 0 \\ 0 & \text{if } x < 0 \end{cases}
$$

$$
F(x) = \begin{cases} 1 - e^{-\lambda x} & \text{if } x \geq 0 \\ 0 & \text{if } x < 0 \end{cases}
$$

<img src="Lecture 4.assets/Screenshot 2025-11-28 at 12.38.41 AM.png" alt="Screenshot 2025-11-28 at 12.38.41 AM" style="zoom:50%;" />

## Normal Distribution, $X \sim N(\mu, \sigma^2)$

$$
f(x) = \phi(x) = \frac{1}{\sqrt{2\pi}\sigma} e^{-\frac{1}{2}\left(\frac{x-\mu}{\sigma}\right)^2}
$$

$$
F(x) = \Phi(x)
$$

There is no analytical formula for the cdf but it can be numerically computed.

<img src="Lecture 4.assets/Screenshot 2025-11-28 at 12.39.09 AM.png" alt="Screenshot 2025-11-28 at 12.39.09 AM" style="zoom:50%;" />

## Pareto Distribution, $X \sim Pareto(x_m, \alpha)$

$$
f(x) = \begin{cases} \frac{\alpha x_m^\alpha}{x^{\alpha+1}} & \text{if } x \geq x_m \\ 0 & \text{if } x < x_m \end{cases}
$$

$$
F(x) = \begin{cases} 0 & \text{if } x < x_m \\ 1 - \left(\frac{x_m}{x}\right)^\alpha & \text{if } x \geq x_m \end{cases}
$$

<img src="Lecture 4.assets/Screenshot 2025-11-28 at 12.39.26 AM.png" alt="Screenshot 2025-11-28 at 12.39.26 AM" style="zoom:50%;" />

## Quantiles

Let $X$ be a continuous random variable and let $p$ be a number between 0 and 1. The $p^{th}$ **quantile** or $100p^{th}$ **percentile** of the distribution of $X$ is the smallest number $q_p$ such that:

$$
F(q_p) = P(X \leq q_p) = p
$$

The **median** of a distribution is its $50^{th}$ percentile.

<img src="Lecture 4.assets/Screenshot 2025-11-28 at 12.39.49 AM.png" alt="Screenshot 2025-11-28 at 12.39.49 AM" style="zoom:50%;" />

##### Example 1: Median of Exponential, $X \sim Exp(\lambda)$

$$
\frac{1}{2} = F(q_{0.5}) = P(X \leq q_{0.5}) = 1 - e^{-\lambda q_{0.5}}
$$

$$
q_{0.5} = -\frac{1}{\lambda} \log\left(\frac{1}{2}\right)
$$

##### Example 2: Median of Uniform in $[1, 2] \cup [3, 4]$

$$
q_{0.5} = 2
$$

## Uniform Distribution in R

pmf, cdf, random generation, and quantile of uniform random variable

```r
dunif(3, min=1, max=5)
## [1] 0.25

punif(3, min=1, max=5)
## [1] 0.5

runif(n=3) #default is uniform[0,1]
## [1] 0.007446826 0.944775617 0.292623820

qunif(0.5, min=1, max=3)
## [1] 2
```

## Exponential Distribution in R

pmf, cdf, random generation, and quantile of an exponential random variable

```r
dexp(3, rate = 0.5)
## [1] 0.1115651

pexp(3, rate = 2)
## [1] 0.9975212

rexp(n=5) # default rate is 1
## [1] 4.60679804 0.32611096 0.01889765 1.49367378 0.70605987

c(qexp(p=0.5), -log(1/2))
## [1] 0.6931472 0.6931472
```

## Normal Distribution in R

pmf, cdf, random generation, and quantile of a normal random variable

```r
dnorm(x=3, mean = 1, sd=2)
## [1] 0.1209854

dnorm(x=-1, mean = -2, sd=0.5)
## [1] 0.1079819

rnorm(n=5)
## [1] -0.4843401 -1.0643711 1.5258292 2.2244114 0.7464652

qnorm(0.5)
## [1] 0
```

## Pareto Distribution in R

pmf, cdf, random generation, and quantile of a Pareto random variable with location $x_m$ and shape 𝛼

```r
library(EnvStats)

dpareto(x=3, location = 1, shape=2)
## [1] 0.07407407

ppareto(q=3, location = 1, shape=2)
## [1] 0.8888889

rpareto(n=5, location = 1, shape=2)
## [1] 1.471863 1.356510 1.347556 1.011351 2.216670

qpareto(p=0.5, location = 1, shape=2)
## [1] 1.414214
```

## Mixtures of Distributions

##### Example 1: Discrete Mixture

To get to your destination you take a taxi if there is one waiting (probability 1/3) at the stand when you arrive or walk if there is no taxi waiting. A taxi takes you exactly 5 minutes. Walking to your destination takes you exactly 35 minutes. What is the cdf of the time to your destination $T$?

$$
P(T = t) = P(T = t | \text{Taxi})P(\text{Taxi}) + P(T = t | \text{No taxi})P(\text{No taxi}) = \begin{cases} \frac{1}{3} & \text{if } t = 5 \\ \frac{2}{3} & \text{if } t = 35 \end{cases}
$$

$$
F_T(t) = \begin{cases} 0 & \text{if } t < 5 \\ \frac{1}{3} & \text{if } 5 \leq t < 35 \\ 1 & \text{if } t \geq 35 \end{cases}
$$

##### Example 2: Continuous Mixture

To get to your destination you take a taxi if one is waiting (probability 1/3) at the stand when you arrive or walk if there is no taxi waiting. Walking to your destination takes you an amount of time distributed as $Exp(\lambda_1)$ with $\lambda_1 = 1/35$. A taxi takes you an amount of time distributed as $Exp(\lambda_2)$ with $\lambda_2 = 1/5$. What is the cdf of the time to get to your destination, $T$?

$$
F_T(t) = P(T \leq t) = P(T \leq t | \text{Taxi})P(\text{Taxi}) + P(T \leq t | \text{No taxi})P(\text{No taxi})
$$

$$
= \frac{1}{3}(1 - e^{-t/5}) + \frac{2}{3}(1 - e^{-t/35})
$$

$$
f_T(t) = \frac{d}{dt}F_T(t) = F_T'(t) = \frac{1}{3}\left(\frac{1}{5}e^{-t/5}\right) + \frac{2}{3}\left(\frac{1}{35}e^{-t/35}\right)
$$

##### Example 3: Mixed Distribution

To get to your destination you take a taxi if one is waiting (probability 1/3) when you arrive or walk if there is no taxi. Walking to your destination takes you exactly 35 minutes. A taxi takes an amount of time distributed as $Exp(\lambda_2)$ with $\lambda_2 = 1/5$. What is the cdf of the time to your destination $T$?

$$
F_T(t) = P(T \leq t) = P(T \leq t | \text{Taxi})P(\text{Taxi}) + P(T \leq t | \text{No taxi})P(\text{No taxi})
$$

$$
P(T \leq t | \text{No taxi}) = \begin{cases} 0 & \text{if } t < 35 \\ 1 & \text{if } t \geq 35 \end{cases}
$$

$$
P(T \leq t | \text{Taxi}) = \begin{cases} 0 & \text{if } t < 0 \\ 1 - e^{-t/5} & \text{if } t \geq 0 \end{cases}
$$

$$
F_T(t) = \begin{cases} 0 & \text{if } t < 0 \\ \frac{2}{3}(1 - e^{-t/5}) & \text{if } 0 \leq t < 35 \\ \frac{1}{3} + \frac{2}{3}(1 - e^{-t/5}) & \text{if } t \geq 35 \end{cases}
$$

- How about the probability density function? **There isn't one!**
- This is an example of a **MIXED** random variable
- MIXED random variables are mixtures of discrete and continuous random variables

## Discrete, Continuous, and Mixed Random Variables

- **Discrete random variables** have probability mass function but do not have probability density function
- **Continuous random variables** have probability density function but do not have probability mass function
- **Mixed random variables** have **neither** probability mass function **nor** probability density function
- **All types of random variables** (discrete, continuous and mixed distributions) **have cumulative distribution function!!**


# Week 5 – Expectation, variance, and transformations of RVs

## Last class

* **Continuous random variables:**
    * Take infinite uncountable values
    * Have a probability density function (pdf)
    * Continuous RV are completely characterized by their pdf or cdf

* **Uniform:** $U[a,b]$
* **Exponential:** $Exp[\lambda]$
* **Normal:** $N(\mu,\sigma)$
* **Pareto:** $Pareto(x_{m},\alpha)$

* **Mixtures of distributions:**
    * Discrete + Discrete = Discrete
    * Continuous + Continuous = Continuous
    * Discrete + Continuous = Neither discrete nor continuous

For a continuous random variable, it follows from the definition of pdf and the fundamental theorem of calculus that for $a \le b$:

$$
P(a<X\le b) = \int_{a}^{b}f_{X}(t)dt = F_{X}(x)|_{a}^{b} = F(b)-F(a)
$$

But $P(a<X\le b)=F(b)-F(a)$ is true for any random variable (discrete, continuous or mixed):
Let $A=\{X\le a\}, B=\{X\le b\}$. Clearly, $A\subset B$ and $B-A=\{a<X\le b\}$.

$$
P(a<X\le b) = P(B-A) = P(B)-P(A) = P(X\le b)-P(X\le a) = F(b)-F(a)
$$

For a continuous RV (but not for a discrete or mixed) this also equals $P(a\le X\le b), P(a<X<b), \dots$

## Expectation for discrete RVs

The expected value is a weighted average of the values a random variable takes, weighted by the probability of taking those values. It's the center of 'gravity' where the distribution 'balances'.

For a **Discrete** random variable $X$, $f_{X}(x)$ the probability mass function of $X$, and $\{x_{1},x_{2},\dots\}$ is the support of $X$.

$$
E[X]=\sum_{x_{i}\in \text{supp}(X)}x_{i}f_{X}(x_{i})
$$

The support of a discrete random variable $X$ is the set of points that $X$ takes with non-zero probability:
$$
\text{supp}(X)=\{x_{i}:P(X=x_{i})>0\}
$$

## Expectation discrete examples: Bernoulli

Bernoulli trial, $X \sim \text{Bernoulli}(p)$

$$
X=\begin{cases}1&p\\ 0&1-p\end{cases}
$$

$f_{X}(0)=p$

$f_{X}(1)=1-p \quad (0\le p\le1)$

$$
E[X]=0\times(1-p)+1\times p=p
$$

## Expectation discrete examples: Binomial

$X \sim \text{Binomial}(n, p)$; models the number of successes in $n$ trials

$$
f_{X}(k)=\binom{n}{k}p^{k}(1-p)^{n-k} \quad k=0,1,\dots,n
$$

$$
E[X]=\sum_{k=0}^{n}k\binom{n}{k}p^{k}(1-p)^{n-k}=\sum_{k=1}^{n}k\binom{n}{k}p^{k}(1-p)^{n-k}= \\
=\sum_{k=1}^{n}k\frac{n!}{(n-k)!k!}p^{k}(1-p)^{n-k}=np\sum_{k=1}^{n}\frac{(n-1)!}{(n-k)!(k-1)!}p^{k-1}(1-p)^{n-k}= \\
=np\sum_{k=1}^{n}\binom{n-1}{k-1}p^{k-1}(1-p)^{n-k}=np\sum_{j=0}^{n-1}\binom{n-1}{j}p^{j}(1-p)^{n-1-j}= \\
=np(p+(1-p))^{n-1}=np
$$

## Expectation discrete examples: Poisson

A discrete random variable $X$ is said to have a $\text{Poisson}(\lambda)$ distribution with parameter $\lambda>0$ if 

$$
P(X=k)=\frac{e^{-\lambda}\lambda^{k}}{k!}
$$

for $k=0, 1, 2, \dots$



Used to model number of events happening in a period of time e.g. number of mutations per unit length in a DNA strand, number of new patients (incidence rates), number of phone calls/particles arriving in a system, etc.

<img src="Lecture 5.assets/Screenshot 2025-11-28 at 12.58.37 AM.png" alt="Screenshot 2025-11-28 at 12.58.37 AM" style="zoom:50%;" />

## Expectation examples: Poisson (contd)

$$
E[X]=\sum_{k=0}^{\infty}kf_{X}(k)=\sum_{k=0}^{\infty}k\frac{e^{-\lambda}\lambda^{k}}{k!}=\sum_{k=1}^{\infty}k\frac{e^{-\lambda}\lambda^{k}}{k!}= \\
=\lambda e^{-\lambda}\sum_{k=1}^{\infty}\frac{\lambda^{k-1}}{(k-1)!}=\lambda e^{-\lambda}\sum_{j=0}^{\infty}\frac{\lambda^{j}}{j!}= \\
=\lambda e^{-\lambda}e^{\lambda}=\lambda
$$

## Expectation for continuous RVs

For a **Continuous** random variable $X$, with $f_{X}(x)$ the probability density function of $X$, the expectation is defined as:

$$
E[X]=\int_{-\infty}^{+\infty}xf_{X}(x)dx
$$

NOTE: Expectation may not exist E.g. Cauchy distribution
$$
f(x)=\frac{1}{\pi(1+x^{2})}, \quad -\infty<x<+\infty
$$

## Expectation examples: continuous with finite support

$X \sim F(x)$

CDF:
$$
F(x)=\begin{cases}0&if~x<0\\ 2x^{2}-x^{4}&if~0\le x\le1\\ 1&if~x\ge1\end{cases}
$$

PDF:
$$
f(x)=F^{\prime}(x)=\begin{cases}4x-4x^{3}&if~0\le x\le1\\ 0&otherwise\end{cases}
$$

Expectation Calculation:
$$
E[X]=\int_{-\infty}^{+\infty}xf(x)dx=\int_{0}^{1}x(4x-4x^{3})dx=4\left(\frac{x^{3}}{3}-\frac{x^{5}}{5}\right)\bigg|_{0}^{1}=\frac{8}{15}
$$

## Expectation examples: continuous with infinite support

$X \sim \text{Exp}[\lambda]$, $f(x)=\lambda e^{-\lambda x}$ for $x\ge0$

$$
E[X]=\int_{-\infty}^{+\infty}xf(x)dx=\int_{0}^{+\infty}x\lambda e^{-\lambda x}dx=\frac{1}{\lambda}\int_{0}^{+\infty}te^{-t}dt
$$

(Using $t=\lambda x, dt=\lambda dx)$

$$
E[X]=\frac{1}{\lambda}\int_{0}^{+\infty}te^{-t}dt=\frac{1}{\lambda}\left(-te^{-t}\bigg|_{0}^{+\infty}-\int_{0}^{+\infty}e^{-t}dt\right)=\frac{1}{\lambda}(-e^{-t})\bigg|_{0}^{+\infty}=\frac{1}{\lambda}
$$

(integrating by parts)

## Expectation for a mixed random variable

For a mixed random variable $X$ with cdf $F(x)=pF_{1}(x)+(1-p)F_{2}(x)$ with $F_{1}$ continuous and $F_{2}$ discrete:

$$
E[X]=p\int_{-\infty}^{+\infty}xf_{1}(x)dx+(1-p)\sum_{x_{i}}x_{i}f_{2}(x_{i})
$$

where $f_{1}(x)$ is the density for the continuous component, $f_{1}(x)=F_{1}^{\prime}(x)$, and $f_{2}(x)$ is the mass function for the discrete component.

## Probabilities as expectations

For a set $A \subset \Omega$ the random variable:

$$
I_{A}(\omega)=\begin{cases}1&\omega\in A\\ 0&\omega\notin A\end{cases}
$$

is called the indicator function of the set $A$.

What is the distribution of $I_{A}$?

$I_{A} \sim \text{Bernoulli}(p), p=P(A) \Rightarrow E[I_{A}]=P(A)$

Allows us to work with random variables (indicator functions) instead of sets and expectations instead of probabilities

Exercise: If $A,B \subset \Omega$, what are $I_{A}I_{B}, \min(I_{A},I_{B}), \max(I_{A},I_{B})$?

## Transformations of random variables

Example: $X \sim F(x)$

$$
F(x)=\begin{cases}0&if~x<0\\ 2x^{2}-x^{4}&if~0\le x\le1\\ 1&if~x\ge1\end{cases}
$$

What is the cdf of $Y=-\sqrt{X+1}$ ?

First, $0\le X\le1 \iff -\sqrt{2}\le-\sqrt{X+1}\le-1$

## Transformations of random variables

For $-\sqrt{2}\le y\le-1$

$$
F_{Y}(y)=P(Y\le y)= \\
=P(-\sqrt{X+1}\le y)= \\
=P(-y\le\sqrt{X+1})= \\
=P(y^{2}-1\le X)= \\
=1-P(X<y^{2}-1)=1-P(X\le y^{2}-1)= \\
=1-F_{X}(y^{2}-1)=1-2(y^{2}-1)^{2}+(y^{2}-1)^{4}
$$

Final CDF:
$$
F_{Y}(y)=\begin{cases}0&if~y<-1\\ 1-2(y^{2}-1)^{2}+(y^{2}-1)^{4}&if~-\sqrt{2}\le y\le-1\\ 1&if~y>-\sqrt{2}\end{cases}
$$

## Change-of-variable formula for the expectation

Continuous $X$:

$$
E[g(X)]=\int_{-\infty}^{+\infty}g(x)f_{X}(x)dx
$$

Discrete $X$:

$$
E[g(X)]=\sum_{x_{i}}g(x_{i})f_{X}(x_{i})
$$

Allows us to compute the expectation of $Y=g(X)$ without deriving the pdf or pmf of $g(X)!!$

## Change-of-variable formula example

In the previous example computing $E[Y]=\int_{-\sqrt{2}}^{-1}yf_{Y}(y)dy$ seems to require knowing/deriving $f_{Y}(y)=F_{Y}^{\prime}(y)$ and integrating using the pdf of $Y$ (a big mess)

The change-of-variable formula allows us to use a shortcut:
$$
E[g(X)]=\int_{-\infty}^{+\infty}g(x)f_{X}(x)dx
$$

Only require us to integrate using the pdf of $X$!
$$
E[-\sqrt{X+1}]=\int_{0}^{1}-(\sqrt{x+1})(2x^{2}-x^{4})dx
$$

Using Mathematica: `Integrate[-Sqrt[(1+x)](2x^2-x^4), {x, 0, 1}]`

$$
E[-\sqrt{X+1}]=-\frac{4}{693}(103\sqrt{2}-40)
$$

## Variance

$$
Var[X]=E[(X-E[X])^{2}]=E[X^{2}]-E[X]^{2}
$$

$Var[X]$ is the average squared deviation from the mean. Measure of dispersion/concentration.

Continuous $X$:
$$
E[X^{2}]=\int_{-\infty}^{+\infty}x^{2}f_{X}(x)dx
$$

Discrete $X$:
$$
E[X^{2}]=\sum_{x_{i}}x_{i}^{2}f_{X}(x_{i})
$$

# Week 6 – Random vectors and independence

## Last class

**Expectation**

* **Continuous:**
    $$E[X]=\int_{-\infty}^{+\infty}xf_{X}(x)dx$$
* **Discrete:**
    $$E[X]=\sum_{x_{i}}x_{i}f_{X}(x_{i})$$
* **Mixed:**
    $$E[X]=w_{d}\sum_{x_{i}}x_{i}f_{X}(x_{i})+w_{c}\int_{-\infty}^{+\infty}xf_{X}(x)dx; \quad w_{d}+w_{c}=1$$

**Variance**

* $$Var[X]=E[(X-E[X])^{2}]=E[X^{2}]-E^{2}[X]$$

**Change of variable formula/LOTUS**

* **Continuous:**
    $$E[g(X)]=\int_{-\infty}^{+\infty}g(x)f_{X}(x)dx$$
* **Discrete:**
    $$E[g(X)]=\sum_{x_{i}}g(x_{i})P_{X}(x_{i})$$

## Random vectors

We are typically interested in not one, but multiple related random variables defined on the same space.

* $X, Y$ random variables or $(X, Y)$ a random vector in $\mathbb{R}^{2}$
    * E.g. weight and height of a randomly selected person
* Geometrically, $(X, Y)$ represents a random point in $\mathbb{R}^{2}$
* More generally, a random vector in $\mathbb{R}^{n}$, $\mathbf{X}=(X_{1},\dots,X_{n})$
    * E.g. expression levels of $n$ genes for an individuals
* We can have discrete, continuous, and mixed random vectors

## Discrete random vectors

A random vector $(X, Y)$ is discrete if it takes a finite or countable number of values
$R_{X,Y}=\{(x_{1},y_{1}),(x_{2},y_{2}),\dots\}$

Joint probability mass function:

* $$P_{X,Y}(x,y)=P(X=x,Y=y)=P(X=x\cap Y=y)$$

* $$P(X\in A\cap R_{X},Y\in B\cap R_{Y})=\sum_{x_{i}\in A}\sum_{y_{j}\in B}P_{X,Y}(x_{i},y_{j})$$

In general, if $C\subset\mathbb{R}^{2}$,

* $$P((X,Y)\in C)=\sum_{(x_{i},y_{j})\in C\cap R_{X,Y}}P_{X,Y}(x_{i},y_{j})$$

$X$ and $Y$ are discrete random variables $\iff (X,Y)$ is a discrete random vector

## Continuous random vectors

A random vector is continuous if it has a joint probability density function:

* $$f_{X,Y}(x,y)\ge0$$
* $$\iint_{\mathbb{R}^{2}}f_{X,Y}(x,y)dx~dy=1$$
* $$P((X,Y)\in C)=\iint_{C}f_{X,Y}(x,y)dx~dy$$

$(X, Y)$ continuous as a random vector $\Rightarrow X$ and $Y$ continuous as individual random variables

Converse is not true: $X$ and $Y$ are continuous $\not\Rightarrow (X,Y)$ continuous as a random vector (it may not have a density)

## Random vectors

The cumulative distribution function (cdf) is defined for both discrete and continuous (and mixture) random vectors:

$$
F_{XY}(x,y)=P(X\le x,Y\le y)=\begin{cases}\int_{-\infty}^{x}\int_{-\infty}^{y}f_{X,Y}(s,t)dsdt & \text{Continuous} \\ \sum_{x_{i}\le x}\sum_{y_{j}\le y}P_{X,Y}(x_{i},y_{j}) & \text{Discrete} \end{cases}
$$

Just like for random variables, the pdf (continuous), the pmf (discrete), or the cdf (both), completely characterize probabilistically a random vector

For a continuous random vector:
$$
f_{X,Y}(x,y)=\frac{\partial^{2}}{\partial x\partial y}F_{X,Y}(x,y)
$$

The distribution (pdf, pmf or cdf) of the component random variables $X$ and $Y$ are called the marginal distribution of $X$ and $Y$ respectively

## Marginal distributions

$(X, Y)$ a random vector

$$
F_{X}(x)=\lim_{y\rightarrow+\infty}F_{X,Y}(x,y) \quad F_{Y}(y)=\lim_{x\rightarrow+\infty}F_{X,Y}(x,y)
$$

For a continuous random vector:

$$
f_{X}(x)=\int_{-\infty}^{+\infty}f_{X,Y}(x,y)dy \quad f_{Y}(y)=\int_{-\infty}^{+\infty}f_{X,Y}(x,y)dx
$$

For a discrete random vector:

$$
P_{X}(x_{i})=\sum_{y_{j}}P_{X,Y}(x_{i},y_{j}) \quad P_{Y}(y_{j})=\sum_{y_{j}}P_{X,Y}(x_{i},y_{j})
$$

## Example: discrete random vector

Let $M$ and $S$ be the minimum and the sum of two independent rolls of fair 3-faced die.

Determine:

* The joint pmf of $M$ and $S$.
* The marginal pmf of $M$ and of $S$.

## Example: continuous random vector

Suppose that the joint cumulative distribution function of $(X, Y)$ is given by:

$$
F_{X,Y}(x,y)=\begin{cases}1-e^{-2x}-e^{-y}+e^{-(2x+y)}& \text{if } x>0, y>0 \\ 0& \text{Otherwise} \end{cases}
$$
<img src="Lecture 6.assets/Screenshot 2025-11-28 at 1.09.26 AM.png" alt="Screenshot 2025-11-28 at 1.09.26 AM" style="zoom:50%;" />

## Example: continuous random vector

$$
F_{X,Y}(x,y)=\begin{cases}1-e^{-2x}-e^{-y}+e^{-(2X+y)}& \text{if } x>0, y>0 \\ 0& \text{Otherwise} \end{cases}
$$

1. Determine the joint probability density function of $X$ and $Y$.
2. Determine the marginal cumulative distribution functions of $X$ and $Y$.
3. Determine the marginal probability density functions of $X$ and $Y$.
4. Find out whether $X$ and $Y$ are independent.
5. Determine $\text{Cov}(X,Y)$ and $\rho(X,Y)$

## Example: continuous random vector

Suppose that the joint probability density function of $X$ and $Y$ is given:

$$
f_{X,Y}(x,y)=\begin{cases}x+cy^{2}&if~0\le x\le1,0\le y\le1\\ 0&Otherwise\end{cases}
$$

1. Find the constant $c$.
2. Determine the joint cumulative distribution functions of $(X, Y)$.
3. Determine the marginal probability density functions of $X$ and $Y$.
4. Find out whether $X$ and $Y$ are independent.
5. Determine \text{Cov}(X,Y) and $\rho(X,Y)$

## Independence of random variables

$X$ and $Y$ are independent if for any $A, B \subset \mathbb{R}$, $\{X \in A\}$ and $\{Y \in B\}$ are independent events:
$$
P(X \in A, Y \in B) = P(X \in A)P(Y \in B)
$$

* Equivalent to the factorization of the joint cdf as a product of the marginal cdfs:
$$
F_{X,Y}(x,y) = F_{X}(x)F_{Y}(y)
$$

* For continuous random vectors, also equivalent to the factorization of the joint pdf as a product of the marginal pdfs:
$$
f_{X,Y}(x,y) = f_{X}(x)f_{Y}(y)
$$

* For discrete random vectors, also equivalent to the factorization of the joint pmf as a product of the marginal pmfs:
$$
P_{X,Y}(x,y) = P_{X}(x)P_{Y}(y)
$$

* Definition of independence and factorization equivalences extend to multiple random variables $X_{1}, \dots, X_{n}$

## Propagation of independence

NOTE this is important and not covered in the book

* If $X$, and $Y$ are independent so are $g(X)$ and $h(Y)$ for $g,h:\mathbb{R}\rightarrow\mathbb{R}$

* If $X_{1},X_{2},\dots,X_{n}$ are independent so are $h_{1}(X_{1}),\dots,h_{n}(X_{n}),$ for $h_{i}:\mathbb{R}\rightarrow\mathbb{R}$

* If $X_{1},\dots,X_{n},Y_{1},\dots,Y_{m}$ are independent then, $g(X_{1},\dots,X_{n}),h(Y_{1},\dots,Y_{m}),$ where $g:\mathbb{R}^{n}\rightarrow\mathbb{R},h:\mathbb{R}^{m}\rightarrow\mathbb{R}$

Examples:

1. $X_{1},X_{2},X_{3},X_{4},Y_{1},Y_{2}$ independent $\Rightarrow Z_{1}=\frac{\sin(X_{1}^{2})+e^{X_{2}}}{X_{3}^{5}+1},Z_{2}=\cos(Y_{1})-Y_{2}^{3}$ are independent

2. $X_{1},X_{2},\dots,X_{n}\stackrel{iid}{\sim} \text{Bernoulli}(p),$ $Y_{1},Y_{2},\dots,Y_{m}\stackrel{iid}{\sim} \text{Bernoulli}(q)$
(iid stands for independent identically distributed)

Let $X=X_{1}+X_{2}+\dots+X_{n}, Y=Y_{1}+Y_{2}+\dots+Y_{m}.$

Then $X\sim \text{Binomial}(n,p)$ and $Y\sim \text{Binomial}(m,q)$ and $X, Y$ are independent

## Expectation of a random vector

$$
E[(X,Y)]=(E[X],E[Y])
$$

Interpretation is analog to that for random variables, 'center' of the two-dimensional distribution, center of mass if we think of probability as mass distributed on the surface of the plane $\mathbb{R}^{2}$

In general,
$$
E[\mathbf{X}]=(E[X_{1}],\dots,E[X_{n}])
$$

Example: $X\sim \text{Exp}(\lambda_{1}), Y\sim \text{Exp}(\lambda_{2})$
$$
E[(X,Y)]=(E[X],E[Y])=\left(\frac{1}{\lambda_{1}},\frac{1}{\lambda_{2}}\right)
$$

## Multi-dimensional LOTUS

$\mathbf{X}=(X_{1},\dots,X_{n})$ a random vector, $g:\mathbb{R}^{n}\rightarrow\mathbb{R}$ a function, then:

$$
E[g(\mathbf{X})] = E[g(X_{1},\dots,X_{n})] = \begin{cases}\int_{\mathbb{R}^{n}}g(x_{1},\dots,x_{n})f_{\mathbf{X}}(x_{1},\dots,x_{n})dx_{1}\dots dx_{n} & \text{if } \mathbf{X} \text{ continuous} \\ \sum_{\mathbf{x}_{i}}g(\mathbf{x}_{i})f_{\mathbf{X}}(\mathbf{x}_{i}) & \text{if } \mathbf{X} \text{ discrete} \end{cases}
$$

Consequences:

* **Expectation is linear:**
$$
E[a_{1}X_{1}+a_{2}X_{2}+\dots+a_{n}X_{n}]=a_{1}E[X_{1}]+a_{2}E[X_{2}]+\dots+a_{n}E[X_{n}]
$$

* $$E[XY]=E[X]E[Y] \quad \text{for independent random variables } X, Y$$

Example of linearity: $X\sim \text{Binomial}(n,p)$

Then, $X=X_{1}+\dots+X_{n}$ where $X_{1},X_{2},\dots X_{n}\sim \text{Bernoulli}(p)$

$$
E[X]=E[X_{1}]+\dots+E[X_{n}]=\underbrace{p+\dots+p}_{\text{n times}}=np
$$

## Covariance

For arbitrary random variables $X$ and $Y$:

$$
Var[X+Y]=Var[X]+Var[Y]+2E[(X-E[X])(Y-E[Y])]
$$

The term:
$$
\text{Cov}(X,Y)=E[(X-E[X])(Y-E[Y])]=E[XY]-E[X]E[Y]
$$
is called the covariance of $X$ and $Y$.

It measures how much $X$ and $Y$ co-vary, i.e. vary together.

* $\text{Cov}(X,Y)>0$ if whenever $X>E[X]$ is likely that also $Y>E[Y]$ and vice versa (and that when $X<E[X]$ also more likely that $Y<E[Y]$)

* $\text{Cov}(X,Y)<0$ if whenever $X>E[X]$ is likely that $Y<E[Y]$ and vice versa (and that when $X<E[X]$ also more likely that $Y>E[Y]$)

* $X,Y$ independent $\Rightarrow \text{Cov}(X,Y)=0$

* Converse is not true: $\text{Cov}(X,Y)=0\Rightarrow X,Y$ independent

## Covariance

Example of additivity of variance for uncorrelated RVs

$X\sim \text{Binomial}(n,p)$

Then, $X=X_{1}+\dots+X_{n}$ where $X_{1},X_{2},\dots X_{n}\stackrel{iid}{\sim} \text{Bernoulli}(p)$

$$
Var[X]=Var[X_{1}]+\dots+Var[X_{n}]+\sum_{i<j}2\text{Cov}(X_{i},X_{j})= \\
=\underbrace{p(1-p)+\dots+p(1-p)}_{\text{n times}}=np(1-p)
$$

## Properties of covariance

* Covariance is linear in each of its terms:
$$
\text{Cov}(aX+bY,cU+dV)=ac\text{Cov}(X,U)+ad\text{Cov}(X,V)+bc\text{Cov}(Y,U)+bd\text{Cov}(Y,V)
$$

$$
\text{Cov}(X,X)=Var[X] \quad (\Rightarrow Var[aX]=a^{2}Var[X])
$$
* **Cauchy-Schwartz inequality**
$$
|E[XY]| \le \sqrt{E[X^{2}]E[Y^{2}]}
$$
* From Cauchy-Schwartz inequality using $X-E[X]$ and $Y-E[Y]$ in place of $X$ and $Y$, it follows that
$$
|\text{Cov}(X,Y)| \le \sqrt{Var[X]Var[Y]} = \sigma_{X}\sigma_{Y}
$$
($\sigma_{X}=\sqrt{Var[X]},\sigma_{Y}=\sqrt{Var[Y]}$ are called the standard deviations of $X$ and $Y$ respectively)

* Equivalently,
$$
-1\le\frac{\text{Cov}(X,Y)}{\sqrt{Var[X]Var[Y]}}\le1
$$

## Correlation

$$
\rho(X,Y)=\frac{\text{Cov}(X,Y)}{\sqrt{Var[X]Var[Y]}} \quad \text{is the correlation between } X \text{ and } Y
$$

* $X, Y \text{ independent } \Rightarrow \rho(X,Y)=0$

* Converse is not true: $\rho(X,Y)=0 \Rightarrow X, Y \text{ independent}$

* $\rho(X,Y)$ is a standardized version of $\text{Cov}(X,Y)$

* $\rho(X,Y)$ is unaffected by changes of units:
$$
\rho(aX+b, cY+d)=\rho(X,Y)
$$

* Covariance it's not invariant: $\text{Cov}(X,Y)=\rho(X,Y)\sigma_{X}\sigma_{Y}$, so the larger $\sigma_{X}$ and $\sigma_{Y}$, the larger $\text{Cov}(X,Y)$ in absolute value (provided $\rho(X,Y)\ne0$)

# Week 7 – Transformation of RVs, Law of large numbers

### Last Class 

- Random vector = multiple random variables defined on the same probability space. 
- Discrete (have joint pmf) and continuous (have joint pdf) random vectors.
- LOTUS to compute the expectation of a transformed random vector. 
- Independence of random variables. 
- Covariance and correlation.

### Distribution of a sum of discrete RVs

(X, Y) a random vector. What is the distribution of $Z=X+Y$?

* If (X, Y) is discrete then
    $$
    P_{Z}(z)=\sum_{x_{i}+y_{i}=z}P_{X,Y}(x_{i},y_{i})
    $$

* Example: Let X and Y be independent random variables with common pmf given by
    $P_{X}(0)=\frac{1}{4}$, $P_{X}(1)=\frac{1}{2}$, $P_{X}(2)=\frac{1}{4}$. Find the pmf of $Z=X+Y$.

### Distribution of a sum of continuous RVs

(X, Y) a random vector and $Z=X+Y$

If (X, Y) is continuous then
$$f_{Z}(z)=\int_{-\infty}^{+\infty}f_{X,Y}(x,z-x)dx=\int_{-\infty}^{+\infty}f_{X,Y}(z-y,y)dy$$

Example: $X\sim Exp(\lambda)$, $Y\sim U[0,1]$, X and Y independent. Find the cdf and the pdf of $Z=X+Y$.

### Bivariate normal distribution

Two random variables X and Y are said to have a **bivariate normal distribution** if their joint pdf is given by:

$$f_{XY}(x,y)=\frac{1}{2\pi\sigma_{X}\sigma_{Y}\sqrt{1-\rho^{2}}}\cdot exp\{-\frac{1}{2(1-\rho^{2})}[(\frac{x-\mu_{X}}{\sigma_{X}})^{2}+(\frac{y-\mu_{Y}}{\sigma_{Y}})^{2}-2\rho\frac{(x-\mu_{X})(y-\mu_{Y})}{\sigma_{X}\sigma_{Y}}]\}$$

$$\mu=\begin{pmatrix}\mu_{X}\\ \mu_{Y}\end{pmatrix}=E\begin{pmatrix}X\\ Y\end{pmatrix}$$ and

$$\Sigma=\begin{pmatrix}Var(X)&Cov(X,Y)\\ Cov(X,Y)&Var(Y)\end{pmatrix}=\begin{pmatrix}\sigma_{X}^{2}&\rho\sigma_{X}\sigma_{Y}\\ \rho\sigma_{X}\sigma_{Y}&\sigma_{Y}^{2}\end{pmatrix}$$ is the variance-covariance-matrix.

where $\rho\in(-1,1),\sigma_{X}>0,\sigma_{Y}>0$.

$$(X,Y)\sim N(\mu,\Sigma)$$

### Sums of normals

* If $X\sim N(\mu_{X},\sigma_{X}^{2})$, $Y\sim N(\mu_{Y},\sigma_{Y}^{2})$ are **independent** then
    $$X+Y\sim N(\mu_{X}+\mu_{Y},\sigma_{X}^{2}+\sigma_{Y}^{2})$$

* If $(X,Y)\sim N(\mu,\Sigma)$ then
    $$X+Y\sim N(\mu_{X}+\mu_{Y},\sigma_{X}^{2}+\sigma_{Y}^{2}+2\rho\sigma_{X}\sigma_{Y})$$

* If $X\sim N(\mu_{X},\sigma_{X}^{2}),Y\sim N(\mu_{Y},\sigma_{Y}^{2})$ but not bivariate normal then $X+Y$ are not necessarily normal.

* Example: $X\sim N(\mu,\sigma^{2}),Y=-X$. $Y\sim N(-\mu,\sigma^{2})$ but $X+Y=0$, a constant random variable.

### Sum of independent exponentials

$X_{1},...,X_{n}\stackrel{iid}{\sim}Exp(\lambda)$ then $Z=X_{1}+...+X_{n}\sim Gamma(n,\lambda)$

A continuous random variable has a **gamma distribution** with parameters $\alpha>0$ and $\lambda>0$ if its probability density function is given by:

$$f(x)=\frac{\lambda(\lambda x)^{\alpha-1}e^{-\lambda x}}{\Gamma(\alpha)}I_{[0,+\infty)}(x)$$

where

$$\Gamma(\alpha)=\int_{0}^{+\infty}t^{\alpha-1}e^{-t}dt$$

for $\alpha>0$ is the **gamma function**.

The gamma function is a generalization of the factorial: $\Gamma[\alpha+1]=\alpha\Gamma[\alpha]$ and $\Gamma[n+1]=n!$ for $n=0,1,2,...$

### Maximum and minimum

$X_{1},...,X_{n}\sim F(x)$ iid random variables and $U=min(X_{1},...,X_{n}),$
$V=max(X_{1},...,X_{n})$

Then:

$$F_{V}(v)=F(v)^{n}$$

(if continuous with density $f(x)$, then $f_{V}(v)=nf(v)F(v)^{n-1}$

$$F_{U}(u)=1-(1-F(u))^{n}$$

(if continuous with density $f(x)$ then $f_{U}(u)=nf(u)(1-F(u))^{n-1}$

### Averaging reduces variability

$X_{1},X_{2}\sim F(x)$ independent

$Var(X_{1})=Var(X_{2})=\sigma^{2}$

$$Var(\frac{X_{1}+X_{2}}{2})=\frac{1}{2^{2}}(Var(X_{1})+Var(X_{2}))=\frac{1}{2^{2}}(\sigma^{2}+\sigma^{2})=\frac{\sigma^{2}}{2}$$

### Averaging reduces variability

$X_{1},X_{2},...$ i.i.d with expectation $\mu$ and variance $\sigma^{2}$

$$\overline{X_{n}}=\frac{X_{1}+...+X_{n}}{n}$$

$$E[\overline{X_{n}}]=\frac{1}{n}(E[X_{1}]+...+E[X_{n}])=\frac{1}{n}\underbrace{(\mu+...+\mu)}_{n~times}=\mu$$

$$Var[\overline{X_{n}}]=\frac{1}{n^{2}}(Var[X_{1}]+...+Var[X_{n}])=\frac{1}{n^{2}}\underbrace{(\sigma^{2}+...+\sigma^{2})}_{n~times}=\frac{\sigma^{2}}{n}$$

### Markov's inequality

If $U\ge0$ is a random variable with finite expectation, then, for every $t>0$:

$$P(U\ge t)\le\frac{E[U]}{t}$$

Intuition:

* Let U be the income of a random selected individual from a population. Taking $t=2E[U]$, Markov's inequality says that $P(U\ge2E[U])\le\frac{1}{2}$. It is impossible for more than half of the population to make at least twice the average income.

* This has to be true because if more than half of the population make more than twice the average income, the average income would have to be higher!

* Taking $t=3E[U]$, we get $P(U\ge3E[U])\le\frac{1}{3}$. It is impossible for more than one third of the population to make at least 3 times the average income.

##### Proof

$U\ge0$ a random variable with finite expectation, $t>0$:

Define the new random variable $U_{t}=\begin{cases}0&if~U<t\\ t&if~U\ge t\end{cases}$

$U_{t}$ is discrete random variable taking only values 0 and t. So, $E[U_{t}]=tP(U\ge t).$

Clearly $U\ge U_{t}$

Expectations preserve inequalities, so, $E[U]\ge E[U_{t}]\Rightarrow E[U]\ge tP(U\ge t)\Rightarrow P(U\ge t)\le\frac{E[U]}{t}$

### Chebyshev's inequality

If X is a random variable with mean $\mu$ and variance $\sigma^{2}$ , then, for every $t>0$:

* $$P(|X-E[X]|\ge t)\le\frac{Var[X]}{t^{2}}$$

or equivalently

* $$P(|X-E[X]|<t)\ge1-\frac{Var[X]}{t^{2}}$$

or equivalently

* $$P(\frac{|X-E[X]|}{\sigma}\ge t)\le\frac{1}{t^{2}}$$

#### Proof

X a random variable with mean $\mu$ and variance $\sigma^{2}$, $t>0$

Consider the non-negative random variable $U=(X-\mu)^{2}$

Apply Markov's inequality to U, with $t^{2}:P(U\ge t^{2})=P((X-\mu)^{2}\ge t^{2})\le\frac{E[(X-\mu)^{2}]}{t^{2}}=\frac{Var(X)}{t^{2}}$

Noticing that $\{|X-\mu|\ge t\}=\{(X-\mu)^{2}\ge t^{2}\}$, we get Chebyshev's inequality:

$$P(|X-\mu|\ge t)\le\frac{Var(X)}{t^{2}}$$

### Chebyshev's inequality consequences

Any random variable with finite variance (continuous, discrete, mixed), regardless of its distribution, has most of its probability mass concentrated within a few standard deviations of its mean.

Taking $t=k\sigma, k=2,3,4$ and applying Chebishev's inequality:

$$P(|X-E[X]|\ge k\sigma)\le\frac{\sigma^{2}}{k^{2}\sigma^{2}}=\frac{1}{k^{2}}$$

$$P(|X-E[X]|\le k\sigma)\ge1-\frac{1}{k^{2}}$$

For $k=2,3,4$ the bound are $3/4$, $8/9$, and $15/16$ respectively

### Weak Law of large numbers (WLLN)

$X_{1},X_{2},...$ i.i.d with finite expectation $\mu$ then:

$$\lim_{n\rightarrow\infty}P(|\overline{X_{n}}-\mu|>\epsilon)=0$$

This form of convergence of random variables is called **convergence in probability** and is denoted as
$$\overline{X_{n}}\stackrel{P}{\rightarrow}\mu$$

Equivalently:

$$\lim_{n\rightarrow\infty}P(|\overline{X_{n}}-\mu|\le\epsilon)=1$$

**The sample mean converges to the true mean**

### (Weak) Law of large numbers

##### Proof

$X_{1},X_{2},...$ i.i.d with finite expectation $\mu$.

To make the proof easier, we will also assume that $\sigma^{2}<+\infty$

But the for the WLLN to hold only the expectation needs to exist. The variance may be infinite.

Let $\epsilon>0$. Apply Chebyshev's inequality to $\overline{X_{n}}:$

$$P(|\overline{X_{n}}-\mu|\ge\epsilon)\le\frac{Var(\overline{X_{n}})}{\epsilon^{2}}=\frac{\sigma^{2}}{n\epsilon^{2}}$$

This implies:

$$\lim_{n\rightarrow\infty}P(|\overline{X_{n}}-\mu|\ge\epsilon)=0$$

### Strong Law of large numbers (SLLN)

$X_{1},X_{2},...$ i.i.d with finite expectation $\mu$.

$$P(\lim_{n\rightarrow\infty}\overline{X_{n}}=\mu)=1$$

This form of convergence of random variables is called **convergence with probability 1** and is denoted as
$$\overline{X_{n}}\stackrel{w.p.1}{\longrightarrow}\mu$$
(also called **almost sure convergence**)

The strong law is **stronger** than weak law because convergence with probability 1 is a stronger concept
than convergence in probability: convergence with probability $1\implies$ convergence in probability (but not the other way around)

### Law of large numbers

$X_{1},X_{2},...,X_{n}\sim N(1,1)$

Five realizations of $\overline{X_{n}}$ as a function of $n$

<img src="Lecture 7.assets/image-20251129161727499.png" alt="image-20251129161727499" style="zoom:50%;" />



# Week 8 – Central Limit Theorem

### Last Class

* **Markov's inequality:** for any RV $U\ge0$
    $$P(U\ge t)\le\frac{E[U]}{t} \quad for~any~t>0$$

* **Chebyshev's inequality:** for any RV $X, Var[X_{i}]<\infty;$
    $$P(|X-E[X]|\ge t)\le\frac{Var[X]}{t^{2}} \quad for~any~t>0$$

* **Law of large numbers:** $X_{1},X_{2},...$ i.i.d with finite expectation $\mu$:
    * **Weak:** $$\lim_{n\rightarrow\infty}P(|\overline{X}_{n}-\mu|>\epsilon)=0$$
    * **Strong:** $$P(\lim_{n\rightarrow\infty}\overline{X}_{n}=\mu)=1$$

### Basic Statistical Model

- Want to learn characteristics of a population:

  * Income of Los Angeles residents

  * Blood pressure of patients form LA county hospital

  * Vaping in among teenagers in California

  * Genotypes at a gene among individuals with Hispanic ancestry


* We model the distribution of the characteristic as a random variable X (e.g. height, blood pressure, vaping (yes vs. no), Genotypes (0,1,2)))
* To learn about X we collect a random sample: $X_{1},X_{2},...,X_{n}$ from $F_{X}(x)$ the distribution of X
* $X_{1},X_{2},...,X_{n}$ have the same probability distribution and are mutually independent.
* The distribution $F(x;\theta)$ of $X_{i}$ is unknown or only partially known
    * E.g. $X_{i}\sim N(\mu,\sigma^{2})$ with known $\sigma^{2}$ but unknown $\mu$
* We conceptualize the observed data $x_{1},...,x_{n}$ as realizations of the random variables $X_{1},...,X_{n}$

### Sample statistics

Sample statistics are empirical summaries of the data:

* sample mean: $$\overline{x}_{n}=\frac{x_{1}+...+x_{n}}{n}$$

* sample variance: $$s_{n}^{2}=\frac{1}{n-1}\sum_{i=1}^{n}(x_{i}-\overline{x}_{n})^{2}$$(sometimes$$\frac{1}{n}\sum_{i=1}^{n}(x_{i}-\overline{x}_{n})^{2})$$

* sample minimum: $$x_{(1)}=min(x_{1},...,x_{n})$$

We think of these as realizations of the corresponding random variables:

$$\overline{X_{n}}=\frac{X_{1}+...+X_{n}}{n}$$

$$S_{n}^{2}=\frac{1}{n-1}\sum_{i=1}^{n}(X_{i}-\overline{X_{n}})^{2}$$

$$X_{(1)}=min(X_{1},...,X_{n})$$

### Central Limit Theorem

$X_{1},...,X_{n}$ i.i.d. $E[X_{i}]=\mu, Var[X_{i}]=\sigma^{2}$ then:

Sum form: $S_{n}=X_{1}+...+X_{n}$

$$Z_{n}=\frac{S_{n}-E[S_{n}]}{\sqrt{Var[S_{n}]}}=\frac{S_{n}-n\mu}{\sqrt{n}\sigma}\stackrel{D}{\rightarrow}N(0,1)$$

Sample mean form: $$\overline{X_{n}}=\frac{X_{1}+...+X_{n}}{n}$$

$$Z_{n}=\frac{\overline{X}_{n}-E[\overline{X}_{n}]}{\sqrt{Var[\overline{X}_{n}]}}=\frac{\sqrt{n}(\overline{X}_{n}-\mu)}{\sigma}\stackrel{D}{\rightarrow}N(0,1)$$

The symbol $\stackrel{D}{\rightarrow}$ denotes **convergence in distribution**. It means that as $n\rightarrow\infty$ the cumulative distribution function of $Z_{n}=\frac{S_{n}-n\mu}{\sqrt{n}\sigma}=\frac{\sqrt{n}(\overline{X}_{n}-\mu)}{\sigma}$ gets closer and closer to the cdf of a standard normal.

Formally, if $F_{n}(x)=F_{Z_{n}}(x)$ denotes the cdf of $Z_{n}$, then $F_{n}(x)\rightarrow\Phi(x)$ for every $x\in\mathbb{R}$, where $\Phi(x)$ is the cdf of a $N(0,1)$ RV.

---

Sum of n i.i.d. exponentials: $S_{n}=X_{1}+...+X_{n}, X_{i}\sim Exp(2)$

<img src="Lecture 8.assets/image-20251129162125105.png" alt="image-20251129162125105" style="zoom:80%;" />

Blue line is pdf of $S_{n}$. Red line is pdf of a normal $N(\frac{n}{2},\frac{n}{4})$

### Example

A runner attempts to pace a 100m race. Her strides (steps) are independently distributed with mean $\mu=0.97$ meters and a standard deviation of $\sigma=0.1$. What is the (approximate) probability that her 100 strides differ from 100 meters by no more than five meters?

### Estimation

We want to learn about a distribution in a population

* e.g. proportion of democrat voters in CA, average blood pressure among covid survivors aged $70+$, vaping frequency among young adults in the US, rate of patient ER night admissions in LA county hospitals

* We take a sample of size $n$ from the population and conceptualize it as a random sample $X_{1},...,X_{n}$ from a distribution $F_{X}(x)$ that is **totally or partially unknown to us**.

* We want to estimate specific characteristics or **parameters** of the underlying distribution:
    * true mean $E[X_{i}]=\mu$ (e.g. $X_{i}$ blood pressure)
    * the true variance, $Var[X_{i}]=\sigma^{2}$ (e.g. $X_{i}$ blood pressure)
    * or a probability like $P(X_{i}=1)$ (e.g. $1=$ democrat voter; $0=$ not democrat voter)
    * or a rate (e.g. expected number of ER patients per hour) ($X_{i}=$ number of patients within a period of $1$-hour)

---

Example 1: To estimate the unknown mean of a population $\mu$ (e.g. blood pressure)

- Natural to use the **sample mean** $\overline{X}_{n}$ to estimate $\mu$ because we know that for large $n$ the sample mean will be close to the true mean.

Example 2. We can model the number of arrivals per hour at an ER unit as a $Poisson(\lambda)$. Suppose we count the arrivals during each on $n$ (non-overlapping) 1-hour intervals to get the random sample $X_{1},...,X_{n}$. Here $\lambda$ is unknown and we want to estimate it.

- A natural estimate is also the **sample mean** $\overline{X}_{n}$ because $E[X_{i}]=\lambda$.

- But using the **sample variance** $S_{n}^{2}$ is also reasonable because $Var[X_{i}]=\lambda$

- In future classes we'll learn how to choose among different options for estimating a parameter of interest

### Estimator vs. estimate

* Estimate: value t that only depends on the dataset $x_{1},x_{2},...,x_{n},$ i.e., t is some function of the dataset $t=h(x_{1},x_{2},...,x_{n}).$ Example: $t=\overline{x}_{n}=\frac{x_{1}+...+x_{n}}{n}$

* An *estimate is a number* (or a vector of numbers in multi-parameter estimation problems)

* **Estimator**: Let $t=h(x_{1},x_{2},...,x_{n})$ be an estimate based on the dataset $x_{1},x_{2},...,x_{n}$. Then $t$ is a realization of the random variable $T=h(X_{1},X_{2},...,X_{n})$. The random variable T is called an estimator.

* *An estimator is a random variable*

* *An estimate is a realization of random variable*

### Sampling distribution

Example: estimating the proportion $p$ of LA teenagers that vape from a sample $Y_{1},...Y_{n}$
$Y_{i}\sim Bernoulli(p)$.

- $Y_{i}$ records whether the teenager vapes (yes=1 vs. no=0)

* The sample proportion $\hat{p}_{n}=\frac{S_{n}}{n}$ of vapers is a natural estimator of $p$ ($S_{n}=Y_{1}+...+Y_{n}$ is the total number of vapers in the sample), because by the LLN $\hat{p}_{n}{\rightarrow}p$

* The sampling distribution is just the standard distribution (pdf, pmf, cdf) of the random variable we call the estimator.

* For example of vapers, the sampling distribution of $\hat{p}_{n}$ is the distribution of the random variable $$\hat{p}_{n}=\frac{S_{n}}{n}$$

### Unbiased Estimators

$X_{1},...X_{n}$ a random sample from distribution F, and $\theta$ a parameter of interest about F (e.g. mean)

* An estimator $T$ of a parameter $\theta$ is unbiased if $E[T]=\theta$

* An unbiased estimator has no systematic tendency to produce estimates that are larger than or smaller than the target parameter $\theta$

* The difference $E[T]-\theta$ is called the bias of the estimator $T$

* If $bias\ne0$ the estimator is called biased

### Sample Mean and sample variance

- $X_{1},...X_{n}$ a random sample with mean $E[X_{i}]=\mu$ and $Var[X_{i}]=\sigma^{2}$

* The sample mean $\overline{X}_{n}$ is an unbiased estimator of the population mean $\mu$.
    $$E[\overline{X}_{n}]=\mu$$

* The sample variance $S_{n}^{2}=\frac{1}{n-1}\sum_{i=1}^{n}(X_{i}-\overline{X}_{n})^{2}$ is an unbiased estimator of the population variance $\sigma^{2}$
    $$E[S_{n}^{2}]=\sigma^{2}$$

### Unbiasedness is not preserved under general transformations

* In general, if $T$ is an unbiased estimator of $\theta$, $g(T)$ is not an unbiased estimate of $g(\theta)$
* Example:
    * $\overline{X}_{n}$ is unbiased for $E[X_{i}]=\mu$
    * But $\overline{X}_{n}^{2}$ is not unbiased for $E[X_{i}]^{2}=\mu^{2}$, Because by Jensen's inequality $E[\overline{X}_{n}^{2}]>E[\overline{X}_{n}]^{2}=\mu^{2}$
* **Jensen's inequality:** if $g(t)$ is a convex function, then $E[g(T)]\ge g(E[T])$. Equality holds only if $g(x)=at+b$
* If $g$ linear $g(t)=at+b, E[g(T)]=E[aT+b]=aE[T]+b=g(E[T])$ so $g(T)$ is unbiased for $g(\theta)$


# Week 9 – Unbiased estimation - Efficiency, MSE

### Last Class-CLT

$X_{1},...,X_{n}\stackrel{i.i.d.}{\sim}X$ $E[X_{i}]=\mu,Var[X_{i}]=\sigma^{2}$ then:

Sum form: $S_{n}=X_{1}+...+X_{n}$

$$
Z_{n}=\frac{S_{n}-E[S_{n}]}{\sqrt{Var[S_{n}]}}=\frac{S_{n}-n\mu}{\sqrt{n}\sigma}\stackrel{D}{\rightarrow}N(0,1)
$$

Sample mean form: $$\overline{X_{n}}=\frac{X_{1}+...+X_{n}}{n}$$

$$
Z_{n}=\frac{\overline{X_{n}}-E[\overline{X_{n}}]}{\sqrt{Var[\overline{X_{n}}]}}=\frac{\sqrt{n}(\overline{X_{n}}-\mu)}{\sigma}\stackrel{D}{\rightarrow}N(0,1)
$$

The symbol $\stackrel{D}{\rightarrow}$ denotes **convergence in distribution**. It means that as $n\rightarrow\infty$ the cumulative distribution function of $Z_{n}=\frac{S_{n}-n\mu}{\sqrt{n}\sigma}=\frac{\sqrt{n}(\overline{X_{n}}-\mu)}{\sigma}$ gets closer and closer to the cdf of a standard normal.

Formally, if $F_{n}(x)=F_{Z_{n}}(x)$ denotes the cdf of $Z_{n}$, then $F_{n}(x)\rightarrow\Phi(x)$ for every $x\in\mathbb{R}$, where $\Phi(x)$ is the cdf of a $N(0,1)$ RV.

### Last Class-Basic statistical model

- Want to learn characteristics of a population:

  - Income of Los Angeles residents

  * Blood pressure of patients from LA county hospital

  * Vaping among teenagers in California

  * Genotypes at a gene among individuals with Hispanic ancestry


* We model the distribution of the characteristic as a random variable X (e.g. height, blood pressure, vaping (yes vs. no), Genotypes (0,1,2))

* To learn about X we collect a random sample: $X_{1},X_{2},...,X_{n}$ from $F_{X}(x),$ the distribution of X

* $X_{1},X_{2},...,X_{n}$ have the same probability distribution and are mutually independent.

* The distribution $F_{X}(x)$ of $X_{i}$ is unknown or only partially known.

* E.g. $X_{i}\sim N(\mu,\sigma^{2})$ with known $\sigma^{2}$ but unknown $\mu$

### Choosing among unbiased estimators. Example

* $X_{1}, \dots, X_{n} \stackrel{i.i.d}{\sim} U[0, \theta]$
* $f_{X}(x) = \frac{1}{\theta}I_{[0,\theta]}(x)$
* $E[X_{i}] = \frac{\theta}{2}$, so $E[\overline{X_{n}}] = \frac{\theta}{2}$
* Then $\widehat{\theta} = 2\overline{X_{n}}$ is an unbiased estimator of $\theta$

Intuitively a natural estimate for theta could also be based on $T = \max\{X_{1}, \dots, X_{n}\}$

* $f_{T}(t) = n\frac{t^{n-1}}{\theta^{n}}I_{[0,\theta]}(t)$
* $E[T] = \frac{n}{n+1}\theta$ so $\widetilde{\theta} = \frac{n+1}{n} T$ is an unbiased estimator of $\theta$

So, both $\widehat{\theta}$ and $\widetilde{\theta}$ are unbiased estimators of $\theta$, which one is better?

### Choosing among unbiased estimators-Example.

Let's perform a simulation to see how the two estimators behave:

```r
set.seed(101)
theta = 2
n = 50
nsims = 500
theta_hat = theta_tilde = numeric(nsims)

for (i in 1:nsims){
    x = runif(n=n, max=theta)
    theta_hat[i] = 2 * mean(x)
    theta_tilde[i] = ((n+1)/n) * max(x)
}
```

### Choosing among unbiased estimators-Example

<img src="Lecture 9.assets/Screenshot 2025-11-30 at 10.25.31 PM.png" alt="Screenshot 2025-11-30 at 10.25.31 PM" style="zoom:67%;" />

### Choosing among unbiased estimators-Example

* We see empirically that $\widetilde{\theta}$ is much less variable than $\widehat{\theta}$
* But also theoretically, $Var[\widetilde{\theta}]=\frac{\theta^{2}}{n(n+2)}$ and $Var[\widehat{\theta}]=\frac{\theta^{2}}{3n}$
* So, $Var[\widetilde{\theta}] < Var[\widehat{\theta}]$, for $n \ge 2$ and goes much faster to zero!
* Additionally, $\widehat{\theta}$ can take values way over the true $\theta$
* So, $\widetilde{\theta}$ is a much better estimate of $\theta$ than $\widehat{\theta}$

### Mean square error

* Although **unbiasedness** is a desirable property, unbiased estimators do not always exist
* Even when they exist, requiring unbiasedness maybe too stringent (i.e. there can be other good estimators that are biased)
* A general performance of an estimator can be judged by the way it spreads around the parameter to be estimated:
  - If $T$ is an estimator for a parameter $\theta$, the **mean squared error** of $T$ is the number:
    $$MSE(T) = E[(T-\theta)^2]$$

* It's easy to show that $MSE(T) = Var(T) + Bias(T)^2$ where $Bias(T) = E[T]-\theta$
* A **biased estimator** with a small bias could be more useful than an **unbiased estimator** with a large variance.
* Better to use $MSE(T)$ to choose between estimators
* When $Bias(T)=0$, $MSE(T) = Var(T)$

### Mean square error - example

$X_{1}, \dots, X_{n} \stackrel{i.i.d}{\sim} Poisson(\mu)$

Two candidate estimators for $p_{0}=P(X_{i}=0)=e^{-\mu}$:

* $\widetilde{p}_{0}=\frac{\text{number of } X_{i}=0}{n}$
* $\widehat{p}_{0}=e^{-\overline{X_{n}}}$

$\widetilde{p}_{0}$ is unbiased but $\widehat{p}_{0}$ is not? Which one is better?

### Mean square error - example

Simulation to see how the two estimators behave

* True $p_{0}=e^{-2} \approx 0.135$

<img src="Lecture 9.assets/Screenshot 2025-11-30 at 10.47.20 PM.png" alt="Screenshot 2025-11-30 at 10.47.20 PM" style="zoom:50%;" />

### Mean square error - example

<img src="Lecture 9.assets/Screenshot 2025-11-30 at 10.47.59 PM.png" alt="Screenshot 2025-11-30 at 10.47.59 PM" style="zoom:50%;" />



# Week 10 – Maximum Likelihood Estimation

### Review - Unbiased Estimators

$X_{1}, \dots, X_{n}$ a random sample from distribution $F$, and a parameter of interest about $F$ (e.g. mean)

* An estimator $T$ of a parameter $\theta$ is **unbiased** if $E[T]=\theta$
* An unbiased estimator has no systematic tendency to produce estimates that are larger than or smaller than the target parameter $\theta$
* $\overline{X_{n}}$ is an unbiased estimator of the population mean $\mu$.
* $S_{n}^{2}=\frac{1}{n-1}\sum_{i=1}^{n}(X_{i}-\overline{X_{n}})^{2}$ is an unbiased estimator of the population variance $\sigma^{2}$
* Unbiasedness is not preserved under transformations.

### Last Class- Choosing among unbiased estimators. Example

* $X_{1}, \dots, X_{n} \stackrel{i.i.d}{\sim} U[0, \theta]$
* $f_{X}(x) = \frac{1}{\theta}I_{[0,\theta]}(x)$
* $E[X_{i}] = \frac{\theta}{2}$, so $E[\overline{X_{n}}] = \frac{\theta}{2}$
* Then $\widetilde{\theta} = 2\overline{X_{n}}$ is an unbiased estimator for $\theta$

Intuitively a natural estimator for $\theta$ would also be based on $T = \max\{X_{1}, \dots, X_{n}\}$

* $f_{T}(t) = n\frac{t^{n-1}}{\theta^{n}}I_{[0,\theta]}(t)$
* $E[T] = \frac{n}{n+1}\theta$ so $\widehat{\theta} = \frac{n+1}{n}T$ is an unbiased estimator of $\theta$

So, both $\widetilde{\theta}$ and $\widehat{\theta}$ are unbiased estimators of $\theta$, which one is better?

### Last Class - Choosing among unbiased estimators-Example

<img src="Lecture 10.assets/Screenshot 2025-11-30 at 10.50.08 PM.png" alt="Screenshot 2025-11-30 at 10.50.08 PM" style="zoom:50%;" />

### Last Class - Choosing among unbiased estimators example.

* We see empirically that $\widetilde{\theta}$ is much less variable than $\widehat{\theta}$
* But also theoretically, $Var[\widetilde{\theta}]=\frac{\theta^{2}}{n(n+2)}$ and $Var[\widehat{\theta}]=\frac{\theta^{2}}{3n}$
* So, $Var[\widetilde{\theta}]<Var[\widehat{\theta}]$ for $n\ge2$ and goes much faster to zero!
* Additionally, $\widehat{\theta}$ can take values way over the true $\theta$
* So, $\widetilde{\theta}$ is a much better estimate of $\theta$ than $\widehat{\theta}$

### Last Class- Mean square error

* Although **unbiasedness** is a desirable property, unbiased estimators do not always exist
* Even when they exist, requiring unbiasedness maybe too stringent (i.e. there can be other good estimators that are biased)
* A general performance of an estimator can be judged by the way it spreads around the parameter to be estimated:
  * If $T$ is an estimator for a parameter $\theta$, the **mean squared error** of $T$ is the number:
    $$MSE(T)=E[(T-\theta)^{2}]$$


* It's easy to show that $MSE(T)=Var(T)+Bias(T)^{2}$ where $Bias(T)=E[T]-\theta$
* A **biased estimator** with a small bias could be more useful than an **unbiased estimator** with a large variance.
* Better to use $MSE(T)$ to choose between estimators
* When $Bias(T)=0$, $MSE(T)=Var(T)$

### Last Class- Mean square error example

$X_{1}, \dots, X_{n} \stackrel{i.i.d}{\sim} Poisson(\mu)$

Two candidate estimators for $p_{0}=P(X_{i}=0)=e^{-\mu}$:
* $\widetilde{p}_{0}=\frac{\text{number of } X_{i}=0}{n}$
* $\widehat{p}_{0}=e^{-\overline{X_{n}}}$

$\widetilde{p}_{0}$ is unbiased but $\widehat{p}_{0}$ is not? Which one is better?

### Last Class - Mean square error example

Simulation to see how the two estimators behave

* True $p_{0}=e^{-2} \approx 0.135$

<img src="Lecture 10.assets/Screenshot 2025-11-30 at 10.52.13 PM.png" alt="Screenshot 2025-11-30 at 10.52.13 PM" style="zoom:50%;" />

### Last Class - Mean square error example

<img src="Lecture 10.assets/Screenshot 2025-11-30 at 10.52.42 PM.png" alt="Screenshot 2025-11-30 at 10.52.42 PM" style="zoom:50%;" />

### Maximum likelihood estimation

Previous examples of estimators were sample analogs of population parameters (e.g. sample mean and sample variance) or intuitive (e.g. estimator based on $\max\{X_{1}, \dots, X_{n}\}$ for $U[0, \theta]$)

Maximum likelihood provides a very general way to construct estimators with good properties. The idea is intuitive:

* Choose as the estimator the value of $\theta$ that **maximizes the chances to produce the observed data.**

Example: An infusion pump is a medical device that delivers fluids - typically medications, nutrients, or saline - into a patient's body in controlled amounts over time. We track time to failure (in hours) for five identical infusion pumps used in a hospital.

* Observed data in hours: $120, 85, 200, 60, 150$
* Assuming independent and identically distributed lifetimes following an **$Exponential(\lambda)$ model.**
* Compute the maximum likelihood estimate of $\lambda$.

### MLE - exponential example

Data: $t_{1}=120$, $t_{2}=85$, $t_{3}=200$, $t_{4}=60$, $t_{5}=150$

Model: i.i.d data with density $f(t|\lambda)=\lambda e^{-\lambda t}$

Likelihood:

$$L(\lambda)=\prod_{i=1}^{5}\lambda e^{-\lambda T_{i}}$$
$$=(\lambda e^{-\lambda\cdot120})(\lambda e^{-\lambda\cdot85})(\lambda e^{-\lambda\cdot200})(\lambda e^{-\lambda\cdot60})(\lambda e^{-\lambda\cdot150})$$
$$=\lambda^{5}exp[-\lambda(120+85+200+60+150)]=\lambda^{5}exp(-615\lambda)$$

log-likelihood:

$$l(\lambda)=log~L(\lambda)=5~log~\lambda-615~\lambda$$

### MLE - exponential example

Setting the score to zero to find the candidate maxima of the log-likelihood:

$$\frac{dl}{d\lambda}=\frac{5}{\lambda}-615$$

$$\frac{5}{\lambda}-615=0\Rightarrow\hat{\lambda}=\frac{5}{615}=0.00813$$

Checking $2^{nd}$ derivative:

$$\frac{d^{2}l}{d\lambda^{2}}=-\frac{5}{\lambda^{2}}<0$$

### Maximum likelihood estimation – exponential example

<img src="Lecture 10.assets/Screenshot 2025-11-30 at 10.55.34 PM.png" alt="Screenshot 2025-11-30 at 10.55.34 PM" style="zoom:50%;" />

### Maximum likelihood estimation - exponential example

Let $T_{1}, \dots, T_{n} \stackrel{i.i.d}{\sim} Exp(\lambda)$ with density $f(t;\lambda)=\lambda e^{-\lambda t}$ for $t>0$. The likelihood and log-likelihood are

$$L(\lambda)=\prod_{i=1}^{n}\lambda e^{-\lambda T_{i}}=\lambda^{n}exp\left(-\lambda\sum_{i=1}^{n}T_{i}\right)$$

$$l(\lambda)=\log L(\lambda)=n\log\lambda-\lambda\sum_{i=1}^{n}T_{i}$$

Differentiate and set to zero:

$$\frac{dl}{d\lambda}=\frac{n}{\lambda}-\sum_{i=1}^{n}T_{i}=0 \Rightarrow \hat{\lambda}=\frac{n}{\sum_{i=1}^{n}T_{i}}$$

### MLE - a more complex example Number of cycles until pregnancy:

Number of cycles until pregnancy:

<img src="Lecture 10.assets/Screenshot 2025-11-30 at 10.56.42 PM.png" alt="Screenshot 2025-11-30 at 10.56.42 PM" style="zoom:50%;" />

### MLE - a more complex example

* Want to estimate $p=P(X=1)$, where $X_{i}$ is the number of cycles up to pregnancy among the $i^{th}$ smoker
* We know that $S=\frac{\text{number of } X_{i}=1}{n}$ is an unbiased estimator for $p$
* This yields the estimate $\widetilde{p}=\frac{29}{100}=0.29$
* But it uses only a fraction of the data discarding the rest. Maybe there is a better estimator using all the data?

### MLE - a more complex example

* Let $X_{i}$ denote the number of cycles up to pregnancy for the $i^{th}$ smoker. We can assume the $X_{i} \sim Geometric(p)$, and the $X_{i}$ are independent. There are 415 smokers

* The probability of observing the data in the first row of the table is then given by:

  $$L(p)=P(X_{1}=x_{1}|p)\times P(X_{2}=x_{2}|p)\times\dots P(X_{100}=x_{100}|p)$$

  $$=p^{29}\cdot(p(1-p))^{16}\dots((1-p)^{11}p)^{3}\cdot((1-p)^{12})^{7}$$

  $$=p^{93}(1-p)^{322}$$

* We want to find $0\le p\le1$ that makes $L(p)$ as large as possible, i.e. find the value of $p$ that maximizes $L(p)$
* Equivalent to finding the maximizer of $l(p)=\log(L(p))$

### MLE - a more complex example

<img src="Lecture 10.assets/Screenshot 2025-11-30 at 10.59.55 PM.png" alt="Screenshot 2025-11-30 at 10.59.55 PM" style="zoom:50%;" />

$$l(p)=93\log(p)+322\log(1-p)$$

$$0=l^{\prime}(p)=\frac{93}{p}-\frac{322}{1-p}\iff p=\frac{93}{415}$$

$$\hat{p}=\frac{93}{415}=0.224$$ is called the maximum likelihood estimate of $p$.

### Maximum likelihood estimation

* The **maximum likelihood estimate** of $\theta$ is the value $\hat{\theta}=\hat{\theta}(x_{1}, x_{2}, \dots, x_{n})$ that maximizes the log-likelihood function $l(\theta)$.
* The corresponding random variable $\hat{\theta}=\hat{\theta}(X_{1}, X_{2}, \dots, X_{n})$ is called the **maximum likelihood estimator** of $\theta$.
* (We often use the same notation, $\hat{\theta}$ for both the estimate and the estimator. We understand which one we are referring to based on context)

### MLE with no analytical solution

Dataset: $x_{1}, \dots, x_{n}$ modeled as a realization of random variables $X_{1}, \dots, X_{n}.$

Where the pdf of $X_{i}$ is a mixture of exponentials:

$X_{i} \sim Exp(\lambda)$ with probability $\frac{1}{2}$ and $Exp(2\lambda)$ with probability $\frac{1}{2}$

$$f(x)=\frac{1}{2}\lambda e^{-\lambda x}+\frac{1}{2}2\lambda e^{-2\lambda x}$$

<img src="Lecture 10.assets/Screenshot 2025-11-30 at 11.01.00 PM.png" alt="Screenshot 2025-11-30 at 11.01.00 PM" style="zoom:50%;" />

### MLE with no analytical solution

```r
set.seed(101)
n = 50

rate = 1
mix = rbinom(n=n, size=1, prob=1/2)
dataset = mix*rexp(n, rate=rate) + (1-mix)*rexp(n, rate=2*rate)

negloglik = function(x, data) {
    -sum(log(0.5*dexp(data, rate=x) + 0.5*dexp(data, rate=2*x)))
}

optimize(f=negloglik, interval=c(0.01, 10), data=dataset)

## $minimum
## [1] 1.37906

## $objective
## [1] 19.78651
```

### MLE with no analytical solution

<img src="Lecture 10.assets/Screenshot 2025-11-30 at 11.01.00 PM.png" alt="Screenshot 2025-11-30 at 11.01.00 PM" style="zoom:50%;" />

### Properties of Maximum likelihood estimators

The maximum likelihood estimator (MLE) is **consistent**:
$$\hat{\theta}_{n} \stackrel{P}{\longrightarrow} \theta \text{ as } n\rightarrow+\infty.$$

* i.e. as the sample size gets larger the MLE gets closer and closer to the true parameter $\theta$.
* Consistency is much stronger that asymptotic unbiasedness.

**Invariance:**

* If $\hat{\theta}$ is the MLE of $\theta$ then $g(\hat{\theta})$ is the MLE of $g(\theta)$.

**Asymptotic minimum variance**

* No other consistent estimator has lower asymptotic mean squared error.

**Asymptotic normality**
* In most situations of interest (but not always, e.g. $U[0, \theta]$) the sampling distribution of the MLE gets closer and closer to a **normal distribution** as $n\rightarrow\infty$.

With few exceptions MLE's are generally **biased estimators**.

### Asymptotic variance of the MLE

Let $X_{1}, \dots, X_{n} \sim f(x;\theta)$ and the log-likelihood function: $l(\theta)=\sum_{i=1}^{n}\log f(X_{i};\theta)$

The **Fisher's information** of $\theta$ (for one sample) is defined as:

$$
I(\theta)=-E\left[\frac{\partial^{2}l(\theta,X)}{\partial\theta^{2}}\right]
$$

If $f(x;\theta)$ is 'well behaved' (e.g. its support does not depend on $\theta$)


$$
\sqrt{n}(\hat{\theta}-\theta) \stackrel{d}{\longrightarrow} N\left(0, \frac{1}{I(\theta)}\right)
$$

* $\frac{1}{nI(\theta)}$ is the asymptotic variance of $\hat{\theta}$

The standard error of the MLE is $se(\hat{\theta})=\frac{1}{\sqrt{nI(\theta)}}$

We can estimate the standard error of the MLE by $\widehat{se}(\hat{\theta})=\frac{1}{\sqrt{nI(\hat{\theta})}}$



# Week 11 – Confidence Intervals

### Last Class - Maximum Likelihood

Maximum likelihood is a general method for estimating parameters of interest

Idea: choose parameter the maximizes the probability of observing the data actually observed

* The probability of observing the data actually observed as a function of parameter = **likelihood**
* Previous examples of estimators were sample analogs of population parameters (e.g. sample mean and sample variance) or intuitive (e.g. estimator based on $\max_{1\le i\le n}X_{i}$ for $U[0,\theta]$)

Maximum likelihood can be used in cases when there is no 'natural' estimator like sample mean or variance

### Maximum likelihood estimation

* The **maximum likelihood estimate** of $\theta$ is the value $\hat{\theta}=\hat{\theta}(x_{1},x_{2}, \dots, x_{n})$ that maximizes the log-likelihood function $l(\theta)$.
* The corresponding random variable $\hat{\theta}=\hat{\theta}(X_{1},X_{2}, \dots, X_{n})$ is called the **maximum likelihood estimator** of $\theta$.
* (We often use the same notation, $\hat{\theta}$ for both the estimate and the estimator. We understand which one we are referring to based on context)

### Properties of Maximum likelihood estimators

The **maximum likelihood estimator (MLE) is consistent**:
$$\hat{\theta}_{n}\rightarrow\theta \text{ as } n\rightarrow+\infty$$

* i.e. as the sample size gets larger the MLE gets closer and closer to the true parameter $\theta$.
* Consistency is **stronger than asymptotic unbiasedness** (which MLEs also have)

**Invariance**:
* If $\hat{\theta}$ is the MLE of $\theta$ then $g(\hat{\theta})$ is the MLE of $g(\theta)$.
* E.g. MLE of $\theta^{2}$ is $\hat{\theta}^{2}$

**Asymptotic minimum variance**
* Lowest asymptotic mean squared error.

**Asymptotic normality**
* The distribution of the MLE gets closer and closer to a **normal distribution** as $n\rightarrow\infty$.

* MLE's are generally **biased estimators** - But bias disappears as sample size increases (asymptotically unbiased).

### Asymptotic variance of the MLE

Let $X_{1}, \dots, X_{n}\sim f(x;\theta)$ and the log-likelihood function: $l(\theta)=\sum_{i=1}^{n}\log f(X_{i};\theta)$

The **Fisher's information** of $\theta$ (for one sample) is defined as:

$$
I(\theta)=-E\left[\frac{\partial^{2}l(\theta,X)}{\partial\theta^{2}}\right]
$$

If $f(x;\theta)$ is 'well behaved' (e.g. its support does not depend on $\theta$):
$$
\sqrt{n}(\hat{\theta}-\theta) \stackrel{d}{\longrightarrow} N\left(0, \frac{1}{I(\theta)}\right)
$$
* $\frac{1}{nI(\theta)}$ is the asymptotic variance of $\hat{\theta}$


The standard error of the MLE is $se(\hat{\theta})=\frac{1}{\sqrt{nI(\theta)}}$

We can estimate the standard error of the MLE by $\widehat{se}(\hat{\theta})=\frac{1}{\sqrt{nI(\hat{\theta})}}$

### Confidence intervals

So far we've considered what are called **point estimators**.

* A point estimator by itself not that useful; need some measure of how variable the estimator is
* To supplement point estimators with information about their variability we can also report their SD, called the **standard error (SE)**
* A better option is to report a whole interval of plausible values for the parameter of interest, i.e. a **confidence interval**.

Based on Chebysheb's inequality, if $T$ is an estimator for $\theta$, and $\sigma_{T}$ is the standard deviation of $T$:

$$P(|T-\theta|\ge2\sigma_{T})\le\frac{3}{4}$$

$$P(\theta\in(T-2\sigma_{T},T+2\sigma_{T}))\ge\frac{3}{4}$$

$(T-2\sigma_{T},T+2\sigma_{T})$ is an **interval estimator** for $\theta$

### Confidence intervals

* Dataset $x_{1}, \dots, x_{n}$ modeled as a realization of random variables $X_{1}, \dots, X_{n}.$
* $\theta$ the parameter of interest (e.g. mean, variance, probability, etc.), and $0<\alpha<1$
* A $(1-\alpha)$-level interval estimator for $\theta$ is a a pair of sample statistics $L_{n}=g(X_{1}, \dots, X_{n})$ and $U_{n}=h(X_{1}, \dots, X_{n})$ such that:
  * $$P(L_{n}<\theta<U_{n})=1-\alpha \text{ for every value of } \theta$$


* The interval $(l_{n}, u_{n})$ where $l_{n}=g(x_{1}, \dots, x_{n})$ and $u_{n}=h(x_{1}, \dots, x_{n}),$ is called a $100(1-\alpha)\%$ **confidence interval** for $\theta$.
* The number $\alpha$ is called the **confidence level**.
* Often, we only require $P(L_{n}<\theta<U_{n})>1-\alpha$ or $P(L_{n}<\theta<U_{n})\approx1-\alpha$
  * These are **conservative** and **approximate** interval estimators respectively

### Interval estimator for the normal mean - variance known

$X_{1}, \dots, X_{n} \stackrel{i.i.d}{\sim} N(\mu, \sigma^{2})$, with $\sigma^{2}$ known. We want to construct an interval estimator for $\mu$.

* $\overline{X_{n}}$ is an unbiased estimator for $\mu$. It is also consistent and it's the MLE (with all its properties)
* We know that $\frac{\overline{X_{n}}-\mu}{\sigma/\sqrt{n}}\sim N(0,1)$
* Then, $$P\left(-z_{\alpha/2}\le\frac{\overline{X_{n}}-\mu}{\sigma/\sqrt{n}}\le z_{\alpha/2}\right)=1-\alpha$$
* Equivalently, $$P\left(\mu\in\left(\overline{X_{n}}-z_{\alpha/2}\frac{\sigma}{\sqrt{n}},\overline{X_{n}}+z_{\alpha/2}\frac{\sigma}{\sqrt{n}}\right)\right)=1-\alpha$$
* $\left(\overline{x_{n}}-z_{\alpha/2}\frac{\sigma}{\sqrt{n}},\overline{x_{n}}+z_{\alpha/2}\frac{\sigma}{\sqrt{n}}\right)$ is a $100(1-\alpha)\%$ confidence interval for $\mu$
* Common confidence levels are $95\%$ and $99\%$

### Interval estimator for the normal mean - variance known

One hundred $95\%$ confidence intervals for $\mu=7.7$

<img src="Lecture 11.assets/Screenshot 2025-11-30 at 11.12.41 PM.png" alt="Screenshot 2025-11-30 at 11.12.41 PM" style="zoom:50%;" />

### Confidence interval for the normal mean - variance unknown

$X_{1}, \dots, X_{n} \stackrel{i.i.d}{\sim} N(\mu, \sigma^{2})$ with $\sigma^{2}$ unknown. We want an interval estimator for $\mu$.

* In most situations the $\sigma^{2}$ is not known, so we cannot use the interval estimator above
* Idea: estimate $\sigma^{2}$ by the sample variance $S_{n}^{2}$ (and $\sigma$ by $S_{n}$)
* $\frac{\overline{X_{n}}-\mu}{S_{n}/\sqrt{n}}$ is not normal; it has a **t-distribution $n-1$ degrees of freedom**, $t(n-1)$
* The pdf of a $t(n)$ distribution is $$f(x)=k_{n}\left(1+\frac{x^{2}}{n}\right)^{-\frac{n+1}{2}}$$ for $-\infty<x<+\infty$, where $k_{n}$ is a constant.

### t-distribution

<img src="Lecture 11.assets/Screenshot 2025-11-30 at 11.13.16 PM.png" alt="Screenshot 2025-11-30 at 11.13.16 PM" style="zoom:50%;" />

### Confidence interval for the normal mean - variance unknown

We know that $\frac{\overline{X_{n}}-\mu}{S_{n}/\sqrt{n}}\sim t(n-1)$

So, $$P\left(\mu\in\left(\overline{X_{n}}-t_{n-1,\alpha/2}\frac{S_{n}}{\sqrt{n}},\overline{X_{n}}+t_{n-1,\alpha/2}\frac{S_{n}}{\sqrt{n}}\right)\right)=1-\alpha$$

$$\left(\overline{x_{n}}-t_{n-1,\alpha/2}\frac{S_{n}}{\sqrt{n}},\overline{x_{n}}+t_{n-1,\alpha/2}\frac{S_{n}}{\sqrt{n}}\right) \text{ is a } 100(1-\alpha)\% \text{ confidence interval for } \mu$$

### Asymptotic interval estimator for the mean

$X_{1}, \dots, X_{n} \stackrel{i.i.d}{\sim} F$ with $E[X_{i}]=\mu$. We want an interval estimator for $\mu$.

* Now we don't know the distribution of $X_{i}$ (it could be normal or anything else)
* The CLT states that: $\frac{\sqrt{n}(\overline{X_{n}}-\mu)}{\sigma}\stackrel{D}{\longrightarrow} N(0,1)$
* A variant of the CLT applies if we replace $\sigma$ with the estimate $S_{n}$: $\frac{\sqrt{n}(\overline{X_{n}}-\mu)}{S_{n}}\stackrel{D}{\longrightarrow} N(0,1)$
* So, $$P\left(\mu\in\left(\overline{X_{n}}-z_{\alpha/2}\frac{S_{n}}{\sqrt{n}},\overline{X_{n}}+z_{\alpha/2}\frac{S_{n}}{\sqrt{n}}\right)\right)\approx1-\alpha$$
* $\left(\overline{X_{n}}-z_{\alpha/2}\frac{S_{n}}{\sqrt{n}},\overline{X_{n}}+z_{\alpha/2}\frac{S_{n}}{\sqrt{n}}\right)$ is an **approximate** $100(1-\alpha)\%$ interval estimator for $\mu$

### Confidence interval for the mean - example

Let $x_{1}, \dots, x_{n}$ be a dataset modeled as a realization of i.i.d random variables $X_{1}, \dots, X_{n}$ with $E[X_{i}] = \mu$

Which interval for $\mu$ would you choose in each of these scenarios?

* $X_{i} \sim N(\mu, 2)$
* $X_{i} \sim N(\mu, \sigma^{2})$
* $X_{i} \sim F$

### Confidence interval for a proportion

$X_{1}, \dots, X_{n} \stackrel{i.i.d}{\sim} Bernoulli(p)$ or equivalently $X=X_{1}+\dots+X_{n} \sim Binomial(n,p)$

* $\hat{p}=\overline{X_{n}}=\frac{X}{n}$ is the MLE of $p$
* $Var(\hat{p})=\frac{p(1-p)}{n}$; $SD(\hat{p})=\sqrt{\frac{p(1-p)}{n}}$
* A natural estimator of $SD(\hat{p})$ is $\hat{se}(\hat{p})=\sqrt{\frac{\hat{p}(1-\hat{p})}{n}}$; standard error of $\hat{p}$
* By the CLT we have $$\frac{\sqrt{n}(\hat{p}-p)}{\sqrt{p(1-p)}}\approx N(0,1)$$
* By a variant of the CLT we have $$\frac{\sqrt{n}(\hat{p}-p)}{\sqrt{\hat{p}(1-\hat{p})}}\approx N(0,1)$$
* So, $$\left(\hat{p}-z_{\alpha/2}\sqrt{\frac{\hat{p}(1-\hat{p})}{n}},\hat{p}+z_{\alpha/2}\sqrt{\frac{\hat{p}(1-\hat{p})}{n}}\right)$$ is an approximate $100(1-\alpha)\%$ interval estimator for $p$
* Can also write as: $(\hat{p}-z_{\alpha/2}\hat{se}(\hat{p}), \hat{p}+z_{\alpha/2}\hat{se}(\hat{p}))$

### Confidence interval for a proportion

Example: $n=1,000$ poll showed that 557 voters intend to vote for candidate A and 443 for candidate B.

$p$ proportion of all voters that intend to vote for A
$\hat{p}=557/1000=0.557=55.7\%$

$\hat{se}(\hat{p})=\sqrt{\frac{\hat{p}(1-\hat{p})}{n}}=\sqrt{0.557(1-0.557)/1000)}=0.0157$

$95\% \text{ CI for } p$: $(\hat{p}-1.96\times\hat{se}(\hat{p}), \hat{p}+1.96\times\hat{se}(\hat{p}))=(0.526,0.588)$

Margin of error $=1.96\times\hat{se}(\hat{p})=0.03$

"This poll is accurate to plus or minus $3\%$ points 19 times out of 20"

### Asymptotic variance of the MLE

Let $X_{1}, \dots, X_{n} \sim f(x;\theta)$ and the log-likelihood function: $l(\theta)=\sum_{i=1}^{n}\log f(X_{i};\theta)$

The **Fisher's information** of $\theta$ (for one observation) is defined as:
$$I_{1}(\theta)=-E\left[\frac{\partial^{2}l_{1}(\theta,X)}{\partial\theta^{2}}\right]$$

where $l_{1}(\theta)=\log f(X;\theta)$ is the log-likelihood for one observation

If $f(x;\theta)$ is 'well behaved' (e.g. its support does not depend on $\theta$)

* $$\sqrt{n}(\hat{\theta}-\theta) \stackrel{d}{\longrightarrow} N\left(0, \frac{1}{I_{1}(\theta)}\right)$$
* $\frac{1}{nI_{1}(\theta)}$ is the asymptotic variance of $\hat{\theta}$
* The standard error of the MLE is $se(\hat{\theta})=\frac{1}{\sqrt{nI_{1}(\theta)}}$
* We can estimate the standard error of the MLE by $\widehat{se}(\hat{\theta})=\frac{1}{\sqrt{nI_{1}(\hat{\theta})}}$

### Asymptotic confidence intervals based on MLES

Estimate of the standard error (i.e. $sd(\hat{\theta}))$:
$$\hat{se}(\hat{\theta})=\frac{1}{\sqrt{nI_{1}(\hat{\theta})}}$$

Based on the asymptotic normality of the MLE an approximate $100(1-\alpha)\%$ confidence interval can be computed as:
$$\left(\hat{\theta}-z_{\alpha/2}\hat{se}(\hat{\theta}), \hat{\theta}+z_{\alpha/2}\hat{se}(\hat{\theta})\right)=\left(\hat{\theta}-\frac{z_{\alpha/2}}{\sqrt{nI_{1}(\hat{\theta})}}, \hat{\theta}+\frac{z_{\alpha/2}}{\sqrt{nI_{1}(\hat{\theta})}}\right)$$

### Asymptotic confidence intervals based on MLES

Example: $X_{1}, \dots, X_{n} \sim Geometric(p)$; $P(X=x)=p(1-p)^{x-1}$

$$L(p)=\prod_{i=1}^{n}p(1-p)^{x_{i}-1}=p^{n}(1-p)^{\sum_{i=1}^{n}X_{i}-n}$$

$$l(p)=n\log(p)+\left(\sum_{i=1}^{n}X_{i}-n\right)\log(1-p)$$

$$l^{\prime}(p)=\frac{n}{p}-\frac{\sum_{i=1}^{n}X_{i}-n}{1-p}=0 \implies p=\frac{n}{\sum_{i=1}^{n}X_{i}}=\frac{1}{\overline{X}_{n}}$$

So, MLE of $p$ is $\hat{p}=\frac{1}{\overline{X}_{n}}$

### Asymptotic confidence intervals based on MLES

```r
set.seed(1909)
nsims = 100; n = 70; p = 0.3
p_hat = replicate(nsims, {X = rgeom(n, p) + 1; 1/mean(X)})
```

<img src="Lecture 11.assets/Screenshot 2025-11-30 at 11.17.12 PM.png" alt="Screenshot 2025-11-30 at 11.17.12 PM" style="zoom:50%;" />

### Asymptotic confidence intervals based on MLEs

$l_{1}^{\prime\prime}(p) = -\frac{1}{p^{2}} - \frac{X-1}{(1-p)^{2}}$ ($l_{1}(p)$ is log-likelihood for a single observation $X$)

Fisher information for one observation:
$$I_{1}(p) = -E[l_{1}^{\prime\prime}(p)] = \frac{1}{p^{2}} + \frac{\frac{1}{p}-1}{(1-p)^{2}} = \frac{1}{p^{2}(1-p)}$$

$$se(\widehat{p}) = \sqrt{(nI_{1}(p))^{-1}} = \frac{p\sqrt{1-p}}{\sqrt{n}}$$

$$\widehat{se}(\widehat{p}) = \frac{\widehat{p}\sqrt{1-\widehat{p}}}{\sqrt{n}}$$

$$\left( \widehat{p} - z_{\alpha/2}\frac{\widehat{p}\sqrt{1-\widehat{p}}}{\sqrt{n}}, \widehat{p} + z_{\alpha/2}\frac{\widehat{p}\sqrt{1-\widehat{p}}}{\sqrt{n}} \right)$$

### Asymptotic confidence intervals based on MLEs

Example $X_{1}, \dots, X_{70} \sim Geometric(p), \overline{X} = 3.714$

$\widehat{p} = 0.269$

$$\widehat{se}(\widehat{p}) = \frac{\widehat{p}\sqrt{1-\widehat{p}}}{\sqrt{70}} = 0.0275$$

$$\left( \widehat{p} - z_{\alpha/2}\widehat{se}(\widehat{p}), \widehat{p} + z_{\alpha/2}\widehat{se}(\widehat{p}) \right) =$$

$$= (0.269 - 1.96 \times 0.0275, \quad 0.269 + 1.96 \times 0.0275) = (0.220, 0.318)$$