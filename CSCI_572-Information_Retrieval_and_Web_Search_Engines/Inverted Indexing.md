# Inverted indexing

### Outline

- Definition of an Inverted index
- Examples of Inverted Indices
- Representing an Inverted Index
- Processing a Query on a Linked Inverted Index
- Skip Pointers to Improve Merging
- Phrase Queries
- biwords
- Grammatical Tagging
- N-Grams
- Distributed Indexing

### Creating an Inverted Index

- An inverted index is typically composed of a vector containing all distinct words of the text collection in lexicographical order (which is called the **vocabulary**) and for each word in the vocabulary, a list of all documents (and text positions) in which that word occurs
  - This is nothing more than an index that one finds at the back of a book

- Terms in the inverted file index are refined:
  - **Case folding**: converting all uppercase letters to lower case
  - **Stemming**: reducing words to their morphological roots
  - **Stop words**: removing words that are so common they provide no information

Like the slide above says, a book typically has an index - 'one book, many words in the index'. When we invert that, we'd create an 'inverted index': 'one word, many books'.

[Here](https://bytes.usc.edu/cs572/s25-555-sear-ch/lectures/InvIndex/docs/TheCBook-2e.pdf) is a cool/venerable book ['The C Programming Language'!]. At the back of the book is the index, starting at p.263 [look for it]. Geek humor - the last page # entry for ['recursion'](https://bytes.usc.edu/cs572/s25-555-sear-ch/lectures/InvIndex/docs/recurself.png) shows 269, which is the very page that lists it :)

### Inverted Index Example

<img src="Inverted Indexing.assets/Screenshot 2025-03-10 at 3.47.59 PM.png" alt="Screenshot 2025-03-10 at 3.47.59 PM" style="zoom:33%;" />

The two parts of an inverted index. The **dictionary** (Index file) is usually kept in memory, with pointers to each postings list , which is stored on disk. The dictionary has been sorted alphabetically and the postings list is sorted by document ID

### Another Example of an Inverted Index

<img src="Inverted Indexing.assets/Screenshot 2025-03-10 at 3.49.01 PM.png" alt="Screenshot 2025-03-10 at 3.49.01 PM" style="zoom:33%;" />

Yet another example (from the book):

<img src="Inverted Indexing.assets/InvIndexEx.png" alt="img" style="zoom:50%;" />

### Processing a Query: An Example

- The Query
  - Which plays of Shakespeare contain the words *Brutus AND Caesar* but NOT *Calpurnia*?

- One Possible Solution
  - One could grep all of Shakespeare’s plays for *Brutus* and *Caesar*, then strip out lines containing *Calpurnia*?
    - Too Slow (for large corpora)
    - Requires lots of space
    - This method doesn’t allow for other operations (e.g., find the word *Romans* near *countrymen*) are not feasible with this approach

### Term-Document Incidence Matrix

One way to think about an inverted index is to consider it as a sparse matrix where rows Represent terms and columns represent documents

<img src="Inverted Indexing.assets/Screenshot 2025-03-10 at 3.50.02 PM.png" alt="Screenshot 2025-03-10 at 3.50.02 PM" style="zoom:33%;" />

### Incidence Vectors

- So we have a 0/1 vector for each term.
- To answer query: take the vectors for *Brutus*, *Caesar* and *Calpurnia* (complemented) and do a bitwise AND.
- 110100 AND 110111 AND 101111 =100100
- So the two plays matching the query are: Anthony and Cleopatra, Hamlet

### Actual Answers to the Query

<img src="Inverted Indexing.assets/Screenshot 2025-03-10 at 3.55.09 PM.png" alt="Screenshot 2025-03-10 at 3.55.09 PM" style="zoom:33%;" />

### Inverted Indexes are Naturally Sparse

- Given 1 million documents and 500,000 terms
- The term x Document matrix in this case will have size 500K x 1M or half-a-trillion 0’s and 1’s.

- But it has no more than one billion 1’s.
  - So the matrix is extremely sparse, only 0.1% of the elements are 1

- So instead we use a data structure for an inverted index that exploits sparsity and then devise algorithms for query processing

### Inverted Index Stored In Two Parts

- For each term T, we must store a list of all documents that contain T.
- Linked lists are generally preferred to arrays
  - Dynamic space allocation
  - Insertion of terms into documents easy
  - However, there is space overhead of pointers, though this is not too serious

<img src="Inverted Indexing.assets/Screenshot 2025-03-10 at 3.56.57 PM.png" alt="Screenshot 2025-03-10 at 3.56.57 PM" style="zoom:33%;" />

### Inverted Index

<img src="Inverted Indexing.assets/Screenshot 2025-03-10 at 3.57.41 PM.png" alt="Screenshot 2025-03-10 at 3.57.41 PM" style="zoom:33%;" />

<img src="Inverted Indexing.assets/Screenshot 2025-03-10 at 3.58.06 PM.png" alt="Screenshot 2025-03-10 at 3.58.06 PM" style="zoom:33%;" />

- Multiple term entries in a single document are merged.

- Frequency information is added.

  - Why frequency? will discuss later.

  <img src="Inverted Indexing.assets/Screenshot 2025-03-10 at 3.58.48 PM.png" alt="Screenshot 2025-03-10 at 3.58.48 PM" style="zoom:33%;" />

  <img src="Inverted Indexing.assets/Screenshot 2025-03-10 at 3.59.24 PM.png" alt="Screenshot 2025-03-10 at 3.59.24 PM" style="zoom:50%;" />

### Query Processing Across the Postings List

- Consider processing the query:

  *Brutus AND Caesar*

  - Locate Brutus in the Dictionary;

    - Retrieve its postings.

    Locate Caesar in the Dictionary;

    - Retrieve its postings.

  - “Merge” the two postings (postings are document ids):

<img src="Inverted Indexing.assets/Screenshot 2025-03-10 at 4.01.03 PM.png" alt="Screenshot 2025-03-10 at 4.01.03 PM" style="zoom:33%;" />

### Basic [naive] merging

##### Basic Merge

Walk through the two postings simultaneously, in time linear in the total number of postings entries

<img src="Inverted Indexing.assets/Screenshot 2025-03-10 at 4.01.40 PM.png" alt="Screenshot 2025-03-10 at 4.01.40 PM" style="zoom:33%;" />

If the list lengths are m and n, the merge takes O(m+n) operations.

##### Query Optimization

- What is the best order for query processing?

- Consider a query that is an AND of t terms.

- For each of the t terms, get its postings, then AND together.

  <img src="Inverted Indexing.assets/Screenshot 2025-03-10 at 4.02.32 PM.png" alt="Screenshot 2025-03-10 at 4.02.32 PM" style="zoom:33%;" />

### Skip pointers - to speed up merging

To speed up the merging of postings we use the technique of **Skip Pointers**

##### The Technique of Skip Pointers

Augment postings with skip pointers (at indexing time)

<img src="Inverted Indexing.assets/Screenshot 2025-03-10 at 4.03.52 PM.png" alt="Screenshot 2025-03-10 at 4.03.52 PM" style="zoom:33%;" />

- Why?
  - To skip postings that will not figure in the search results.

- How?
  - Where do we place skip pointers?

##### Query processing with skip pointers

<img src="Inverted Indexing.assets/Screenshot 2025-03-10 at 4.04.33 PM.png" alt="Screenshot 2025-03-10 at 4.04.33 PM" style="zoom:33%;" />

Suppose we've stepped through the lists until we process 8 on each list.

When we get to 16 on the top list, we see that its successor is 32.

But the skip successor of 8 on the lower list is 31, so we can skip ahead past the intervening postings.

Aside: skip pointers (aka [skip lists](https://www.geeksforgeeks.org/skip-list/)) can be used to search a linked list of sorted items faster than O(n), ie. in O(sqrt(n))...

##### Facts on Skip Pointers

- skip pointers are added at indexing time; they are shortcuts, and they only help for AND queries and they are useful when the corpus is relatively static
  - there are two questions that must be answered:
    1. where should they be placed?
    2. how do the algorithms change?
- More skips means shorter skip spans, and that we are more likely to skip. But it also means lots of comparisons to skip pointers, and lots of space storing skip pointers. Fewer skips means few pointer comparisons, but then long skip spans which means that there will be fewer opportunities to skip.
- A simple heuristic for placing skips, which has been found to work well in practice, is that for a postings list of length P, use sqrt{P} evenly-spaced skip pointers. This heuristic possibly can be improved upon as it ignores any details of the distribution of query terms.
- Building effective skip pointers is casy if an index is relatively statics it is harder if a postings list keeps changing because of updates. A malicious deletion strategy can render skip lists ineffective.
- See the YouTube video http://www.youtube.com/watch?v=tPsCQOsa7j0

### Phrase queries [searching multiple words in order]

##### Phrase queries

- We want to answer queries such as “stanford university”’ — as a phrase
- Thus the sentence “I went to university at Stanford” is not a match.
  - The concept of phrase queries has proven easily understood by users; about 10% of web queries are phrase queries
- No longer suffices to store only`<term : docs>` entries

### One approach: index bi-words

##### Using Biword Indexes for Phrase Searching

- A biword (or a 2-gram) is a consecutive pair of terms in some text
- To improve phrase searching one approach is to index every biword in the text 
- For example the text “Friends, Romans, Countrymen” would generate the bi-words
  - *friends romans*
  - *romans cauntrymen* 
- Each of these bi-words is now a dictionary term

##### Handling Longer Phrase Queries

- Consequences

  - Biwords will cause an explosion in the vocabulary database
  - Queries longer than 2 words will have to be broken into biword segments

- Example: suppose the query is the 4 word phrase

  - *stanford university palo alto*

  - The query can be broken into the Boolean query on biwords: 

    stanford university **AND** university palo **AND** palo alto

- Matching the query to terms in the index will work, but may also produce false positives (i.e. occurrences of the biwords, but not the full 4 word query)

### Another approach: position index for each term

##### Alternate Solution Using Positional Indexes

- Store, for each term, entries of the form:

  <number of docs containing term;

  doc1: position1, position2 ... ;

  doc2: position1, position2 ...;

  etc.>

##### Positional Index Example

for each term in the vocabulary, we store postings of the form 

doclD: position1, position2, ...,

where each position is a token index in the document. Each posting will also usually record the term frequency. Adopting a positional index expands required postings storage significantly, even if we compress position values/offsets

<img src="Inverted Indexing.assets/Screenshot 2025-03-10 at 4.12.13 PM.png" alt="Screenshot 2025-03-10 at 4.12.13 PM" style="zoom:33%;" />

- Nevertheless, this expands postings storage substantially

##### Processing a Phrase Query

- Extract inverted index entries for each distinct term: to, be, or, not.
- Merge their *doc:position* lists to enumerate all positions with “*to be or not to be*”.

<img src="Inverted Indexing.assets/Screenshot 2025-03-10 at 4.13.32 PM.png" alt="Screenshot 2025-03-10 at 4.13.32 PM" style="zoom:33%;" />

-  In document 4 the word “to” appears in position 16 and the word “be” appears in position 17, so they are adjacent

### Another approach: extended biword

##### Another Approach

- Among possible queries, nouns and noun phrases often appear, e.g. “abolition of slavery", “renegotiation of the constitution”
- But as seen above, related nouns can often be divided from each other by various function words
- These needs can be incorporated into the biword indexing model in the following way:
  - First, we tokenize the text and perform **part-of-speech-tagging**. We can then group terms into nouns, including proper nouns, (N) and function words, including articles and prepositions, (X), among other classes.
  - Now deem any string of terms of the form NX*N to be an extended biword. Each such extended biword is made a term in the vocabulary.
  - E.g. “renegotiation of the constitution” is mapped to N X X N (two nouns and two others), so the others are ignored and the two word phrase “renegotiation constitution” is added to the index
- Programs that identify a word’s part-of-speech tag are based on statistical or rule-based approaches and are trained using large corpora

##### Some High Frequency Noun Phrases

<img src="Inverted Indexing.assets/Screenshot 2025-03-10 at 4.15.27 PM.png" alt="Screenshot 2025-03-10 at 4.15.27 PM" style="zoom:33%;" />

- The phrases above were identified by POS tagging; The data above shows that common phrases are used more frequently in patent data as patents have a very formal style: many of the TREC phrases are proper nouns, whereas patent phrases are those that occur in all patents

### n-gram [generalization of 'biword']

##### Building n-gram Indexes

- Generalizing from bi-words, an n-gram is any sequence of n consecutive words
- N-grams can be identified at the time of parsing
- N-grams of all lengths form a Zipf distribution with a few common phrases occurring very frequently and a large number occurring with frequency 1
- Common n-grams are usually made up of stop words (e.g. “and the” “there is”)
- For each n-gram, the inverted index will need pointers to all dictionary terms containing it — the "postings"
- Therefore, the larger the value of n, the larger the amount of space required to hold all n grams

##### Google's N-Gram Facts

- Google made available a file of n-grams derived from the web pages it indexed
- http://googleresearch.blogspot.com/2006/08/all-our-n-gram-are-belong-to-you.html
- Statistics for the Google n-gram sample
  - Number of tokens 1,024,908,267,229 (1 trillion, . . . )
  - Number of sentences 95,119,665,584
  - Number of unigrams 13,588,391
  - Number of bigrams 314,843,401
  - Number of trigrams 977,069,902
  - Number of four grams 1,313,818,354
  - Number of five grams 1.176.470,663

- For specific examples of 3-gram and 4-gram data sce the web page above

##### Comparing N-Grams Across Languages

- S.Yang et al, N-gram statistics in English and Chinese: Similarities and differences, ICSC, 2007, Int’l Conf. on semantic computing, 454-460

- http://static.googleusercontent.com/external_content/untrusted_dlcp/research.google.com/en/us/pubs/archive/33035.pdf

- They analyzed 200 million randomly sampled English and Chinese Web pages and concluded:

  1. The distribution of the unique number of n-grams is similar between English and Chinese, though the Chinese distribution is shifted to larger N
  2. The distribution indicates that on average 1.5 Chinese characters correspond to 1 English word
  3. While frequency distributions of uni-grams and bi-grams are very different, the frequency distribution for 3-grams and 4-grams are strikingly similar

  Here is Google's [ngram viewer](https://books.google.com/ngrams/) and a [guide](https://books.google.com/ngrams/info) for it.

### Distributed indexing - to speed the process

##### Distributed Indexing

- For web-scale indexing one must use a distributed computing cluster
- Individual machines are fault-prone
  - Can unpredictably slow down or fail
- How do we exploit such a pool of machines?
- Must we maintain a master machine directing the indexing job — considered “safe”.
- Break up indexing into sets of (parallel) tasks.
- Master machine assigns each task to an idle machine from a pool.

##### Parallel Tasks

- One approach is to use two sets of parallel tasks
  - Parsers
  - Inverters
- Break the input document corpus into splits
  - Each split is a subset of documents
- Master assigns a split to an idle parser machine
- Parser reads a document at a time and emits (term, doc) pairs
- Parser writes pairs into j partitions
- Each for a range of terms’ first letters
  - (e.g., a-f. g-p, q-z) — here j=3.
- Now to complete the index inversion

##### Data Flow

<img src="Inverted Indexing.assets/Screenshot 2025-03-10 at 4.22.10 PM.png" alt="Screenshot 2025-03-10 at 4.22.10 PM" style="zoom:33%;" />

##### Inverters

- Collect all (term, doc) pairs for a partition
- Sorts and writes to postings list
- Each partition contains a set of postings

<img src="Inverted Indexing.assets/Screenshot 2025-03-10 at 4.22.47 PM.png" alt="Screenshot 2025-03-10 at 4.22.47 PM" style="zoom:33%;" />

##### Simplest Approach to Dynamic Indexing

- Maintain “big” main index
- New docs go into “small” auxiliary index
- Search across both, merge results periodically
- Deletions
  - Invalidation bit-vector for deleted docs
  - Filter docs output on a search result by this invalidation bit-vector
- Periodically, re-index into one main index

### Text analysis - the heart of it all

Text analysis [including for inverted index creation] is an interesting topic, with ML being increasingly used for it. To get a taste of pre-ML techniques, look [here](https://ladal.edu.au/tutorials/introta/introta.html) for ex. [more [here.](https://ladal.edu.au/tutorials.html)].