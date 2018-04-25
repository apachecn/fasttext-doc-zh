---
id: supervised-tutorial
title: Text classification
---

文本分类是许多应用程序的核心问题，例如垃圾邮件检测，情感分析或智能回复。 在本教程中，我们将介绍如何使用fastText工具构建文本分类器。

## 什么是文本分类？

文本分类的目标是将文档（如电子邮件，博文，短信，产品评论等）分配给一个或多个类别。 这些类别可以是评论分数，垃圾邮件与非垃圾邮件的划分，或者文档的编写语言。 如今，构建这种分类器的主要方法是机器学习，即从样本中学习分类规则。 为了构建这样的分类器，我们需要标注数据，它由文档及其相应的类别（也称为标签或标注）组成。

作为一个例子，我们建立了一个分类器，该分类器将 [stack exchange](https://stackexchange.com/) 网站上有关烹饪的问题自动分类为几个可能的标签之一，例如`pot`，`bowl` 或 `baking`。

##  安装 fastText

本教程的第一步是安装并构建 fastText。 它只需要一个能够良好支持 c++11 的 c++ 编译器。

让我们从下载[最新版本](https://github.com/facebookresearch/fastText/releases)开始：

```bash
$ wget https://github.com/facebookresearch/fastText/archive/v0.1.0.zip
$ unzip v0.1.0.zip
```

移动到 fastText 目录并构建它:

```bash
$ cd fastText-0.1.0
$ make
```

运行二进制文件（不带任何参数）将打印高级文档，显示 fastText 支持的不同用例：

```bash
>> ./fasttext
usage: fasttext <command> <args>

The commands supported by fasttext are:

  supervised              训练一个监督分类器
  quantize                量化模型以减少内存使用量
  test                    评估一个监督分类器
  predict                 预测最有可能的标签
  predict-prob            用概率预测最可能的标签
  skipgram                训练一个 skipgram 模型
  cbow                    训练一个 cbow 模型
  print-word-vectors      给定一个训练好的模型，打印出所有的单词向量
  print-sentence-vectors  给定一个训练好的模型，打印出所有的句子向量
  nn                      查询最近邻居
  analogies               查找所有同类词

```

在本教程中，我们主要使用`supervised`，`test` 和 `predict` 子命令，它们对应于学习（和使用）文本分类器。 有关 fastText 其他功能的介绍，请参见[单词向量的教程](https://fasttext.cc/docs/en/unsupervised-tutorial.html)。

## 获取和准备数据

正如上述介绍中所提到的，我们需要标记数据来训练我们的监督分类器。 在本教程中，我们将构建一个分类器来自动识别烹饪问题的类别。 让我们从[Stack exchange 网站的烹饪部分](http://cooking.stackexchange.com/)下载问题示例及其相关标签：

```bash
>> wget https://s3-us-west-1.amazonaws.com/fasttext-vectors/cooking.stackexchange.tar.gz && tar xvzf cooking.stackexchange.tar.gz
>> head cooking.stackexchange.txt
```

文本文件的每一行都包含一个标签列表，其后是相应的文档。 所有标签都以 `__label__` 前缀开始，这就是 fastText 如何识别标签或单词是什么。 然后对模型进行训练，以预测给定文档的标签。

在训练我们的第一个分类器之前，我们需要将数据分为训练集和验证集。 我们将使用验证集来评估该学习分类器对新数据的适用程度。

```bash
>> wc cooking.stackexchange.txt 
   15404  169582 1401900 cooking.stackexchange.txt
```

我们的完整数据集包含 15404 样本。 我们将其分为拥有 12404 个样本的训练集和拥有 3000 个样本的验证集：

```bash
>> head -n 12404 cooking.stackexchange.txt > cooking.train
>> tail -n 3000 cooking.stackexchange.txt > cooking.valid
```

## 我们的第一个分类器

我们现在准备好训练第一个分类器了：

```bash
>> ./fasttext supervised -input cooking.train -output model_cooking
Read 0M words
Number of words:  14598
Number of labels: 734
Progress: 100.0%  words/sec/thread: 75109  lr: 0.000000  loss: 5.708354  eta: 0h0m 
```

命令行选项 `-input` 指示包含训练样本的文件，而选项 `-output` 指示保存模型的位置。 训练结束时，在当前目录中创建一个 `model_cooking.bin` 文件，其中包含了已经训练好的模型。

可以通过命令行直接交互式地测试分类器：

```bash
>> ./fasttext predict model_cooking.bin -
```

然后输入一个句子。我们来试一下：

*Which baking dish is best to bake a banana bread ?*

其预测的标签是 `baking`，非常贴切。 现在让我们尝试第二个例子：

*Why not put knives in the dishwasher?*

模型预测出的标签是 `food-safety`，这是不相关的。 不知何故，这个模型似乎在简单的例子上反而失败了。 为了更好地了解其预测质量，我们通过运行以下验证数据对其进行测试：

```bash
>> ./fasttext test model_cooking.bin cooking.valid                 
N  3000
P@1  0.124
R@1  0.0541
Number of examples: 3000
```

只给定一个真实标签用于预测，fastText 的输出是精确度 (`P@1`) 和 召回率 (`R@1`)。我们也可以计算给定五个真实标签用于预测的精确度和召回率：

```bash
>> ./fasttext test model_cooking.bin cooking.valid 5               
N  3000
P@5  0.0668
R@5  0.146
Number of examples: 3000
```

## 高级读者：精确度和召回率

精确度是由 fastText 所预测标签中正确标签的数量。 召回率是所有真实标签中被成功预测出的标签数量。 我们举一个例子来说明这一点：

*Why not put knives in the dishwasher?*

在 Stack Exchange 上，这句话标有三个标签：`equipment`，`cleaning` 和 `knives`。 模型预测出的标签前五名可以通过以下方式获得：

```bash
>> ./fasttext predict model_cooking.bin - 5
```

前五名是 `food-safety`, `baking`, `equipment`, `substitutions` and `bread`.

因此，模型预测的五个标签中有一个是正确的，精确度为 0.20。 在三个真实标签中，只有 `equipment` 一个被该模型预测出，召回率为 0.33。

更多详细信息，请参阅[相关维基百科页面](https://en.wikipedia.org/wiki/Precision_and_recall)。

## 使模型更好

使用缺省参数运行 fastText 所获得的模型在分类新问题时非常糟糕。 让我们尝试通过更改默认参数来提高性能。

### 预处理数据

看看这些数据，我们发现有些单词包含大写字母或标点符号。 提高我们模型性能的第一步之一是应用一些简单的预处理。 粗略的标准化可以通过命令行工具获得，例如`sed`和 `tr`：

```bash
>> cat cooking.stackexchange.txt | sed -e "s/\([.\!?,'/()]\)/ \1 /g" | tr "[:upper:]" "[:lower:]" > cooking.preprocessed.txt
>> head -n 12404 cooking.preprocessed.txt > cooking.train
>> tail -n 3000 cooking.preprocessed.txt > cooking.valid 
```

让我们在被预处理过的数据上训练一个新的模型吧：

```bash
>> ./fasttext supervised -input cooking.train -output model_cooking
Read 0M words
Number of words:  9012
Number of labels: 734
Progress: 100.0%  words/sec/thread: 82041  lr: 0.000000  loss: 5.671649  eta: 0h0m h-14m 

>> ./fasttext test model_cooking.bin cooking.valid 
N  3000
P@1  0.164
R@1  0.0717
Number of examples: 3000
```

我们观察到，由于预处理，词汇量更小（从 14k 到 9k）。精确度也开始上升4％！

### 更多的迭代和更快的学习速率

默认情况下，由于我们的训练集只有 12k 个训练样本，因此 fastText 在训练过程中仅看到每个训练样例五次，这太少了。 可以使用 -epoch 选项增加每个示例出现的次数（也称为迭代数）：

```bash
>> ./fasttext supervised -input cooking.train -output model_cooking -epoch 25 
Read 0M words
Number of words:  9012
Number of labels: 734
Progress: 100.0%  words/sec/thread: 77633  lr: 0.000000  loss: 7.147976  eta: 0h0m
```

让我们测试一下新模型：

```bash
>> ./fasttext test model_cooking.bin cooking.valid                                        
N  3000
P@1  0.501
R@1  0.218
Number of examples: 3000
```

这好多了！ 另一种改变我们模型学习速度的方法是增加（或减少）算法的学习速率。 这对应于处理每个样本后模型变化的幅度。 学习率为 0 意味着模型根本不会改变，因此不会学到任何东西。好的学习速率在 `0.1 - 1.0` 范围内。

```bash
>> ./fasttext supervised -input cooking.train -output model_cooking -lr 1.0  
Read 0M words
Number of words:  9012
Number of labels: 734
Progress: 100.0%  words/sec/thread: 81469  lr: 0.000000  loss: 6.405640  eta: 0h0m

>> ./fasttext test model_cooking.bin cooking.valid                         
N  3000
P@1  0.563
R@1  0.245
Number of examples: 3000
```

更好了！我们试试学习速率和迭代次数两个参数一起变化：

```bash
>> ./fasttext supervised -input cooking.train -output model_cooking -lr 1.0 -epoch 25
Read 0M words
Number of words:  9012
Number of labels: 734
Progress: 100.0%  words/sec/thread: 76394  lr: 0.000000  loss: 4.350277  eta: 0h0m

>> ./fasttext test model_cooking.bin cooking.valid                                   
N  3000
P@1  0.585
R@1  0.255
Number of examples: 3000
```

现在让我们多添加一些功能来进一步提高我们的性能！

### word n-grams

最后，我们可以通过使用 word bigrams 而不是 unigrams 来提高模型的性能。 这对于词序重要的分类问题尤其重要，例如情感分析。

```bash
>> ./fasttext supervised -input cooking.train -output model_cooking -lr 1.0 -epoch 25 -wordNgrams 2
Read 0M words
Number of words:  9012
Number of labels: 734
Progress: 100.0%  words/sec/thread: 75366  lr: 0.000000  loss: 3.226064  eta: 0h0m 

>> ./fasttext test model_cooking.bin cooking.valid                                                 
N  3000
P@1  0.599
R@1  0.261
Number of examples: 3000
```

只需几个步骤，我们就可以从 12.4％ 到达 59.9％ 的精度。 重要步骤包括：

* 预处理数据 ;
* 改变迭代次数 (使用选项 `-epoch`, 标准范围 `[5 - 50]`) ;
* 改变学习速率 (使用选项 `-lr`, 标准范围 `[0.1 - 1.0]`) ;
* 使用 word n-grams (使用选项 `-wordNgrams`, 标准范围 `[1 - 5]`).

## 高级读者: 什么是 Bigram?

'unigram' 指的是单个不可分割的单位或标记，通常用作模型的输入。 例如，根据模型的不同，'unigram' 可以是单词或字母。 在 fastText 中，我们在单词级别工作，因此 unigrams 是单词。

类似地，我们用 'bigram' 表示2个连续标记或单词的连接。 类似地，我们经常谈论 n-gram 来引用任意 n 个连续标记或单词的级联。

例如，在 'Last donut of the night' 这个句子中，unigrams是 'last'，'donut'，'of'，'the' 和 'night'。 bigrams 是 'Last donut', 'donut of', 'of the' 和 'the night'。

Bigrams 特别有趣，因为对于大多数句子，只需查看 n-gram 的集合即可重建句子中单词的顺序。

让我们通过一个简单的练习来说明这一点，给定以下 bigrams，试着重构原始的句子：'all out'，'I am'，'bubblegum'，'out of' 和 'all all'。
通常将一个单词称为一个 unigram。

## Scaling things up

Since we are training our model on a few thousands of examples, the training only takes a few seconds. But training models on larger datasets, with more labels can start to be too slow. A potential solution to make the training faster is to use the hierarchical softmax, instead of the regular softmax [Add a quick explanation of the hierarchical softmax]. This can be done with the option `-loss hs`:
由于我们正在通过几千个示例来训练我们的模型，所以训练只需几秒钟。但是在更大的数据集上训练模型，使用更多的标签可能会太慢。 使训练更快的潜在解决方案是使用分层softmax，而不是常规softmax [添加分层softmax的快速解释]。 这可以通过选项'-loss hs`完成：
```bash
>> ./fasttext supervised -input cooking.train -output model_cooking -lr 1.0 -epoch 25 -wordNgrams 2 -bucket 200000 -dim 50 -loss hs
Read 0M words
Number of words:  9012
Number of labels: 734
Progress: 100.0%  words/sec/thread: 2199406  lr: 0.000000  loss: 1.718807  eta: 0h0m 
```

Training should now take less than a second.

## Conclusion

In this tutorial, we gave a brief overview of how to use fastText to train powerful text classifiers. We had a light overview of some of the most important options to tune.
