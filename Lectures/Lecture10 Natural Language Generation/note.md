# Natural Language Generation (NLG)

## What is NLG

> NLP = Natural LAnguage Understanding (NLU) + Natural Language Generation (NLG)

## Uses of NLG

- machine translation systems
- digital assistant systems
- summarization systems
- ChatGPT ...

## Some Problems

### Repitition

**Simple solution**: avoid repeated n-grams.

**Complex solutions**:

- use a different training objective
  - *Unlikelihood objective* penalize generation of already-seen tokens
  - *Coverage loss* prevents attention mechanism from attending to the same words.
- use a different decoding objective
  - *Contrastive decoding* searches for strings x that maximize $\log_{prob_largeLM}(x) - \log_{prob_smallLM}(x)$

### Open-ended Generation

对于更开放的语句生成（如讲故事），使用 greedy 或 beam search 效果不一定好（结果太单一了）。可以对生成的概率分布使用

- Top-k sampling: 选取概率最高的 k 个样本，从中进行随机取样。缺点是当概率分布较集中或较分散时效果不好
- Top-p sampling: 预先规定一个概率 p，从概率高到低相加直到超过 p，这时对选取到的样本进行随机取样
- More solutions
- ...

## Temperature

在使用 softmax 计算概率分布时，引入参数 $\tau$：

$$
P_t(y_t = w) = \frac{\exp(S_w / \tau)}{\sum_{w' \in V} \exp(S_{w'} / \tau)}
$$

- 当 $\tau > 1$ 较大时，分布更均匀，输出更多样化
- 当 $\tau < 1$ 较小时，分布更集中，输出更单一化

## Reward Estimation

**reward function**:

- BLEU (machine translation, but bad for more open-ended tasks)
- ROUGE (summarization)
- CIDEr (image captioning)
- SPIDEr (image captioning)
- ...

总的来说，可以分为：

- 基于 n-gram 的 word matching
- 基于特定的 model 的，例如 vector similarity / word mover's distance / BERT score / sentence mover's similarity / BLEURT
- ...