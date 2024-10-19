# 9/30 Lecture 1

### What is NLP

- **Wiki: Natural language processing** (**NLP**) is a field of computer science, artificial intelligence, and computational linguistics concerned with the interactions between computers and human (natural) languages.

### Go beyond the keyword matching

- Identify the structure and meaning of words, sentences, texts and conversations
- Deep understanding of broad language
- NLP is all around us

### NLP is a pretty old topic!

<img src="Lecture Notes.assets/image-20240930141912271.png" alt="image-20240930141912271" style="zoom:30%;" />

##### Google Translate

- Launched in 2006, App in 2011, WordLens 2015 (Take a picture and translate)

##### Machine Translation

- Translate language

##### Question Answering

- Watson computer wins at Jeopardy in February 2011
- Siri launched in October 2011

##### Sentiment/Opinion Analysis

- First research paper: 2002
- TwitrRatr: 2018

##### Text Classfication

##### Information Extraction

##### Conversational Assistant Systems

##### My Model Wrote A Sonnet For You!

### ChatGPT

- Let’s have a try! https://chat.openai.com/ 

- **Input**: When I found out my grandma was in the hospital I felt a particular color. When someone cut me off in traffic I felt a different color. What is the most likely color I would see if I combined these two colors?
  - `blue is sad, red is anger, combine these would be **purple**`

- **Input**: Michael is at that really famous museum in France looking at its most famous painting. However, the artist who made this painting just makes Michael think of his favorite cartoon character from his childhood. What was the country of origin of the thing that the cartoon character usually holds in his hand?
  - ChatGPT answer: 
    - Michael is likely at the Louvre in France, looking at the **Mona Lisa**, painted by Leonardo da Vinci. If Leonardo da Vinci makes Michael think of his favorite childhood cartoon character, that character is likely **Leonardo** from the **Teenage Mutant Ninja Turtles**. Leonardo, the turtle, is known for wielding **katana swords**, which are traditionally from **Japan**. Therefore, the country of origin of the thing that the cartoon character usually holds in his hand is **Japan**.

### Goals of the course

- Introduce you to NLP problems & solutions 
- Models, algorithms, and tools that are out there to solve language-related problems you want to tackle
- How to design and evaluate your own task/model/algorithm/tool
  - Using data and statistics
  - Using your own creativity
  - Using the latest advances

- At the end you should:
  - Agree that language is subtle & interesting 
  - Feel some ownership over the models/algorithms/tools
  - Understand research papers in the field

### What are the challenges?

#### Ambiguity: Favorite Headlines

- Iraqi Head Seeks Arms `Head and arms` 
- Juvenile Court to Try Shooting Defendant `try means trail`
- Teacher Strikes Idle Kids
- Stolen Painting Found by Tree `Find near the tree`
- Kids Make Nutritious Snacks `kids are nutritious snacks`
- Local High School Dropouts Cut in Half `if you drop out from high school you will be cut`

#### Part-of-Speech (POS) Tagging and Ambiguity

- “Back” can be an adjective, noun, particle, or verb.
  - The **back** *door* (adjective)
  - *On my* **back** (noun)
  - *Win the voters* **back** (particle)
  - *Promised to* **back** *the bill* (verb)

#### Named Entity Recognition (NER) and Ambiguity

- Type ambiguity
  - Example: <img src="Lecture Notes.assets/image-20240930144728140.png" alt="image-20240930144728140" style="zoom:80%;" />

#### Syntactic Parsing and Ambiguity

<img src="Lecture Notes.assets/Screenshot 2024-09-30 at 2.48.07 PM.png" alt="Screenshot 2024-09-30 at 2.48.07 PM" style="zoom:30%;" />

### Course Information

##### Levels of Language

- **Phonetics/phonology/morphology**: what words (or subwords) are we dealing with? 

  - cat, cats, dog, dogs(z), box, boxes. 

- **Semantics**: What’s the literal meaning?

  - What does a sentence mean?

    - Papa eats the caviar with a spoon.

      <img src="Lecture Notes.assets/Screenshot 2024-09-30 at 3.04.30 PM.png" alt="Screenshot 2024-09-30 at 3.04.30 PM" style="zoom:50%;" />

- **Syntax**: What phrases are we dealing with? Which words modify one another?

  ​	<img src="Lecture Notes.assets/Screenshot 2024-09-30 at 3.03.39 PM.png" alt="Screenshot 2024-09-30 at 3.03.39 PM" style="zoom:50%;" />

