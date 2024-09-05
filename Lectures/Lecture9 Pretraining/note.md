# Pretraining

## BPE 算法

由于 word modeling 对大多数语言不适用（因为往往会遇到 unknown word，不好处理），但是一些语言（例如英语），有一些从 character 到 word 的构词法，可以考虑 "subword modeling"。使用 BPE (Byte-Pair Encoding) 算法可以自动得出需要的 subword。

## Pretraining 对象

有两种 pretraining 的方式：

- 预训练 word embedding，缺点是训练出来的 word embedding 可能对下游任务不适用
- 预训练 whole model，可以通过和下游任务对接，进行 transfer learning 进行调整。例如对于 BERT，可以先使用简单的 mask-predict 任务进行预训练，然后对接下游任务。

## Pretraining 方式

### Encoder Only

例如 BERT，由于 encoder 会获取前后文信息，可以使用 Masked LM 任务：

![](https://cdn.jsdelivr.net/gh/KinnariyaMamaTanha/Images@main/202409040949173.png)

一些 BERT 的变体：

- RoBERTa: train BERT for longer and remove next sentence prediction
- SpanBERT: masking contiguous spans of words makes a harder, more useful pretraining task

由于 finetuning 整个模型对内存要求较高，也可以使用 parameter-efficient finetuning 方法，例如 lightweight finetuning, prefix-finetuning, prompt tuning 等。也可以使用 low-rank adaptation 等方法。

### Encoder-Decoder

类似 language modeling，不过提供一个不被预测的 **prefix** 给 encoder，需要被预测的 sentence 给 decoder：

![](https://cdn.jsdelivr.net/gh/KinnariyaMamaTanha/Images@main/202409041004284.png)

可用于问答系统等。

### Decoder Only

可以用作 language modeling，不能“见到” future words，预训练后可参与语句生成等任务，GPT 是代表之一。