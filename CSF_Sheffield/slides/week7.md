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

![1](https://github.com/Qianlinnn/Qianlinnn.github.io/raw/master/CSF_Sheffield/img/week7/1.png)

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

Security Validatioin

* 在SSDL的实施中检查“缺陷”  Check for "flaws" in the implementation of the SSDL
* 理想情况下，发现安全验证 • Ideally, security validation finds
  * 没有可以更早解决/发现的问题 No issues that can be fixed/detected earlie
  * 仅早期无法检测到的问题（例如，不安全的默认配置，缺少安全文档） Only issues that cannot be detected earlier (e.g., insecure default configurations, missing security documentation)

生产环境中的渗透测试不同 Penetration tests in productive environments are different

* 他们测试实际配置 They test the actual configuration
* 他们测试生产环境（例如，云/托管）They test the productive environment (e.g., cloud/hosting)

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

![2](https://github.com/Qianlinnn/Qianlinnn.github.io/raw/master/CSF_Sheffield/img/week7/2.png)



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

* 威胁建模是一个过程，通常作为软件开发早期步骤的一部分，通过该过程可以识别，列举和确定潜在威胁的优先级 Threat modelling is a process, usually as part of the early steps of software development, by which potential threats are identified, enumerated, and prioritized
* 像攻击者一样思考 Think like an attacker
  * 高价值资产在哪里？ Where are the high-value assets?
  * 我最容易受到攻击的地方是？Where am I most vulnerable to attack?
  * 最相关的威胁是什么？What are the most relevant threats?
  * 是否有可能没有引起注意的攻击媒介？ Is there an attack vector that might go unnoticed?

## Understanding the Threats and Risks 了解威胁和风险

* 高级攻击媒介 • High-level attack vectors

  * 击败安全机制 Defeating a security mechanism
  * 滥用应用程序功能 Abusing an application feature
  * 利用安全性不足或实施不力 Exploiting the insufficient security or poor implementation

* 请记住，您的应用程序是大型系统的一部分 Remember, your application is part of a larger system

* 一个简单的应用程序会迅速爆炸成复杂的事物 A simple application explodes quickly into something complex

  ![3](https://github.com/Qianlinnn/Qianlinnn.github.io/raw/master/CSF_Sheffield/img/week7/3.png)

* 在考虑全局之前，尽量不要决定体系结构审查或安全评估的范围 Try not to decide the scope of an architecture review or security assessment before thinking of the big picture

* 系统中最薄弱的地方可能不是您所想的 The weakest point in a system may not be what you think

* 掌握了正确的信息，发现漏洞可能只是一个简单的问答环节 With the right information on-hand, discovering vulnerabilities can be a simple matter of Q&A

* 功能安全性差 Poor functional security

* 不安全的功能  Insecure features

## Threat Modelling: what we need

* 商业：了解系统应该做什么，例如，在 Business: Knowledge what the system should do, e.g., in terms of
  * 场景 Scenarios
  * 用例 Use cases
* 体系结构：了解信息/数据如何在系统中“流动”，例如：Architectural: Knowledge how information/data "flows" in the system, e.g., in terms of
  * 方框图/组件图 Block/component diagrams
  * 数据流程图 Data-flow diagrams
* 功能安全性：如何打败攻击，例如，在 Functional Security: How to defeat an attack, e.g., in terms of
  * 计划的安全技术/检查/过程 Planned security technologies/checks/processes
* 攻击者的目标：了解攻击者可能想要实现的目标，例如，在 Attackers’ Goals: Knowledge what an attacker might want to achieve, e.g., in terms of
  * 攻击树Attack Trees
  * 威胁树Threat Trees
* 专家团队，例如 A team of experts, e.g.
  * 软件架构师 Software architect 
  * 产品拥有者  Product owner  
  * 首席开发人员 Lead developer 
  * 安全专家 Security experts  
  * 领域专家 Domain experts
* 一个“结构化”的过程 A "structured" process to
  * 确保没有忘记重要的方面 Ensure that no important aspects got forgotten
  * 确定结果的优先级并记录在案 Results are prioritized and documented

## Identifying Threats: STRIDE 识别威胁：STRIDE

* STRIDE是CIA常见威胁类型的扩展
  * Confidentiality 保密
  * Integrity 诚信
  * Availability 可用性
* STRIDE
  * Spoofing Identity 欺骗身份
  * Tampering with Data 篡改数据
  * Repudiation 否认某事的真实性或有效性。
  * Information Disclosure 信息披露
  * Denial of Service 拒绝服务
  * Elevation of Privilege 特权提升

## Summary

* 威胁建模通常是一种结构化的头脑风暴方法 Threat modelling often a structured way of brain-storming
* 结果应记录在案  Results should be documented
  * 包含已识别的威胁（优先级高！）Containing the identified threats (with priorities!)
    * 辨别威胁/风险是否能被接受 Either acknowledging that a threat/risk is accepted
      * 最好有理由说明为什么风险可以接受 Ideally with justification why the risk is acceptable
    * 或针对已识别威胁的计划对策 Or the planned countermeasures for an identified threat
      * 理想情况下应该提供信息如何能正确地实施对策  Ideally with information how to test that the countermeasure is implemented correctly

## How to Discuss and Assess Software Security Issues?如何讨论和评估软件安全性问题？

* 我们需要
  * 风险评估的通用方法 A common method for risk assessment
    * 通用漏洞评分系统（CVSS） Common Vulnerability Scoring System 
  * 明确定义的语言，使我们能够命名不同的安全问题，即定义明确的概念/名称 A clearly-defined language that allows us to name different security issues, i.e., well- defined concepts/names
    * OWASP前十名
    * 普通弱点枚举 Common Weakness Enumeration (CWE):
  * 引用已知漏洞的系统 A system for referencing known vulnerabilities
    * 与供应商无关 Vendor-independent, e.g.,
      * 常见漏洞和披露（CVE）数据库 Common Vulnerabilities and Exposures (CVE) Database
      * 美国国家漏洞数据库（NVD）The U.S. National Vulnerability Database (NVD)
      * HPI VulnDB HPI VulnDB
    * 供应商特定的，例如 Vendor-specific,
      * Microsoft安全公告和公告 Microsoft Security Bulletins and Advisories:
      * SAP安全说明（仅适用于客户） SAP Security Notes (only available to customers):



## CVSS：Common Vulnerability Scoring System常见漏洞评分系统

* 评估软件漏洞严重性的行业标准 Industry standard for rating the severity of software vulnerabilities
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

![4](https://github.com/Qianlinnn/Qianlinnn.github.io/raw/master/CSF_Sheffield/img/week7/4.png)

* BaseScore舍入到小数点后一位

## CVSS：通用漏洞评分系统（版本2）

### Computing the CVSS Base Metrics (Version 2): Example

* 示例：缓冲区溢出漏洞影响Web服务器软件，该软件允许远程用户获得对系统的部分控制权，包括导致系统关闭的能力

* 虽然较低的CVSS分数表示较低的风险，但它们不是“绝对真理”！

* Consider Heartbleed (CVE-2014-0160)
  
  * 过去十年中最著名的漏洞之一One of the most well-known vulnerabilities of the last decade
  
  * 可能会完全泄露服务器密钥 Full disclosure of server key possible
  
  * CVSS：5.0 / 10
  
  * 很可能是唯一具有CVSS警告/解释的CVE：
  
    "“ CVSS v2评分评估了该漏洞对漏洞所在主机的影响。 在评估此漏洞对您的组织的影响时，请考虑受保护数据的性质，并根据组织对风险的接受程度采取行动。 尽管CVE-2014-0160不允许无限制地访问目标主机上的内存，但成功的利用会从内存位置泄漏信息，这些内存位置可能包含特别敏感的信息，例如加密密钥和密码。 窃取此信息可能会对信息系统造成其他攻击，其影响将取决于该数据的敏感性和该系统的功能。"



## CVSS: Common Vulnerability Scoring System (Version 3)

* 版本3尝试提供更细粒度的评估
  * 引入了新的指标，例如范围（S）和用户交互（UI）Introduces new metrics such as Scope (S) and User Interaction (UI)
  * 将旧的指标（例如身份验证（Au））更新为较新的指标，例如，所需权限（PR） Updates old metrics such as Authentication (Au) to newer ones, e.g., Privileges Required (PR)
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

## CVSS: Example 1

* Consider the following vulnerability in the database system MySQL  (CVE-2013-0375) 考虑数据库系统MySQL（CVE-2013-0375）中的以下漏洞
  * A vulnerability in the MySQL Server database could allow a remote, authenticated  user to inject SQL code that MySQL replication functionality would run with high  privileges. A successful attack could allow any data in a remote MySQL database to  be read or modified. MySQL Server数据库中的漏洞可能允许经过身份验证的远程用户注入MySQL复制功能将以高特权运行的SQL代码。 成功的攻击可能允许远程MySQL数据库中的任何数据被读取或修改。
* Consider the following vulnerability in Apache Tomcat (CVE-2009-0783) 考虑以下Apache Tomcat中的漏洞（CVE-2009-0783）
  * Apache Tomcat 4.1.0 through 4.1.39, 5.5.0 through 5.5.27, and 6.0.0 through 6.0.18  permits web applications to replace an XML parser used for other web applications,  which allows local users to read or modify the (1) web.xml, (2) context.xml, or (3) tld  files of arbitrary web applications via a crafted application that is loaded earlier than  the target application. Apache Tomcat 4.1.0到4.1.39、5.5.0到5.5.27以及6.0.0到6.0.18允许Web应用程序替换用于其他Web应用程序的XML解析器，从而允许本地用户读取或修改（ 1）通过精心制作的应用程序加载的任意Web应用程序的web.xml，（2）context.xml或（3）tld文件，该应用程序早于目标应用程序加载。
* Consider the following vulnerability in DocuWiki (CVE-2014-9253)
  * DokuWiki contains a reflected cross-site scripting (XSS) vulnerability. This  vulnerability allows an attacker with privileges to upload a malicious SWF file to a  vulnerable site to perform XSS attacks against victims who follow crafted links to  those malicious SWF files. Victims following those crafted links would execute  arbitrary script in the victim’s browser session within the trust relationship between  their browser and the vulnerable serverDokuWiki包含一个反映的跨站点脚本（XSS）漏洞。 此漏洞使攻击者有特权将恶意SWF文件上载到易受攻击的站点，以对受恶意链接到这些恶意SWF文件的受害者进行XSS攻击。 遵循这些精心设计的链接的受害者将在受害者的浏览器会话中，在受害者的浏览器与易受攻击的服务器之间的信任关系内执行任意脚本

## Software Vulnerabilities and Secure Programming

## CWE: Common Weakness Enumeration CWE：常见弱点枚举

* Catalog (ontology) of software weaknesses and vulnerabilities软件弱点和漏洞的目录（本体）
  * A language for describing software vulnerabilities 描述软件漏洞的语言
* Very fine-grained (and not necessarily disjoint) 粒度非常细（不一定是相交的）
* Different "entry points" for browsing, e.g., 用于浏览的不同“入口点”，例如
* New vulnerability types added continuously不断添加新的漏洞类型
* Used in the Common Vulnerabilities and Exposures (CVE) entries在“常见漏洞和披露”（CVE）条目中使用
* "Most critical" vulnerabilities:“最严重”漏洞：CWE-25 

## Software Vulnerability Classes  OWASP Top Ten OWASP软件漏洞类别前十名

* Open Web Application Security Project (OWASP) 开放式Web应用程序安全项目（OWASP）
* Strictly limited to 10 vulnerabilities that developers should focus on ("most critical") 严格限制开发人员应关注的10个漏洞（“最严重”）
* Updated frequently (every few years), based on collecting data from industry 根据行业数据进行频繁更新（每隔几年）
* OWASP Top Ten 2017:OWASP 2017十佳：
  * A1:2017-Injection 
  * A2:2017-Broken Authentication 
  * A3:2017-Sensitive Data Exposure 
  * A4:2017-XML External Entities (XXE)
  * A5:2017-Broken Access Control
  * A6:2017-Security Misconfiguration 
  * A7:2017-Cross-Site Scripting (XSS) 
  * A8:2017-Insecure Deserialization 
  * A9:2017-Using Components with Known Vulnerabilities 
  * A10:2017-Insufficient Logging & Monitoring

## Vulnerability Databases (Reports)  CVE: Common Vulnerabilities and Exposures 漏洞数据库（报告）CVE：常见漏洞和披露

* CVE is a database of software vulnerabilities  CVE是软件漏洞的数据库
  * Each entry has a unique id 每个条目都有唯一的ID
  * Entries usually contain 条目通常包含
    * Textual description of the vulnerability  漏洞的文字描述
    * Description of the affected software and version 受影响软件和版本的说明
    * Type of vulnerability (CWE)  漏洞类型（CWE）
    * Patch/fix instructions (if available) 补丁/修复说明（如果有）
    * Availability of an exploit (a proof of concept that shows how to make use of a vulnerability)  漏洞的可用性（概念证明，显示如何利用漏洞）
    * Standardized risk assessment: Common Vulnerability Scoring System (CVSS) 标准化的风险评估：通用漏洞评分系统（CVSS）
  * No obligation to register CVEs 没有注册CVE的义务
    * Vendors may apply for a CVE id  供应商可以申请CVE ID
    * Security researchers may apply for a CVE id 安全研究人员可以申请CVE ID
    * Most FLOSS projects register CVEs 大多数FLOSS项目都注册了CVE
  * Vendors (or security research firms) may have their system, e g., 供应商（或安全研究公司）可能拥有其系统，例如
    * Microsoft Security Bulletin Microsoft安全公告

## A Closer Look at the OWASP Top Ten A1: 2017 – Injection

## A1: 2017 – Injection: SQL Injection

* “Injection flaws, such as SQL, NoSQL, OS, and LDAP injection, occur when  untrusted data is sent to an interpreter as part of a command or query.  The attacker’s hostile data can trick the interpreter into executing  unintended commands or accessing data without proper authorization.” “当将不可信数据作为命令或查询的一部分发送到解释器时，就会出现诸如SQL，NoSQL，OS和LDAP注入之类的注入缺陷。 攻击者的敌对数据可能会诱使解释器执行未经预期的命令或未经适当授权而访问数据。”
* Input from untrusted sources is used, without further  checking, as part of a database query (i.e., a SQL expression) 来自不受信任来源的输入无需进一步检查即可用作数据库查询的一部分（即SQL表达式）
* Also known as (examples)  
  * CWE-89 – Failure to Preserve SQL Query Structure CWE-89 –无法保留SQL查询结构
* Affected languages  受影响的语言
  * Any programming language that interfaces with a database can be affected, e.g., Python, Java,Ruby, PHP, C#, SQL (stored procedures), ... 与数据库接口的任何编程语言都可能受到影响，例如Python，Java，Ruby，PHP，C＃，SQL（存储过程），...
* Possible impact  可能的影响
  * SQL injections can result in data loss, unauthorized access, SQL注入会导致数据丢失，未授权访问，
* Secure programming recommendation 安全编程建议
  * Use a prepared statement that ensures that query parameters are not used as SQL commands使用准备好的语句确保查询参数不用作SQL命令
* Prepared statements  – Why do they protect us? 准备好的陈述 –他们为什么保护我们？
  * Provide a clear separation between data (e.g., query parameters) and code (e.g., SQL statements)明确区分数据（例如查询参数）和代码（例如SQL语句）
  * Can provide further type checks at compile time (parameter must be an integer, a string, etc.) 可以在编译时提供进一步的类型检查（参数必须是整数，字符串等）
* Prepared statements – A warning! 准备好的声明–警告！
  * Prepared statements seem to be the universal solution to prevent SQL injections.  While this is (mostly) true, they need to be used correctly!准备好的语句似乎是防止SQL注入的通用解决方案。 尽管这是正确的，但仍需要正确使用它们！
  * Consider the following (insecure!) use of a prepared statement 考虑以下（不安全！）对准备好的语句的使用

##  A1: 2017 – Injection: Command Injection A1：2017年–注入：命令注入

* Input from untrusted sources is used, without further checking, as part of a system command.来自不受信任来源的输入将用作系统命令的一部分，而无需进一步检查。
* Also known as (examples)  也称为（示例）
  * CWE-78 – Improper Neutralization of Special Elements used in an OS Command CWE-78 – OS命令中使用的特殊元素的不适当中和
* Affected languages  受影响的语言
  * Any programming language that allows executing system commands can be affected, e.g., Bash,  Python, Java, Ruby, PHP, C#, ... 会影响允许执行系统命令的任何编程语言，例如Bash，Python，Java，Ruby，PHP，C＃，...
* Possible impact  可能的影响
  * Command injections can result in data loss, unauthorized access, ... 命令注入会导致数据丢失，未授权访问，...

* Vulnerable code (Python)
* Secure programming recommendation  
  * Use system call that passes arguments as an array 使用将参数作为数组传递的系统调用
  * Like in SQL injection, subprocess.Popen() can be used insecurely! 与SQL注入一样，subprocess.Popen（）也能不被安全的使用！
* Vulnerable code (Ruby/Rails) 易受攻击的代码（Ruby / Rails）
  * Secure programming recommendation
    * Use system call that passes arguments as additional string arguments 使用将参数作为附加字符串参数传递的系统调用
    * Instead of the open with a pipe, you should use Open3 而不是用管道打开，应该使用Open3
    * Lastly, do not use eval 最后，不要使用eval
* Vulnerable code (Java)
* Secure programming recommendation
  * Use whitelisting 使用白名单

## A2: 2017 – Broken Authentication被破坏的身份验证 eg

**“Application functions related to authentication and session management are often implemented  incorrectly, allowing attackers to compromise passwords, keys, or session tokens, or to exploit  other implementation flaws to assume other users’ identities temporarily or permanently"与身份验证和会话管理相关的应用程序功能常常被错误地实施，从而使攻击者能够破坏密码，密钥或会话令牌，或者利用其他实施缺陷来临时或永久地假定其他用户的身份。**

* Also known as (examples)
  * CWE-259 – Hard-Coded Password CWE-259 –硬编码密码
  * CWE-261 – Weak Cryptography for Passwords CWE-261 –密码的弱密码学
  * CWE-287 – Improper Authentication CWE-287 –不正确的身份验证

* Affected languages 受影响的语言
  * Any framework (or custom implementation) providing authentication, e.g., Python/Django, Ruby/Rails, Java/JSP, ... 提供身份验证的任何框架（或自定义实现），例如Python / Django，Ruby / Rails，Java / JSP，...

* Note
  * Often also caused by insecure business processes (e.g., non-validated password recovery) 通常还由不安全的业务流程引起（例如，未经验证的密码恢复）
* Possible impact 可能的影响
  * Broken authentication can lead to the exposure of resources or functionality to unintended actors, possibly providing  attackers with sensitive information or even execute arbitrary 身份验证失败可能会导致资源或功能暴露给意外的参与者，从而可能为攻击者提供敏感信息甚至执行任意

##  A3: 2017 – Sensitive Data Exposure A3：2017年–敏感数据曝光

**“Many web applications and APIs do not properly protect sensitive data, such as financial, healthcare, and PII.  Attackers may steal or modify such weakly protected data to conduct credit card fraud, identity theft, or other  crimes. Sensitive data may be compromised without extra protection, such as encryption at rest or in transit,  and requires special precautions when exchanged with the browser.”“许多Web应用程序和API不能正确地保护敏感数据，例如金融，医疗保健和PII。 攻击者可能会窃取或修改这些受保护程度不高的数据，以进行信用卡欺诈，身份盗用或其他犯罪。 在没有额外保护的情况下，敏感数据可能会受到损害，例如静态或传输中的加密，并且与浏览器进行交换时需要采取特殊的预防措施。”**

* Also known as (examples)
  * CWE-200 – Information Exposure  CWE-200 –信息暴露
  * CWE-201 – Information Exposure Through Sent Data CWE-201 –通过发送数据公开信息
  * CWE-202 – Exposure of Sensitive Data Through Data Queries CWE-202 –通过数据查询公开敏感数据
* Affected languages
  * All
* Note
  * Often also caused by insecure business processes or using debug mode in production systems通常也是由于业务流程不安全或在生产系统中使用调试模式引起的
* Possible impact
  * Sensitive data exposure can lead to the loss of data, provide additional information to attackers that build  the basis for further attacks, ...敏感的数据泄露可能导致数据丢失，向攻击者提供其他信息，为进一步的攻击奠定基础，...

## A4: 2017 – XML External Entities (XXE)A4：2017年– XML外部实体（XXE）

**“Many older or poorly configured XML processors evaluate external entity references within XML documents. External entities can be used to disclose internal files using the file URI handler, internal file shares, internal port scanning, remote code execution, and denial of service attacks.”许多旧的或配置不当的XML处理器会评估XML文档中的外部实体引用。 外部实体可以使用文件URI处理程序，内部文件共享，内部端口扫描，远程代码执行和拒绝服务攻击来公开内部文件。”**

* Also known as (examples)
  * CWE-611 – Improper Restriction of XML External Entity Reference ('XXE') CWE-611 – XML外部实体引用（'XXE'）的不当限制
* Affected languages 
  * All languages processing XML encoded data, in particular web-based systems, ...所有处理XML编码数据的语言，特别是基于Web的系统，...
* Possible impact
  * XXE often allows attackers to read arbitrary files from the system, denial of service, or  escalation of privileges (e.g., for XML-based authentication systems such as SAML), ... XXE通常允许攻击者从系统中读取任意文件，拒绝服务或特权升级（例如，对于基于XML的身份验证系统，例如SAML），...

* XML Billion Laughs Attack 
  * This looks like an XML document with one root element lolz, containing the entity &lol9 这看起来像一个带有一个根元素lolz的XML文档，其中包含实体＆lol9
  * &lol9 expands to a string containing ten &lol8 entities  ＆lol9扩展为包含十个＆lol8实体的字符串
  * Each &lol8 expands to a string containing ten &lol7, ...每个＆lol8扩展为包含十个＆lol7的字符串，...
  * After full expansion, this small XML documents will contain 109 "lol"s (requiring nearly 3 GB of memory) 全面扩展后，这个小的XML文档将包含10的9次方个“lol”（需要近3 GB的内存）



## A5: 2017 – Broken Access Contro A5：2017年-损坏的访问控制

**“Restrictions on what authenticated users are allowed to do are often not properly  enforced. Attackers can exploit these flaws to access unauthorized functionality and/or  data, such as access other users’ accounts, view sensitive files, modify other users’ data,  change access rights, etc.”“通常没有正确执行对经过身份验证的用户的限制。 攻击者可以利用这些缺陷来访问未经授权的功能和/或数据，例如访问其他用户的帐户，查看敏感文件，修改其他用户的数据，更改访问权限等。”**

* Also known as (examples)
  * CWE-284 - Improper Access Control (3.2) CWE-284-不当访问控制（3.2）

## A6: 2017 – Security Misconfiguration A6：2017年–安全配置错误

**“Security misconfiguration is the most commonly seen issue. This is commonly a result of insecure default configurations, incomplete or ad hoc configurations, open cloud storage, misconfigured HTTP headers, and verbose error messages containing sensitive information. Not only must all operating systems, frameworks, libraries, and applications be securely configured, but they must be patched and upgraded in a timely fashion.”安全配置错误是最常见的问题。 这通常是由于不安全的默认配置，不完整或临时的配置，开放的云存储，错误配置的HTTP标头以及包含敏感信息的详细错误消息所导致的。 不仅必须安全配置所有操作系统，框架，库和应用程序，而且还必须及时修补和升级它们。”**

## A7: 2017 – Cross Site Scripting (XSS) A7：2017年–跨站点脚本（XSS）

* 问题
  * User input is directly displayed in an output web page, without any sanitation.  The typical attack pattern is: 用户输入直接显示在输出网页上，没有任何环境。 典型的攻击模式是：
    * 1 The attacker identifies a web site with XSS vulnerabilities 攻击者识别出具有XSS漏洞的网站
    * 2 The attacker creates a URL that submits malicious input (e.g., including malicious links or  JavaScript code) to the attacked web site 攻击者创建一个URL，该URL向被攻击的网站提交恶意输入（例如，包括恶意链接或JavaScript代码）
    * 3  The attacker tries to induce the victim to click on the URL (e.g., by including the link in an email)   攻击者试图诱使受害者单击URL（例如，通过在电子邮件中包含链接）
    * 4  The victim clicks the URL, hence submitting malicious input to the attacked web site  受害者单击URL，从而向受攻击的网站提交恶意输入
    * 5  The web site response page includes malicious links or malicious JavaScript code (executed on the  victim’s browser) 网站响应页面包含恶意链接或恶意JavaScript代码（在受害者的浏览器上执行）
* Fix(修复)
  * General recommendation: Use a well tested sanitization library (do not write your own)一般建议：使用经过良好测试的杀毒库（请勿自己编写）
  * This example uses the OWASP Java HTML Sanitizer Project 本示例使用OWASP Java HTML Sanitizer项目
* Summary
  * Problem 问题
    * User input is directly displayed in an output web page 用户输入直接显示在输出网页中
  * Affected Languages
    * All programming languages used for building web sites, e.g., Perl, Python, Java, ASP, ASP.NET, JSP,  PHP, C#, VB.Net, Ruby, ...用于构建网站的所有编程语言，例如Perl，Python，Java，ASP，ASP.NET，JSP，PHP，C＃，VB.Net，Ruby，...
  * Countermeasures 应对措施
    * Sanitize any user input which might reach output statements (including statements that write to  a database or that save cookies) 清除可能到达输出语句（包括写入数据库或保存cookie的语句）的所有用户输入
    * Encode the output using HTML encoding, so that any malicious link or JavaScript code remains  uninterpreted by the browser (use custom HTML encoding or custom HTML unencoding to  preserve some safe HTML tags) 使用HTML编码对输出进行编码，以便浏览器无法解释任何恶意链接或JavaScript代码（使用自定义HTML编码或自定义HTML未编码来保留一些安全的HTML标签）

## A8: 2017 – Insecure Deserialization A8：2017年–不安全的反序列化

**“Insecure deserialization often leads to remote code execution. Even if deserialization  flaws do not result in remote code execution, they can be used to perform attacks,  including replay attacks, injection attacks, and privilege escalation attacks.”不安全的反序列化通常会导致远程执行代码。 即使反序列化缺陷不会导致远程代码执行，也可以将它们用于执行攻击，包括重播攻击，注入攻击和特权升级攻击。”**



## A9: 2017 – Using Components with Known Vulnerabilities A9：2017年–使用具有已知漏洞的组件

**“Components, such as libraries, frameworks, and other software modules, run with the  same privileges as the application. If a vulnerable component is exploited, such an attack  can facilitate serious data loss or server takeover. Applications and APIs using  components with known vulnerabilities may undermine application defenses and enable  various attacks and impacts.”“组件（例如库，框架和其他软件模块）以与应用程序相同的特权运行。 如果利用了易受攻击的组件，则此类攻击可能会导致严重的数据丢失或服务器接管。 使用具有已知漏洞的组件的应用程序和API可能破坏应用程序防御，并造成各种攻击和影响。”**



## A10: 2017 – Insufficient Logging & Monitoring A10：2017年–记录和监控不足

**“Insufficient logging and monitoring, coupled with missing or ineffective integration with  incident response, allows attackers to further attack systems, maintain persistence, pivot  to more systems, and tamper, extract, or destroy data. Most breach studies show time to  detect a breach is over 200 days, typically detected by external parties rather than  internal processes or monitoring.”“日志记录和监控不足，再加上事件响应的缺失或无效集成，使攻击者可以进一步攻击系统，保持持久性，转向更多系统以及篡改，提取或破坏数据。 大多数违规研究表明，检测到违规的时间超过200天，通常是由外部各方而不是内部流程或监视来检测。”**

## A Special Class:  Memory Corruption 特殊类别的内存损坏

*  Microsoft: 70% of all security bugs are memory safety issues 微软：所有安全漏洞中的70％是内存安全问题
* Buffer overflow: Problem 缓冲区溢出：问题
  * User data and control flow information (e.g., function pointer tables, return addresses) are  mixed together on the stack and on the heap, hence user data exceeding a buffer may  corrupt control flow information 用户数据和控制流信息（例如，函数指针表，返回地址）在堆栈和堆上混合在一起，因此超出缓冲区的用户数据可能会破坏控制流信息
* Buffer overflow: Memory layout 缓冲区溢出：内存布局
* Buffer overflow: Impact
  * Denial of service (crashing process) 拒绝服务（崩溃过程）
    * Warning: Usually this is only an indication of more severe impact vectors 警告：通常，这仅表示更严重的影响向量
  * Heartbleed (CVE-2014-0160) 
    * CVSS Severity (version 2.0)CVSS严重性（2.0版）
      * CVSS v2 BaseScore: 5.0 MEDIUM  
      * Vector: (AV:N/AC:L/Au:N/C:P/I:N/A:N) 向量：（AV：N / AC：L / Au：N / C：P / I：N / A：N）
    * Impact: Allows unauthorized disclosure of informat 影响：允许未经授权披露信息

* CVE-2006-3444 
  * CVSS Severity (version 2.0)
    * CVSS v2 BaseScore: 7.5 HIGH
    * Vector: (AV:N/AC:L/Au:N/C:P/I:P/A:P)
  * Impact: Allows local users to obtain privileges影响：允许本地用户获得特权
* Buffer overflow: Prevention/Fix 缓冲区溢出：预防/修复
  * Use counted versions of string functions (and read their documentation, see line 7)  使用计数版本的字符串函数（并阅读其文档，请参见第7行）
  * Use safe string libraries, or C++ strings 使用安全的字符串库或C ++字符串
  * Check loop termination and array boundaries 检查循环终止和数组边界
  * Use C++/STL containers instead of C arrays 使用C ++ / STL容器而不是C数组
* Use fgets(buf, n, stdin) instead of gets(buf) 使用fgets（buf，n，stdin）代替gets（buf）

## Buffer overflow: Summary

*  Problem: User data and control flow information (e.g., function pointer tables, return  addresses) are mixed together on the stack and on the heap, hence user data exceeding a  buffer may corrupt control flow information  问题：用户数据和控制流信息（例如，函数指针表，返回地址）在堆栈和堆上混合在一起，因此超出缓冲区的用户数据可能会破坏控制流信息
* Affected Languages
  * C, C++ 
  * Assembly languages 汇编语言
  * Unsafe sections of C# C＃的不安全部分
  *  Runtimes of safe languages (e.g., JVM)  安全语言的运行时（例如JVM）
  * OS interfaces  OS接口
  * External libraries (FFI) 外部库（FFI)
* Countermeasures
  * Use of counted versions of string functions 使用计数版本的字符串函数
  * Use of safe string libraries or C++ strings   使用安全的字符串库或C ++字符串
  * Carefully check loop terminations, array  boundaries, etc. 仔细检查回路终端，阵列边界等。
  * Use of C++/STL containers (instead of arrays)  使用C ++ / STL容器（而不是数组）
  * Check API and use it correctly 检查API并正确使用
  *  • Use of size_t size_t的使用
* Keep Up-to-date With Language Development 与语言发展保持同步
  * Programming languages/tools continue to evolve 编程语言/工具不断发展
    * Learn  学习
    * Avoid deprecated functions  避免使用过时的功能
    * Update your (old) code  更新您的（旧）代码
    * Take compiler warnings serious  认真对待编译器警告
    * Use compilation protections (e.g., -fstack-protector)  使用编译保护（例如-fstack-protector）
    * Avoid old tutorials/books/stack overflow discussions 避免过时的教程/书籍/堆栈溢出讨论

## Why Is It So Difficult? Does this program filter <SCRIPT> tags?该程序是否过滤<SCRIPT>标签？

* And now look at a real sanitisation library 现在看一个真正的卫生库

## Conclusion

* Many vulnerabilities are caused by missing input or output sanitization许多漏洞是由于缺少输入或输出清理而造成的
* In general, use (in this order) 通常，使用（按此顺序）
  * Framework provided counter measures (e.g., SQL prepared statement) 框架提供了对策（例如，SQL预准备语句）
  * Whitelisting 白名单
  * Blacklisting 黑名单
* Avoid writing your own sanitizers, use well tested and widely used implementations, 避免编写自己的杀毒软件，使用经过良好测试和广泛使用的实施方式，例如，





