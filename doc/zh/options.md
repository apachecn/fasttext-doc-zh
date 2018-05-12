# 选项列表

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
  -minCount           词出现的最少次数 [5]
  -minCountLabel      标签出现的最少次数 [0]
  -wordNgrams         单词 ngram 的最大长度 [1]
  -bucket             桶的个数 [2000000]
  -minn               char ngram 的最小长度 [3]
  -maxn               char ngram 的最大长度 [6]
  -t                  抽样阈值 [0.0001]
  -label              标签前缀 [__label__]

以下用于训练的参数是可选的:
  -lr                 学习速率 [0.05]
  -lrUpdateRate       更改学习速率的更新速率 100]
  -dim                字向量的大小 [100]
  -ws                 上下文窗口的大小 [5]
  -epoch              迭代次数 [5]
  -neg                负样本个数 [5]
  -loss               损失函数 {ns, hs, softmax} [ns]
  -thread             线程个数 [12]
  -pretrainedVectors  监督学习的预训练词向量 []
  -saveOutput         是否应该保存输出参数 [0]

以下量化参数是可选的:
  -cutoff             要保留的词和 ngram 的数量 [0]
  -retrain            微调 embeddings（假如应用 -cutoff 参数的话） [0]
  -qnorm              分别量化范数 [0]
  -qout               量化分类器 [0]
  -dsub               每个子向量的大小 [2]
```

默认值可能因模式而异。 (Word-representation 模型 `skipgram` 和 `cbow` 使用 5 作为 `-minCount` 的默认值)

