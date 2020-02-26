# Language modeling

## Application of LMs

* Word likelihood for query completion in information retrieval 信息检索中查询完成的词似然
* Language detection 语言检测
* Grammatical error detection (“You’re welcome” or “Your welcome”?) 语法错误检测
* Speech recognition (“I was tired too.” or “I was tired two.”?) 语音识别

## Problem setup 问题设定

* 训练数据经常是一个很大的句子集合x^m 里面有单词x_n:

![]()

## Calculate sentence probabilities 计算句子概率

我们想要学习一个模型，这个模型能够返回一个没见过的句子x的概率

![]()

## Unigram language model 一元语言模型

* 计算整个语料库中每个单词出现在句子x中的概率：

![3]()

**Note: "s" 可能也被算进去了**



## What could go wrong?

![]()

* 最有可能的字是"<s>" (3/3 = 1)
* 最有可能的单字句子是"<s>"

* 最有可能的两个字句子是"<s><s>"
* 最有可能的N-word 句子是 N *"<s>"

## Maximum Likelihood Estimation

* 我们假设每个单词都依赖于先前所有单词：

![5]()

哪里错了？

## 最大似然估计

![6]()

* 当我们以更多的单词为条件时，计数变得稀疏

## Bigram 语言模型2-gram

* 假设选择一个单词只取决于在它之前的那一个单词

![7]()

### From counts to probabilities: 从计数到概率

![8]()

* 从二元数计数矩阵中，通过将每个像小块除以其行的合适的字母组合计数来计算概率。

![9]()

## Example: Bigram language model

![10]()

## Longer contexts(N-gram LMs)

![11]()

* 文本越长：the more likely to capture long-range dependencies更可能捕获长期依赖
  * “I saw a tiger that was really very...” fierce or talkative
  * 稀疏计数（零概率）
  *  5-gram和数十亿个术语的训练集是常见的

## Unknown words(未知的单词)

* 如何一个单词从来没有出现在训练集，那么任何句子包含它的概率为0
* 它会发生是因为：
  * 所有语料库都是有限的
  * 出现了新的单词
* 常见的解决方案：
  * 通过用特殊的UNKNOWN词汇替换低频词，在训练数据中生成未知词
  * 使用类别不明的单词 e.g. 名字和数字

## Implementation details(实施细节)

* 处理大型数据集需要效率
  * 使用日志概率避免下溢（数量少）
  * 用于稀疏计数的高效数据结构，例如 有损数据结构Bloom过滤器）

* 我们如何训练和评估我们的语言模型？
  * 我们需要训练/开发/测试数据
  * 评估方法

## Intrinsic Evaluation: Accuracy 内部评估：准确性

* How well does our LM predict the next word? 我们的语言模型预测下一个单词有多好?
* Accuracy: how often the LM predicts the correct word
* The higher the better

## Intrinsic evaluation: Perplexity:困惑度： （如果每个时间步都根据语言模型计算的概率分布随机挑词，那么平均情况下，挑多少个词才能挑到正确的那个）

![12]()



* 测量预测一个样本一个概率分布为多好
* 越低越好

**为什么一个bigram的语言模型的困惑度会比unigram语言模型低？**

Answer: **There is more context to predict the next word!**

## 困惑度的问题

![13]()

* 并不总是与应用程序性能相关
* 无法评估非概率语言模型



## 外在评价

* 句子完成
* 语法错误纠正：检测“奇怪”句子并提出替代方案
* 自然语言产生：喜欢更自然的句子
* 语音识别
* 机器翻译

## Smoothing: 平滑处理

* 当我们词汇中的单词在测试数据中出现未见过的文本内容时会发生什么？
* 他们会被赋值为出现可能性为0
* Smoothing or discounting能挽救：从富人哪里偷并给穷人

![14]()

## Add-1 Smoothing 加-1平滑处理

* Add-1 smoothing加1给了所有的bigram计数

![15]()

* 假装我们见过所有的bigram词一次

## Add-k Smoothing

* Add-1 分配太多的概率质量给未见过的bigram组合，最好用add-k, k<1

![16]()

* **k是一个超参数：在开发集上选择最佳值！**

## Interpolation: 插值

* 较长的文本更有用
* "dog bites。。。"比 "bites。。。"要好
* 但只有在他们足够频繁的情况下：
* canid(犬科动物)bites 比 bites要好
* 我们可以结合单字，二元和三字概率的证据吗？

## 简单线性插值

对一个trigram语言模型

![17]()

* unigram，bigram和trigram概率的加权平均值
* 我们如何选择λs的值？ 在开发集上进行参数调整！

## Backoff(平衡策略方法) 

Backoff: 基本思想是若某个n-gram并没有在语料中找到，那么就计算(n-1)gram的count值作为该ngram的估计。然后引入 ![[公式]](https://www.zhihu.com/equation?tex=%5Clambda) 参数，将估计值与n-gram的原始值做融合.

![18]()

没有！ 是否必须对概率为P的情况折现概率？ 并将质量分配给较短的文本

![19]()

β是(n-k)-gram的剩余概率质量

## Absolute Discounting

* 使用2200万个单词进行训练和测试(held-out)
* 您可以在给定训练里预测保持（测试）设置的平均数吗？
* Testing counts = training counts - 0.75

![20]()

* d = 0.75, 对λ进行调整，以确保我们具有有效的概率分布

*  Kneser-Ney discounting的组成部分

  * 第一感觉： 一个单词可能很常见，但如果只遵循很少的上下文，

    Francisco is frequent but almost always follows San 旧金山很频繁，但几乎总是跟随圣

  * 在bigram的上下文中，unigram概率找到xn应成为新的延续的可能性。

## Stupid Backoff

* 我们真的需要概率吗？ 估计额外的参数需要花费大量语料。
* 如果scores是充足的，那么stupid backoff工作的更好

![21]()

* Empirically found that λ = 0.4 works well 根据经验发现λ= 0.4效果很好
* They called it stupid because they didn’t expect it to work well! 他们称其为“愚蠢”是因为他们没想到它能很好地工作！

## Syntax-based language models: 基于语法的语言模型

![22]()

## More data defeats smarter models

![23]()











Reference: 

[知乎整体介绍](https://zhuanlan.zhihu.com/p/36393614)









