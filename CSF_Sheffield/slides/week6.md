# Week 6: Formal Analysis of Security Protocols

## What are Formal Methods(形式化方法)?

* 当一种语言具有明确定义的语法和语义时，它就是形式语言。 此外，通常会有一个演绎系统来确定陈述的真实性
* 用正式语言指定模型（或构造）是正式的
* 标准协议符号不是正式的。

### Formal Modeling and Analysis of Protocols协议的正式建模和分析

* 目标：对协议及其属性进行正式建模，并提供数学上合理的方式来推理这些模型
* Basis: suitable abstraction of protocols 基础：合适的协议摘要
* Analysis: with formal methods based on mathematics and logic分析：采用基于数学和逻辑的形式方法

### Formal Methods

![1]()

### Overview

![2]()

### Alice & Bob (AnB) Notation:  Message Sequence Charts Alice和Bob（AnB）表示法：消息序列图

![3]()

### A Formal Alice & Bob (AnB) Language 正式的爱丽丝与鲍伯（AnB）语言

![4]()

Role Scripts

* A protocol is described by a role script for each role  name一个协议是通过对每一个校色名来说被每一个角色文本描述被描述
* Role names are variables of type agent 角色名称是代理类型的变量
* Signal (sig) events are used for property specification  and verification信号（sig）事件用于属性指定和验证

## The Dolev-Yao-Style Intruder

### Overview

![5]()

### Danny Dolev & Andrew C. Yao

考虑一个公共密钥系统，其中每个用户用X表示

* 有一个公共加密函数E_X
  * 每个用户都能使用这个函数
* 还有一个私人解密功能 D_X
  * 只有X能使用这个函数

这些函数有个性质E_X D_X = D_X E_X = 1

* Dolev-Yao入侵者：
  * 控制网络（读取，拦截，发送）
  * 也是用户，称为Z
  * 可以将E_X应用于任何X
  * 可以申请D_Z

## Conclusion

* 安全协议很难设计
* 正式方法有助于精确定义协议和安全目标
* 正式方法有帮助！



