# SSDL

##  CIA Hacking Tools Revealed

* Summary
  * 这是有关中情局对国内外政府和公民使用的黑客手段的泄密事件
* Origin
  * 据称是来自美国弗吉尼亚州兰利市中央情报局网络情报中心的部门

* 体量
  * 7,818个网页和943个附件
* 时限
  * 文件为2013-2016年
* 首先分析
  * 没有证据表明加密已损坏！
  * 利用软件漏洞的非常有效的技术！
    * 使用已知错误和未知错误（零天）
* Conclusion
  * 开发的软件的质量（安全性，正确性……）需要提高！

## 为什么让软件正确那么难？

* 源代码的演变
* 在以下的方面增加了：
  * 代码大小
  * 代码复杂度
  * 产品数量
  * 产品版本
  * 使用的技术（编程语言， 框架）
* 软件维护挑战
  * 用户需求 —>增加系统数量—>增加需要更长的维护时间

## A path Toward(More) Secure Software 通往（更多）安全软件的道路

![1]()

Training: 

* 安全意识 Security awareness 
* 安全编程 Secure programming 
* 威胁建模 Threat modelling  
* 安全测试 Security testing  
* 数据保护和隐私 Data protection and privacy  
* 安全专家课程("硕士") Security expert curriculum ("Masters")

Risk Identification

* 风险识别（“高级威胁建模”）Risk identification ("high-level threat modelling")  
* 威胁建模  Threat modelling 
* 数据隐私影响评估 Data privacy impact assessment

Plan Security Measures

* 规划产品标准合规性 Plan product standard compliance
* 计划安全功能  Plan security features
* 计划安全测试 Plan security tests
* 计划安全响应 Plan security response

Secure Development & Security Testing

* Secure programming 安全编程
* Static code analysis (SAST)  静态代码分析（SAST）
* Code review 代码审查
* Dynamic testing(e.g., IAST, DAST)动态测试
* Manual testing  手动测试
* External security assessment 外部安全评估

A Path Towards(More) Secure Software

* 在SSDL的实施中检查“缺陷”  Check for "flaws" in the implementation of the SSDL
* 理想情况下，发现安全验证 • Ideally, security validation finds
  * 没有可以更早解决/发现的问题 No issues that can be fixed/detected earlie
  * 仅早期无法检测到的问题（例如，不安全的默认配置，缺少安全文档） Only issues that cannot be detected earlier (e.g., insecure default configurations, missing security documentation)

生产环境中的渗透测试不同

* 他们测试实际配置
* 他们测试生产环境（例如，云/托管）

Secure Operations

* 了解安全操作概念 Understanding security operations concepts
* 需要了解/最低特权 Need-to-know/least privilege
* 职责分离 Separation of duties and responsibilities
* 监视特殊特权（例如，操作员，管理员）Monitor special privileges (e.g., operators, administrators)
* 标记，处理，存储和销毁敏感信息• Marking, handling, storing, and destroying of sensitive information

Security Response

* Execute the security response plan 执行安全响应计划
* Security related external communication 安全相关的外部通讯
* Incident handling 事件处理

* Security patches 安全补丁
* Monitoring of third party components 监控第三方组件

## Secure Software Development Lifecycle for Cloud/Agile 云/敏捷的安全软件开发生命周期

![2]()



## Summary

* 应用程序/软件安全性很重要
* 攻击者（和政府）利用软件漏洞
* 回顾著名的iPhone案例：FBI支付了超过100万美元以使用iPhone
* 对实际加密（即数学）的攻击很少（但同样有效）
* 应用程序/软件安全主要是软件工程/编程问题！



## Threat Modelling

### Motivation 动机

观察：

保护系统很昂贵< ————> 并非所有系统都对攻击者同样有用

* Let’s consider you want to secure your bike
  * 您想保护什么？
    * 您的旧城市自行车
    * 您的新款时尚自行车
  * 对谁？
    * 寻常的供给者
    * 有针对性的攻击
  * Available countermeasures 可用的对策
    * 便宜的自行车锁
    * 昂贵的锁
  * 最易损坏的部位
    * 仅锁定前轮
    * 锁定车架

## Threat Modelling As Part of A SSDL 威胁建模作为SSDL的一部分

* 威胁建模是一个过程，通常作为软件开发早期步骤的一部分，通过该过程可以识别，列举和确定潜在威胁的优先级
* 像攻击者一样思考
  * 高价值资产在哪里？
  * 我最容易受到攻击的地方是？
  * 最相关的威胁是什么？
  * 是否有可能没有引起注意的攻击媒介？

## Understanding the Threats and Risks 了解威胁和风险

* 高级攻击媒介

  * 击败安全机制
  * 滥用应用程序功能
  * 利用安全性不足或实施不力

* 请记住，您的应用程序是大型系统的一部分

* 一个简单的应用程序会迅速爆炸成复杂的事物

  ![3]()

