# 10/23 Lecture

##### Position Encoding

<img src="Week 4.assets/image-20241023141051522.png" alt="image-20241023141051522" style="zoom:40%;" />

<img src="Week 4.assets/image-20241023142104023.png" alt="image-20241023142104023" style="zoom:33%;" />

##### Position Embedding Visualization

<img src="Week 4.assets/image-20241023142255784.png" alt="image-20241023142255784" style="zoom:50%;" />

##### Position embedding discussion

- Bottomline: Transformer models need positional encoding – the position encoding proposed in the original paper is also referred to as sinusoidal position encoding.
  - Will this position encoding repeat themselves?
- How does positional embedding work mathematically?
  - $E_{in} = E_w + E_p$
  - When calculation attention, $A_{ij} = E_{in}^i W_qW_k^t E_{in}^j$
  - Ignoring the $W_qW_k^t$ term for simplicity, $A_{ij} = E_{in}^i E_{in}^j = (E_w^i + E_p^i) (E_w^j + E_p^j) = E_w^iE_w^j + E_w^iE_p^j + E_w^jE_p^i + E_p^iE_p^j $
    - The same words with different position: different attention
    - The same words with similar/same relative position distance: similar/same attention (The same position is a special case of "similar relative position distance").

##### Different position embedding strategies

- Original Transformer paper: Sinusoidal embedding
  - Used in all legacy decoder-only large-pretrained models (e.g., <u>GPT-2/3</u>). 
  - GPT4 didn’t disclose its position embedding details, but they cited rotary position embedding (it is believed that they use RoPE).
- Learned position embedding:
  - Used in encoder only large-pretrained transformer models, such as <u>BERT, RoBERTa, ALBERT, DistilBERT, ERNIE</u>
- [Rotary position embedding (RoPE)](https://arxiv.org/abs/2104.09864):
  - Used in all newer (open) decoder-only large-pretrained models, such as <u>LlaMA-1/2/3, GPT-J, Pythia, Mistral</u>, and probably in 

##### Residual Connections and Layer Norm

<img src="Week 4.assets/image-20241023151529745.png" alt="image-20241023151529745" style="zoom:50%;" />

- Issue of information loss -- Self-attention can decide not to attend to itself

  - -> Add input back again in each sublayer!

  <img src="Week 4.assets/image-20241023151549473.png" alt="image-20241023151549473" style="zoom:44%;" />

##### Transformer Decoders

<img src="Week 4.assets/image-20241023153815844.png" alt="image-20241023153815844" style="zoom:50%;" />

##### Masked Self-Attention

- The goal is to make the model ***causal***: it means the output at a certain position can only depend on the words in the left-side context. The model **must not** be able to see future words.

<img src="Week 4.assets/image-20241023152601921.png" alt="image-20241023152601921" style="zoom:50%;" />

- Why? How? For what tasks will we need this masked self-attention?

##### Masked Self-Attention

- Attention masks

  <img src="Week 4.assets/image-20241023153314124.png" alt="image-20241023153314124" style="zoom:33%;" />

  - Add to the QKT attention BEFORE softmax.

  

- What’s the effect?

  <img src="Week 4.assets/image-20241023153352480.png" alt="image-20241023153352480" style="zoom:33%;" />

  - Can we multiply this to the QKT attention AFTER softmax?

##### Transformer Decoders

<img src="Week 4.assets/image-20241023153938232.png" alt="image-20241023153938232" style="zoom:50%;" />

##### Cross-Attention in Transformer Decoders

- The **query vectors** come from the previous layer in the **decoder**.
- The **key** and **value** vectors come from the **encoder** outputs (usually from the last layer of the encoder).

<img src="Week 4.assets/image-20241023154007976.png" alt="image-20241023154007976" style="zoom:50%;" />

##### Cross-Attention in Transformer Decoders

<img src="Week 4.assets/image-20241023154032837.png" alt="image-20241023154032837" style="zoom:50%;" />

- The key and value vectors are from the source sentence (encoder).
- The query vectors are from the target sentence (decoder).

##### Cross-Attention in Transformer Decoders

<img src="Week 4.assets/image-20241023154051048.png" alt="image-20241023154051048" style="zoom:50%;" />

- Does the sequence lengths need to be the same?
- Does the word embedding sizes need to be the same?
- Does the hidden dimensions need to be the same?
- In practice, most transformer models have embedding dimension and the hidden dimension to be exactly the same.

##### Exercise

- Source: conduis prudemment toi

- Target: drive safe

  <img src="Week 4.assets/Screenshot 2024-10-23 at 3.47.10 PM.png" alt="Screenshot 2024-10-23 at 3.47.10 PM" style="zoom:50%;" />

- Attention score = ?

##### Self Attention (Cheng et al. 2016, Vaswani et al. 2017)

- Each element in the sequence attends to elements of that sequence → context sensitive encodings!

<img src="Week 4.assets/image-20241023154754439.png" alt="image-20241023154754439" style="zoom:50%;" />

##### Cross Attention (Bahdanau et al. 2015)

- Each element in a sequence attends to elements of another sequence

  <img src="Week 4.assets/image-20241023154819043.png" alt="image-20241023154819043" style="zoom:50%;" />

### Putting everything togeter

<img src="Week 4.assets/image-20241023154834529.png" alt="image-20241023154834529" style="zoom:50%;" />

<img src="Week 4.assets/image-20241023154913357.png" alt="image-20241023154913357" style="zoom:50%;" />

##### Decoder-only Transformers

- Modern LLMs are all decoder-only transformers
  - Closed source: GPT-2, GPT-3, ChatGPT, Claude, Gemini
  - Open source: Llama, Mistral, Phi
- Essentially, transformer encoder + the causal mask, or transformer decoder without the encoder-decoder cross-attention layer. That’s it!
- What are the benefits and drawbacks of this design?

##### Summary

- Transformer model is proposed for the Machine Translation task.
  - It achieved best performance on machine translation and can be trained much faster than convolutional or recurrent NNs. 
  - It contains a transformer encoders 
  - and a transformer decoders (which is a slight variations of the encoders to consider the cross-attention and the unidirectional nature of the decoding process).
- The transformer is the first model that uses only attention as its underlying mechanism.
- <u>It is the dominant architecture for NLP models nowadays and the backbone for large pre-trained language models.</u>