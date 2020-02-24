## What's the problem if authenticate without a password using "SQL injection"

![1]()

* 1 Username = '
    * 会弹出提示Syntax error message
    * 因为SQL的结构是username = '''
* 2 Username = ' OR '1' 
    * 该输入会导致第一个输入是空即username是空的，而第二个是true，所以所有的返回都是true,因此能够轻易得到所有数据
    
* 3 username = ' OR 1=1 --';
    * --代表的是comment：注释，他不会对其他的部分产生影响，所以跟case 2一样，返回都是true，能得到所有用户数据
    
* Example 1： 
 
![2]()
    主要输入值用的是最后一个VALUES('student_name')
    
    如： student_name = Alice
    INSERT INTO students (name) VALUES('Alice'); ——> Alice is inserted in students table
    
* Example 2：

![3]()

* 该代码的意思是，将Robert插入students table中，然后删除students table

## Identity and AAA(Authentication, Authorization and Access Control)
* 三个关于安全的基础概念：CIA
    * Confidentiality(保密性)
        * Protecting information from disclosure to unauthorized parties(保护信息不泄露给未授权方)
    * Integrity(完整性) 
        * Protecting information from being  modified by unauthorized parties(保护信息免遭未经授权的各方修改)
    * Availability
        * Ensuring that information is  available (accessible) to  authorized parties(确保授权方可以访问（访问）信息)
        
* To decide if a subject (e.g., a human person) is a member of a  authorized party that can access (i.e., execute an operation such as  read, write, or execute on) an object (resource) (i.e., a physical  object, a function call, data/information), we need to solve
  为了决定一个对象(如：人类)是否可以访问（即执行诸如读取，写入或在其上执行）对象(如物理对象的操作的授权方的成员，函数调用，数据/信息）
    * Identification(身份)
        * Associating an identity with a subject(将身份和主题相关联)
    * Authentication（认证方式）
        * Verifying the validity of something (usually the identity claimed by a system entity)验证事物的有效性（通常是系统实体要求的身份）
    * Authorization (授权动作)
        * Granting (or denying) the right or permission of a system entity to access a object 授予（或拒绝）系统实体访问对象的权利
    * Access Control(访问控制)
        * Controlling access of system entities (on behalf of subjects) to objects based on a  access control policy ("security policy")根据访问控制策略（“安全策略”）控制系统实体（代表主题）对对象的访问

## Mechanisms for identity authentication (身份认证机制)
* The most widely used mechanisms for authentication are
    * something that you forget(know)
        * e.g. a password or a PIN 密码
    * something that you lost(have)
        * e.g. a smart card or a one-time password generator 一次性密码产生器或者一张值智能钥匙卡
    * something that you were
        * e.g. Biometric characteristics e.g., a facial scan/photograph 面部识别
    * Context location, e.g. a place you visited (your current location)
        * e.g. Being physical close to an object, being in a secure building 如异地登陆提醒来辨别
        

## Example  of something that you know: password 密码
* password(密码)
    * 广泛使用(widely used)
    * 很难记住（hard to remember）
    * 不会总是安全的(social enginerring):
    
* 好的密码应该长且随机(good password should be long and random)
* 好的系统(good system)
    * 允许密码有随机长度(Allow for passwords of arbitrary length)
    * 存储密码散列和加盐(Store passwords hashed and salted)

[salt计算机安全意思的由来](https://www.zhihu.com/question/23767509)
* 以下措施真的有帮助吗：
    * 经常更改密码(change password frequently)
    * 使用一个特定的结构,如大写和小谢字母，特殊字符  • Use a certain structure (e.g., upper and lower case characters, special characters)

## 密码是一个好的二因子认证方式吗？(即谈论密码的局限性)
* 用户能更改密码(the password can be changed by the user)即，任何人多可能更改
* PIN是被写在一封信上的(the pin was sent in a letter)即：如果有人捡到了信，那个人就能进入系统

## Example: Hardware Tokens(硬件令牌)
* 示例：
    * 芯片卡(chip card)
    * 一次性密码产生器(One-time password generator)
    * Your UCard
* 我们看到了向软—令牌的转变，例如您手机上的一次性密码应用(we see a shift towards soft-tokens, e.g. a one-time password app on your mobile)

## Example: Biometric(生物信息)
* Biometric
    * 使用身体特征来验证身份(Uses characteristics of your body to authenticate the identity)
        * 指纹 (Fingerprint)
        * 视网膜扫描 (Retina scan)
    * 乍一看非常有前途 Very promising on the first sight
    * 缺点：看一下好莱坞电影 Downside
    * 许多待解决的问题：
        * 指纹算不算被法律保护的机密
        * 生物传感器有时会被骗
## Access Control Models(访问控制模型):
* 典型的访问控制模型专注于认证上
    * 指定谁可以做什么(许可) Specification of who is allowed to do what(permission)
    * 如何升级/改变许可 How to update/change permissions
* 关系是一个简单的访问控制模型的示例 An example of a simple access control model is a relation
    Subject X Object X request 主体对目标的请求
* 实际上，这个相当复杂
    * 可能取决于系统状态(or context) Might depend on the system state (or context)  
    * 主体和权限会随着时间而变化 Subjects and permissions change over time
    * 访问权也许要求履行义务 Access rights might require the fulfillment of obligations  
    * 运行会有错误 Implementation bugs 
    * 访问控制需要被强制执行 Access control needs to be enforced
## Forms of Access Control(访问控制的格式)
* 访问控制也许会有多种形式
    * 物理保护 physical protection
        * 如：大门，旋转栅门e.g. gates， turnstiles
    * 网络流量 Network traffic：
        * E.g. 防火墙 firewalls
    * 硬件
        * e.g.内存管理 memory management
    * 运行系统 operating system
        *e.g.文件系统 file system
    * 不同的程序有不同的访问控制 Application level
        *e.g. google login, databases

## A Exemplary Infrastructure for Access Control Enforcement 实施访问控制的示例性基础架构   
* policy Enforcement point(PEP) 协议执行点
* policy Decision point(PDP) 协议决定点
* Authentication not shown
![4](

## 协议VS模型 Policies vs Models
* 一份安全协议将会定义什么是被允许或者禁止的
    * 它类似于制定一套法律
    * 根据规则和/或要求定义 Defined in terms of rules and/or requirements
* 一个安全模型是一类系统（及其行为）的（正式）表示形式
    * 在选定的抽象级别上突出显示安全功能
    * 提供制定具体协议的词汇表
    
## The Access Control Matrix Model(访问控制矩阵模型)
* 基于主体对目标物体的权利授予的思想（Based on the ideas of privileges of subjects on objects（Based on the ideas of privileges of subjects on objects）
    * 主体(subjects)： 用户，代理商，团体，
    * 目标物体(ojects): 数据， 内存，文件 data,memory banks, files
    * 权限（privileges): 读，写，更改的权限
* Abstract：抽象
    * a model 一个模型
* implementation：实施
    * 一个机制 A mechanism

### Protection state(保护状态)
* 一个保护状态（关于一系列权限P 是由三个元素组成的（S.O.M）
    * 一系列现在的主体S. A set of current subjects S
    * 一系列现在的目标物体O. A set of current objects O
    * 一个访问控制矩阵M，定义了：
        * 针对每一个主体对目标物体的权限(s,o) 
        * 一个关系 S * O * P
* 举例：
    ![5]()
* Alice, Bob, Charlie are subjects
* File 1, File 2, File 3 are objects
* Matrix entries are set of privileges (rights)

## Role-Based Access Control(RBAC)基于角色的访问控制
* 针对以下两者我们如何才能规范一项协议： How can we formalize a policy for more than
    * 成千上百万的申请访问者
    * 相似数量的目标物体
* 相像一下银行
* 一个访问控制矩阵是最不可能维护的
* 观察：
    * 主体(用户）经常会有角色身份 subjects(users) often have roles
        * e.g.消费者，雇员，学生等等
    * 而同样的身份分享同样的权利
        * 该校学生才可以上课
* RBAC的核心思想
    * 为企业的工作职能创建角色(Create roles for job functions in enterprises)
    * 为用户分配角色（根据他们的职责）Assign users to roles (based on their responsibilities)
    * 为每个角色分配一组权限 Assign a set of permissions to each role
* RBAC通过引入角色来使用户和权限脱钩
    ![6]()
    
## Beyond RBAC
### RBAC要考虑的问题：
* 角色层次结构 Role hierachies
* 谁可以更改权限 who can change permission
* 上下文信息(约束) context information(constraints)
* 用户切换角色(Users switching roles)

* 大部分实际的 RBAC应用程序都是使用扩展/修改的版本
* 广泛使用 widely used
* other access control models
    * 随意访问控制 Discreionary access control
        * 拥有者可以更改权限
        * Unix/linux文件系统
    * 数据分类： 除了将主题分组，还可以将对象分组
        * 可以扩展到la Bell-LaPadula的信息流模型
            * 数据分类层次
            * 有的人可以将数据从较低分类的文档复制到较高分类的文档
            * 有的人值能阅读分类较低的文件
        * 如何对信息进行重新分类？
# Next Generation Access control
* 传统访问控制（如本讲座所述）重点
    * 控制对文档/数据/信息的访问
    * 快速评估/决定的决定
    * 可以立即执行的决定
* 今天，我们在许多领域转向使用控制
    * 控制文件的使用
        * 您可以阅读这本书，但不能将其赠与他人
        * 您可以在接下来的两周内看三遍电影
    * 您可能会遇到DRM（数字版权管理）形式的使用控制
        * “媒体行业”非常喜欢DRM
    * 用于使用控制/ DRM的技术
        * 加水印（违反/滥用是经济/法律上的追究）
        * 监视（在封闭/受信任的环境中更轻松，例如，使用受信任的操作系统和/或受信任的查看器）
    * 使用控制方面的挑战和未解决的问题
        * 技术（示例）
            * 如何有效实施使用控制
            * 如何在开放环境中实施使用控制
        * Ethical(道德)
        