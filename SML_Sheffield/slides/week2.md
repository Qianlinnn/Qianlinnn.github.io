# RDD
## Key concepts
* Resilient Distributed Datasets(弹性分布式数据集)： 让程序员能够以容错得放视在大型集群上执行计算

* Resilient：容错，能够重新计算由于节点故障而导致丢失或者损坏得分区

* Distributed： 数据位于集群中的多个节点上

* Dataset  分区元素得集合， 如：元组或其他对象(代表您所使用得数据的记录)

* RDD 是Apache Spark中主要的抽象数据对象，也是Spark的核心。 它允许并行操作元素集合

## RDD Traits(RDD特性)

* In-memory(内存中)， 即RDD内部的数据尽可能多的存储在内存中
* Immutable or read only(b不可变或只读): 一旦创建就不会更改， 只能使用对新RDD的转换来进行转换
* Lazy evaluated(惰性评估)：在执行出发操作之前， RDD的数据不可用或无法转换
* Cacheable(可缓存的)： 可以将所有数据保存在一个讲究的存储中，如内存(默认和最优先)或磁盘(由于访问速度而最不受欢迎)
* Parallel(并行)： 并行处理数据
* Typed(类型化)： 即RDD的值是有类型的，例如RDD[Long]或RDD[(Int, String)]。从2.0开始就有了Dataset/Dataframe
* Partitioned(分区化)： RDD中的数据拆分为多个分区，然后分不在集群中的各个节点上(每个JVM可能有一个分区，也可能不对应单个节点)

## RDD operations(RDD操作)
* Transformation: 返回一个新的RDD
    * 当调用转换函数时，没有任何评估，他只是需要一个RDD并返回一个新的RDD
    * Transformation function 包括map, filter, flatMap, groupByKey, reduceBykey, aggregateByKey, filter, join, etc.
    
* Action: 评估并且返回一个新的值
    * 在RDD对象上调用Action函数时， 此时将计算所有数据处理查询，并返回结果值
    * Action操作包括 reduce, collect, count, first, take, countByKey, foreach, saveAsTextFile,etc

## Working with RDDs(用RDDs来工作)

* 从一个数据源创建一个RDD
    * 通过一个并行已存在的python集合(列表list)
    * 通过(transforming)转换一个已有的RDDs
    * 从HDFS里的文件或者其他任意存储系统
    
* 对一个RDD使用转换操作：eg. map，filter
* 对一个RDD使用Action操作 eg. collect, count

