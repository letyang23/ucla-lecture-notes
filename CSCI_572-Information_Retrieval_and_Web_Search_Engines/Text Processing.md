# Text processing

### Standing Queries

- The path from IR to text classification:

  - You have an information need to monitor, say:
    - Unrest in the Niger delta region

  - You want to rerun an appropriate query periodically to find new news items on this topic
  - You will be sent new documents that are found
  - i.e. it’s not ranking but classification (relevant vs. not relevant)

- Such queries are called standing queries
  - Long used by “information professionals”
  - A modern mass instantiation is Google Alerts
- Standing queries are (hand-written) text classifiers

<img src="Text Processing.assets/Screenshot 2025-03-10 at 3.17.07 PM.png" alt="Screenshot 2025-03-10 at 3.17.07 PM" style="zoom:33%;" />

### Spam filtering: Another text classification task

<img src="Text Processing.assets/Screenshot 2025-03-10 at 3.17.55 PM.png" alt="Screenshot 2025-03-10 at 3.17.55 PM" style="zoom:33%;" />

### Categorization/Classification

- Given:

  - A representation of a document d

    - Issue: how to represent text documents.
    - Usually some type of high-dimensional space — bag of words

  - A fixed set of classes:

    $C = {c_1, c_2,...,c_j}$

- Determine:
  - The category of d by generating a classification function, say y(d)
  - We want to build classification functions (“classifiers”).

### Document Classification 

<img src="Text Processing.assets/Screenshot 2025-03-10 at 3.19.58 PM.png" alt="Screenshot 2025-03-10 at 3.19.58 PM" style="zoom:33%;" />

### Classification Methods (1)

- Manual classification
  - Used by the original Yahoo! Directory
  - Looksmart, about.com, ODP, PubMed
  - Accurate when job is done by experts
  - Consistent when the problem size and team is small
  - Difficult and expensive to scale
    - Means we need automatic classification methods for big problems

### Classification Methods (2)

- Hand-coded rule-based classifiers
  - One technique used by news agencies, intelligence agencies, etc.
  - Widely deployed in government and enterprises
  - Vendors provide “IDE” for writing such rules

- Hand-coded rule-based classifiers
  - Commercial systems have complex query languages
  - Accuracy is can be high if a rule has been carefully refined over time by a subject expert
  - Building and maintaining these rules is expensive

### Classification Methods (3): Supervised learning

- Given:

  - A document d

  - A fixed set of classes:

    $C = {c_1, c_2, ..., c_j}$

  - A **training set** D of documents each with a label in C

- Determine:

  - A learning method or algorithm which will enable us to learn a classifier y

  - For a test document d, we assign it the class

    $y(d)\in C$

- Supervised learning
  - Naive Bayes (simple, common) 
  - k-Nearest Neighbors (simple, powerful)
  - Support-vector machines (newer, generally more powerful)
  - ... plus many other methods
  - No free lunch: requires hand-classified training data
  - But data can be built up (and refined) by amateurs
- Many commercial systems use a mixture of methods

### The bag of words representation

<img src="Text Processing.assets/Screenshot 2025-03-10 at 3.24.37 PM.png" alt="Screenshot 2025-03-10 at 3.24.37 PM" style="zoom:33%;" />

<img src="Text Processing.assets/Screenshot 2025-03-10 at 3.24.50 PM.png" alt="Screenshot 2025-03-10 at 3.24.50 PM" style="zoom:33%;" />

### Features

- Supervised learning classifiers can use any sort of feature
  - URL, email address, punctuation, capitalization, dictionaries, network features
- In the simplest bag of words view of documents
  - We use only word features
    - we use all of the words in the text (not a subset)

### Feature Selection: Why?

- Text collections have a large number of features
  - 10,000 — 1,000,000 unique words ... and more
- Selection may make a particular classifier feasible
  - Some classifiers can’ t deal with 1,000,000 features
- Reduces training time
  - Training time for some methods is quadratic or worse in the number of features
- Makes runtime models smaller and faster
- Can improve generalization (performance)
  - Eliminates noise features
  - Avoids overfitting

### Feature Selection: Frequency

- The simplest feature selection method:
  - Just use the most common terms
  - No particular foundation
  - But it make sense why this works
    - They are the words that can be well-estimated and are most often available as evidence
