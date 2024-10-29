# 10/14 Lecture (2nd half after quiz 1)

### 5. Sequence-to-Sequence (Seq2Seq) Models

###### Outline

- Sequence to sequence modeling problems
- From language modeling to machine translation – RNN Seq2seq models
- Seq2seq with attention

#### Background: Seq2seq modeling

- The sequence-to-sequence setup:
  - A sequence x1, x2, … xn goes in 
  - A different sequence y1, y2, … ym comes out. E.g. -- 
    - Speech recognition: Speech in, word sequence out 
    - Machine translation: Word sequence in, word sequence out
    - Dialogue : User statement in, system response out 
    - …

<img src="Week 3.assets/image-20241026200525181.png" alt="image-20241026200525181" style="zoom:50%;" />

##### Seq2seq (Sutskever et al., 2014)

<img src="Week 3.assets/image-20241026201711151.png" alt="image-20241026201711151" style="zoom:50%;" />

#### RNN Seq2Seq Models

##### Seq2seq model

<img src="Week 3.assets/image-20241026202341975.png" alt="image-20241026202341975" style="zoom:50%;" />

- What’s the difference between the encoder and the decoder RNNs?
  - `For Encoder, they don't suppose to produce output. For decoder, they does not accept real input system. and length can be different. `

##### From LM to MT? (Language Model to Machine Translation)

- Why not predict the translation of "the students opened their" instead of the next word?

  <img src="Week 3.assets/image-20241026202616511.png" alt="image-20241026202616511" style="zoom:50%;" />

`We encode this sequence to some vector. For machine translation, we predict the translation instead of next word.`

##### Recap: RNN-LMs

<img src="Week 3.assets/image-20241026203137272.png" alt="image-20241026203137272" style="zoom:50%;" />

##### From RNN-LM to MT

- Encode the source sentence into a vector 
  - This vector is the product of an RNN (encoder RNN)
  - What do we take from the encoder RNN to be the sentence vector?
    - `encoder encode everything into a vector and feed this into another RNN.`
- Feed the sentence vector to <u>another RNN</u> (the decoder)
  - Where should this vector go?
    - `h0`
- We'll train them together in what's called the sequence-to-sequence (seq2seq) or encoder-decoder model more generally.

<img src="Week 3.assets/image-20241026204304462.png" alt="image-20241026204304462" style="zoom:25%;" />

<img src="Week 3.assets/image-20241026205111619.png" alt="image-20241026205111619" style="zoom:50%;" />

- Extension: encoder often a bidirectional RNN (two RNNs working in opposite directions) 
  - What are the benefits?

#### Seq2Seq formally/mathematically

- Encoder-decoder

- Two RNNs (typically LSTMs or GRUs)

- Source sequence $x= (x_1, x_2,..., x_{|x|})$ represented as word embedding vectors

- Target sequence $y= (y_1, y_2,..., y_{|y|})$

- At the end of the encoding process, we have the final hidden state $h_{|x|}^{(src)}$

  ​	$h_j^{(src)} = RNN_\theta(h_{j-1}^{(src)}, x_{j-1})$

- Hidden state initialization:

  - Set the initial states of the decoder $h_0^{(tar)}$ to $h_{|x|}^{(src)}$

#### Seq2seq (cont.)

- At each step of the decoder, compute $h_j^{(tar)}$

  ​	$h_j^{(tar)} = RNN_{\theta}(h_{j-1}^{(tar)}, y_{j-1})$

- $y_{j-1}$: **ground truth previous word** during training (“teacher forcing”), and **previously predicted word** at inference time.

- $\theta$ – parameters (weights) of the network

#### Seq2seq (cont.)

- Predicted word at time step *j* is given by a softmax layer:

  $p(y_j) = softmax(W_{out}h_j^{(tar)})$

- $W_{out}$ is a weight matrix

- Softmax function:

  ​	$softmax(y)_k = \frac{exp(y_k)}{\sum_{j=1}^{|V|}exp(y_j)}$

- $y_k$is the value of the $k_{th}$ dimension of the output vector **y** (note that **boldface** denotes a **vector** while non-boldface denotes a scalar).

#### Softmax example

<img src="Week 3.assets/image-20241027221502228.png" alt="image-20241027221502228" style="zoom:50%;" />



# 10/28 Lecture (after Quiz 1)

- Project midterm report
  - Literature review and baseline model you want to use!
  - Papers in the project description (suggest reading). Every paper, literature review like the **related work** section in these research papers.

#### RNN LM vs Seq2Seq, mathematically

- LM
  - $p(y_j|y_1, y_2,...,y_{j-1}) = softmax(Uh_j+b_U)_j$
  - $h_j = f(W_hh_{j-1} + W_ee_j + b_w); e_j = E_{e_j}$
  - $f$ is a nonlinear function (tanh, usually). $U, W, E$ are learned weight matrices; $b_W$ and $b_U$ are bias terms. $E$ is the 'embedding' matrix.

- Seq2Seq
  - $p(y_j|y_1, y_2, ... , y_{j-1}, x_1, ... , x_m) = softmax(U^{(d)}h_j^{d}+b_{U^{(d)}})_j$
  - $ h_j^{(d)} = f(W_{h^{(d)}} h_{j-1}^{(d)} + W_{e^{(d)}} e_j^{(d)} + b_{W^{d}}); \, e_j^{(e)} = E _{e_j^{(d)}}$
  - $$ h_0^{(d)} = h_m^{(e)}; h_j^{(e)} = f(W_{h^{(e)}} h_{j-1}^{(e)} + W_{e^{(e)}} e_j^{(e)} + b_{W^{(e)}}); \, e_j^{(e)} = E _{e_j^{(e)} }$$
  - Where the superscription \((e), (d)\) denotes encoder and decoder, and the subscript denotes position. 
  - **Note:** Separate weight matrices for output and input side, but basically one big RNN!

#### From Language Model to Translation Model

- An RNN LM estimates 
  $$ p(\mathbf{y} = y_1, y_2, \dots, y_n) = p(y_1)p(y_2 | y_1) \dots p(y_n | y_1, y_2, \dots, y_{n-1}) $$

- A seq2seq TM also estimates the probability of $\mathbf{y}$ but conditions it on an input sequence $\mathbf{x}$. It's a **conditional language model**:
  $$ p(\mathbf{y} | \mathbf{x}) = p(y_1 | \mathbf{x})p(y_2 | y_1, \mathbf{x}) \dots p(y_n | y_1, y_2, \dots, y_{n-1}, \mathbf{x}) $$

- Trained as one big RNN (with two sets of parameters switched in the middle), basically in the same way as RNN-LM.

<img src="Week 3.assets/image-20241028175715570.png" alt="image-20241028175715570" style="zoom:50%;" />



### Seq2Seq with Attention

##### Motivated by the MT task

NMT is the **flagship task** for NLP Deep Learning

- **NMT research has pioneered many of the recent innovations of NLP Deep Learning**

- In **2018**: NMT research continues to **thrive**
  - Researchers have found **many, many improvements** to the "vanilla" seq2seq NMT system we've presented today
  - But **one improvement** is so integral that it is the new vanilla...

**ATTENTION**

<img src="Week 3.assets/image-20241028180420929.png" alt="image-20241028180420929" style="zoom:50%;" />

#### Attention

- **Attention** provides a solution to the bottleneck problem.
- **Core idea**: on each step of the decoder, _focus on a particular part_ of the source sequence.
- First we will show via diagram (no equations), then we will show with equations.

##### Seq2Seq with Attention

<img src="Week 3.assets/image-20241028180651623.png" alt="image-20241028180651623" style="zoom:50%;" />























