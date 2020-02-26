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

![1]()

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

  ![2]()

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
* Unary ratings
  * Good, purchase