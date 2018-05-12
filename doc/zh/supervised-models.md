# 监督模型

这个页面收集了几个预先训练好的监督模型，其训练数据来自于几个不同的数据集。

### Description(描述)

常规模型使用 [1] 中描述的步骤进行训练. 可以使用我们 github 存储库中的 classification-results.sh 脚本来复现它们。通过使用相应的监督设置并将以下参数添加到量化子命令中来构建量化模型.

```bash
-qnorm -retrain -cutoff 100000
```

### Table of models(模型表格)

每个条目描述了模型的测试精度和大小。 您可以单击表格单元格来下载相应的模型.

| 数据集 | ag 新闻 | 亚马逊评论全部 | 亚马逊评论极性 | dbpedia |
|-----------|-----------------------|-----------------------|------------------------|------------------------|
| regular   | [0.924 / 387MB](https://s3-us-west-1.amazonaws.com/fasttext-vectors/supervised_models/ag_news.bin) | [0.603 / 462MB](https://s3-us-west-1.amazonaws.com/fasttext-vectors/supervised_models/amazon_review_full.bin) | [0.946 / 471MB](https://s3-us-west-1.amazonaws.com/fasttext-vectors/supervised_models/amazon_review_polarity.bin) | [0.986 / 427MB](https://s3-us-west-1.amazonaws.com/fasttext-vectors/supervised_models/dbpedia.bin) |
| compressed | [0.92 / 1.6MB](https://s3-us-west-1.amazonaws.com/fasttext-vectors/supervised_models/ag_news.ftz)    | [0.599 / 1.6MB]( https://s3-us-west-1.amazonaws.com/fasttext-vectors/supervised_models/amazon_review_full.ftz)   | [0.93 / 1.6MB]( https://s3-us-west-1.amazonaws.com/fasttext-vectors/supervised_models/amazon_review_polarity.ftz)  | [0.984 / 1.7MB]( https://s3-us-west-1.amazonaws.com/fasttext-vectors/supervised_models/dbpedia.ftz) |

| 数据集 | 搜狗新闻 | 雅虎回答 | yelp review 极性 | yelp 评论全部 |
|-----------|----------------------|------------------------|----------------------|------------------------|
| regular   | [0.969 / 402MB](https://s3-us-west-1.amazonaws.com/fasttext-vectors/supervised_models/sogou_news.bin) | [0.724 / 494MB](https://s3-us-west-1.amazonaws.com/fasttext-vectors/supervised_models/yahoo_answers.bin)| [0.957 / 409MB](https://s3-us-west-1.amazonaws.com/fasttext-vectors/supervised_models/yelp_review_polarity.bin)| [0.639 / 412MB](https://s3-us-west-1.amazonaws.com/fasttext-vectors/supervised_models/yelp_review_full.bin)|
| compressed | [0.968 / 1.4MB](https://s3-us-west-1.amazonaws.com/fasttext-vectors/supervised_models/sogou_news.ftz)   | [0.717 / 1.6MB](https://s3-us-west-1.amazonaws.com/fasttext-vectors/supervised_models/yahoo_answers.ftz)       | [0.957 / 1.5MB](https://s3-us-west-1.amazonaws.com/fasttext-vectors/supervised_models/yelp_review_polarity.ftz) | [0.636 / 1.5MB](https://s3-us-west-1.amazonaws.com/fasttext-vectors/supervised_models/yelp_review_full.ftz)  |

### References(参考)

如果您使用这些模型, 请引用以下文章:

[1] A. Joulin, E. Grave, P. Bojanowski, T. Mikolov, [*Bag of Tricks for Efficient Text Classification*](https://arxiv.org/abs/1607.01759)

```markup
@article{joulin2016bag,
  title={Bag of Tricks for Efficient Text Classification},
  author={Joulin, Armand and Grave, Edouard and Bojanowski, Piotr and Mikolov, Tomas},
  journal={arXiv preprint arXiv:1607.01759},
  year={2016}
}
```

[2] A. Joulin, E. Grave, P. Bojanowski, M. Douze, H. Jégou, T. Mikolov, [*FastText.zip: 压缩文本分类模型*](https://arxiv.org/abs/1612.03651)

```markup
@article{joulin2016fasttext,
  title={FastText.zip: Compressing text classification models},
  author={Joulin, Armand and Grave, Edouard and Bojanowski, Piotr and Douze, Matthijs and J{\'e}gou, H{\'e}rve and Mikolov, Tomas},
  journal={arXiv preprint arXiv:1612.03651},
  year={2016}
}
```
