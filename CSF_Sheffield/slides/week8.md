# Security Testing

## Static Analysis Overview(静态分析概述)

* Finding security vulnerabilities 查找安全漏洞
  * Static application security testing (SAST) 静态应用程序安全测试（SAST）

 ![1](https://github.com/Qianlinnn/Qianlinnn.github.io/raw/master/CSF_Sheffield/img/week8/1.png)

* Is everything secure?
  * 此工具称为“代码保证工具（cat）” This tool is called “Code Assurance Tool (cat)”  
  * cat工具报告可能包含漏洞的每一行 "The cat tool reports each line that might contain a vulnerability"
  * 它也支持报告不误报的模式 "It supports also a mode that reports no false positives"

* 我们要查找的内容：可能导致安全漏洞的编程模式 What We Want to Find: Programming Patterns That May Cause Security Vulnerabilities
  * 主要有两种模式
    * Local issues (no data-flow dependency), e.g.,   本地问题（不依赖数据流），例如
      * Insecure functions   不安全的功能
      * Secrets stored in the source code 秘密存储在源代码中
    * 数据流相关问题Data-flow related issues, e.g.,
      * Cross-site Scripting (XSS)  跨站点脚本（XSS）
      * Secrets stored in the source code 秘密存储在源代码中

* Trust own developers, i.e., focus on finding "obvious" bugs 信任自己的开发人员，即专注于发现“显而易见的”错误

## Dynamic Analysis Overview  动态分析概述

* Finding security vulnerabilities  查找安全漏洞
  * Dynamic application security testing (DAST) 动态应用程序安全测试（DAST）

![2](https://github.com/Qianlinnn/Qianlinnn.github.io/raw/master/CSF_Sheffield/img/week8/2.png)

* Sniffers and Proxies 嗅探器和代理
  * Tools for inspecting network traffic 检查网络流量的工具
* Sniffers  嗅探器          **Safe**
  * Observe traffic in real-time 实时观察流量
  * Capture traffic for later analysis (or replay)捕获流量以供以后分析（或重放）
  * No modification of traffic/systems  不修改流量/系统
  * Examples: Wireshark, tcpdump 示例：Wireshark，tcpdump
* Intercepting Proxies 拦截代理     **Dangerous**
  * Observe and capture traffic 观察和捕获流量
  * Can block traffic 可以阻止流量
  * Can change traffic/content "in transit" 可以在“运输中”更改流量/内容
  * Modify traffic of systems 修改系统流量
  * Examples: mitmproxy, Fiddler, OWASP ZAP 示例：mitmproxy，Fiddler，OWASP ZAP

## Combining Static and Dynamic Security Testing 结合静态和动态安全测试

* Combining Multiple Security Testing Methods and Tools: Different Test Focus 结合多种安全测试方法和工具：不同的测试重点(CMTMT)
* Risks of only using only SAST 仅使用SAST的风险
  * Wasting effort that could be used more  wisely elsewhere 浪费的精力可以在其他地方更明智地使用
  * Shipping insecure software 运送不安全的软件
* Examples of SAST limitations SAST限制的示例
  * Not all programming languages supported 不支持所有编程语言
  * Covers not all layers of the software stack 不涵盖软件堆栈的所有层
* A comprehensive approach combines 综合方法结合
  * Static approaches (i.e., SAST) 静态方法（即SAST）
  * Dynamic approaches (i.e., IAST or DAST) 动态方法（即IAST或DAST）

![3](https://github.com/Qianlinnn/Qianlinnn.github.io/raw/master/CSF_Sheffield/img/week8/3.png)

* Combining Multiple Security Testing Methods and Tools: Different Risk 结合多种安全测试方法和工具：不同的风险

* Using static analysis has a low security risk  使用静态分析的安全风险低
  * In the worst case, you will learn potential vulnerabilities in your software 在最坏的情况下，您将了解软件中的潜在漏洞
* Dynamic security testing is dangerous! 动态安全测试很危险！你可能：
  *  Break your productive IT landscape (e.g., mistyping an IP address)   打破您的生产IT格局（例如，错误地IP地址）
  * Destroy/corrupt your database (e.g., testing SQL injections) 破坏/破坏您的数据库（例如，测试SQL注入）
  *  Violate compliance policies (granting access to data you should not see) 违反合规政策（授予对您不应该看到的数据的访问权限）
* These are no reasons not to use dynamic tests 没有理由不使用动态测试
  * Approval from the IT department might be necessary  可能需要IT部门的批准
  * Dedicated test systems (and infrastructure) 专用测试系统（和基础架构）
  * Necessary expertise (security and domain/app knowledge) 必要的专业知识（安全性和域/应用知识）

## False Positives and False Negatives 错误肯定和错误否定

* 所有结果都是真实的问题吗？
  * Both static and dynamic tools suffer from false positives (and false negatives)静态和动态工具都遭受假正确（和误错误）

![4](https://github.com/Qianlinnn/Qianlinnn.github.io/raw/master/CSF_Sheffield/img/week8/4.png)

* An informal definition 非正式定义
  * If a static analysis tool reports a finding 如果静态分析工具报告了发现
    * It can be exploitable (true positive) 可以被利用（true positive）
    * It cannot be exploitable (false positive)  无法利用 (false positive)
  * If a static analysis tool does not report a finding 如果静态分析工具未报告发现结果
    * The code is secure (true negative) 代码是安全的(true negative）
    * The code contains a vulnerability (false negative) 代码中包含一个漏洞(false negative)
* Let us take the view point of a 让我们以一个观点
  * Developer: "I want a tool with zero false positives!"  开发人员：“我想要一个零误报的工具！”
    * False positive肯定会造成不必要的努力
  * Security expert: "I want a tool with zero false negatives!" 安全专家：“我想要一个假阴性为零的工具！”
    * False negatives increase the overall security risk 假阴性会增加整体安全风险

## False Negatives (假阴性)Reasons and Recommendations (Examples)

* Fundamental: Under-approximation of the tool (method)基础知识：工具（方法）的近似度较低，	
  * Missing language features (might intercept data flow analysis)  语言功能缺失（可能会拦截数据流分析）
  * Missing support for complete syntax (parsing errors) 缺少对完整语法的支持（分析错误）
    * Report to tool vendor! 向工具供应商报告！
* Configuration: Lacking knowledge of insecure frameworks,  配置：缺乏不安全框架的知识，
  * e.g.,  Insecure sinks (output) and sources (input) 例如，不安全的接收器（输出）和源（输入）
    * Improve configuration! 改善配置！
* Unknown security threats: For us, e.g.,  未知的安全威胁：对我们来说，例如
  * XML verb tampering   XML动词篡改
    * Develop new analysis for tool! (Might require support from tool vendor) 开发工具的新分析！ （可能需要工具供应商的支持）

##  False positive  原因和建议（示例）

* 基础知识：工具（方法）的过度逼近，例如，
  * Pointer analysis 指针分析
  * Call stack 调用堆栈
  * Control-flow analysis 控制流分析
    * Report to tool vendor! 向工具供应商报告！
* Configuration: Lacking knowledge of security framework, e.g.,  配置：缺乏对安全框架的了解，例如
  * Sanitisation functions  消毒功能
  * Secure APIs 安全的API
    * Improve configuration! 改善配置！
* Mitigated by attack surface: Strictly speaking a true finding, e.g,  受攻击面缓解：严格来说是一个真实发现，例如，
  * No external communication due to firewall  由于防火墙而无法进行外部通信
  * SQL injections in a database admin tool 数据库管理工具中的SQL注入
    * Should be fixed! 应该固定！
    * In practice often mitigated during audit, or local analysis configuration 在实践中，通常可以在审核或本地分析配置过程中缓解
* Prioritisation of Findings  A Pragmatic Solution for Too Many Findings 对结果进行优先级排序是对太多结果的实用解决方案
  * What needs to be audited? 需要审核什么？
  * What needs to be fixed? 需要解决什么问题？
    * As security issue (response effort) 作为安全性问题（响应工作）
    * Quality issue 质量问题
  * Different rules for不同的规则
    * Old code 旧代码
    * New code 新代码

## Security Testing: Fuzzing  The Origins  模糊起源

* The term "fuzzing" originates from a  1988 class project, taught by Barton  Miller at the University of Wisconsin  “模糊”一词起源于1988年的一个班级项目，该项目由威斯康星大学的Barton Miller教授

* Core idea 核心思想
  * Create large random strings  创建较大的随机字符串
  * Pipe input into UNIX utilities  将输入管道传输到UNIX实用程序
  * Check if they crash  检查它们是否崩溃
* Very simple, but very effective  很简单，但是很有效

## Fuzzing  Challenges 模糊测试

* Detecting input channel 检测输入通道
  * Tested UNIX utilities accept input as command line argument or via STDIN经过测试的UNIX实用程序接受输入作为命令行参数或通过STDIN
  * In contrast, modern scenarios require support for various protocols and data types (e.g.,  WebRequests using JSON) 相反，现代方案要求支持各种协议和数据类型（例如，使用JSON的WebRequests）
* Input generation 输入生成
  * Tested UNIX tools accepted any string as input 经过测试的UNIX工具接受任何字符串作为输入
  *  In contrast, modern scenarios often require valid input files (e.g. SQL, JPG, JavaScript) 相反，现代方案通常需要有效的输入文件（例如SQL，JPG，JavaScript）

* Deciding if the response is a bug (vulnerability) or not 确定响应是否是错误（漏洞）
  * Tested Unix utilities crashed ("core dump") or hung 经过测试的Unix实用程序崩溃（“核心转储”）或挂起
  * In contrast, modern scenarios are more complex, e.g., fuzzing for finding SQL injections 相反，现代方案更加复杂，例如，模糊查找SQL注入
    * How does the correct response look like? 正确的响应看起来如何？
    * How does an "exploit" look like? “漏洞利用”的外观如何？
    * What is the assessment for a data base error?  对数据库错误的评估是什么？
  * When did we fuzz enough (coverage)?  我们什么时候开始足够的模糊（覆盖）？

## Random Fuzzing 随机模糊

* Very simple 非常简单
* Inefficient 低效
  * Random input is often reject, as a specific format is required 随机输入经常被拒绝，因为需要特定的格式
  * Probability of causing a crash is very low 导致崩溃的可能性非常低
* Likely to generate random HTML documents  可能生成随机HTML文档
  * <html></html>
  * <html>AAAA</html>
  * <html></html></html>
  * <html>/</<>></html> 
  * <html></body>&</body></html>

## Mutation-based Fuzzing 基于变异的模糊测试

* Idea: Mutate existing data samples to create test data想法：对现有数据样本进行突变以创建测试数据
* Little or no knowledge of the structure of the inputs is assumed 假设很少或根本不了解输入的结构
* Anomalies are added to existing valid inputs 将异常添加到现有有效输入中
* Anomalies may be completely random or follow some heuristics 异常可能是完全随机的或遵循一些启发式
* Requires little to no set up time 几乎不需要设置时间
* Dependent on the inputs being modified 取决于要修改的输入
* May fail for protocols with checksums, those which depend on challenge response, etc. 对于带有校验和的协议，依赖于质询响应的协议等，可能会失败。
* Example Tools: Taof, GPF, ProxyFuzz, Peach Fuzzer 示例工具：Taof，GPF，ProxyFuzz，桃子模糊器
* Advantages 优点:
  * Easy to setup and automate 易于设置和自动化
  * Requires little to no knowledge of the input format/protocol  几乎不需要甚至不需要输入格式/协议的知识
* Disadvantages 缺点
  * Effectiveness limited by selection of initial data set  有效性受到初始数据集选择的限制
  * Has problems with file formats/protocols that require valid checksums 文件格式/协议存在问题，需要有效的校验和

## Generation-based Fuzzing 基于世代的模糊测试

* Idea: Define new tests based on models (specifications) of the input format  想法：根据输入格式的模型（规格）定义新测试
* Generate random inputs with the input specification in mind (RFC, documentation, etc.)  根据输入规范（RFC，文档等）生成随机输入
* Add anomalies to each possible spot 将异常添加到每个可能的位置
* Knowledge of the input format allows to prune input that are rejected by the application  了解输入格式后，可以删减应用程序拒绝的输入
* Input can be specified by a grammar (grammar-based fuzzing) 输入可以通过语法指定（基于语法的模糊测试）
* Example tools: SPIKE, Sulley, Mu-4000, Peach Fuzzer 示例工具：SPIKE，Sulley，Mu-4000，桃子模糊器
* Advantages:
  * Completeness (you can measure how much of the specification has been covered) 完整性（您可以衡量已经涵盖了多少规范）
  * Can handle complex inputs (e.g., that require matching checksums) 可以处理复杂的输入（例如，需要匹配的校验和）
* Disadvantages:
  * Building a generator can be a complex problem 建造生成器可能是一个复杂的问题
  * Specification needs to be available 需要特定的配置规格才能用

## Advanced Fuzzing Techniques 先进的模糊技术

* Idea: Generate input based on behaviour/responses of the program 想法：根据程序的行为/响应生成输入
* Greybox-Fuzzing (Concolic Testing) 冲突测试
  * Uses symbolic execution to trigger unused paths  使用符号执行触发未使用的路径
  * Invented by Microsoft and used for fuzzing file input routines (e.g., in MS Office) 由Microsoft发明，用于模糊文件输入例程（例如，在MS Office中）
* Autodafe
  * Fuzzing by weighting attacks with markers通过使用标记加权攻击来进行模糊测试
  * Open Source

* Evolutionary Fuzzing System (EFS) 进化模糊系统（EFS）
  * Generate tests cases/inputs based on code coverage metrics 根据代码覆盖率指标生成测试用例/输入
* AFL (American Fuzzy Lop) and LibFuzzer AFL（美国模糊圈）和LibFuzzer
  * Compile time instrumentation (coverage) and genetic algorithms (mutations) 编译时检测（覆盖）和遗传算法（变异）

## Security of Third-party Components 第三方组件的安全性

## How we develop software

* How it used to be 过去的样子
  * Only few external dependencies  只有很少的外部依赖 
    ("HelloWorld" only requires system libs) （“ HelloWorld”仅需要系统库）
  * Full control over source code 完全控制源代码
* How we do it today
  * Many dependencies  ("HelloWorld" requires over 20 external libs) 许多依赖项（“ HelloWorld”需要20多个外部库）
  * Only control over small fraction of source 仅控制源的一小部分

## Types of Third-party Software

![5](https://github.com/Qianlinnn/Qianlinnn.github.io/raw/master/CSF_Sheffield/img/week8/5.png)

 ## Vulnerabilities in Components 组件中的漏洞Heartbleed

* 想像
  * You are the Chief Product Security Officer for a software vendor  您是软件供应商的首席产品安全官
  * Your products consume many different external libraries  您的产品使用许多不同的外部库
  * Different products consume different versions of the same library 不同的产品使用同一库的不同版本
* Now assume a severe vulnerability in an external library is published  现在假设发布了外部库中的严重漏洞
  * How do you decide which products to fix first?  您如何决定首先修复哪些产品？
  * How do you decide how to fix (upgrade vs. down-port)? 您如何确定修复方法（升级与降低端口）？

## What to do?

![6](https://github.com/Qianlinnn/Qianlinnn.github.io/raw/master/CSF_Sheffield/img/week8/6.png)

* There seem to be an easy fix 似乎很容易解决
  * Always use the latest version, i.e., update your dependencies as quickly as you can! 始终使用最新版本，即，尽快更新依赖项！
* Fast Upgrades Can Create Risks 快速升级会带来风险

## How Can We Minimise the Risk? Design Your Application Securely 如何使风险最小化？ 安全设计应用程序

* Make the part of your application that needs to process critical data as small as possible  (minimise the amount of code that you need to trust)  使您的应用程序中需要处理关键数据的部分尽可能小（最小化您需要信任的代码量）
  * If a third-party library never touches confidential data, a vulnerability in that library is most likely not  critical to you! 如果第三方库从不接触机密数据，则该库中的漏洞对您而言可能不是很关键！

## Select Your Dependencies Wisely 明智地选择您的依赖库

* prefer projects 更喜欢的项目
  * With an active development community 拥有活跃的开发社区
  * That use build systems, programming techniques that you are familiar with 使用您熟悉的构建系统和编程技术
  * That fit your support/release strategy 适合您的支持/发布策略
  * That follow best practices in secure development 遵循安全开发的最佳实践
  * Using security testing tools 使用安全测试工具
  * Publishing regularly fixes and communicate openly about problems 定期发布修复程序并就问题进行公开交流
  * Having coding guidelines (and following them)  制定编码准则（并遵循它们）
  * Smaller components might have a smaller attack surface 较小的组件可能具有较小的攻击面

## Document and Monitor Your Dependencies 记录并监视您的依赖关系

* Maintain a software inventory of all used component versions and where they are used  维护所有使用的组件版本及其使用位置的软件清单
  * There are tools that can help (but they are not perfect), e.g.,  有些工具可以提供帮助（但并不完美），例如，
    * Your build system (e.g., paket, maven, npm) 您的构建系统（例如paket，maven，npm）
    * OWASP dependency checker OWASP依赖项检查器
  * They can also help to check license violations 他们还可以帮助检查违反许可证的情况
  * Do not forget recursive (and hidden) dependencies 不要忘记递归（和隐藏）依赖项
* Check daily for new published vulnerabilities 每天检查是否有新发布的漏洞
  * CVEs (NVD) cover only a small fraction, many projects do not publish CVEs (e.g., only list vulnerabilities on their own website, etc.)   CVE（NVD）仅占一小部分，许多项目不发布CVE（例如，仅在其自己的网站上列出漏洞等）。
  * Again, there are tools to help you, e.g.,同样，有一些工具可以帮助您，例如
    * OWASP dependency checker OWASP依赖项检查器
    * retire.js

## Maintain Your Dependencies (and Applications)

* Upgrade components with security fixes and ship updates to customers 使用安全修复程序升级组件并将更新发送给客户
* Plan for efforts for down-porting patches 规划下移植补丁的工作
* Assign people responsible for maintaining components either  指派负责维护组件的人员
  * Locally in the development team, or在开发团队本地，或
  * Create a global maintenance team 建立全球维护团队
  * Alternatively, there are also companies offering commercial support for (nearly) any component 另外，也有公司为（几乎）任何组件提供商业支持

## Harden Your Development Environment 强化您的开发环境

* Check that you download the right component and, e.g., 检查您是否下载了正确的组件，例如
  * Not one with a similar name  没有一个名字相似的组件
  * Or some forked github repository 或一些分叉的github存储库
* Ensure that downloads are using secure connections (https) and that signatures of signed packages are checked 确保下载使用安全连接（https），并检查已签名软件包的签名
* Use an own "artifactory" (package server) storing 使用自己的“人工工厂”（程序包服务器）存储
  * The currently used version(s) of a component and  组件的当前使用版本和
  * All previously used versions  所有以前使用的版本
* Containerise your build 容器化开发的软件
* Only allow restricted network access from/to the build system/container 仅允许从/到构建系统/容器的受限网络访问

## Secure Consumption of Third-party Libraries  第三方模块的的安全使用

## Research Areas

* Analyse statically vulnerability reports and external software repository   分析静态漏洞报告和外部软件存储库
  *  Which versions (commit ranges) are vulnerable?  哪些版本（提交范围）容易受到攻击？
  * Which API calls are vulnerable?  哪些API调用容易受到攻击？
  * How much did the API change between consumed version and the next fixed version?  API在已使用版本和下一个固定版本之间有多少变化？
* Derive fix recommendations 导出修复建议
* Analyse consuming software (statically and/or dynamically) 分析消耗的软件（静态和/或动态）
  * Is the vulnerable API actually invoked? 实际调用了易受攻击的API吗？
  * Does the consuming software implement protection mechanisms?  消费软件是否实施保护机制？
  * Could the consuming software implement protection mechanisms? 消费软件可以实施保护机制吗？
* Generalise to global cost models 推广到全球成本模型
  * Maintenance of third-party libraries 第三方库的维护
  * Allow project managers to plan average development efforts 允许项目经理计划平均开发工作







