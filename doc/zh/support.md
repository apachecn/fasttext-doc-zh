---
id: support
title: Get started
---

## 什么是快速文本?

fastText是一个用于高效学习单词表示和句子分类的库.

## 要求

fastText建立在现代 Mac OS 和 Linux 发行版上.
由于它使用C ++ 11功能, 因此需要具有良好C ++ 11支持的编译器.
这些包括:

* (gcc-4.6.3 or newer) or (clang-3.3 or newer)

使用 Makefile 进行编译, 因此您需要有一个可行的 **make**. 对于单词相似性评估脚本, 您需要:

* python 2.6 or newer
* numpy & scipy

## 建立快速文本


为了构建 `fastText`, 请使用以下内容:

```bash
$ git clone https://github.com/facebookresearch/fastText.git
$ cd fastText
$ make
```

这将产生所有类以及主二进制文件的目标文件 `fasttext`.
如果您不打算使用默认的系统范围编译器, 请更新 Makefile 开头定义的两个宏 (CC 和 INCLUDES).

