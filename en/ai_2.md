## 2. Basic ideas of modern language models

### Historical context and basic concepts
Neural networks were created as a way to teach a machine to approximate complex dependencies in data. The simplest element - the perceptron - takes input features, weights them, adds a bias, and checks whether a threshold is crossed. A single perceptron gives only linear separation, but a multilayer perceptron (MLP) with nonlinearities can approximate almost any function.

Weights are adjusted automatically with backpropagation: the network compares its prediction with the correct value and step by step adjusts parameters to reduce the loss.

Language needs one more step - turning text into numbers. Tokenization does this: it splits text into tokens, most often subwords. This makes the system robust to rare or new words. Then tokens are projected into high‑dimensional vectors (embeddings). The semantic intuition is simple: words close in meaning have close vectors; the geometry encodes similarity and associations.

For a long time, recurrent networks (RNN) and their variants LSTM/GRU dominated. They read the sequence token by token, keeping a hidden state as “memory.” In practice this often broke on long‑range dependencies (vanishing or exploding gradients), and more importantly, computation was sequential and scaled poorly on modern hardware. This is where transformers offered a new path.

### Fundamental principles of transformers
First of all, a transformer is an autocompletion model: given a sequence of tokens, it estimates the probability distribution of the next token and chooses the most likely one. Then this predicted token is appended to the sequence, and the process repeats step by step until we get a complete result. How does it guess the next token? The key is the attention mechanism, which lets the model focus on relevant parts of the context.

Before each new step, every word in the sentence looks at all the others and decides whom to consider and by how much. The word formulates its “question”: what do I need right now? This is the query (Q). Each other word has a “label” that says what it is about - the key (K). And it has “content” it can contribute - the value (V). Attention computes “how much” weights between the current word’s question and the labels of the others, and then mixes their content according to these weights. The result is a new representation of the word that has taken relevant context into account.

A simple example without formulas. “Ivan bought oranges. They were ripe.” For the word “They,” the most useful is to look at “oranges,” so the attention weight to “oranges” will be the largest; to “Ivan” - smaller; to function words - smaller still. The new representation of the token “They” becomes a weighted mixture of the contents of other words, where “content” is what the word can “pass” (the value, V).

From here follow the components and dimensions (short and with an example). We have the matrix of token representations X of size n×d_model (n is sequence length, d_model is the vector size of a token representation, typically 512–4096 numbers, the “width” of a layer).

For simplicity, take one attention “head” with dimension d_head (the “width” of one head’s subspace: how many numbers a Q/K/V vector has for this head, typically 64–128). An attention head is a separate “channel” with its own weight matrices W_Q, W_K, W_V (each of size d_model×d_head for this head) - these are the parameters the model learns during training. Such a head “catches” its own type of dependencies.

This can be written for one attention head as:

$$
A = \mathrm{softmax}\!\left(\frac{QK^{\top}}{\sqrt{d_{head}}}\right),\quad \text{out} = A\,V.
$$

The product QK^T gives the “similarities” between queries and keys: how much my “what do I need?” matches your “what are you about?”. Division by √d_head keeps numbers in a reasonable range so softmax does not wipe out small differences. Softmax over rows turns similarities into weights from 0 to 1 that sum to 1 - that is, “how much trust” we allocate to each word. Multiplying A by V takes a weighted mixture of their contents - we get the same “context taken into account.”

In multi‑head attention, several heads work in parallel in different subspaces, their outputs are concatenated and passed through an output linear projection W_O (of size H·d_head×d_model), which returns the dimension back to d_model. Then a residual connection and layer normalization are added, after which the result goes through a small MLP and again gets a residual connection with normalization. At the end, the last layer’s representation is projected to the vocabulary size and softmax gives the probability distribution of the next token.

