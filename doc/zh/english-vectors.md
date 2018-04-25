---
id: english-vectors
title: English word vectors
---

这一篇整合了一些之前用 fasttext 训练的词向量。

### 下载经过训练的词向量

你可以从下面下载单词向量，他们基于学习不同的数据来源，并且被预先训练过：

1. [wiki-news-300d-1M.vec.zip](https://s3-us-west-1.amazonaws.com/fasttext-vectors/wiki-news-300d-1M.vec.zip) :一百万的词向量，这些词向量是在 2017 维基百科，UMBC 基于网络的语料库和 statmt.org 新闻数据集训练得到的(16B)
2. [wiki-news-300d-1M-subword.vec.zip](https://s3-us-west-1.amazonaws.com/fasttext-vectors/wiki-news-300d-1M-subword.vec.zip) : 一百万的带有子词信息的词向量，这些词向量是在 2017 维基百科，UMBC 基于网络的语料库和 statmt.org 新闻数据集的训练得到的(16B)

3. [crawl-300d-2M.vec.zip](https://s3-us-west-1.amazonaws.com/fasttext-vectors/crawl-300d-2M.vec.zip) : 两百万的词向量，这些词向量是在 Common Crawl 上训练得到的。(600B)

### 格式

文件的第一行包含了词汇表中单词的数量以及向量的大小。
每一行包含了一个单词和它的向量，就像是 fasttext 文本格式默认的那种样子。
每个值都是由空格隔开。
单词是按照频数降序排列的。

### 许可证明

这些词向量在 [*Creative Commons Attribution-Share-Alike License 3.0*](https://creativecommons.org/licenses/by-sa/3.0/) 可以看到。

### 参考资料

如果你使用了这些词向量，请引用下面的文章：

T. Mikolov, E. Grave, P. Bojanowski, C. Puhrsch, A. Joulin. [*Advances in Pre-Training Distributed Word Representations*](https://arxiv.org/abs/1712.09405)

```markup
@inproceedings{mikolov2018advances,
  title={Advances in Pre-Training Distributed Word Representations},
  author={Mikolov, Tomas and Grave, Edouard and Bojanowski, Piotr and Puhrsch, Christian and Joulin, Armand},
  booktitle={Proceedings of the International Conference on Language Resources and Evaluation (LREC 2018)},
  year={2018}
}
```