- **Pragmatics**: What should you conclude from the fact that I said something? How should you react?

  - What does *the speaker* mean? (context: in a stuffy room)

    <img src="Lecture Notes.assets/Screenshot 2024-09-30 at 3.05.47 PM.png" alt="Screenshot 2024-09-30 at 3.05.47 PM" style="zoom:80%;" />

    

### Course Information

- Website: https://violetpeng.github.io/cs263_fall24.html
  - Last two weeks are course project final presentation
    - Count to participation
  - Assignment 1 release on Wednesday (individual assignment)
    - Read a paper, run a demo from th paper and present it
    - We will pick out the good demo to Expo

- Participation have 10% of the grade
  - Piazza, peer review for homework and final project

- Group project, 4 people

- Two in-class quiz

  - one single-sided page of notes allowed

- Extra-credit:

  - Outstanding in-class participator and piazza receive grade bump

    

# 10/2 Lecture

Assignment 1 and project description is released today.

Sign up for paper to present, reproduce the code and write a demo

peer review and class/TA/Piazza participation

### Introduction to lexical semantics

#### How do we represent a word?

- How do we “understand” a word?

- How can we know the relation/distance/similarity between words **computationally**?

  `In number? In vector? In Graph?`

##### Representing words as discrete symbols

- Naïve way: represent words as atomic symbols: student, talk, university (BoW)

- Represent word as a **“one-hot”** vector (**独热**) 
   [ 0       0           0           1                 0  …     0 ]

  egg   student  talk  university   happy   buy   

   `egg = [1 0 0 0 0]`
  
   `student = [0 1 0 0 0]`
  
   `talk = [0 0 1 0 0]`
  
   `Insufficient and words have no connection with each other`
  
- How large is (what’s the dimension of) this vector?
  - Vector dimension = number of words in vocabulary 
    - PTB data: ~50k, 
    - Google 1T data: 13M

##### Issues

- Dimensionality is large; vector is sparse
- No similarity
  - $V_{happy}$  = [0 0 0 1 0 ... 0 ]
  - $V_{sad}$    = [0 0 1 0 0 ... 0 ]
  - $V_{milk}$   = [1 0 0 0 0 ... 0 ]
  - $V_{happy} • V_{sad}  = V_{happy} • V_{milk}$ = 0
- Cannot represent new words

##### How about unseen words/phrases

- Example: Shakespeare corpus consists of N=884,647 word tokens and a vocabulary of V=29,066 word types
- Only 30,000 word types occurred
  - Words not in the training data ⇒ no representation, 0 probability

#### What is Lexical Semantics

Word meanings that can help decide:

- Word Similarity 
  - Distributional (Vector) Models of Meaning
- Word Relations
- Word Sense Disambiguation
- Semantic Roles

##### Intuition of Semantic Similarity

| Semantically Close | Semantically Distant |
| ------------------ | -------------------- |
| bank-money         | doctor-mall          |
| apple-fruit        | painting-January     |
| tree-forest        | math-river           |
| bank-river         | apple-penguin        |
| pen-paper          | nurse-fruit          |
| run-walk           | pen-river            |
| mistake-error      | clown-rocket         |
| car-wheel          | car-algebra          |

##### Why Are Two Words Related?

- Meaning
  - Two concepts are close in terms of meaning (want-desire)
- World knowledge
  - Two concepts have similar properties, often occur together, or occur in similar contexts (pencil-pen, pen-ink, dog-cat)
- Psychology
  - We often think of the two concepts together (voting-home address, red-luck[in some culture]) 

#### Validity of Semantic Similarity

- Is semantic distance `(how far apart word meanings are)` a valid linguistic phenomenon? -> how would you approach this problem?
- Experiment (Rubenstein and Goodenough, 1965)
  - Compiled a list of word pairs
  - Subjects asked to judge semantic distance (from 0 to 4) for each pair
- Results
  - Rank correlation between subjects is ~ 0.9
  - People are **consistent**!

- What can we use semantic similarity for? (discussion)

###### Word similarity for plagiarism detection

<img src="Lecture Notes.assets/image-20241002143554129.png" alt="image-20241002143554129" style="zoom:30%;" />

`Semantic similarity will help catch plagiarism`

###### Word similarity for historical linguistics: semantic change over time

<img src="Lecture Notes.assets/image-20241002143614545.png" alt="image-20241002143614545" style="zoom:33%;" />

`From start, gay means happy and until now gay means homosexual. Use semantic similarity help help us understand the semantic change over the time`

