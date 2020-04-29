# Sequence Labelling and Part-of-Speech Tagging 序列标记和词性标记

* Our first sequence modelling problem: Language  Modelling 我们的第一个序列建模问题：语言建模
* What about if we want to assign a label to each word in a  sequence?  如果我们要给序列中的每个单词分配标签怎么办
  * Sequence labelling!序列标签！

## Applications

* Part-of-Speech([POS]([https://zh.wikipedia.org/wiki/%E8%A9%9E%E9%A1%9E](https://zh.wikipedia.org/wiki/詞類))) tagging 词类标记

  * (x, y) = ([I, studied, in, Sheffield],

    ​            [Pronoun, Verb, Preposition, ProperNoun])

* Named Entity Recognition(命名实体识别)

  * (x, y) = ([Giannis, Antetokounmpo, plays, for, the, Bucks],

    ​              [Person, Person, NotEnt, NotEnt, NotEnt, Org])

* Machine Translation( reconstruct word alignments) 重建单词对齐

  * (x, y ) = ([la, maison, bleu], 
  * ​              [the, house, blue])

## Parts of Speech (POS)

* Label words according to their syntactic function in a sentence:根据句子中的句法功能标记单词：

  ![1]()

* What could they be useful for?

  * text classification 文本分类
  * language modelling 语言建模
  * syntactic parsing 句法解析
  * named entity recognition 命名实体识别
  * question answering 问题回答

## PoS tags 词类标签

* Open class:
  * nouns, verbs, adjectives
* Closed class:
  * determiners, prepositions, conjunctions, etc

## PoS definitions PoS定义

* 大多数研究使用：Penn Treebank PoS tag set
* 包括45个标签，区分以下内容：
  * 动词主动时态 vs 过去时态
  * 单数或复数名词
* Penn Tree Bank inspired by English 宾夕法尼亚树银行受到英语启发。 最近的工作集中在Universal PoS tag set上：
  * 17个粗略标签：一个名词类，一个动词类，等等。
  * 考虑22种语言而开发

## Sequence labelling: Problem Setup 序列标签：问题设置

* Data consists of word sequences with label sequences: 数据由带有标签序列的单词序列组成：
  * ![2]()
  * Learn a model f that predicts the best label sequence:了解预测最佳标签序列的模型f：

![3]()

* y ∈ Y^N 是所有可能的标签序列组合的集合，并且Y = {A，B，C ...}是每个单词的可能类别。

## Could we us a dictionary-based model?我们可以使用基于字典的模型吗？

{'the': 'determiner', ' can': 'modal','fly': 'verb'}

但相同的单词在不同的语境里可以有不同的tag。

I                 can                               fly

pronoun  modal(情态动词)         verb

**vs**:

I                can                 fly

pronoun  verb              noun

can和Brown corpus里11.5%的字有不止一个tag

## Can we use a Markov modal(马尔可夫模型)?

使用tag y 替代文字

![3]()

我们的训练数据应该能告诉我们下面的tagging 是不可能的

I                 can             fly

**pronoun** **modal**      **noun**

## Hidden Markov Model([HMM]([https://zh.wikipedia.org/wiki/%E9%9A%90%E9%A9%AC%E5%B0%94%E5%8F%AF%E5%A4%AB%E6%A8%A1%E5%9E%8B](https://zh.wikipedia.org/wiki/隐马尔可夫模型)))

![4]()

* 标签y_i(如 PoS tags) 是出现词的隐藏状态
* 假设：
  * PoS标签中的一阶马尔可夫（当前标签仅取决于前一个的标签）
  * 每一个词只取决于它自己的POS tag

## HMM： Derivation 求导

![5]()



第一个式子意思是当y = y^时， P(y|x)取到了最大值

第二个式子字的概率是恒定的，因此去掉分母值得相对大小不会变化

对第三个式子使用一阶马尔可夫，当前得概率只取决于前一个得标签

就得到了第四个式

## HMM: training

* Maximum likelihood estimation(i.e. counts!):

  ​	![6]()

  transition probabilities: 转移概率 从一个状态变成另一个状态的概率

  emission probabilities: 发射概率 假设下一个状态是q_j, 现在的状态是q_i, emission probabilities = P(O_k|q_i) 该概率就是在当前状态生成O_k的概率

  

  x = [START, I, can, fly, End]

  y = [START, PPSS, MD, NN, END]

  P(y|x) = P(I|PPSS) P(PPSS|START)

  ​               P(can|MD)P(MD|PPSS)

  ​				P(fly|NN)P(NN|MD)

## Decoding/Inference 解码/推理

* 因此我们有解码/推断句子最可能的标签序列所需要知道的一切

  ![7]()

* 我们需要评估|y|^N 个序列

## HMMs: 一切额外的点

* Higher order HMMs(高阶HMMs):
  * 更长的语境，更高成本的推导
  * 收益通常很小
* Smoothing(平滑)：
  * 当我们看到未见过的单词/标签或者标签与标签组合的时候会发生什么？
  * 使用我们在语言建模讲座中学到的方法！

## HMMs: Limitation

* 它们产生单词和标签的概率，我们只需要标签的概率
* 没有重叠的要素（如：一元模型和二元模型
* 没有子字词功能（如后缀）

## Conditional Random Fields: Extend LR for Sequence  Labelling 条件随机字段：扩展LR以进行序列标记

* Logistic回归还可以提供概率，但支持更灵活的表示形式！
* 给定一个单词，该单词的候选标签和前一个单词的标签，使用(multi-class LR)来预测可能性最大的标签 —> 条件随机字段



## Conditional Random Fields

* 分解每个句子 x = [x_1, ... x_N] 预测：

  ![8]()

* 对每一个单词x_n

  ![9]()

* 如何建立一个特征向量φ(x_n, y_n, y_(n-1), n)?

## CRF: feature vectors

φ1(x_n, y_n, y_(n-1), n) = 1, if y_n = ADVERB, 并且第n个单词是以 -ly结束; 否则是0.例如："usually","casually"

φ2(xn, yn, yn−1, n) = 1 if n = 1, yn = VERB,并且句子结尾是用一个疑问号。否则是0

## CRF: Inference

Normalisation factor(归一化因子)不得不给所有句子进行所有可能的标签顺序评分。因此就被忽视了

![10]()

## CRF: Training

* 通过最小化negative log-likelihood objective 来训练

  ![11]()

* 使用随机梯度下降Stochastic Gradient Descent

## Decodin with Viterbi

* 枚举HMM和CRF中所有可能的标签序列是很棘手的！
* 动态编程：存储和重复使用计算
* 由于独立性假设而可能
* 跟踪每个单词到达每个PoS标签的最高可能性以及我们如何到达那里

![12]()

## Viterbi: Data structure [维比特算法]([https://zh.wikipedia.org/wiki/%E7%BB%B4%E7%89%B9%E6%AF%94%E7%AE%97%E6%B3%95](https://zh.wikipedia.org/wiki/维特比算法))

* Viterbi score matrix V|y|*N

  * 标签集合 y, 句子 x = [x_1,...x_N]

  * 对于带有标签y的单词n，每个单元格包含最高概率。 

  * 一阶马尔可夫：仅取决于前一个标签yn-1 

    ![13]()

## Vierbi: Data structures

* Backpointer matrix(反向指标矩阵) backptr|y|*N:

  * 而不是最高分，保留获得它的前一个标签

  * argmax代替max

    ![14]()

## Viterbi algorithm

![15]()

* Break the large arg max into smaller ones, left-to-right 从左到右将大arg max分解为较小的arg max

## Beam Search: Inexact Decoding 光束搜索：不精确解码

* 维特比通过评估所有选项来执行精确搜索（在假设条件下）
* 由于不精确而更快，即使用Beam Search避免标记某些候选序列

## Beam search

* 做维特比，但在每个步骤中只保留最佳的k个假设
* 如果波束大小为1，则我们进行贪婪搜索
* 小于10的光束通常会接近精确搜索，但速度要快得多，光束必须具有相同的长度才能进行比较
* 当我们需要复杂的特征函数（即避免马尔可夫假设）时很有吸引力

## Beam Search: Example

![16]()

##  Beam Search: algorithm

![17]()