- In practice, this is often 90% as good as better methods
- Smarter feature selection — future lecture

### SpamAssassin

- Naive Bayes has found a home in spam filtering
  - Paul Graham’ s A Plan for Spam
    - http://www.paulgraham.com/spam.html

- Widely used in spam filters
- But many features beyond words:
  - black hole lists, etc.
  - particular hand-crafted text patterns

[Here](http://www.paulgraham.com/spam.html) is Paul's page, on his spam filtering expts.

[Here](https://spamassassin.apache.org/) is SpamAssassin, and [this](https://spamassassin.apache.org/old/tests_3_3_x.html) is an old page with results of tests performed.

##### Naive Bayes is Not So Naive

- Very fast learning and testing (basically just count words)
- Low storage requirements
- Very good in domains with many equally important features
- More robust to irrelevant features than many learning methods
  - Irrelevant features cancel each other without affecting results

### Evaluating Categorization

- Measures: precision, recall, F1, classification accuracy
- **Classification accuracy**: r/n where n is the total number of test docs and r is the number of test docs correctly classified

### Recall: Vector Space Representation

- Each document is a vector, one component for each term (= word).
- Normally normalize vectors to unit length.
- High-dimensional vector space:
  - Terms are axes
  - 10,000+ dimensions, or even 100,000+
  - Docs are vectors in this space

- How can we do classification in this space?

### Classification Using Vector Spaces

- In vector space classification, training set corresponds to a labeled set of points (equivalently, vectors)
- **Premise 1**: Documents in the same class form a contiguous region of space

- **Premise 2**: Documents from different classes don’t overlap (much)
- Learning a classifier: build surfaces to delineate classes in the space

### Test Document of what class?

<img src="Text Processing.assets/Screenshot 2025-03-10 at 3.33.34 PM.png" alt="Screenshot 2025-03-10 at 3.33.34 PM" style="zoom:33%;" />

### Test Document = Government

<img src="Text Processing.assets/Screenshot 2025-03-10 at 3.34.01 PM.png" alt="Screenshot 2025-03-10 at 3.34.01 PM" style="zoom:33%;" />

### Definition of Centroid

$$
\vec{\mu}(c) = \frac{1}{|D_c|} \sum_{d \in D_c} \vec{v}(d)
$$

- Where $D_c$ is the set of all documents that belong to class c and v(d) is the vector space representation of d.

- Note that centroid will in general not be a unit vector even when the inputs are unit vectors.

### Rocchio classification

- Rocchio forms a simple representative for each class: the centroid/prototype
- Classification: nearest prototype/centroid

In [Rocchio classification](https://nlp.stanford.edu/IR-book/html/htmledition/rocchio-classification-1.html), centroids (one for each term group) are used to specify regions; lines/planes/hyperplanes between centroids produce convex **Voronoi** regions. The new/incoming term's closest centroid is used to classify the term.

### k Nearest Neighbor Classification

- kNN = k Nearest Neighbor
- To classify a document d:
  - Define k-neighborhood as the k nearest neighbors of d
  - Pick the majority class label in the k-neighborhood
  - For larger k can roughly estimate P(c|d) as #(c)/k

### Test Document = Science

<img src="Text Processing.assets/Screenshot 2025-03-10 at 3.37.53 PM.png" alt="Screenshot 2025-03-10 at 3.37.53 PM" style="zoom:33%;" />

### Nearest-Neighbor Learning

- Learning: just store the labeled training examples D
- Testing instance x (under 1NN):
  - Compute similarity between x and all examples in D.
  - Assign x the category of the most similar example in D.
- Does not compute anything beyond storing the examples.
- Also called:
  - Case-based learning
  - Memory-based learning
  - Lazy learning
- Rationale of kNN: contiguity hypothesis

### k Nearest Neighbor

- Using only the closest example (1NN) subject to errors due to:
  - A single atypical example.
  - Noise (i.e., an error) in the category label of a single training example.
- More robust: find the k examples and return the majority category of these k
- k is typically odd to avoid ties; 3 and 5 are most common

### kNN: Discussion

- No feature selection necessary
- No training necessary
- Scales well with large number of classes
  - Don't need to train n classifiers for n classes
- Classes can influence each other
  - Small changes to one class can have ripple effect
- Done naively, very expensive at test time
- In most cases it’s more accurate than NB or Rocchio