###### Word similarity reflects gender stereotype

<img src="Lecture Notes.assets/Screenshot 2024-10-02 at 2.36.30 PM.png" alt="Screenshot 2024-10-02 at 2.36.30 PM" style="zoom:33%;" />

### Theoretical foundation of distributional semantics

- **Intuitions**: Zellig Harris (1954):
  - “oculist and eye-doctor … occur in almost the same environments”
  - “If A and B have almost identical environments we say that they are synonyms.”
- Firth (1957): 
  - “You shall know a word by the company it keeps!”

`Theory: We can know the semantic similarity with the words comes with them.`

###### Intuition for distributional word similarity

- Words that occur in the same contexts tend to have similar meanings

  <img src="Lecture Notes.assets/image-20241002143730393.png" alt="image-20241002143730393" style="zoom:33%;" />

###### More intuition for distributional word similarity

```
A bottle of tesgüino is on the table
Everybody likes tesgüino
Tesgüino makes you drunk
We make tesgüino out of corn.
```

- From context words humans can guess **tesgüino** means
  - an alcoholic beverage like **beer**
- Intuition for algorithm:
  - Two words are similar if they have similar word contexts.

### Two classes of vector representation

- Sparse vector representations
  1. Mutual-information weighted word co-occurrence matrices

- Dense vector representations:
  2. *Singular value decomposition (and Latent Semantic Analysis)*
  3. Neural-network-inspired models (skip-grams, CBOW)
  4. *Brown clusters*

##### Shared intuition

- Model the meaning of a word by “embedding” in a vector space.
- The meaning of a word is a vector of numbers
  - Vector models are also called “**embeddings**”.
  - `Not a one hot vector`
- Contrast: word meaning is represented by a vocabulary index (“word number 545”  ->  one hot vector)
  - The drawbacks of one-hot vector is discussed in the previous lecture.

#### Sparse Vector Representations

Word-document matrix

Word-word matrix

PPMI and Cosine similarity

##### Term-document matrix

- Each cell: count of term $t$ in a document $d:tf_{t,d}$ :
  - <u>Each document</u> is a *count vector* in $ℕ^v$: a column below `As You Like It [1 2 37 6] (竖排)`
  - Each word is a count vector in $ℕ^d$: a row below `Fool: [37 58 1 5] （横排）`

|         | As You Like It | Twelfth Night | Julius Caesar | Henry V |
| ------- | -------------- | ------------- | ------------- | ------- |
| battle  | 1              | 1             | 8             | 15      |
| soldier | 2              | 2             | 12            | 36      |
| fool    | 37             | 58            | 1             | 5       |
| clown   | 6              | 117           | 0             | 0       |

​	`From this matrix, we can see Battle and Soldier are closer to each other than Battle and Fool (Similarity of the words)`

- Two **documents** are similar if their vectors are similar
  - `Example: Julius Caesar [8 12 1 0]` and `Henry V [15 36 5 0]`
- Two **words** are similar if their vectors are similar
  - Example: `fool [37 58 1 5]` and `clown [6 117 0 0]`

### Measuring similarity: cosine

`cosine similarity over dot product (it's normalized!) `

- Divide the dot product by the length of the two vectors!

  <img src="Lecture Notes.assets/image-20241002144416982.png" alt="image-20241002144416982" style="zoom:33%;" />

- This turns out to be the cosine of the angle between them!

  <img src="Lecture Notes.assets/image-20241002144428145.png" alt="image-20241002144428145" style="zoom:33%;" />

### Recap: Dot Product between Vectors

- To calculate the dot product

<img src="Lecture Notes.assets/Screenshot 2024-10-02 at 2.48.08 PM.png" alt="Screenshot 2024-10-02 at 2.48.08 PM" style="zoom:50%;" />

### Cosine for computing similarity

- Recap for Cosine Similarity

<img src="Lecture Notes.assets/image-20241004184626719.png" alt="image-20241004184626719" style="zoom:50%;" />

<img src="Lecture Notes.assets/image-20241004184736504.png" alt="image-20241004184736504" style="zoom:50%;" />



###### Visualizing vectors and angles

<img src="Lecture Notes.assets/image-20241002144856197.png" alt="image-20241002144856197" style="zoom:30%;" />

`Dimension 1 is DOC1, Dimension 2 is DOC2`

##### Issues about the term-document matrix

- Document can be very long
  - Some far-away words appear in the same documents are no longer that relevant/similar.
