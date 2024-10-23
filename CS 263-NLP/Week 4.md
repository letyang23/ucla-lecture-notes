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