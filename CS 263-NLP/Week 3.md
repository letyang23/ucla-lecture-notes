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