* 在考虑全局之前，尽量不要决定体系结构审查或安全评估的范围

* 系统中最薄弱的地方可能不是您所想的

* 掌握了正确的信息，发现漏洞可能只是一个简单的问答环节

* 功能安全性差

* 不安全的功能

## Threat Modelling: what we need

* 商业：了解系统应该做什么，例如，在
  * 场景
  * 用例
* 体系结构：了解信息/数据如何在系统中“流动”，例如：
  * 方框图/组件图 Block/component diagrams
  * 数据流程图 Data-flow diagrams
* 功能安全性：如何打败攻击，例如，在
  * 计划的安全技术/检查/过程 Planned security technologies/checks/processes
* 攻击者的目标：了解攻击者可能想要实现的目标，例如，在
  * 攻击树Attack Trees
  * 威胁树Threat Trees
* 专家团队，例如
  * 软件架构师 Software architect 
  * 产品拥有者  Product owner  
  * 首席开发人员 Lead developer 
  * 安全专家 Security experts  
  * 领域专家 Domain experts
* 一个“结构化”的过程
  * 确保没有忘记重要的方面
  * 确定结果的优先级并记录在案

## Identifying Threats: STRIDE 识别威胁：STRIDE

* STRIDE是CIA常见威胁类型的扩展
  * Confidentiality 保密
  * Integrity 诚信
  * Availability 可用性
* STRIDE
  * Spoofing Identity 欺骗身份
  * Tampering with Data 篡改数据
  * Repudiation 抵赖
  * Information Disclosure 信息披露
  * Denial of Service 拒绝服务
  * Elevation of Privilege 特权提升

## Summary

* 威胁建模通常是一种结构化的头脑风暴方法
* 结果应记录在案
  * 包含已识别的威胁（优先级高！）
    * 辨别威胁/风险是否能被接受
      * 最好有理由说明为什么风险可以接受
    * 或针对已识别威胁的计划对策
      * 理想情况下应该提供信息如何能正确地实施对策

## How to Discuss and Assess Software Security Issues?如何讨论和评估软件安全性问题？

* 我们需要
  * 风险评估的通用方法
    * 通用漏洞评分系统（CVSS）
  * 明确定义的语言，使我们能够命名不同的安全问题，即定义明确的概念/名称
    * OWASP前十名
    * 普通弱点枚举
  * 引用已知漏洞的系统
    * 与供应商无关
      * 常见漏洞和披露（CVE）数据库
      * 美国国家漏洞数据库（NVD）
      * HPI VulnDB
    * 供应商特定的，例如
      * Microsoft安全公告和公告
      * SAP安全说明（仅适用于客户）



## CVSS：Common Vulnerability Scoring System常见漏洞评分系统

* 评估软件漏洞严重性的行业标准
  * 版本3是最新版本，正在逐步取代版本2
  * 正在为将来的第4版收集“愿望清单”
  * 在讲座中，我们将从版本2开始，然后转到版本3
  * 衡量三个关注领域
    * 漏洞固有质量的基本指标 Base Metrics
    * 随时间变化的特征的时间度量 Temporal Metrics
    * 针对特定实施或环境的漏洞的环境度量 Environmental Metrics
  * 将为这些度量标准组中的每个度量标准组生成一个数字分数（通常以包含所有三个值的向量形式发布）

##  CVSS: Common Vulnerability Scoring System

* 这六个指标用于计算BaseScore

![4]()

* BaseScore舍入到小数点后一位

## CVSS：通用漏洞评分系统（版本2）

### Computing the CVSS Base Metrics (Version 2): Example

* 示例：缓冲区溢出漏洞影响Web服务器软件，该软件允许远程用户获得对系统的部分控制权，包括导致系统关闭的能力
* 虽然较低的CVSS分数表示较低的风险，但它们不是“绝对真理”！
* Consider Heartbleed (CVE-2014-0160)
  * 可能会完全泄露服务器密钥
  * CVSS：5.0 / 10
  * 很可能是唯一具有CVSS警告/解释的CVE：



## CVSS: Common Vulnerability Scoring System (Version 3)

* 版本3尝试提供更细粒度的评估
  * 引入了新的指标，例如范围（S）和用户交互（UI）
  * 将旧的指标（例如身份验证（Au））更新为较新的指标，例如，所需权限（PR）
* CVSS v3基本向量
  * 可利用性指标
    *  Attack Vector攻击向量（AV）：Network网络，Adjacent相邻，Local本地，Physical物理
    * Attack Complexity攻击复杂度（AC）：low低，High高
    * Privileges Required 所需特权（PR）：None无，Low低，High高
    * 用户交互（UI）：None无，Required必需
  * Scope（S）：changed，unchanged
  * Impact Metrics 影响指标
    * Confidentiality Impact: High, Low, None 机密性影响：高，低，无
    * Integrity Impact: High, Low, None 诚信影响：高，低，无
    * Availability Impact: High, Low, None 可用性影响：高，低，无











