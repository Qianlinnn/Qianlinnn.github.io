
# Text units
* **word**(**token/term**): 一个或者多个不包含空格的字符序列。有时候还会包括n-grams
* **document(text sequence/snippet)** 句子，段落，社交媒体帖子等

## Document-Word Matrix(文档-文字矩阵)
* 一个矩阵 X, |*D*|X|*V*| 行是在语料库里*D*的的文档个数， 列是在*V*里面的词汇表
* 每一个文档，都要计算属于词汇表的单词出现了多少次
* X也可以把文档中所有文字的one-hot 向量相加然后转置他们

# tf-idf 公式
  ![image](https://github.com/Qianlinnn/NLP-/raw/master/img/idf_tfidf%E5%85%AC%E5%BC%8F.png)

      
# Label 种类
* 积极的或消极的 
* 主题（如运动 政策）
* 作者名字
* 在文章打分时是通过还是fail
* 是否支持立场(stance)
* 具有有限类集的任何人物

## 把label更抽象一点
* binary(0 or 1),如该电影评论是积极的还是消极的
* multi-class(1 out of k classes)如一个新闻文章的主题是什么（从运动，政策，商务，科技里选）
* multi-label(n out of k classes)这个新闻可能涉及到多个领域，可能是运动政策等等
* real number， 预测一个电影的评分是多少，我们通常叫他回归

## 文本类型(Text types)
* 新闻文章
* 社交媒体帖子
* 法律，生物医学文本
* 任意类型的文本

## 监督性学习
![superviesed learning](https://github.com/Qianlinnn/NLP-/raw/master/img/%E7%9B%91%E7%9D%A3%E5%AD%A6%E4%B9%A0%E6%B5%81%E7%A8%8B%E5%9B%BE.png)
相像你在准备一场考试
* 训练集数据组成了你过去的考试试卷
* 在训练期间，你通过过去的试卷进行学习
* 可以用验证机来测量预测准确率
* 最后在实际考试(test data)中就可以被老师评价了

### expression
给了M对数据，文档x（向量）和正确的标签y
  ![Dtrain公式](https://github.com/Qianlinnn/NLP-/raw/master/img/Dtrain.png)

用一个模型或者分类器f，参数为w，针对新的文档x取预测他的标签y
  ![y = f(x,w)](https://github.com/Qianlinnn/NLP-/raw/master/img/f().png)
  
  
## Binary logistic regression(二元逻辑回归)
* 假设一个文档向量使用counts/ N 即单词/特征
* 我们的第一个分类器就是一个线性模型，就是文档x里的每一个元素都跟weight wi 相关，叫做逻辑回归
* 如何去预测标签y如积极的 1， 消极的0情绪，并且哟个概率来表示呢？


### 逻辑回归示意图
 ![逻辑回归示意图](https://github.com/Qianlinnn/NLP-/raw/master/img/%E9%80%BB%E8%BE%91%E5%9B%9E%E5%BD%92%E7%A4%BA%E6%84%8F%E5%9B%BE.png)

### 二元逻辑回归公式
* 计算输入向量x和权重向量w的点积z，并且加入一个偏移量b
        z = dot(w,x) + b
        
* 计算积极情绪使用下面的方程表示
![积极](https://github.com/Qianlinnn/NLP-/raw/master/img/%E7%A7%AF%E6%9E%81%E6%83%85%E7%BB%AA.png)

* 预测最高可能性的哪一类标签
![sigmoid预测](https://github.com/Qianlinnn/NLP-/raw/master/img/sigmoid%E5%87%BD%E6%95%B0%E6%9C%80%E9%AB%98%E5%8F%AF%E8%83%BD%E6%80%A7.png)

#### sigmoid function
表达式

![function expression](https://github.com/Qianlinnn/NLP-/raw/master/img/sigmoid%E5%87%BD%E6%95%B0%E8%A1%A8%E8%BE%BE%E5%BC%8F.png)

图像

![function image](https://github.com/Qianlinnn/NLP-/raw/master/img/sigmoid%E5%87%BD%E6%95%B0%E5%9B%BE%E5%83%8F.png)

### Multiclass Logistic Regression(多类别逻辑回归)
* 超过一个类别 y ∈ Y = {0,...,k} 如一个新闻可能有三个类别，它是关于运动(y=0)，政治(y=1)，或者科技(y=2)

* y一个关于权重的矩阵 W， size为k*n， k是种类的数量， n是输入向量特征的数量

* 每一个种类y都会有一个权重向量w



#### 公式
* 计算输入向量和权重矩阵，并且加入一个便宜向量，结果向量是z
![多类别逻辑回归结果向量表达式](https://github.com/Qianlinnn/NLP-/raw/master/img/%E5%A4%9A%E7%B1%BB%E5%88%AB%E9%80%BB%E8%BE%91%E5%9B%9E%E5%BD%92%E8%A1%A8%E8%BE%BE%E5%BC%8F.png)

* 通过softmax函数来计算每一个种类的出现概率

![softmax计算每一个种类概率表达式](https://github.com/Qianlinnn/NLP-/raw/master/img/softmax%E5%87%BD%E6%95%B0%E8%AE%A1%E7%AE%97%E7%B1%BB%E5%88%AB%E6%A6%82%E7%8E%87%E8%A1%A8%E8%BE%BE%E5%BC%8F.png)

* 预测出现概率最高的种类
![softmax函数最高概率表达式](https://github.com/Qianlinnn/NLP-/raw/master/img/softmax%E6%9C%80%E5%A4%A7%E6%A6%82%E7%8E%87%E8%A1%A8%E8%BE%BE%E5%BC%8F.png)

* softmax函数是将向量所有值压缩到0-1之间，且和为1，从而得到概率分布
[softmax函数解释链接](https://www.zhihu.com/question/23765351)

![softmax函数解释图](https://github.com/Qianlinnn/NLP-/raw/master/img/softmax%E5%87%BD%E6%95%B0%E7%A4%BA%E6%84%8F%E5%9B%BE.png)

##### 如何训练得到权重参数w
* 首先用0s来初始化w
* 然后通过迭代训练集来调整w
* (我们怎么知道该如何调整呢):需要一个方程区计算预测label和真实label的差距(cost function)
* 然后我们就可以不断迭代训练来减小差值

## Binary Cross-Entropy Loss(二元互熵损失)
* 假设权重向量w应该将正确分类的log似然值最大化：
         log(P(y_i = c|x_i;w))
* 因为我们想要最小化损失函数的，因此我们需要取log似然值得相反数,单个类别的损失函数：
  ![损失函数如下](https://github.com/Qianlinnn/NLP-/raw/master/img/%5Blog%E4%BC%BC%E7%84%B6%E5%80%BC%E7%9B%B8%E5%8F%8D%E6%95%B0.png)
  
* 交叉熵损失随着预测概率与实际标记的偏离而增加。

*log 是自然对数



