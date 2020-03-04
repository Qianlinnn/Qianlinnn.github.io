## Scalable K -means

## What is Cluster Analysis?

* 查找对象组，以使一组中的对象彼此相似（或相关），而与其他组中的对象不同（或不相关）

  ![1](https://github.com/Qianlinnn/personal-study-zone/blob/master/SML_Sheffield/img/week4/1.png)

## Cluster Analysis(聚类分析)

* 将数据分为有意义的，有用的（或两者）（集群）
* 自动寻找类别的技术研究
* 聚类可以帮助捕获数据
* 进一步分析的起点
* 在广泛的领域中发挥重要作用：心理学，生物学，统计学，模式识别，信息检索，机器学习和数据挖掘等

## 了解聚类

* 类或具有某些相似性的概念上，在人们分析描述世界的方式中起着重要作用

* 人类擅长将对象划分为组（聚类）并将特定对象分配给这些组（分类）。 例如。 孩子们可以快速将照片中的物体标记为建筑物，车辆，人，动物等

## 聚类的应用

* 生物学
  * 聚类分析有助于创建所有生物的分类法：王国，门，阶级，秩序，家庭等
  * 基因/蛋白质数据的聚类分析有助于注释基因/蛋白质的功能
* 信息检索
  * 群集帮助将搜索结果分为少量群集，每个群集都捕获查询的特定方面。 例如。 对“电影”的查询可能会返回归类为评论，预告片，开始和剧院等类别的网页
* Climate(气候)
  * 已应用聚类分析来发现极地地区和海洋地区的大气压力对陆地气候有重大影响的模式
* Psychology and medicine.
  * 识别不同类型的疾病（例如抑郁症）
  * 检测疾病的空间或时间分布模式
  * 帮助将具有相似模式的患者分组

* Business
  * 聚类分析可用于将客户划分为少数几个组，以进行其他分析和营销活动
* Anomaly/outlier detection 异常/异常检测

## Anomaly/Outlier Detection 异常/异常检测

* 什么是异常/异常值？
  * 与其余数据有很大不同的一组数据点
* 应用：
  * 信用卡欺诈检测：购买行为
  * 网络入侵检测：异常行为
  * 生态系统干扰：台风，火灾
  * 公共卫生：SARS，禽流感，HxNx
  * 医学：异常症状/检查结果

## Clustering-Based  Anomaly/Outlier Detection 基于聚类的异常/离群值检测

* 将数据分为不同密度的组
* 选择小聚类中的点作为候选离群值
* 计算候选点和非候选类之间的距离
* 如果候选点距离所有其他非候选点都远，则它们是异常值

## Hierarchical vs Partitional  Clustering 分层聚类与分区聚类

* 分区聚类
  * 将一组数据对象简单地划分为不重叠的子集（群集），以便每个数据对象恰好在一个子集中
* Hierarchical clustering分区聚类
  * 一组嵌套的集群，组织成一个层次树
  * 树中的每个节点（集群）（叶节点除外）都是其子节点（子集群）的并集，树的根是包含所有对象的集群

![2](https://github.com/Qianlinnn/personal-study-zone/raw/master/SML_Sheffield/img/week4/2.png)

![3](https://github.com/Qianlinnn/personal-study-zone/raw/master/SML_Sheffield/img/week4/3.png)

## Hierarchical vs Partitional Clustering

![4](https://github.com/Qianlinnn/personal-study-zone/raw/master/SML_Sheffield/img/week4/4.png)



可以将分层聚类视为分区聚类的序列，并且可以通过在特定级别切割层次树来获取该序列的任何成员来获得分区聚类



## Types of Clusters: Center-Based 集群类型：基于中心

* Center-based (Prototype-based)基于中心（基于原型）
  * 群集是一组对象，因此群集中的对象比群集的“中心”更靠近（更相似），而不是其他任何群集的中心
  * 群集的中心通常是质心，群集中所有点的平均值或质心（质心不重要（例如，分类的）时），它是群集中最具“代表性”的点

![5](https://github.com/Qianlinnn/personal-study-zone/raw/master/SML_Sheffield/img/week4/5.png)

## Types of Clusters: Density-Based  群集类型：基于密度

* 基于密度
  * 聚类是点的密集区域，由低密度区域与其他高密度区域隔开
  * 当簇不规则或相互缠绕，并且有杂音和异常值时使用

![6](https://github.com/Qianlinnn/personal-study-zone/raw/master/SML_Sheffield/img/week4/6.png)

## K-means Clustering K均值聚类

* 基于原型的分区聚类方法

* 每个群集都与一个质心（中心点）相关联

* 每个点都分配给具有最接近质心的聚类

* 群集之前必须指定群集数(簇the number of clusters)K

* 输入：

  * 一组n =数据点的X = {x1，x2，…，xn}
  * 簇数k

* 对于群集“中心”的集合C = {c1，c2，…，ck}，定义平方误差和 Sum of Squared Error（SSE）为：

  ![7](https://github.com/Qianlinnn/personal-study-zone/raw/master/SML_Sheffield/img/week4/7.png)

  d（x，C）：x到C中最近的中心的距离

* 目标：找到使目标函数φ_X（C）最小的中心C

## Determine the number of clusters 确定集群数

**有多种确定K的方法**

* K可以任意设置为任意数字
* K可以根据进一步分析的需要确定
* K可以根据现场知识或在数据可视化过程中获得的知识来确定
* 可以先设置不同的K，然后根据某些条件找到最佳K

## K-means Clustering: Example

![8](https://github.com/Qianlinnn/personal-study-zone/raw/master/SML_Sheffield/img/week4/8.png)

## Lloyd Algorithm 劳埃德算法 [劳埃德算法和k means算法](https://www.cnblogs.com/zhxuxu/p/9860654.html)

* 以k个任意中心{c1，c2，…，ck}（通常从数据点随机选择）开始
* 执行EM类型的本地搜索，直到收敛
* 主要优点：简单，可扩展（迭代）
* 步骤：
  * 选定k个点作为起始(centroids)重心点
  * 重复接下来的步骤：
    * 通过把所有的点分配到最近的中心附近
    * 重新计算每一个集群中心
  * 直到重心点不再改变

## 劳埃德算法的问题

* 需要多次迭代才能收敛
* 对初始化非常敏感
* 随机初始化可以轻松地使同一群集中的两个中心
  * K均值陷入局部最优

## Lloyd Algorithm: Initialization

![9](https://github.com/Qianlinnn/personal-study-zone/raw/master/SML_Sheffield/img/week4/9.png)

![10](https://github.com/Qianlinnn/personal-study-zone/raw/master/SML_Sheffield/img/week4/10.png)

![11](https://github.com/Qianlinnn/personal-study-zone/raw/master/SML_Sheffield/img/week4/11.png)

![12](https://github.com/Qianlinnn/personal-study-zone/raw/master/SML_Sheffield/img/week4/12.png)

## K means++  [Arthur et al. ’07]

* 分散中心

* 从数据集中随机选择第一个中心c1

* Repeat for 2 ≤ i ≤ k:

  * 重复2≤i≤k:

    * 选择c_i等于从分布中采样的数据点x0：

      ![13](https://github.com/Qianlinnn/personal-study-zone/raw/master/SML_Sheffield/img/week4/13.png)

      定理：O(log k)-初始化后立即逼近最佳

## K-means ++有什么问题？

* 需要K传递数据
* 在大数据应用中，不仅数据是海量的，而且K通常也很大（例如，容易地为1000）。
* 不缩放！

## 解决方案的第一感

* K-means ++每次迭代采样一个点并更新其分布
* 如果我们以较大的概率独立采样每个点来进行过采样，该怎么办？
* 直观上等同于更新发行版频率却不那么高
  * 粗采样
* 结果足够：K-均值

## K-means|| Initialization(k-方法初始化)

![14](https://github.com/Qianlinnn/personal-study-zone/raw/master/SML_Sheffield/img/week4/14.png)

![15](https://github.com/Qianlinnn/personal-study-zone/raw/master/SML_Sheffield/img/week4/15.png)

![16](https://github.com/Qianlinnn/personal-study-zone/raw/master/SML_Sheffield/img/week4/16.png)

![17](https://github.com/Qianlinnn/personal-study-zone/raw/master/SML_Sheffield/img/week4/17.png)

![18](https://github.com/Qianlinnn/personal-study-zone/raw/master/SML_Sheffield/img/week4/18.png)

## K-means||[Bahamani et al. '12']

* Choose L > 1
* 将C初始化为任意点
* 对于R迭代，请执行以下操作：
  * 以概率独立地采样X中的每个点x
  * 将所有采样点添加到C
* 将C中的（加权）点聚类以找到最终的k个中心

## K-means||: Intuition

* Lloyd和K-means ++之间的插值

  ​	![19](https://github.com/Qianlinnn/personal-study-zone/raw/master/SML_Sheffield/img/week4/19.png)

## K-means||: Benefits

* 使用K-means ++对中间中心进行聚类，总逼近因子 O（log k）
* K-means|| 要与嘈杂的异常值混淆，比K-means ++难得多
* K均值|| 减少Lloyd迭代次数甚至超过K-均值++

## K-means in Spark

* k：所需集群的数量。

* maxIter：最大迭代次数
* initMode：指定随机初始化或通过k-means ||初始化 （比较）
* initSteps：确定k均值||中的步数。 算法（默认= 2，高级
* tol：确定我们认为k均值收敛的距离阈值
* seed：设置随机种子（以便多次运行具有相同结果

## Running Scalable K-means

* 数据应该缓存以提高性能（运行程序时检查警告）

## Limitations of K-means

* 当聚类下述的条件不同时，K均值有问题
  * 尺寸
  * 密度
  * 非球形
* 当数据包含异常值时，K均值会出现问题。

分别如下图所示：

![20](https://github.com/Qianlinnn/personal-study-zone/raw/master/SML_Sheffield/img/week4/20.png)

![21](https://github.com/Qianlinnn/personal-study-zone/raw/master/SML_Sheffield/img/week4/21.png)

![22](https://github.com/Qianlinnn/personal-study-zone/raw/master/SML_Sheffield/img/week4/22.png)

## Overcoming K-means limitations

![23](https://github.com/Qianlinnn/personal-study-zone/raw/master/SML_Sheffield/img/week4/23.png)

![24](https://github.com/Qianlinnn/personal-study-zone/raw/master/SML_Sheffield/img/week4/24.png)

![25](https://github.com/Qianlinnn/personal-study-zone/raw/master/SML_Sheffield/img/week4/25.png)

## Pre-processing & Post-processing

* pre-processing预处理
  * Normalize the data 正则化数据
  * Eliminate outliers 消除异常值
* Post-processing后期处理
  * 消除可能代表异常值的小型集群
  * 拆分“松散”集群，即具有较高SSE的集群
  * 合并“关闭”且具有较低SSE的群集