# Attention is all you need
## 不知道的点
- dominant sequence transduction models
Transformer 作为"主导的序列转导模型"（dominant sequence transduction models）
在原始 Transformer 论文中，有一个非常经典的表述：
"Transformers are dominant sequence transduction models" 
"Sequence transduction"（序列转导/序列转换）指的是将一个序列转换为另一个序列的任务，比如机器翻译（源语言序列 → 目标语言序列）。
在 Transformer 出现之前，RNN/LSTM/GRU 是 NLP 中处理这类任务的主流架构。Transformer 通过纯注意力机制取代了递归结构，成为了序列转导任务的主导架构（dominant architecture）。

什么是 Sequence Transduction（序列转导/序列转换）？
Sequence transduction 指的是将一个输入序列映射到另一个输出序列的任务。这个词在 NLP 中比 "sequence-to-sequence" 更正式一些，但含义基本相同。

| 任务   | 输入序列               | 输出序列        |
| ---- | ------------------ | ----------- |
| 机器翻译 | "Hello world" (英文) | "你好世界" (中文) |
| 语音识别 | 音频特征序列             | 文本序列        |
| 文本摘要 | 长文章                | 短摘要         |
| 对话生成 | 用户问题               | 系统回复        |


为什么用 "dominant"（主导的）？
在 2017 年 Transformer 提出之前，序列转导任务的主流（主导）架构是：
1. RNN/LSTM/GRU（循环神经网络）
按时间步逐个处理 token
天然适合序列，但无法并行化，训练慢
长距离依赖困难（梯度消失）
2. CNN（卷积神经网络）
用卷积核捕捉局部模式
可以并行，但感受野有限，长距离依赖需要很多层
3. Encoder-Decoder + Attention
最好的模型还会在编码器和解码器之间加入注意力机制（如 Bahdanau attention、Luong attention）
但注意力只是辅助，核心仍然是 RNN/CNN

BLEU（Bilingual Evaluation Understudy）
BLEU 是一种自动评估机器翻译质量的指标，由 IBM 在 2002 年提出。
核心思想
BLEU 通过比较机器翻译输出与一个或多个人工参考翻译之间的n-gram 重叠度来打分。
具体计算
统计机器输出中 1-gram、2-gram、3-gram、4-gram 与参考翻译匹配的比例
加入简短惩罚（brevity penalty）：防止模型输出过短的句子来获得高分
最终得分范围：0 ~ 1（或表示为 0 ~ 100）

| BLEU 分数 | 质量水平            |
| ------- | --------------- |
| < 10    | 很差，几乎不可读        |
| 10-20   | 勉强可懂            |
| 20-30   | 可以理解，但有不少错误     |
| 30-40   | 质量较好            |
| 40-50   | 质量很好，接近人类水平     |
| > 50    | 非常流畅，难以区分是否人工翻译 |

Transformer 在 WMT 2014 英德翻译上达到 28.4 BLEU，在当时是显著突破——比之前最好的结果（包括集成模型）高出 2 个 BLEU 以上。

## 神经网络学习
### 神经网络科普
zhuanlan.zhihu.com/p/404173054
### RNN
zhuanlan.zhihu.com/p/112998607
#### 问题
- RNN中输入和输出序列必须是等长的，怎么理解？
这是因为在经典的RNN结构图中，RNN随着时间步展开，确实是输入一个xt就立刻输出一个yt 。在这种最原始的单层结构下，输入和输出确实是等成的，这里的序列是指时间序列x和y。