The key advantage of the transformer is full parallelization over tokens during training: we do not need to process the sequence step by step, we can compare everything with everything at once. This improves modeling of long‑range dependencies and opens the door to efficient scaling. Empirical scaling laws show that quality grows systematically as we increase parameters, data, and compute in the right proportions. In practice this is done through different forms of parallelism (data/model/pipeline/tensor), mixed precision (FP16/BF16 instead of 32‑bit for speed), optimizer sharding, and checkpointing. At the same time, careful data preparation and corpus balance are often no less important than extra FLOPs (floating‑point operations - a measure of compute power).

The cost of self‑attention grows quadratically with context length: twice the window is roughly four times the compute and memory. Therefore, extending context needs engineering: relative positional encodings, caching/buffering, and sparse or local attention. In applied systems this is complemented by external knowledge search (RAG - Retrieval‑Augmented Generation) and caching so we do not push everything into the model at once.

### Limitations and future directions
Despite breakthrough abilities with language, LLMs have systemic limits. They are prone to “hallucinations” - confidently generating falsehoods in zones of uncertainty; they are sensitive to prompt wording; they lack built‑in fact‑checking. The most noticeable limitation is a lack of true long‑term memory: anything beyond the context window is lost, so the model does not “remember” the user or a long process in a strict sense. Cost and energy, bias, safety and privacy, and limited planning and reasoning without tools also matter.

Promising directions include integration of external memory and knowledge indexes (RAG, personal stores), new attention schemes with lower complexity, compression and recurrent memory over long ranges, more reliable validation of statements (source checking, self‑assessment of confidence). Critically important is post‑deploy learning: safe loops for continual learning, online updates of knowledge, and guided RLHF in production. Integration with tools and agents is also growing actively, allowing the model to act in the world and not only generate text.

### Summary
Transformer LLMs are a technological breakthrough on the level of the first computers or the Internet. They learned to see long‑range dependencies, scale across clusters, and work with language in ways that seemed impossible not long ago. But this is likely not the last step on the path to real AGI (artificial general intelligence). To move from “large autocompletion” to broad reasoning ability, we need true long‑term memory, safe post‑deploy learning, and new inductive biases for reliable planning and reasoning. The breakthrough has already happened; now it is time for the next ones.


### Sources and further reading

- [Attention Is All You Need](https://arxiv.org/abs/1706.03762) - A. Vaswani et al., 2017.
- [The Illustrated Transformer](https://jalammar.github.io/illustrated-transformer/) - J. Alammar, 2018.
- [Language Models are Few-Shot Learners](https://arxiv.org/abs/2005.14165) - T. Brown et al., 2020.
- [Scaling Laws for Neural Language Models](https://arxiv.org/abs/2001.08361) - J. Kaplan et al., 2020.
- [Training Compute-Optimal Large Language Models](https://arxiv.org/abs/2203.15556) - J. Hoffmann et al., 2022.
- [SentencePiece: A simple and language independent subword tokenizer and detokenizer for Neural Text Processing](https://arxiv.org/abs/1808.06226) - T. Kudo, J. Richardson, 2018.
- [Neural Machine Translation of Rare Words with Subword Units](https://arxiv.org/abs/1508.07909) - R. Sennrich, B. Haddow, A. Birch, 2016.
- [Efficient Transformers: A Survey](https://arxiv.org/abs/2009.06732) - Y. Tay, M. Dehghani, D. Bahri, 2020.
- [Retrieval-Augmented Generation for Knowledge-Intensive NLP](https://arxiv.org/abs/2005.11401) - P. Lewis et al., 2020.
- [Training language models to follow instructions with human feedback](https://arxiv.org/abs/2203.02155) - L. Ouyang et al., 2022.
- [Constitutional AI: Harmlessness from AI Feedback](https://arxiv.org/abs/2212.08073) - Y. Bai et al., 2022.
- [3Blue1Brown: Neural network](https://www.youtube.com/watch?v=aircAruvnKk&list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi) - 3Blue1Brown video series about neural networks


