# Week1
## Why is NLP challenging?
* 自然语言不像编程语言是被设计出来的，它们是自己发展演变而来
    * 新的单词不断出现
    * 解析自然语言的规则是很灵活的
    * 模糊性是内在的
* 世界的知识对于解释来说是非常有必要的
* 许多语言，方言，语言风格

## why statical NLP?
* 传统的(rule-based)基于规则的人工智能
    * 需要专家的知识来指定规则
    * 不能灵活得适应多种语言，领域，应用程序
* 从数据学习（机器学习）适用于：
    * 进化：仅从新数据中学习
    * 适应不同的应用：只需学习适当的目标表示

## 注意事项
* 探索任务时，尝试一些简单的规则来检验我们的假设通常很有用
* 实际上，对于某些任务，基于规则的方法规则尤其是在行业中(对应上面的rule)：
    * 问题回答
    * 自然语言产生
* 如果我们不知道如何执行任务，那么ML算法不太可能为我们找到答案

## NLP =? ML
* NLP是计算机科学，人工智能（AI）和语言学的融合
* ML提供了通过从数据中学习来解决问题的统计技术（当前占主导地位的AI范例）
* ML通常用于对NLP任务进行建模

## NLP =? Computational linguistics
* 两者都主要使用文本作为数据
* 在计算语言学（CL）中，使用计算/统计方法来支持语言现象和理论的研究
* 在NLP中，范围更广泛。 计算方法用于翻译文本，提取信息，回答问题等
* The top NLP scientific conference is called:
**Annual Meeting of the Association for Computational Linguistics**