- There are usually <u>only a small number of documents</u> 
  - The dimension of the count vector for each word is small.
  - The statistics would be less robust/reliable.

### The word-word or word-context matrix

- Instead of entire documents, use smaller contexts
  - Paragraph
  - Window of ± 4 words
- A word is now defined by a vector over counts of context words
- Instead of each vector being of length D
- Each vector is now of length $|V|$
- The word-word matrix is $|V|\times|V|$

##### Word-Word matrix Input: sample contexts ± 7 words

<img src="Lecture Notes.assets/image-20241002150804072.png" alt="image-20241002150804072" style="zoom:50%;" />

`total of 7 words before "apricot", and 7 words after "apricot"`

##### Output: word-context matrix

<img src="Lecture Notes.assets/image-20241004190911560.png" alt="image-20241004190911560" style="zoom:80%;" />

<img src="Lecture Notes.assets/Screenshot 2024-10-02 at 3.10.27 PM.png" alt="Screenshot 2024-10-02 at 3.10.27 PM" style="zoom:80%;" />

`We can represent the word by either vertical or horizontal vector`

#### Word-word matrix

- We showed only 4x6, but the real matrix is 50,000 x 50,000 `vocabulary size x vocabulary size`

  - So it’s very **sparse** -- Most values (~98%) are 0.

- The size of windows depends on your goals

  - The shorter the windows , the more **syntactic** the representation 
    - `句法关系 example: "the" and noun`
    - ± 1-3 very syntactic
    
  - The longer the windows, the more **semantic** the representation 
    - `语义关系example: "doctor" and "hospital"`
    - ± 4-10 more semantic
  
  - Even longer, you will get **topical** representations
    -  `主题关系，example: climate and change`
    - ± 10+ more topical
  

#### Problem with raw counts

- Raw word frequency is not a great measure of association between words (why)?
  - It’s very skewed
    - “the” and “of” are very frequent, but maybe not the most discriminative
    - `every word appear with "the" and "of"`
- We’d rather have a measure that asks whether a context word is **particularly informative** about the target word.
  - <u>Positive Pointwise Mutual Information (PPMI)</u>

### Pointwise Mutual Information

**Pointwise mutual information**:

​	Do events x and y co-occur more than if they were independent?

<img src="Lecture Notes.assets/image-20241002151241748.png" alt="image-20241002151241748" style="zoom:33%;" />

​	`P(x,y) = x和y一起出现的概率`

​	`P(x) and P(y) = x和y单独出现的概率`

**PMI between two words**:

​	 Do words x and y co-occur more than if they were independent? 

<img src="Lecture Notes.assets/Screenshot 2024-10-02 at 3.13.17 PM.png" alt="Screenshot 2024-10-02 at 3.13.17 PM" style="zoom:33%;" />

- What’s the range of PMI?	$-\infty$ to $+\infty$

- But the negative values are problematic
  - It’s not clear people are good at “unrelatedness”

- So we just replace negative PMI values by 0

- Positive PMI (PPMI) between word1 and word2:

<img src="Lecture Notes.assets/Screenshot 2024-10-02 at 3.15.28 PM.png" alt="Screenshot 2024-10-02 at 3.15.28 PM" style="zoom:33%;" />

###### Exercise

**Count(w,context)**

|             | computer | data | pinch | result | sugar |
| ----------- | -------- | ---- | ----- | ------ | ----- |
| apricot     | 0        | 0    | 1     | 0      | 1     |
| pineapple   | 0        | 0    | 1     | 0      | 1     |
| digital     | 2        | 1    | 0     | 1      | 0     |
| information | 1        | 6    | 0     | 4      | 0     |

<img src="Lecture Notes.assets/image-20241002151623203.png" alt="image-20241002151623203" style="zoom:33%;" />

`This is raw count`

`Total of 19 counts`

$p(w=information, c=data)$ 

=Total times information and data appeared / total counts 

$=6/19=0.32$

$p(w=information) = 11/19 = 0.58$

$p(c=data) = 7/19 = 0.37$

- Answer = $pmi(information, data) = log_2\frac{P(x,y)}{P(x) P(y)} = log_2\frac{0.32}{0.37*0.58} = 0.57$

###### Calculate for every one of them

<img src="Lecture Notes.assets/image-20241004193040284.png" alt="image-20241004193040284" style="zoom:80%;" />

#### Low-dimensional Representations

- Problem with W-W matrixes:
  - Number of basis concepts is large (high-dimensional)
  - Basis is not orthogonal 
     (i.e., not linearly independent)
