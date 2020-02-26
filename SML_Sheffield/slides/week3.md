# Week 3

# RecSys and Collaborative Filtering (推荐系统和协同过滤)



## Recommender System

* Implicit, targeted, intelligent advertisement  隐式，针对性的智能广告
* Online stores: effective, popular marketing 网店： 有效受欢迎的市场

## Tasks of a Recommender system

* Predict relevant/useful/interesting items for given  user (in a given context) 预测给定用户的相关/有用/有趣的项目（在给定上下文中）
* Predict to what extent these items are  relevant/useful/interesting 预测这些商品在何种程度上相关/有用/有趣
* A ranking task (searching as well) 排名任务（搜索也是）
   	* 对项目进行排名，以便与给定用户（在给定上下文中）最相关/最有用/最有趣的项目会显示在排名的顶部

## Two basic Classes of Recsys

* Collaborative filtering systems 协同过滤系统
* Content-based recommender systems 基于内容的推荐系统

## What is collaborative filtering?

![1](https://github.com/Qianlinnn/personal-study-zone/raw/master/SML_Sheffield/img/week3/1.png)

* 根据过往的记录进行信息过滤

* 推荐系统：预测，推荐

* 强力/智能的市场工具

  * Electronic Word of Mouth marketing 

    电子口碑营销

  * 将参观者转变成消费者(电子销售员)

* 组成部分

  * 用户(消费者)： 提供评分的人
  * 商品：被评分的
  * 评分： interest

* 针对一个用户历史在社区的评分偏好数据来预测他对一件没有评分过的商品的喜好程度

  ![2](https://github.com/Qianlinnn/personal-study-zone/raw/master/SML_Sheffield/img/week3/2.png)

* 维护一个数据库，该数据库里有许多用户对各种各样物品的评分

* 对一个给定的用户，找到其他相似的用户，这些相似的用户的评分会跟给定的客户密切相关

* 被推荐的物品应该是被相似的用户高度评价了的，而不是被给定的用户高度评价了的

* 几乎所有现有的在线商店都在使用

## Rating Types

* Explicit ratings：明确评分
  * 用户给自己购买的产品评分
  * 对一个用户的偏好有一个精准地表述
  * 收集数据是一个挑战
* Implicit ratings: 隐式评级
  * 对用户行为的观察
  * 可以花费极少或者没有成本就能收集到数据
  * 评分推断可能是不精确的

## Rating Scales(评分区间)

 * Scalar ratings:(标量等级)
   	* Numerical scales
      	* 1-5,1-7, etc
* Binary ratings:(二元评分)
  * 同意或者不同意，好或者坏,etc
* Unary ratings 一元评级
  * Good, purchase
  * 缺少评分意味着没有信息

## Proferred application domains(更适合的领域)

* 许多商品
* 许多评分
* 用户数量超过推荐物品的数量
* 用户给多项物品评分
* 对社区的每一个使用者而言，有其他跟他品味相似的用户
* 物品评价要求个人品味
* 商品长期存在
* 口味也长期存在
* 物品都是相似的

## Collaborative FIltering(协同过滤)

* 输入： 用户对物品的评分
* 输出：推荐的物品被推送给用户u1
  * 物品被与u1相似的客户所喜欢
  * 相似的用户 = 用户喜欢相似的东西

## Collaborative filtering method(协同过滤方式)

* Memory-based(根据记忆)
  * 根据过去的评分预测评分
    * 将其他用户给的评分给出加权评分
    * User-based & item-based
*  Model-based(根据模型)
  * 根据过去的评分给客户建模
  * 通过这些模型来预测评分

## Prediction Accuracy

![3](https://github.com/Qianlinnn/personal-study-zone/raw/master/SML_Sheffield/img/week3/3.png)

## Challenge - Cold Start

* 新用户
  * 评论初始的物品
  * 没有私人定制的推荐
  * 需要描述口味
  * 人口统计信息
* 新商品
  * 非协同过滤: 没有内容分析，没有元数据
  * 随机挑选物品
* 新社区
  * 为部分社区提供评分激励
  * 一开始产生的是没有协同规律的推荐

## Challenge: Sparsity & Scalability 稀疏性和可伸缩性

* Sparsity
  * 稀疏用户-商品矩阵
* Scalability
  * 上百万的用户和物品

![4](https://github.com/Qianlinnn/personal-study-zone/raw/master/SML_Sheffield/img/week3/4.png)

# Matrix Factorisation for Collaborative Filtering(协同过滤的矩阵分解)

## Matrix Factorisation Methods

* 特性

  * 通过项目评级模式推断的因素向量来表征项目和用户
  * 项目和用户因素之间的高度对应性导致了推荐
  * 灵活：允许合并其他信息，例如隐式反馈，时间影响和置信度

* 依赖于矩阵输入数据

  * 一维代表用户
  * 其他维度代表物品

  ![5](https://github.com/Qianlinnn/personal-study-zone/raw/master/SML_Sheffield/img/week3/5.png)

## Two Data types(两种数据类型）

* 高质量明确的feedback:
  * 包括用户对他们对产品感兴趣的明确输入
  * 我们将明确的用户反馈称为评分
  * 通常是稀疏矩阵，因为任何单个用户可能只对可能项目的一小部分进行了评分
* 隐式反馈：
  * 通过观察用户行为简介反映意见
  * 购买历史记录，浏览历史记录，偶所默示，鼠标移动
  * 通常表示事件的存在还是不存在
  * 通常以密集填充的矩阵表示

## 基本矩阵分解模型

* 将用户和项目都映射到维度为k的联合潜在因子空间

*  以用户项目交互被建模，是用(inner product)内积来建立的

* 每个商品i与一个向量q_i关联，每个用户u与一个向量p_u关联，

  * q_i 衡量商品拥有这些因素的程度
  * p_u衡量用户对商品的兴趣成都
  * 生成的点积抓住了用户和物品之间的互动，用户对物品特点的整体兴趣

* 用户u对商品i的评分通常用r_(ui)来表示，有以下公式：

  ![6](https://github.com/Qianlinnn/personal-study-zone/raw/master/SML_Sheffield/img/week3/6.png)

* 主要的挑战是计算每个物品的因素向量(q_i)和客户向量(p_u)之间的映射

* 我们可以捕获用户和项目之间的潜在关系

* 我们可以生成原始评分矩阵的低维表示

* (Factor rating matrix)因子评级矩阵R使用奇异值分解得到Q,S,P

* 减小矩阵S到k维

* 计算两个结果矩阵Q_k*S_k(qT) and Sk*Pk(p)

* 这些结果矩阵可以被用来给用户和物品计算推荐分数

* 我们可以简单的计算q的i行和p的u列的点积

  ![7](https://github.com/Qianlinnn/personal-study-zone/raw/master/SML_Sheffield/img/week3/7.png)

## 通过MF实现的推荐系统的挑战

* 用户项目评分矩阵中的稀疏性导致
* 当矩阵的数据不完整时，传统的SVD未定义
* 粗心地只解决相对较少的已知条目很容易过度拟合

## 如何填补缺失值

* 较早的系统依靠估算来填补缺失的评分并使评分矩阵密集，例如使用用户和商品的平均评分
* 问题：
  * 插补可能会非常昂贵，因为它会大大增加数据量
  * 不正确的估算可能会使数据失真

## Matrix Factorisation with Missing  Values(缺少值的矩阵分解)

* 仅直接建模观察到的评分

  * 避免通过正则化模型过度拟合
  * 要学习因子向量（pu和qi），系统将已知等级的正则化平方误差最小化

  ![8](https://github.com/Qianlinnn/personal-study-zone/raw/master/SML_Sheffield/img/week3/8.png)

  * 目标是通过预测未来未知评分的方式来归纳之前的评分
  * 常数控制正则化的程度(the constant controls the extent of regularisation)

## Alternating Least Squares(交替最小二乘法)

* 因为q_i和p_u都是未知数，所以对象函数不是凸的
* 但是，如果固定了未知数之一，则优化问题将变成二次方程，并且可以通过最佳方式解决
* 交替最小二乘法再固定的q_i和固定的p_u之间旋转
* 当所有的p_u都固定后，系统会通过解决最小二乘法的问题来重新计算q_i

![9](https://github.com/Qianlinnn/personal-study-zone/raw/master/SML_Sheffield/img/week3/9.png)

* 上面两句翻译为：
  * 我们可以将矩阵P固定为某个矩阵，这样最小化问题就等于
  * 类似得，固定了Q

# Collaborative Filtering in Spark

## CF in Spark ML

* numBlocks: 用户和商品被划分为块得数量，以并行化计算(默认为10)
* rank: 模型中潜在因子得数量(默认为10)
* maxlter: 要运行的最大迭代次数(默认为10)
* regParam: ALS中的正则化参数
* hiddenPrefs：指定是使用显式反馈ALS变体还是适用于隐式反馈数据的变量（默认为false，这意味着使用显式反馈）
* alpha：适用于ALS的隐式反馈变量的参数，用于控制偏好观察中的基线置信度（默认为1.0）
* nonnegative: 是否对最小二乘使用非负约束（默认为false）

## Blocked IMplementation of ALS(ALS的块状话实施)

* 将两组因素（“用户”和“商品”）分组进块
* 通过仅在每次迭代中将每个用户向量的一个副本发送到每个商品块，并且仅针对需要该用户特征向量的商品块，来减少通信
* 需要预先计算有关评级矩阵的信息，以确定每个用户的“外部链接”（它将贡献哪些商品块）和每个商品块的“内部链接”信息（它接收哪些特征向量） 取决于每个用户块）。
* 这允许我们在每个用户块和项目块之间仅发送特征向量数组，并让项目块查找用户的评分并根据这些消息更新项目。

## Explicit vs. Implicit Feedback(显性和隐性反馈)

* 如果我们只能访问隐式反馈（例如，观看次数，点击次数，购买，喜欢，分享等），该怎么办。
* ICDM2008：用于隐式反馈数据集的CF
* 将数据视为代表观察用户动作强度的数字（例如，＃clicks，观看电影所花费的累积时间），与观察到的用户偏好的置信度相关。 然后，该模型尝试查找可用于预测用户对某项商品的期望偏好的潜在因素。
* 一个（另一个）偏好矩阵“ P”的低秩近似，其中，如果r大于0，则P的元素为1；如果r小于或等于0，则P的元素为0。