## 向量和向量空间
* 一个向量x是d个元素(坐标)的一个一维数组, 可以通过index来标识

    ![1](https://github.com/Qianlinnn/personal-study-zone/raw/master/NLP_Sheffield/img/week1/1.png)
    
* 矩阵X，大小为n * d: 是n个向量的集合，也被称为向量空间

    ![2](https://github.com/Qianlinnn/personal-study-zone/raw/master/NLP_Sheffield/img/week1/2.png)
    
* Example:

    ![3](https://github.com/Qianlinnn/personal-study-zone/raw/master/NLP_Sheffield/img/week1/3.png)
    
## Vector similarity(向量相似度)
   
   ![4](https://github.com/Qianlinnn/personal-study-zone/raw/master/NLP_Sheffield/img/week1/4.png)

**Note: x1在此处的公式里是行向量**

## Vector Space of Text(文本的向量空间)
* 相似度坐标图如下图所示
  
  ![5](https://github.com/Qianlinnn/personal-study-zone/raw/master/NLP_Sheffield/img/week1/5.png)

## 文本向量表示的必要性
* 对单词的含义进行编码，以便我们可以计算单词之间的语义相似度。 例如。 篮球与足球或食谱更相似吗？
* 便于文件检索，例如 检索与查询相关的文档（网络搜索）
* 将机器学习应用于文本数据，例如 聚类/分类算法对向量进行运算。 

## Text units(文本单位)
* 未处理的文本：As far as I’m concerned, this is Lynch at his best. ‘Lost Highway’ is a
dark, violent, surreal, beautiful, hallucinatory masterpiece. 10 out of 10
stars
* Word(token/term)：一个或多个不包含空格的字符序列
* document(text sequence/snippet): 句子，段落，部分，章节，整个文档，搜索查询，社交媒体帖子，转录语音，伪文档
* 

[n-gram，tf_idf详解](https://medium.com/machine-learning-intuition/document-classification-part-2-text-processing-eaa26d16c719)

## tokenization(划分词)
[分词_极客时间](https://easyai.tech/ai-definition/tokenization/)
* Tokenisation 是为了从原文当中获得不同的分词组合。 简单形式：空白行划分词，或者使用正则表达式

![6](https://github.com/Qianlinnn/personal-study-zone/raw/master/NLP_Sheffield/img/week1/6.png)

* 其他预处理步骤也许遵循：小写，标点符号/数字/停止/不频繁的单词删除和词干

![7](https://github.com/Qianlinnn/personal-study-zone/raw/master/NLP_Sheffield/img/week1/7.png)

## Decide what/how do you want to represent: Obtain a  vocabulary(确定您想表达什么/如何表达：获取词汇)

* 假设一个语料库D，语料库D里包含了m个预处理的文档（如电影评论或推特）
* 词汇表V是一个集合，包含D中的所有k个为一次w_i
    V = {w_1,...,wk}
通常这些语料库会被扩展到n—grams （n个单词的连续序列）

## Words: Discrete vectors(离散型向量)

![8](https://github.com/Qianlinnn/personal-study-zone/raw/master/NLP_Sheffield/img/week1/8.png)

## Problems with discrete vectors(离散型向量的问题)

![9](https://github.com/Qianlinnn/personal-study-zone/raw/master/NLP_Sheffield/img/week1/9.png)

* 由上可算出杏和凤梨的cos相似度为0，但实际上二者是有联系的

## Words: Word-Word Matrix(term-context)字对字矩阵，术语-上下文
* 一个矩阵X，大小为n*m, n =|V| n代表目标文字(目标单词库)， m=|Vc|(文本文字)
* 对于每一个目标文字，计算它在文本x_j出现了多少次
* 计算每一个目标文字左右各k个字的范围内，出现了多少次context words
* 在一个大规模文本的语料库里计算频率
* 通常目标文字和文本文字词汇表是相同的，从而组成了一个方阵

![10](https://github.com/Qianlinnn/personal-study-zone/raw/master/NLP_Sheffield/img/week1/10.png)

**图里的数据只是假设做举例用，并不能和上面的文本一一对应**

## Document-Word Matrix(Bag-of-words)

* 一个矩阵X， 尺寸大小为|D|*|Y|， 行是语料库中的文档，列是V(目标单词)里面的单词
* 对每一个文档统计目标单词都共出现了多少次

![11]()

* X同样可以通过加入所有的文档中one-hot vectors然后转置得到
**矩阵的第一行应该是文本里面的context word，然后第一列是目标文字，这样形成的就是01向量**

## Problems with counts
* 常用词(文章，代词等)在文本文字中占主导地位，但它们并没有提供丰富的内容
* 举例说明：如果把词the加进文本文字里，它往往是最多的那个名词

![12](https://github.com/Qianlinnn/personal-study-zone/raw/master/NLP_Sheffield/img/week1/12.png)
*这个问题也出现在document-word 矩阵中，解决办法是对这些向量分配权重

## Weighting the Word-Word Matrix: Distance discount(根据离某一个词的距离远近来分配权重)
* 根据文本文字与目标词的距离来分配权重，越远的单词，权重越小
    * 对一个范围±k， 在每一个位置上的文本文字乘以 (k-distance)/k, e.g. for k = 3
    
    ![13](https://github.com/Qianlinnn/personal-study-zone/raw/master/NLP_Sheffield/img/week1/13.png) 

## weighting the word-word matrix: pointwise mutual information(PMI)逐点相互信息
* PMI: 两个单词w_i 和 w_j 一起出现与相当于独立出现的频率
    
    ![14](https://github.com/Qianlinnn/personal-study-zone/raw/master/NLP_Sheffield/img/week1/14.png)
**其中#(.)代表计数|D|代表的是目标词与问本次成对的数量**
* 正的值能够量化相关性，使用PMI值替代了计数
* 而负的PMI值通常被忽略
    PPMI(w_i,w_j) = max(PMI(wi,wj), 0)
**即PPMI的值取0和PMI的最大值，因为PMI可能为负**

## Problems with Dimensionality
* Count-based matrices 计数的矩阵（for words and documents)经常表现很好，但是：
    * high dimensional: 词汇表的尺寸会到数百万级别
    * very sparse(非常稀疏)：单词仅与少数单词同时出现，文档仅包含很小一部分的词汇表的单词
* Solution：将数据维度降维

* Truncated Singular Value Decomposition(截断奇异值分解)
* 一种查找数据集最重要维度的方法，这些维度通过将矩阵分解为潜在因子来使数据的变化最大
* truncated-SVD公式为：
    
    ![15](https://github.com/Qianlinnn/personal-study-zone/raw/master/NLP_Sheffield/img/week1/15.png)
* 近似是好的，通过学习低维潜在空间，利用冗余来消除噪声
[奇异值分解教程](https://web.mit.edu/be.400/www/SVD/Singular_Value_Decomposition.htm)

### Singular Value Decomposition on Word-Word matrix(在文字对句子矩阵进行奇异值分解)
图示如下:

![16](https://github.com/Qianlinnn/personal-study-zone/raw/master/NLP_Sheffield/img/week1/16.png)

### Singular Value Decomposition on Document-Word matrix(文字对文档矩阵的奇异值分解)

* 同样被叫做Latent Semantic Analysis(LSA)潜在语义分析
* U^(n*k)代表着文档插入项
* V^(n*k)代表着目标文字插入项
* 可以得到一个文档x_new的心的插入项u_new,通过将文档的计数向量投影到现在空间：

![17](https://github.com/Qianlinnn/personal-study-zone/raw/master/NLP_Sheffield/img/week1/17.png)

## Evaluation: Word Vectors(评估： 文字向量)
* 固有的特性：
    * similarity(相似性)： 根据单词对的语义相似性对它们进行排序
    * In-context similarity(上下文相似性):在句子中替换一个单词而改变它的意思
    * analogy(打个比方):雅典之于希腊，就是罗马就是之于？(意大利) 因为雅典是希腊的首都
* 外在的特性：
    * 通过使用他们来改善任务的表现：
    * 通过bag of vectors(embedding)来替代bag of words
      
## Best word vectors?(单词向量是最好的吗？)
* high-dimensional count-based 和 low-dimensional with SVD哪个更好？
* Levy 在2015年展示了文本窗口大小， 稀有字的删除会更有用
* 选择要获取计数的文本很重要。文字越多，低维方法的缩放越好。

## 局限性： Word Vectors
* Polysemy(一词多义)：一个单词的所有出现（及其所有含义）都由一个向量表示。
    * 对于给定任务，调整单词向量以表示适当的意义通常很有用
* Antonyms(反义词): 出现在相似的上下文中，很难将它们与同义词区分开
* Compositionality(组成性): 单词序列组成的意思是什么
    * 尽管我们也许可以获取短短语的上下文向量，但这并不能扩展到整个句子，段落等。
    * 组合单词向量，即加/乘
    * 很快，我们将看到从单词嵌入（递归神经网络）中学习单词序列嵌入的方法！
    
## Evaluation: Document Vectors
* Intrinsic(内在的属性)
    * 文档相似性
    * 信息检索
* Extrinsic(外在的应用)：
    * 文档分类，抄袭检测

## Limitatioin: Document Vectors
* 即使互虐单词的顺序，但语言仍然是能看出顺序的