- Some function words are too frequent (e.g., the, of, to) 
  - Syntax has too much impact

`We want low-dimensional and dense`

#### Bonus: Latent Semantic Analysis

- Factorization: Apply SVD (Singular Value Decomposition) to the matrix to find latent components
  - Uncovers relationships not explicit in the corpora
  - Term vectors projected to k-dim latent space

`Matrix decomposition, from word-word matrix to k-dim small matrix`

`construct original matrix when you multiply three matrix together`

<img src="Lecture Notes.assets/image-20241004193543439.png" alt="image-20241004193543439" style="zoom:80%;" />

In our case, d == n

### Dense Vector Representations

- Word2Vec

- Continuous Bag of Words (CBOW) and SkipGram

#### Word2Vec

- LSA `Latent Semantic Analysis`: a compact/low-dimensional representation of co-occurrence matrix `No longer use LSA`
- Prediction-based models: Another way to get dense vectors
  - Similar to using co-occurrence counts [Levy&Goldberg (2014), Pennington et al. (2014)]
- Easy to incorporate new words or sentences

`Use Neural Network to do the same thing`

Why is this a problem for LSA?

`When you have new documents, you have to reconstruct the matrix`

#### Word2Vec

- **Skip-gram** (Mikolov et al. 2013a) **CBOW** (Mikolov et al. 2013b)
- Train a neural network to predict neighboring words
  - Inspired by **neural net language models (will cover later in the quarter)**.
  - In doing so, <u>*learn dense embeddings for the words*</u> in the training corpus.
- Advantages:
  - Fast, easy to train
  - Available online in the **word2vec** package
  - Including sets of pretrained embeddings!

##### Skip-gram vs. Continuous bag-of-words

<img src="Lecture Notes.assets/image-20241004194838151.png" alt="image-20241004194838151" style="zoom:80%;" />

`skip-gram ends up being more popular, but the intuition is same between these two models`

##### How to represent the words?

- We want to obtain <u>*low-dimensional vector*</u> representations for the words.

  - So all $w_{(t)}s$ will be represented as vectors

  - How do we get these vectors?

    - Randomly initialize and learn from the data 

      `Randomly initialize vector representation for each of the word, and learn from the data (back propagation, gradient descendent)`

### Objective of Word2Vec (Skip-gram)

- Maximize the log likelihood (minimize the negative log likelihood) of context word $w_{t-m}, w_{t-1}, w_{t+1},..., w_{t+m}$ given center word $w_t$

  $$J(\theta) = \frac{-1}{T}\sum_{t=1} \sum_{-m\le j \le m, j\ne 0} logp(w_{t+j}|w_t)$$

  <img src="Lecture Notes.assets/image-20241004195924377.png" alt="image-20241004195924377" style="zoom:80%;" />

  <img src="Lecture Notes.assets/image-20241004195734004.png" alt="image-20241004195734004" style="zoom:67%;" />

  - m is usually 5-10
  - `inner summation is to sum the context words, outer sum is to sum the center words`

- How to model $logP(w_{t+j})|w_t$?

  $p(w_{t+j} | w_t) = \frac{exp(u_{w_{t+j}}\cdot v_{w_t}}{\sum_{w'\in V}exp(u_{w'}\cdot v_{w_t})})$ The soft max function, or normalized exponential function

  - <img src="Lecture Notes.assets/image-20241004200403849.png" alt="image-20241004200403849" style="zoom:80%;" />

- Every word has 2 vectors

  - $v_w$ : when w is the center word (also called input embeddings)

  - $u_w$: when w is the context word (also called output embeddings)

`We need to create two matrix S, with dimension V x D(or K)`

`Optimize the objective function based on the data`

Skip-gram walk through in next class

# 10/7 Lecture 3

###### Recap for the dot product

<img src="Lecture Notes.assets/image-20241007141111484.png" alt="image-20241007141111484" style="zoom:50%;" />

`highlight is wrong at the last row`

<img src="Lecture Notes.assets/image-20241007141152041.png" alt="image-20241007141152041" style="zoom:50%;" />

<img src="Lecture Notes.assets/image-20241007141226641.png" alt="image-20241007141226641" style="zoom:50%;" />

- The **mn** th element of the new matrix is the dot product of the $m^{th}$ row of the first matrix and the $n^{th}$ column of the second, and we simply do this for every combination of rows on the left and columns on the right.

<img src="Lecture Notes.assets/image-20241007141306828.png" alt="image-20241007141306828" style="zoom:50%;" />