![RDD工作图](https://github.com/Qianlinnn/ScalableML/raw/master/img/RDD%E5%B7%A5%E4%BD%9C%E5%9B%BE.png)

* 用户可以控制另外两个方面:
    * 持续性
    * 分区
    
## 创建RDDs

* 从HDFS，text files， Amazon S3，Apache HBase， SequenceFiles,以及任何其他 Hadoop 输入格式
    * sc.parallelize()
    * sc.hadoopFile()
    
* 从一个文件中创立一个RDD
    * val inputfile = sc.textFile("...", 4)
        * RDD 分布在4个分区中
        * 元素是输入line
        * 惰性执行意味着现在不执行任何操作

## Spark Transformations(Spark 转换)
* 从已有的datasets创建新的数据集
* 使用惰性评估： 结果不会马上计算出来，而是记住一套装欢应用于base dataset
    * Spark优化所需的计算
    * Spark从故障中恢复
* 一些转换函数如下所示

![转换函数示意图](https://github.com/Qianlinnn/ScalableML/raw/master/img/%E8%BD%AC%E6%8D%A2%E5%87%BD%E6%95%B0%E7%A4%BA%E6%84%8F%E5%9B%BE.png)

## Spark Actions
* 让Spark执行之前transformation的命令来转换源
* Action命令是让Spark获得结果的动作
* 一部分Action函数

![Action函数示意图](https://github.com/Qianlinnn/ScalableML/raw/master/img/action%E5%87%BD%E6%95%B0%E7%A4%BA%E6%84%8F%E5%9B%BE.png)

## Lineage Graph(血统图)
* RDD 保持了血统踪迹()
* RDD 有足够多关于它来源的信息，可以根据稳定存储的数据来计算它的分区
* 举例：如果丢失了错误分区， Spark通过相应的line分区上应用过滤器来重建错误，分区可以在不同节点上并行进行计算，而不必回滚整个程序。

[Lineage详细介绍](https://www.jianshu.com/p/0e0b84d43d67)
## Operation示意图

示意图

![operations示意图](https://github.com/Qianlinnn/ScalableML/raw/master/img/operation%E7%A4%BA%E6%84%8F%E5%9B%BE.png)

逐步示意图

![逐步示意图](https://github.com/Qianlinnn/ScalableML/raw/master/img/%E9%80%90%E6%AD%A5%E7%A4%BA%E6%84%8F%E5%9B%BE.png)

    
## SparkContext
* SparkContext: 是Spark应用程序的Spark入口点,但入口点从2.0版本开始变成了SparkSession

* SparkContext实体创建后可以被用来：
    1.	 创建RDDs
    2.	创建累加器
    3.	创建广播变量：将数据从一个节点发送到其他节点，且这些数据只能读，无法更新，
    4.	进入Spark 服务并开始工作

* SparkContext本质上来说是Spark执行环境的客户端并且作为Spark应用程序的主文件

* 一个Spark 程序必须做的第一件事就是创建SparkContext对象，这个对象可以告诉Spark怎么去进入一个集群

* Spark shell中，变量名为sc的变量已经被创建，它是一种特殊的可识别的解释器的SparkContext

## RDD Persistence(RDD 持续性): Cache/Persist(缓存)

* Spark最重要的功能之一是在内存中跨操作缓存一个数据集

* 当保留(缓存)一个RDD文件时， 每个节点都会储存一部分数据， 你可以在其他action命令中重复使用该文件

* 每个缓存的RDD文件可以使用不同的保存级别来进行存储。
    *如：仅保存在内存：
	    
	    1 将RDD作为反序列化的java对象存储在JVM中
		
		2 如果RDD不能容纳在内存中，这些内存将不会被缓存，并在需要时重新计算
		
		3 这是默认级别

	*内存和硬盘：
		
		1 如果RDD不能容纳再内存，保存这些分区也无法容纳在硬盘， 并且也无法在他们被需要时能够被阅读

## 为什么要缓存RDD：
	
* 如果要再次执行 errors.count()， 这个文件将会被再次载入和计算

* 持久化将会告诉Spark去缓存数据进内存， 并且可以为之后对同样数据进行actioin操作而减少数据载入的花费

* Error.persist()将不执行任何操作，这事一个懒惰的操作，但是RDD会说：先读取此文件，然后缓存内容。 该动作将触发计算和数据缓存。

## Spark Key-Value RDDs

* 跟map reduce类似，spark 也支持 key-values (感觉跟字典类似)
	
* 一组 RDD 的每一个元素都是一个成对的元组（数据无法更改么？）

* 一些key-value 转换方法
    
    1 Reducebykey(返回一个新的分布式数据集对)
	
    2 SortBykey()： 返回一个新的数据对并且根据key以上升趋势排列

    3 Groupbykey(): 返回一个新的数据对

## 面临的挑战
*   1 挑战：如何从各种不同的数据源中执行ETL操作（提取，转换，加载）
    
    解决办法： 一个dataframe的 API可以在外部数据源和Spark的内置RDD上执行相关操作

    2 挑战：执行高级分析（比如机器学习， 图像处理）这些非常难以用相关系统来表达
    
    解决办法： 一个高度扩展的优化器，Catalyst可以使用scala的特征值来添加可组合的规则，控制代码生成，并且定义扩展。

## DataFrame-based API for MLlib:

* 又被称为 “管道” API, 这个API是用于连接构建ML管道的接口

* 在2.0版本中， 这个dataframe-based API 将会变成对于MLlib的初级API
    * 社区投票
    * 如：org.apache.spark.ml, pyspark.ml
    

* 基于RDD模式的API将会进入维护模式：
    * 仍然会有bug修复，但不会有新功能
    * 如: org.apache.spark.mllib, pyspark.mllib

## 构建Spark： 数据框架和数据集
* Dataframe:（架构， 通用无类型）
    * 通过索引进入， 被叫做column（像一个table）
* Dataset(静态类型，强类型)
    * Dataframe = dataset[Row]
    * 在Apache Spark2.0中统一了
* RDD是低级的（如汇编器）， dataframe和数据集建立在RDD之上
* 新的libraries(包)：以Datasets和Dataframe为基础制作

## Unified API
unified API 示意图

![unified API 示意图](https://github.com/Qianlinnn/ScalableML/raw/master/img/Unified%20API%E7%A4%BA%E6%84%8F%E5%9B%BE.png)

## typed and un-typed APIs(类型化和非类型化API)

示意图

![typed and un-typed APIs](https://github.com/Qianlinnn/ScalableML/raw/master/img/typed%20and%20un-typed%20APIs.png)






## Dataset APIs 优点
* 静态类型 且 运行时数据类型安全：
    * SQL的限制最少，直到运行时才出现语法错误
    * DF/DS:在编译时检测到语法错误

* 对结构化和半结构化数据的高度抽象和自定义视图 e.g JSON


* 结构简单的API，
    *丰富的语义和特定于域的操作

* Performance and Optimization
	SQL Catalyst

## DataFrame:
    
    * 具有相同架构的行的分布式集合
    
    * 可以从外部数据源或RDD构造成本质上为Row对象的RDD
    
    * 支持关系运算符（eg where， groupby）以及spark操作
    
    * 懒惰评估： 未实现的逻辑计划

Dataframe示意图

![Dataframe示意图](https://github.com/Qianlinnn/ScalableML/raw/master/img/DataFrame%E7%A4%BA%E6%84%8F%E5%9B%BE.png)

## Compare DF and RDD speed

* Spark Dataframes很快

![df_rdd速度比较示意图](https://github.com/Qianlinnn/ScalableML/raw/master/img/df_rdd%E9%80%9F%E5%BA%A6%E6%AF%94%E8%BE%83%E7%A4%BA%E6%84%8F%E5%9B%BE.png)

## 空间有效性：

![空间有限性比较示意图](https://github.com/Qianlinnn/ScalableML/raw/master/img/%E7%A9%BA%E9%97%B4%E6%9C%89%E6%95%88%E6%80%A7%E6%9F%B1%E7%8A%B6%E5%9B%BE.png)

## Machine learning library (MLlib)
* ML algorithms: 常用的学习算法如分类，回归，聚类，协同过滤

* Featurization（特征化）：特征提取， 转换， 维度下降， 选取

* Piplines（管线）： 用于构建评估并且调整机器学习管线的工具

* Persistence(持久化): 保存和假再算法，模型和管线

* Utilities（实用程序）： 线性代数，统计信息，数据处理等

## Main concepts in pipelines(管线里的主要概念)

* DataFrame: 一种机器学习 dataset，它可以容纳多种数据类型. 例如, 存储文本， 特征向量， 真是标签和预测的不同列

* Transformer(转换器): 将一个DataFrame转换为另一个DataFrame的算法 如： ML算法DataFrane -> 模型

* Pipeline(管线): 将多个Transformer(转换器)和Estimators(估计器)连接在一起以指定一个机器学习工作流

* Parameter(参数): 所有转换器和估计器

# ML Pipelines(机器学习管线)

* ML Pipelines: 用于创建和调整机器学习管线的高级API。

* Spark DataFrame: 将数据的分布式集合组织到命名列中。
    * 关系数据库中的表
    * R或者python的DataFrame
 
 ML pipeline示意图：
 
 ![ML pipeline示意图](https://github.com/Qianlinnn/ScalableML/raw/master/img/ML_Pipeline%E7%A4%BA%E6%84%8F%E5%9B%BE.png):
 
 ## Spark MLlib Piplines
 
 Spark MLlib Piplines代码以及示意图
 
 ![Spark MLlib Piplines代码以及示意图](https://github.com/Qianlinnn/ScalableML/raw/master/img/Spark_MLib_Pipelines%E4%BB%A3%E7%A0%81%E4%BB%A5%E5%8F%8A%E7%A4%BA%E6%84%8F%E5%9B%BE.png)
 
 ## 举例： 文本分类
 
 ![文本处理示意图](https://github.com/Qianlinnn/ScalableML/raw/master/img/%E6%96%87%E6%9C%AC%E5%88%86%E7%B1%BB%E7%A4%BA%E6%84%8F%E5%9B%BE.png)
 
 ## ML Workflow(机器学习工作流)
 
 ![机器学习工作流](https://github.com/Qianlinnn/ScalableML/raw/master/img/%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0%E5%B7%A5%E4%BD%9C%E6%B5%81%E7%A4%BA%E6%84%8F%E5%9B%BE.png)
 
 ## Load Data
 
 ![load_data图1](https://github.com/Qianlinnn/ScalableML/raw/master/img/load_data%E5%9B%BE1.png)
 
 ![load_data图2](https://github.com/Qianlinnn/ScalableML/raw/master/img/load_data%E5%9B%BE2.png)
 
 ## Extract Features
 
 ![extract_features](https://github.com/Qianlinnn/ScalableML/raw/master/img/Extract_features.png)
 
 ![extract_features](https://github.com/Qianlinnn/ScalableML/raw/master/img/Extract_features%E5%9B%BE2.png)
 
 ## train a model
 
 ![train_model](https://github.com/Qianlinnn/ScalableML/raw/master/img/train_moedel.png)
 
 ## evaluate model
 
 ![evaluate_model](https://github.com/Qianlinnn/ScalableML/raw/master/img/evaluate_model.png)
 
 ## ML Pipelines
 
 ![ML pipelines](https://github.com/Qianlinnn/ScalableML/raw/master/img/ML_pipelines%E4%B8%8B%E9%9D%A2%E7%9A%84%E5%9B%BE.png)
 
 ## Parameter Tuning
 
 ![Parameter_tuning]()
 
 ##  How Spark Works
 
* 用户应用程序创建RDD，对其进行转换并运行操作。
* 这导致运算符的DAG（有向无环图)。
* DAG分为多个阶段
* 每个阶段都作为一系列任务（每个分区一个任务）执行

## Word Count in Spark
* 示意图

![word_count_in_spark示意图](https://github.com/Qianlinnn/ScalableML/raw/master/img/word_count%E7%A4%BA%E6%84%8F%E5%9B%BE.png)

## Execution plan

![Execution_plan示意图](https://github.com/Qianlinnn/ScalableML/raw/master/img/execution_plan%E7%A4%BA%E6%84%8F%E5%9B%BE.png)

* The scheduler(排程器)检查RDD的血统图以建立阶段的DAG

* stage是RDD的顺序，二者不能改变顺序

* 两者的边界是 shuffles stage(洗牌阶段)

[map 和flatmap说明](https://blog.csdn.net/WYpersist/article/details/80220211)

## Stage Execution(阶段执行)

![阶段执行](https://github.com/Qianlinnn/ScalableML/raw/master/img/%E9%98%B6%E6%AE%B5%E6%89%A7%E8%A1%8C.png)

* 在新的RDD里为每一个分区创建一个任务
* 序列化任务
* 安排并运送任务去执行
* 所有这些都在内部发生

# Word Count in Spark(作一个整体的视角)
* 在Spark里使用scala统计单词

![whole_view_word_count](https://github.com/Qianlinnn/ScalableML/raw/master/img/whole_view_word_count.png)

## RDD 操作

![RDD操作](https://github.com/Qianlinnn/ScalableML/raw/master/img/RDD%20operation.png)

# Setting the Level of Parallelism](设置并行度)

* 所有对RDD操作都采用可选的第二个参数来表示任务数量
    * words.reduceByKey((x,y) => x + y, 5)
    * words.groupByKey(5)

## Using Local Variables(使用局部变量)
* 在闭包中使用的任何外部变量将自动发送到集群：

* Some Caveats(y一些警告)
    * 每个task(任务)都会得到一个新的copy(副本)
    * 变量必须可以序列化

# Shared Variables(共享变量)：broadcast variable(广播变量) and accumulator(累加器)
* 当使用transformation和action函数来执行动作时， Spark会自动将包含该函数的闭包推送给工作程序，以便它可以在工作程序上运行
* 闭包或数据结构中的任何变量或数据将与闭包一起分发到工作程序节点(很绕)
* 在集群节点上执行某个函数（例如map或reduce）后，该函数使用的变量是所有变量的单独复制品。
* 通常这些变量是常量，但是他们不能通过workers来有效的分享
* 考虑下这些使用场景
    * 具有较大全局变量的迭代或单个作业
        * 将大型只读查询表发送给工作程序
        * 使用ML算法将大型特征向量发送给工作程序
        * 问题: 每次迭代都无法将大数据发送给每个工作程序
        * 解决方案：Broadcast variables广播变量
    * 计算程序执行期间发生的事件
        * 有多少输入行是空白的
        * 有多少输入记录被损坏
        * 问题：闭环只有一个方向：从驱动程序—>工作程序
        * 解决办法： 累加器

## Boradcast Variable
* 允许程序员在每台计算机上保留一个只读变量，而不是将其副本与任务一起发送。
    * 例如，为每个节点有效地提供大型输入数据集的副本
* Spark还尝试使用有效的广播算法分配广播变量，以降低通信成本
* 广播变量是通过调用SparkContext.broadcast（v）从变量v创建的。 可以通过调用value方法来访问其值。
    * e.g. scala > val broadcastVar =sc.broadcast(Array(1, 2, 3))
* 在集群上运行的任何函数中，都应使用广播变量而不是值v，以使v不会多次传送给节点

## Accumulators(累加器)
* 累加器是仅通过关联和交换操作“添加”的变量，因此可以有效地并行支持。
* 用于实现计数器（如MapReduce）或总和
* Spark天然支持数字类型的累加器，程序员可以添加对新数据类型的支持
* 只有驱动程序可以读取累加器的值，而任务不能读取
* 通过调用SparkContext.accumulator（v）从初始值v创建累加器。(见lab2)

      
[什么是闭包](https://zhuanlan.zhihu.com/p/22229197)
[什么是共享变量](https://juejin.im/post/5d1465b7f265da1b7a4b85e9)

    
 
 
 

