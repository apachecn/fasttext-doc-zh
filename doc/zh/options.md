---
id: options
title: List of options
---

调用不带参数的命令来列出可用参数及其默认值:

```bash
$ ./fasttext supervised
空的输入或输出路径.

以下参数是强制性的:
  -input              训练文件路径
  -output             输出文件路径

  以下参数是可选的:
  -verbose            冗长等级 [2]

以下字典参数是可选的:
  -minCount           最少的词出现次数 [5]
  -minCountLabel      标签发生次数最少 [0]
  -wordNgrams         单词 ngram 的最大长度 [1]
  -bucket             桶的桶数 [2000000]
  -minn               min length of char ngram [3]
  -maxn               max length of char ngram [6]
  -t                  sampling threshold [0.0001]
  -label              labels prefix [__label__]

  以下用于训练的参数是可选的:
  -lr                 学习率 [0.05]
  -lrUpdateRate       更改学习率的更新率 100]
  -dim                字向量的大小 [100]
  -ws                 上下文窗口的大小 [5]
  -epoch              epochs 的数量 [5]
  -neg                抽样的负片数 [5]
  -loss               损失函数 {ns, hs, softmax} [ns]
  -thread             线程数 [12]
  -pretrainedVectors  pretrained Vectors 预训练词语向量监督学习[]
  -saveOutput         是否应该保存输出参数 [0]

 以下量化参数是可选的:
  -cutoff             要保留的字数和n gram 数量 [0]
  -retrain            微调嵌入如果应用截止 [0]
  -qnorm              分别量化范数 [0]
  -qout               量化分类器 [0]
  -dsub               每个子向量的子尺寸 [2]
```

默认值可能因模式而异. (Word-representation 模型 `skipgram` 和 `cbow` 使用 5. 作为 `-minCount` 的默认值)