`Looks like it calculated wrong in the first column`

### Skip-gram walk through

For sentence:

The man who passes the sentence should swing the sword.

`We have context window with +-1, center word is "passes", context window "who", "the"`

`Then we can have two training samples (passes, who), (passes, the)`

`We can create 10 examples for training word2vec (since length = 10)`

<img src="Lecture Notes.assets/quote_ned_stark.png" alt="img" style="zoom:50%;" />

<img src="Lecture Notes.assets/word2vec_skip-gram.png" alt="img" style="zoom:50%;" />

https://aegis4048.github.io/demystifying_neural_network_in_skip_gram_language_modeling

1. input layer one-hot encoded vector
2. word-embedding matrix - a.k.a "Lookup table"
3. Hidden (Projection) layer for center word (**passes**)
4. word-embedding matrix for context words (the, who)
5. Dot-product of center words with everything
6. Softmax output Layer of range [0,1) Sum = 1

- How to minimize $J(\theta)$
  - Gradient descent
  - Modern deep learning framework will do this automatically.
    - All we need to do is the word embedding (in the skip-gram walk through)

`we start with randomly initialize embedding and during the training process, we will make the center word embedding more like its neighbors`

##### Intuition for learning

- Start with some initial embeddings (e.g., random)
- iteratively make the embeddings for a word 
  - more like the embeddings of its neighbors 
  - less like the embeddings of other words. 

#### Summary

- In order to support downstream applications like search, question answering, etc. we need ways to reason computationally about **meaning**. **Lexical semantics** addresses *meaning* at the word level.
  - `We convert words into vectors to represent meaning`

- Word similarity can be obtained by Characterizing a word by the other words it appears near
  - Which can yield sparse count-based representations
    - `word-document` or `word-word` representation
  - Or dense representations, which can be obtained by matrix factorization or neural network-inspired methods
- Representations can be evaluated on human semantics tasks
  - analogy
  - synonym identification
  - unrelated word identification

### Natrual Language Models (Lecture Slide 3)

##### What is a language model?

`Predict (probability of) the next words`

<img src="Lecture Notes.assets/Screenshot 2024-10-12 at 10.45.26 PM.png" alt="Screenshot 2024-10-12 at 10.45.26 PM" style="zoom:33%;" />

- Probability distributions over sentences (i.e., word sequences)

  ​	$P(W) = P(w_1w_2w_3...w_k) = \Pi^n_{k=1}P(w_k|w_1w_2w_3...w_{k-1})$

- Can use them to **generate** strings

  ​	$P(w_k|w_1w_2w_3...w_{k-1})$

- **Rank** possible sentences

  - P(“Today is Tuesday”) > P(“Tuesday Today is”)

  - P(“Today is Tuesday”) > P(“Today is UCLA”)


`Lanugage model for 1. generation (now) 2. rank possiblity (before)`

#### Language model applications

- Translation
- AutoComplete
- Correct Typo...

###### Context-sensitive spelling correction

- Which is most probable?
  - … I think they’re okay …
  - … I think there okay …
  - … I think their okay …
- Which is most probable?
  - … by the way, are they’re likely to …
  - … by the way, are there likely to …
  - … by the way, are their likely to …

###### Machine Translation

<img src="Lecture Notes.assets/image-20241007144743637.png" alt="image-20241007144743637" style="zoom:50%;" />

###### Smart reply

###### Language generation for everything-GPT

### N-Gram Language Model

- N-grams: a contiguous sequence of n tokens from a given piece of text

  <img src="Lecture Notes.assets/image-20241007145037924.png" alt="image-20241007145037924" style="zoom:50%;" />

  N-gram LMs models $p(x_{t:t+n})$, or $p(x_{t+n}|x_{t:t+n-1})$.

#### Independence (Markov) Assumption

`Current word only depend on recent words`

- Make an <u>n-gram</u> independence assumption: probability of a word only depends on a fixed number of previous words (<u>history</u>)
  - **trigram model**: $P(w_i| w_1…w_{(i-1)}) ≈P(w_i | w_{i-2} w_{i-1})$
  - **bigram model:**  $P(w_i| w_1…w{(i-1)}) ≈P(w_i | w_{i-1})$
  - **unigram model:** $P(w_i| w_1…w{(i-1)}) ≈P(w_i)$

#### Estimating Trigram Conditional Probabilities

`Count and Divide. Count how many time three words appear divided by count of two words appear.`

