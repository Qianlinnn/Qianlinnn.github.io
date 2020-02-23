# Introduction to Spark and ShARc

## Where Does Big Data come from
* 发生在网络世界，能记录一切东西
* 用户也会产生内容如社交媒体

## graph Data(图形数据)
* 许多有趣的数据都有图形结构
    * 社交网络
    * 电脑网络
    * Road network
    
## Key Data Management Concept(关键的数据管理概念)
* 一个data model(数据模型)是一个描述数据概念的集合
* 一个schema(模式)是一个使用给定数据模型的特定数据集合的描述

[什么是schema](https://blog.csdn.net/u010429286/article/details/79022484)

## The Structure Spectrum

![数据结构光谱](https://github.com/Qianlinnn/ScalableML/raw/master/img2/week1/%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%E5%85%89%E8%B0%B1.png)

## 结构化数据（数据库）
* Database：一个关系数据模型，用来描述一个数据库是如何结构化和使用的
* Schema： 是数据结构的组织的蓝图，这个蓝图是用来让人知道一个数据库是如何建立起来的
* 程序员必须静态指定架构

## Semi-Structured Data
* 是一种自描述结构而不是正式的结构， 标签或者标记是用来分割语义元素。
* the column types(柱的种类) ——> 是数据的模式
    * Spark在读取每一行数据时都在动态地推断该数据的schema(模式)
    * 程序员静态指定架构
* 出现的越来越多如： XML, JSON

## 非结构化数据
* 只有一列具有字符串或二进制类型的示例：
    * 如facebook帖子 instgram图片
    
* 组织中所有数据的70％至80％以上（Shilakes 1998）

* 将结构强加于非结构化数据

![结构光谱图ETL](https://github.com/Qianlinnn/ScalableML/raw/master/img2/week1/ETL.png)

[结构化数据，半结构化数据，非结构化数据说明](https://blog.csdn.net/liangyihuai/article/details/54864952)
## The Big Data Problem
* 1.数据增长快于计算速度，2. 不断增长的数据源，网络，移动，科学…… 3. 每18个月将大小增加一倍•但是，CPU速度和存储瓶颈将停滞不前
* 一台机器无法处理甚至无法存储所有数据！
* 解决方案是在计算机集群上分发数据

## Apache Spark
* 快速通用的集群计算系统，可与Hadoop互操作
* 通过以下方式提高效率：
    * 内存中的计算原语(原语的意思是执行过程中不可被打断的基本操作) ——> 比普通计算机块100倍
    * 通用计算图
* 通过以下方式提高可用性：   ——> 少了2到5倍的代码量
    * 丰富的APIs 在Scala, Java, Python 
    * 交互式外壳
    
## Spark Model(Spark模型)
* 根据分布式数据集上的转换编写程序
* RDD(s)
    * 可以存储在整个群集的内存或磁盘中的对象的集合
    * 并行功能转换（map, filter等）
    * 故障自动重建

## Spark for Data Science
* DataFrame
    * 结构化的数据
    * 基于Python和R Pandas的熟悉API
    * 分布式优化运行
* Machine Learning Pipelines(机器学习管线)
    * 机器学习工作流程的简单构建和调整

## The Spark Computing Framework
* 提供编程抽象和并行运行时间，以隐藏容错和慢速机器的复杂性

* “这是一项操作，请对所有数据运行”
    * 我不在乎它在哪里运行（您可以安排时间）
    * 实际上，可以在不同的节点上两次运行它 比如：当它失败时

## Apache Spark Ecosystem

![ Apache Spark生态系统](https://github.com/Qianlinnn/ScalableML/raw/master/img2/week1/Apache%20Spark%E7%94%9F%E6%80%81%E7%B3%BB%E7%BB%9F.png) 

## Spark Components(Spark组件)
* Spark程序首先创建一个SparkContext / SparkSession对象（驱动程序）
    * 告诉Spark如何以及在何处访问集群
    * 连接到几种类型的集群管理器（例如YARN或它自己的管理器）
* Cluster manager(集群管理器):
    * 跨应用程序分配资源
* Spark executor(Spark 执行程序) (worker)
    * 进行运算
    * 访问数据存储

![Spark组件](https://github.com/Qianlinnn/ScalableML/raw/master/img2/week1/Spark%E7%BB%84%E4%BB%B6.png)

## Spark and SQL contexts（Spark 和SQL上下文）
* Spark程序是两个程序
    * A driver program(驱动程序)和a workers program(工人程序)
    * work programs在集群节点或者本地线程上运行
* Spark程序首先创建一个SparkContext对象   
    * (目的是)告诉Spark如何以及在何处访问集群
    * pySpark shell自动创建SparkContext
    * （jupyter笔记本）和程序必须创建一个新的SparkContext
    * 2.0.0+：SparkSession作为入口点（RDDDataFrame）
* 程序接下来创建一个sqlContext对象
* 使用sqlContext创建DataFrames

## Spark Essentials: Master(主参数)
* SparkContext / SparkSesion的主参数确定我们使用的集群的类型和大小

![Master_parameters](https://github.com/Qianlinnn/ScalableML/raw/master/img2/week1/Master_parameters.png)

## Spark example(log Mining)

step 1

![example_1](https://github.com/Qianlinnn/ScalableML/raw/master/img2/week1/example_1.png)

step 2

![example_2](https://github.com/Qianlinnn/ScalableML/raw/master/img2/week1/example_2.png)

step 3

![example_3](https://github.com/Qianlinnn/ScalableML/raw/master/img2/week1/example_3.png)

![example_3_2](https://github.com/Qianlinnn/ScalableML/raw/master/img2/week1/example_3_2.png)

![example_3_3](https://github.com/Qianlinnn/ScalableML/raw/master/img2/week1/example_3_3.png)

![example_3_4](https://github.com/Qianlinnn/ScalableML/raw/master/img2/week1/example_3_4.png)

![example_3_5](https://github.com/Qianlinnn/ScalableML/raw/master/img2/week1/example_3_5.png)

step 4

![example_4](https://github.com/Qianlinnn/ScalableML/raw/master/img2/week1/example_4.png)

**Note**: 上面过程的统计‘php’ action函数运行图省略了，因为与第一个mysql的count函数的运行过程是一样的

## Spark Program Lifecycle
* 从外部数据创建DataFrames或从驱动程序中的集合创建createDataFrame
* 懒惰地将它们转换为新的DataFrames
* cache()(缓存)一些DataFrames以便重用
* 执行动作以执行并行计算并产生结果

尽可能使用Spark转换和操作：搜索DataFrame参考API
    