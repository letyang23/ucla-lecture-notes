# 10/9 Lecture 4

##### Announcements

- Quiz 1 next Wednesday, Practice Quiz on gradescope
  - Monday's lecture won't be in quiz.
  - Closed book. Bring 1 sided note, handwritten, calculator.
  - 5% of the grade (2 quiz).
- GCP free credit
- Project planning report dues next Wednesday, 11:59pm
  - Finalize your team. If your own project, write out the description.

---

##### What we have learned so far

- Word embeddings
  - `Word2vec, PPMI, word-word, word-document`

- Language models
  - `Feedforward Language Model`
  - `N-Gram Language Model`

- What’s the similarities and differences of the two?

- Similarities:
  - Both are backed up by the distributional semantics theory `meaning of the word decided by the neighbors`
  - Both can be learned by statistical methods (count and divide) and neural networks
  - Both learn word representations
- Differences
  - Word embeddings `the goal is to` learns “semantic representation” (vectors) for words
  - Language models estimate probabilities of sentences (and generate sentences)
    - `P(w,...,w_n) =pi P(wi|w_1...i-1)`

##### How about Long-Term Dependencies?

`n-gram model model n words. feedforward language model is neuralized version of n-gram`

- What does it mean by “long-term dependency” in language modeling?Consider an example
  - Kevin's eye was caught by one number that was highlighted in the last report; this number represented the new algorithm's ability to create lengthy and coherent text on its own. This is unprecedented. The text contained more than 500 words, but the algorithm had generated many more than that – several thousands in fact. Kevin opened up two other files that contained several thousand words of AI generated text each. ...[52 words]... 
    Kevin rubbed his hands together in ___
    - `excitement. Because the word "unprecedented"`
    - `we want AI read an entire document now to be able to do sth.`
    - `both n-gram and feedforward are fall short on this long text modeling ability.`
    - `n-gram at most go for 8/9 gram`

### Outline

- Recurrent Neural Networks (RNNs)

- Long Short-Term Memory Network (LSTMs)
- RNNs/LSTMs for Language Modeling
- Decoding Algorithms

##### Rcall Feedforward Neural language model

<img src="Week 2.assets/Screenshot 2024-10-13 at 8.20.02 PM.png" alt="Screenshot 2024-10-13 at 8.20.02 PM" style="zoom:50%;" />

#### Recurrent Neural Networks (RNNs)

- Main idea: make use of ***sequential*** information

- How RNN is different from feedforward neural network?

  - Feedforward neural networks assume all inputs are ***independent*** of each other
  - Feedforward neural networks look at a fixed context window
  - In many cases (especially for language), these are not idea

- What does RNNs do?

  - Perform **the same computation** at every step of a sequence (that’s what **recurrent** stands for)

  - Inputs to the next step depend on previous computations

- Another way of interpretation – RNNs have a “**memory**”
  - To store previous computations

#### Recurrent Neural Networks (RNNs)

<img src="Week 2.assets/Screenshot 2024-10-13 at 8.25.13 PM.png" alt="Screenshot 2024-10-13 at 8.25.13 PM" style="zoom:50%;" />

`parameters: v,u,w`

<img src="Week 2.assets/Screenshot 2024-10-13 at 8.25.29 PM.png" alt="Screenshot 2024-10-13 at 8.25.29 PM" style="zoom:50%;" />

`arrow denotes parameters, nodes represents variables, either input/output/hidden state.`

<img src="Week 2.assets/Screenshot 2024-10-13 at 8.33.17 PM.png" alt="Screenshot 2024-10-13 at 8.33.17 PM" style="zoom:50%;" />

- Mathematically, the computation at each time step:

<img src="Week 2.assets/Screenshot 2024-10-13 at 8.35.01 PM.png" alt="Screenshot 2024-10-13 at 8.35.01 PM" style="zoom:50%;" />

`Linear -> non linear activation -> Linear -> Non linear activation (softmax)` 

`softmax to normalize`

`recurrence happen on h`

##### Problem of Long-Term Dependencies

- What if we want to predict the next word in a <u>long sentence</u>?

- Do we know which <u>past information</u> is helpful to predict the next <u>word</u>?

- In theory, RNNs are capable of handling <u>long-term dependencies.</u>