- P(mast | before the) = Count(before the mast)/Count(before the)
- In general, for any trigram, we have
  - $P(w_i | w_{i-2} w_{i-1})= \frac{Count (w_{i-2} w_{i-1} w_i)}{Count (w_{i-2} w_{i-1})}$

##### An example

<img src="Lecture Notes.assets/Screenshot 2024-10-07 at 2.56.17 PM.png" alt="Screenshot 2024-10-07 at 2.56.17 PM" style="zoom:50%;" />

##### Practical details (I)

- Trigram model assumes two-word history `P(wi|w_i-2, w_i-1)`

- But consider these sentences:

  | w1    | w2   | w3   | W4     |
  | ----- | ---- | ---- | ------ |
  | he    | saw  | the  | yellow |
  | feeds | the  | cat  | daily  |

- What's wrong?
  - a sentence shouldn't end with 'yellow'
  - a sentence shouldn't begin with 'feeds'
- Does the model capture these problems?

##### Beginning / end of sequence

- To capture behavior at beginning/end of sequences, we can augment the input:

  | $w_{-1}$ | w0    | W1    | w2   | w3   | w4     | w5    |
  | -------- | ----- | ----- | ---- | ---- | ------ | ----- |
  | <bos>    | <bos> | he    | saw  | the  | yellow | <eos> |
  | <bos>    | <bos> | feeds | the  | cats | daily  | <eos> |

   

- That is, assume $w_{-1}=w_{0}=<bos>$ and $w_{n+1}=<eos>$ so:
  - $P(w)=∏_{i=1}^{n+1}P(w_i | w_{i-2} w_{i-1})$

- Now $P(<eos>|yellow, .)$ is low, indicating this is not a good sentence

- $P(feeds|<bos>, <bos>)$ should also be low

`we pad n-1 <bos> but only 1 <eos>, because we only need conditional probability of <eos> given all the previous context to decide whether we properly end the sentence or not. We don't need multiple of <eos> because they will render similar effect.`

##### Beginning / end of sequence （第二部分）

- Alternatively, we could model all sentences as one (very long) sequence, including punctuation

  - two cats live in sam 's barn . sam feeds the cats daily . yesterday , he saw the yellow cat catch a mouse . [...]

    - This is the standard practice for LLM training

      `When we combine them to a long sentences, all of subsequent sentences now has beginning and end words, so we don't need <eos> and <bos> anymore`.

      `we don't have upper cases because it will make the vocabulary size larger. But cons is we could miss the Capitalize (make it easier for model) and miss the different meaning`

- Now, trigram probabilities like P(. | cats daily) and P(, | . yesterday) tell us about behavior at sentence edges

- Here, all tokens are lowercased. What are the pros/cons of <u>not</u> doing that?

##### Practical details (II)

​	$P(W) = P(w_1w_2w_3...w_k) = \Pi^n_{k=1}P(w_k|w_1w_2w_3...w_{k-1})$

<img src="Lecture Notes.assets/Screenshot 2024-10-12 at 11.45.06 PM.png" alt="Screenshot 2024-10-12 at 11.45.06 PM" style="zoom:50%;" />

`we have to multiply the probability to vocabulary size, therefore, it will become very small rapidly`

- Word probabilities are typically very small.

- Multiplying lots of small probabilities quickly gets so tiny we can't represent the numbers accurately. `Under-float problem`

- So in practice, we typically use log probabilities

  - Since probabilities range from 0 to 1, log probs range from -∞ to 0
  - Instead of <u>multiplying</u> probabilities, we <u>add</u> log probs

  - Often, negative log `negative log -> positive number` probs are used instead; these are often called "costs"; lower cost = higher prob

### Neural Language Models

#### Feedforward neural language model

- Model $p(x_t |x_{t-n+1:t-1}) $with a neural network. `model the n-gram probability using neural network` 

<img src="Lecture Notes.assets/image-20241007152234294.png" alt="image-20241007152234294" style="zoom:50%;" />

##### Why?

- Potentially generalize to unseen contexts

  - Example: “the shoes are blue”

  - This does not occurs in training corpus but 

      “the glasses are red” does.

  - If the word representations of “red” and “blue” are similar, and “shoes” and “glasses” are somewhat similar, then the model can generalize.

- Why are “red” and “blue” similar?
  - Because we saw “red skirt”, “blue skirt”, “red pen”, ”blue pen”, etc.
  - Their word embeddings are similar.

##### How to model word similarities?

