# Scalable PCA

## PCA - Dimensionality Reduction

* 假设：数据位于低维子空间附近，如2维(D)空间位于1(d)条直线, 三维空间位于2维(d)平面
* 数据可以在该子空间的坐标轴上有效表示

## 为什么要降维？

* 发现隐藏的相关性/话题
  * 经常一起出现的单词
* 删除多余和噪音特征
  * 不是所有的单词都是有用的
* 解释和可视化
* 更轻松地存储和处理数据

## 降维

* 未处理的数据是复杂并且高维的
* 降维使用更简单，更紧凑的表示形式描述数据
* 这种表示方式可以使数据中有趣的模式更清晰或更容易看到

* 目标：找到一个更好的数据表示形式
  * Representation learning 表征学习
* 我们如何定义更好？
* 举例：
  * 最小化重建误差
  * 最大化方差
  * 他们给出了同样的解决方案 — PCA 主成分分析

## PCA 算法

* Input: N 个数据点 每一个数据点是D维向量
* PCA 算法
  * 1. X_0 是一个N*D的数据矩阵，每一个数据点伴随的是一个行向量x_n 
  * 2. X: 在X_0中的每个行向量减去均值
  * 3.  Σ <— X^T X 对X的散点图矩阵Gramian (scatter) 
  * 4.  查找Σ的特征向量和特征值
  *  PCs U(D * d) <—  特征值最大的d个特征向量
* PCA 特征对于 y D维：U^T* y (d维)
  * 零相关，按方差排序

## 多少个成分Components?

* 检查特征值(eigen-values)的分布
* 取足够多的特征向量来覆盖80-90％的方差

## 其他实用的小贴士

* PCA假设（线性，正交）并不总是合适的
* 具有不同基础假设的PCA的各种扩展，例如流形学习，内核PCA，ICA
* 中心化至关重要，即在应用PCA之前，我们必须对数据进行预处理，以使所有特征均值为零
* PCA结果取决于数据缩放
* 在应用PCA之前，有时会在实践中对数据进行重新调整

## Problems and limitations问题和局限性

* 如果hi一个非常大维度的数据？
  * 如图像(D > = 100*100)
* 问题：
  * Gramian matrix的size 就是D^2,也就是10^8
* 奇异值分解
  * 可用的高效算法
  * 一些操作只找到顶部特征向量

## SVD

* Factorization problem 分解问题

  * 1. 查找概念/主题/流派因素分析
  * 2. 降维

  ![1]()

  * 以上的矩阵实际上是二维的，因为所有行都能通过缩放[1,1,1,0,0]和[0,0,0,1,1]来重建 D = 5, —> d =2

## SVD -定义

![2]()

* A: n * m的矩阵（如： n 个文档， m个术语）
* U: n * r 的矩阵(n个文档， r个概念)
* Λ: r * r的对焦矩阵（每一个concept的强度）(r：矩阵的秩)
* V: m * r的矩阵(m个术语， r个概念)

## SVD — 性质

总是可以将矩阵A分解为A = U* Λ* V ^T

* 当 U，Λ，V是unique的(行列式不等于0？)
* U, V: 列正交（如， 列都是单位向量，与其他的正交）
  * U^T * U = I; V^T * V = I(I: 单位矩阵 )
* Λ : 奇异值是非负值，并按降序排序

## SVD  <——> 特征分解

* SVD 给了我们：

  * A = U* Λ* V^T

* Eigen-decomposition(特征分解)

  * B = W  Σ WT
    * U,V,W是正交的(U^T * U = I)
    * Λ, Σ 是对角的

* Relationship:

  ![3]()

## SVD for PCA

通过SVD来进行PCA

* 形成N* d的数据矩阵，每个数据点具有一个行向量
* X减去在X_0里面每行的行向量均值x
*  U Λ VT  <— SVD of X
* X的右奇异向量V等于X^T * X的特征向量 —> the PCs
* Λ中的奇异值等于X^T * X的特征值的平方根

## SVD - Properties

矩阵的光谱分解：

![4]()



## SVD - Interpretatioin

'documents', 'terms' and 'concepts'

* U: document-to-concept 相似矩阵
* V：term-to-concept相似矩阵
* Λ：它的对角线元素： 每个概念的强度

projection 投影

* Best axs to project on:("best" = min sum of squares of projection errors)最佳投影轴：（“最佳” =投影误差的最小平方和）

## SVD -Example

![5]()

![6]()

![7]()

![8]()

## SVD - Dimensioinality Reductioin

* Q: how exactly is(further) dim.reduction done 更近一步的降维怎么做
* A: 把最小的奇异值设置为0的时候
* 注意：3个0奇异值已经移除了



## PCA & SVD in Spark MLlib

* 如果是非大规模的：computePrincipalComponents() from RowMatrix
* 如果是大规模的： computeSVD() from RowMatrix

## SVD in Spark MLlib(RDD)

* 一个m*n的数据矩阵A（m > n)
* 对于大型矩阵，通常我们不需要完整的因式分解，而仅需要前k个奇异值及其关联的奇异矢量。
* 节省存储空间，降低噪声并恢复矩阵的低阶结构（降维）
* 假设m > n, SVD  A = U Λ V^T
* 奇异值和右奇异向量是根据A^T * A(通常小于A)的特征值和特征向量
* 左奇异向量是通过矩阵相乘 U=A*V *Λ ^−1 ,如果用户通过computeU 参数请求的话

## Selection of SVD Computation

* Auto自动
* 如果n 比较小(n < 100) 或者k相对较大(k > n/2)
  * 在本地首先计算A^T * A 然后计算它最大的特征值和特征向量

* 否则的话
  * 计算A^T* A v在一个分布式的方式并且将它送到ARPACK 在节点计算最大的几个特征值和特征向量