- But in practice, <u>they are not!</u> Reading: [vanishing gradient problem](https://en.wikipedia.org/wiki/Vanishing_gradient_problem).

<img src="Week 2.assets/image-20241013212120043.png" alt="image-20241013212120043" style="zoom:50%;" />

### Long Short Term Memory (LSTM)

- A ***special type*** of recurrent neural networks.

- Explicitly designed to capture the **long-term dependency**.

- It solves/mitigates the vanishing gradient problem of vanilla RNN.

- So, what is the **structural difference** between RNN and LSTM?

##### Difference between RNN and LSTM

<img src="Week 2.assets/image-20241013212547332.png" alt="image-20241013212547332" style="zoom:50%;" />

`For RNN is very simple, just tanh activation`

`For LSTM, there are much more parameters and activations.`

#### Core Idea Behind LSTM

- Key to LSTMs is the **memory cell state**

- LSTMs memory cells **add** and **remove** information as the sequence goes. Mathematically, it turns the cascading ***multiplications*** in vanilla RNNs into ***additions***. 

- How? Through a structure called **gate**.

- LSTM has **three gates** to **control** the memory in the cells
  - `Input gate, forget gate, and output gate`

<img src="Week 2.assets/image-20241013213017753.png" alt="image-20241013213017753" style="zoom:50%;" />

#### Step-by-Step LSTM Walk Through

- The **input gate decides** what information will be taken from *the current input* and stored in the cell state

- Two parts – 

  - A **sigmoid** layer (**input gate layer**): decides what values we’ll update

  - A **tanh⁡** layer: creates a vector of new candidate values, $\tilde{C_t}$

- **Example**: add the gender of the new subject to the cell state

  - Replace the old one we’re forgetting

<img src="Week 2.assets/Screenshot 2024-10-13 at 9.33.58 PM.png" alt="Screenshot 2024-10-13 at 9.33.58 PM" style="zoom:50%;" />

`Input: X_t`

`The gate itself is a linear combination of current input and the previous hidden state.`

`i this gate will be a vector of 0 to 1.`

`C_t is a temporary, intermediate variable.`

`we apply the same linear transformation to get the C.`

- The forget gate decides what information will be thrown away

- A **sigmoid** layer decides what values we’ll forget

  - Looks at $h_{t-1}$ and $x_t$ and outputs a vector of numbers between 0 and 1

  - 1 represents **completely keep this**, 0 represents **completely get rid of this**

- **Example**: forget the gender of the old subject, when we see a new subject

<img src="Week 2.assets/image-20241013214337467.png" alt="image-20241013214337467" style="zoom:50%;" />

- **Next step**: update old state by $C_{t-1}$ into the new cell state $C_t$
- Multiply old state by $f_t$
  - Forgetting the things we decided to forget earlier
- Then we add $i_t*\tilde{C_t}$
  - Adding in new information

<img src="Week 2.assets/image-20241013215256281.png" alt="image-20241013215256281" style="zoom:50%;" />

- **Final step**: decide what we’re going to output
- First, we compute an **output gate**.
  - Which decides what parts of the cell state we’re going to output
- Then, we put the cell state through **tanh** and multiply it by the output of the sigmoid gate

<img src="Week 2.assets/image-20241013215729456.png" alt="image-20241013215729456" style="zoom:50%;" />

#### Putting Everything Together

<img src="Week 2.assets/image-20241013215911401.png" alt="image-20241013215911401" style="zoom:50%;" />

#### LSTMs Summary

- LSTMs is an (advanced) variation of RNNs.
- It captures long-term dependencies of the inputs.
- Shown to be efficient in many NLP tasks. 
- A standard component to encode text inputs during 2014 - 2018.

### RNN/LSTM Language Models

<img src="Week 2.assets/image-20241013220404228.png" alt="image-20241013220404228" style="zoom:50%;" />

##### Training a RNN Language Model

<img src="Week 2.assets/image-20241013220728373.png" alt="image-20241013220728373" style="zoom:50%;" />

`negative log prob of "student" -> "open" -> "their" -> "exams"`

#### Training an RNN Language Model

- Get a corpus of text which contains a sequence of words $w_1,...,w_t$ 
- Feed the sequence into an RNN, compute output distribution $\hat{w_t}$ **for every step t.**
  - i.e., predict the probability distribution for every next word, given all previous context words
- Negative log-likelihood of the target word, or cross-entropy loss at each step
  - $L(θ) = - log P(wt|w_{1:t-1} ; θ)$
- Average each step’s loss to get the loss for the entire training set.

#### Learning neural language models

- **Maximize the log-likelihood (minimize negative log-likelihood)** of observed data, w.r.t. parameters **θ** of the neural language model

  <img src="Week 2.assets/image-20241013221148650.png" alt="image-20241013221148650" style="zoom:50%;" />

- **Parameters** **θ** (in an RNN language model):
  - Word embedding matrix **R**
  - RNN weights: **W**, **U**, **b, V**, **c** `Parameter U, V, W`
  - LSTM weights: $W^i, W^f, W^o, W^g, U^i, U^f, U^o, U^g$ (optional, $b^i, b^f, b^o, b^g$)  `Input gate, output gate, forget gate, and central memory.`

- **Gradient descent** with learning rate *η*:

  <img src="Week 2.assets/image-20241013221319876.png" alt="image-20241013221319876" style="zoom:50%;" />



# 10/14 Lecture 5 (1st half)

### Decoding algorithms for LMs

##### Decoding: selecting the word to generate at each time step

- Greedy search: select word with the highest $p(x_t |x_{1:t-1})$ given by the softmax layer

  <img src="Week 2.assets/image-20241015184328928.png" alt="image-20241015184328928" style="zoom:50%;" />

  `2 issues: 1. it always give you only one response (highest probability one). 2. It's not guaranteed to give you the best.`

- **Beam search**: explore several different hypotheses instead of just a single one

  `we don't want be that greedy, in case later there is better solution.`

  - keep track of k most probable partial translations at each decoder step instead of just one!  `instead of 1 best, take k best answers`
  - choose *k* words with the highest $p(y_i)$ at each time step.
  - k – beam size (typically 5-10)  `k^2 hypothesis`

##### Beam search decoding: example

- Beam size = 2. Showing log-likelihood:

<img src="Week 2.assets/image-20241015185111356.png" alt="image-20241015185111356" style="zoom:33%;" />

<img src="Week 2.assets/image-20241015185130859.png" alt="image-20241015185130859" style="zoom:33%;" />

​	`Since beam size = 2, we will trim down (get rid of people -2.3 and person -3.2)`

​	`P(poor|start, the) = -1.90`

`you don't do it on the joint probability, instead, you prune using P(poor|start, the) * P(the|start)`

`This is not the log probability. It's actually joint probability log P(poor|S, the) + log P(the|start) basically addition of the log probability. `

<img src="Week 2.assets/image-20241015202707550.png" alt="image-20241015202707550" style="zoom:50%;" />

`get rid of -3.12 and -3.53 (person and but)`

<img src="Week 2.assets/image-20241015202815283.png" alt="image-20241015202815283" style="zoom:50%;" />

##### Does beam search always return the most probable sequence?

- `No. Beam Search is invented to solve the problem of the greedy algorithm to not find the most powerful sequence.`
- `trade-off between the computational resources. Just a heuristic search algorithm.`

##### What are the termination conditions of beam search?

`end of sequence token`

#### What’s the effect of changing beam size k?

- Small k has similar problems to greedy decoding (k=1)
  - Unnatural, incorrect (due to errors in earlier decoding stage), generic

- Larger k means you consider more hypotheses 

- Increasing k reduces some of the problems above 
  - Larger k is more computationally expensive 
  - Increasing k can also introduce other problems
  - E.g., in open-ended tasks like chit-chat dialogue, large k can make output more generic
    - `"I don't know"`

#### Sampling-based decoding

- Pure sampling
  - at each step t, randomly sample from the probability distribution $p(x_t |x_{1:t-1})$ to obtain your next word. 
  - Like greedy decoding, but sample instead of argmax. 
- Top-k sampling 
  - at each step t, instead of randomly sampling from $p(x_t |x_{1:t-1})$, restricted to just the top-k most probable words (k = number of words)
  - Like pure sampling, but truncate the probability distribution 
  - k=1 is greedy search, k=V is pure sampling 
  - Increase k to get more diverse/risky output 
  - Decrease k to get more generic/safe output

​	`at each step, instead randomly sample one, we sample from top k`

- Top-P sampling 
  - at each step t, instead of randomly sampling from $p(x_t |x_{1:t-1})$, restricted to the most probable words up to the total probability mass of P.
  - Like top-k sampling, truncate the probability distribution, but in a different way 
  - P=1 is pure sampling 
  - Increase P to get more diverse/risky output 
  - Decrease P to get more generic/safe output

#### Decoding algorithms: summary

- **Greedy decoding** is a simple method; usually gives low quality output 
- **Beam search** (especially with large beam size) searches for high probability output 
  - Delivers better quality than greedy, but if beam size is too large, can return high-probability but unsuitable output (e.g. generic, short) 
- **Sampling methods** are a way to get more diversity and randomness 
  - Good for open-ended / creative generation (chit-chat, poetry, stories) 
  - Top-k and top-p sampling allows you to control diversity