<img src="Lecture Notes.assets/Screenshot 2024-10-07 at 3.25.58 PM.png" alt="Screenshot 2024-10-07 at 3.25.58 PM" style="zoom:50%;" />

### Neural Networks Recap 

- Let’s consider a 3-layer neural network

  <img src="Lecture Notes.assets/image-20241007152621385.png" alt="image-20241007152621385" style="zoom:50%;" />
  
  `feedforward language model is just 3-layer neural network`

##### How NN Makes Predictions

- forward pass: take input, and produce output

  `another is backward pass: update your parameters such that it optimize your objective function.`

- Just a bunch of linear transformation and applying the activation functions to introduce *non-linearity*

<img src="Lecture Notes.assets/Screenshot 2024-10-07 at 3.27.10 PM.png" alt="Screenshot 2024-10-07 at 3.27.10 PM" style="zoom:50%;" />

##### Learning the Parameters

- Find parameters that minimize the loss (or maximizes the likelihood) of the training data L(x, y).
- How to minimize the loss function?
  - Gradient Descent – **batch** or **mini batch** or **stochastic**!

- We need *gradients* of the loss function with respect to the parameters – what are our parameters? 

- How to compute the gradients of the parameters?
  - Backpropagation algorithm!

(Skip for calculus)

### Feedforward Neural language model

- Model $p(x_{t+n} |x_{t:t+n-1})$ with a neural network. 

<img src="Lecture Notes.assets/Screenshot 2024-10-07 at 3.31.41 PM.png" alt="Screenshot 2024-10-07 at 3.31.41 PM" style="zoom:50%;" />

`1. put embeddings into vector/matrix 2. Pass it through a linear layer (Projection layer) 3. do a activiation and put it through another linear layer. 4. Then put it through softmax layer `



`Say if you have a trigram model representation, then you have previous two words as input, then you get two embeddings. In order to combine these two embeddings, you put it (concatenate) in a long vector (from 1 x n to 1 x 2n). Then you pass it through a linear layer. After linear layer, you get a hidden representation, then you do a activation (tanh). Then you get another linear layer (linear projection). Then you do the softmax on the linear layer. After this softmax you will get a {1 x v} vector. Each element of the vector is the probability distribution over all the vocabulary. `



`What if we have a trigram with n=100 dimension of the word embedding? -Then we get 200 (2x100) word embedding -> become a 1x200 vector `

##### Recall word embeddings

- Word tokens map to vectors in a **low-dimensional space**

- Conditional word probabilities are produced by **neural network models** on vectors of **word embeddings**

- **Vector-space representation** enables semantic/syntactic **similarity** between words/sentences
- Use cosine similarity can measure word similarity
  
- Find nearest neighbours: synonyms, antonyms
  
- Algebra on words: {king} – {man} + {woman} = {queen}

##### Vector-space representation of words

<img src="Lecture Notes.assets/Screenshot 2024-10-07 at 3.42.07 PM.png" alt="Screenshot 2024-10-07 at 3.42.07 PM" style="zoom:50%;" />

#### Learning continuous space language models

- Input:
  - N-gram word history (**low-dimensional vector representation**)
- Output:
  - target word (**1-hot vector representation**)
- **Function** that **approximates** the conditional word likelihood $p(x_t | context)$:
  - Similar mechanism in skip-gram -- $p(x_{t±m} | x_t)$ `Estimate the probability of context word given center word`
  - Similar mechanism in CBOW -- $p(x_t|x_{t±m})$ ` Use context word to predict the probability of center word`
  - Feed-forward neural network -- $p(x_t | x_{t-n+1:t-1})$ `same mechanism, but we're using the previous N-word to predict the next word.`
  - Recurrent neural network -- $p(x_t | x_{1:t-1})$ `we use all history of previous word to predict the next word.`
  - …

`all of them uses neighbors to determine the meaning. just every step we going a little more complex`

###### Learning continuous space language models

- How do we **learn the word representations** for each word in the vocabulary?
- How do we **learn the model** that predicts the next word or its representation $ẑ_t$ given a word history?
  - `What are the parameters of feedforward neural networks? (3-layer neural network)`
  - `linear matrices, biases, word embediing.`

- Simultaneous learning of **model** and **representation** 
  - What are the parameters of the model?

##### Limitation of the Feedforward Neural Language Model

- Sparsity – Solved `No thing will have 0 probability as estimation`
- Word Similarity – Solved `We can figure out red blue are similar, because their word embedding is similar`
- Finite/fixed Context – Not solved yet `always a fix window`

Next time:

- RNN language models
