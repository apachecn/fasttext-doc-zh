---
id: language-identification
title: Language identification
---

### 说明

我们发布了两种语言识别模型，可以识别176种语言（请参阅下面的ISO代码列表）。 这些模型是通过 [Wikipedia](https://www.wikipedia.org/) ， [Tatoeba](https://tatoeba.org/eng/)和 [SETimes](http://nlp.ffzg.hr/resources/corpora/setimes/) 的数据进行训练，在 [CC-BY-SA](http://creativecommons.org/licenses/by-sa/3.0/) 下使用。

我们发布两个版本的模型：

* [lid.176.bin](https://s3-us-west-1.amazonaws.com/fasttext-vectors/supervised_models/lid.176.bin) ，这个模型更快更准确，但有一个文件的大小有126MB;
* [lid.176.ftz](https://s3-us-west-1.amazonaws.com/fasttext-vectors/supervised_models/lid.176.ftz) ，这是个只有917kB的压缩版的模型。

这些模型都是使用UTF-8数据进行训练的，因此需要使用UTF-8作为输入。

### 许可

这些模型根据 [*Creative Commons Attribution-Share-Alike License 3.0*](https://creativecommons.org/licenses/by-sa/3.0/) 进行发布。

### 支持的语言列表
```
af als am ar ar as as ast av az azb ba bar bcl be bg bh bn bo bpy br bs bxr ca cbk ce ceb ckb co cs cv c cy cy de deqq dsb dty dv el eml en eo es et eu faf fr fr fyy ga gd gl gn gom gu gv he hi hif hr hsb ht hu hyia id ie ieo io is it ja jbo jv ka kk km kn ko krc ku kv kw ky la lb lez li lmo lo lrc lt lv mai mg mhr min mk ml mn mr mrj ms mt mwl my mym mzn nah nap nds ne new nl nn no oc or os pa pam pfl pl pms pnb ps pt qu rm ro ru rue sa sah scn sco sd sh si sl sl so sq sr su sv sw ta te tg th t t t tr t t tyv ug uk ur uz vec vep vi vls vo wa war wuu xal xmf yi yo yue zh
```

### 参考

如果您使用这些模型，请引用以下论文：

[1] A. Joulin, E. Grave, P. Bojanowski, T. Mikolov, [*Bag of Tricks for Efficient Text Classification*](https://arxiv.org/abs/1607.01759)
```
@article{joulin2016bag,
  title={Bag of Tricks for Efficient Text Classification},
  author={Joulin, Armand and Grave, Edouard and Bojanowski, Piotr and Mikolov, Tomas},
  journal={arXiv preprint arXiv:1607.01759},
  year={2016}
}
```
[2] A. Joulin, E. Grave, P. Bojanowski, M. Douze, H. Jégou, T. Mikolov, [*FastText.zip: Compressing text classification models* ](https://arxiv.org/abs/1612.03651)
```
@article{joulin2016fasttext,
  title={FastText.zip: Compressing text classification models},
  author={Joulin, Armand and Grave, Edouard and Bojanowski, Piotr and Douze, Matthijs and J{\'e}gou, H{\'e}rve and Mikolov, Tomas},
  journal={arXiv preprint arXiv:1612.03651},
  year={2016}
}
```
