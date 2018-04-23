---
id: cheatsheet
title: Cheatsheet
---

## Word representation learning(词表示学习)

为了学习单词向量:

```bash
$ ./fasttext skipgram -input data.txt -output model
```

## Obtaining word vectors(获取单词向量)

为 `queries.txt` 包含单词的文本文件打印单词向量.

```bash
$ ./fasttext print-word-vectors model.bin < queries.txt
```

## Text classification(文本分类)

为了训练一个文本分类器, 请执行以下操作:

```bash
$ ./fasttext supervised -input train.txt -output model
```

一旦模型被训练完毕, 您可以使用以下公式计算测试集上的k (P@k and R@k) 的精准和召回来评估它:

```bash
$ ./fasttext test model.bin test.txt 1
```

为了获得一段文字的k个最可能的标签，使用:

```bash
$ ./fasttext predict model.bin test.txt k
```

为了获得一段文字的k个最可能的标签及其相关概率,请使用:

```bash
$ ./fasttext predict-prob model.bin test.txt k
```

如果你想计算句子或段落的向量表示, 请使用:

```bash
$ ./fasttext print-sentence-vectors model.bin < text.txt
```

## Quantization(量化)

为了创建一个 `.ftz` 内存占用量较小的文件, 请执行以下操作:

```bash
$ ./fasttext quantize -output model
```

所有其他命令（如测试）也适用于此模型

```bash
$ ./fasttext test model.ftz test.txt
```
