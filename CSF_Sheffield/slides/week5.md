# Week 5: Security Protocols 安全协议

## Motivation

* RSA，AES等提供（可能）非常好的密码原语

* 我们如何使用这些原语构造安全的分布式应用程序？
  * Securing Internet connections 保护互联网连接
  * E-commerce 电子商务
  * E-banking 电子银行
  * E-voting  电子投票 
  * Mobile communications 移动通讯
  * Digital contract signing 数字合同签署

## Establishing an authentic channel:  NSPK 建立认证的渠道：NSPK

* Alice wants to be sure that she talks to Bob (authenticity)

* Needham and Schroeder proposed in 1978 the following protocol (NSPK) Needham和Schroeder在1978年提出了以下协议（NSPK）

* A nonce (number once) 随机数（一次编号）是一个新的秘密，只有生成它的人才能知道

  ![1]()

## NSPK: Correctness

* Goal: Mutual Authenticity (Two-way Authentication) After executing the protocol  successfully目标：相互认证（双向认证）成功执行协议后
* Alice and Bob can be sure to talk to each other (and not to somebody else)

![2]()

## NSPK: Lowe’s Attack Lowe的进攻

协议通常很小且令人信服，并且常常是错误的

![3]()

## NSPK Lowe’s fix

* Needham-Schroeder with Lowe’s fix. Needham-Schroeder的Lowe修复程序：

![4]()

## Definitions

* 协议由一组规则（约定）组成，这些规则确定两个或更多实体之间的消息交换

* Security (or cryptographic) protocols  安全（或密码）协议使用密码机制来实现安全目标。

Examples: Entity or message authentication, key establishment, integrity,  timeliness, fair exchange, non-repudiation, 示例：实体或消息身份验证，密钥建立，完整性，及时性，公平交换，不可否认性，

## Building a Key Establishment Protocol 建立密钥建立协议

### Scenario: Overview 场景：概述

* An attempt to design a good protocol (from first principles)  尝试设计良好的协议（从第一原理开始）
* 第一步：建立通信体系结构我们选择一个常见的场景（很多）：
  * 一组用户，其中任何两个用户可能希望为随后的安全通信建立新的会话密钥。
    * 成功完成密钥建立（和实体身份验证）只是安全通信会话的开始。 进一步的通信（通常也通过协议）可以基于此密钥
    * 用户不一定诚实！ （稍后再说）
  *  There is an honest server.有一个诚实的服务器
    * 通常称为“受信任的服务器”，但信任≠诚实！ 我们假设诚实的服务器永远不会欺骗，也不会泄露用户机密

### Scenario: The Details 细节

* 因此，在这种情况下，我们考虑具有三个角色的协议：
  * initiator role A (Alice) 发起者角色A（爱丽丝）
  * responder role B (Bob) 响应者角色B（鲍勃
  * server role S 服务器角色S
* 在协议的具体执行中，角色由代理a.k.a 实体a,b,c（charly), s,i(intruder)入侵者
* 我们使用i作为入侵者的名字。 重要提示：在我们的模型中，没有任何代理人知道我不诚实。
* 协议的目的：
  * 在协议的末尾，k_(AB)应该被A和B（并且可能）还有 S（会被立即忘记的）所知晓，而不是其他组织。
  * A和B可以假设k_(AB)是新生成的。newly generated
* 问题的规范化（稍后我们将考虑）：
  * 我们如何规范协议的步骤和目标？
  * 我们如何规范化“知识”，“secrecy”，“newly”

### First Attempt: Specification 首次尝试：规格

* Our first attempt: a protocol that consists of three messages我们的首次尝试：包含三个消息的协议
  * A通过联系S发送要共享会话密钥(key: A,B)的两方的标识来联系
  * S 把密钥 k_(AB)发送给A
  * A 把密钥 k_(AB)传递给B
* k_(AB)不包含任何关于A或者B的信息，他仅仅是代表会话密钥的位串的名称
* 在我们检查该协议的（缺乏）安全性之前，请注意，这是一个非常不完整的协议规范

![5]()

* 仅指定成功运行中传递的消息：
  * 没有收到格式错误的描述消息或根本没有收到消息的情况下的情况
  * 通常针对安全协议执行此操作，因为错误消息通常与安全无关（异常情况如何？）
* 没有规定实体的内部动作
  * 没有规定实体的内部动作，例如 “创建新的K_（AB）”并存储它是A和B的密钥
* 隐式假设：A和B“知道”接收到的消息是协议的一部分
  * 通常会省略网络计算机能够跟踪特定协议运行进度所需的此类详细信息。
  * 这可能包括应使用哪个密钥来解密已加密的收到消息的详细信息。
* 尽管通过仅显示成功运行的消息来指定协议存在明显的局限性，但它仍然是描述安全协议的最流行方法
* 但是，有许多方法已经解决了这些问题，以使符号“消除歧义”

* 等效表示形式：Alice＆Bob表示法：

  ![6]()

  请注意，发送者/接收者的名称（例如，“ A” —>"B"）不是消息的一部分，也不是消息自动（安全地）到达目的地的情况。

### Block Examples First Attempt: A First Problem

* 这个协议有问题吗？会话密钥k_(AB)一定要传输到A和B，而不是其他的第三方
* 在诸如Internet和公司网络之类的典型通信系统中的现实假设：

**安全性假设1：入侵者能够窃听以安全协议发送的所有消息**

—>使用加密算法和关联的密钥。

### Second Attempt: Specification

* Second attempt: 
  * 假定S最初与系统的每个用户U共享一个秘密密钥sk（U，S）：
    * sk(A,S)是S与A的密钥
    * sk(B,S)是S与B的密钥
    * S加密加密信息
* Problems:  
  * Eavesdropping? No.
* 完美的密码学假设加密的消息只能由拥有解密所需密钥的合法收件人读取。 。 。

### Second Attempt: Problems 

* 问题不是协议放弃了密钥k_（AB），而是有关谁还拥有k_（AB）的信息不受保护。
* 入侵者不仅可以窃听已发送的消息，还可以捕获并更改消息

 **安全性假设2：入侵者能够拦截网络上的消息并将消息发送给任何人（使用任何发件人名称）。**

* 入侵者可以完全控制协议消息流经的通道。
  * 入侵者可以完全控制网络
* 与普通的通信协议相比，我们假设恶意代理的最坏情况
  * 尽管在该协议的合法运行中可能不超过4或5条消息，但是入侵者可以参与的变种数量非常多
  * 这些变化涉及无限数量的消息，每个消息都必须满足协议的安全要求

### Second Attempt: A Simple Attack

* 入侵者i只是拦截了从a到b的消息，然后用D代替a的身份（D是任何代理名称）。

=> b认为他与D共享密钥，而实际上他与a共享密钥

![7]()

* 这种攻击的结果将取决于使用该协议的情况，但是可能包括诸如b这样的行为，即向a泄露信息，而该信息本应仅与D共享。
* 尽管我没有获得k_ab，但是我们仍然可以认为该协议已损坏，因为它不满足用户应该知道谁知道会话密钥的要求。
* 但是，还有另一种（更严重的）攻击。 

###  Second Attempt: Another Attack

![8]()

* i更改了从a到s的消息，以便s为a和i生成密钥k_（ai）并使用入侵者的密钥sk（i，s）对其进行加密
* 由于a无法区分供其他主体使用的加密消息，因此她不会检测到更改
  * kai只是表示a的会话密钥的位串的正式名称，因此它会被a接受
  * i 拦截了从a发给b的消息，因此a不会检测到任何异常
* 因此a将相信b已经成功完成了该协议，而 i 知道kai，因此可以伪装成b并学习a发送给b的所有信息。
* 与之前的攻击相反，如果i是已知为s的合法系统用户，则此攻击将成功

**安全性假设3：入侵者可以是合法的协议参与者（内部人员），也可以是外部方（外部人员），或二者兼而有之。**

## Third Attempt: Specification

* 为了克服这些攻击，需要将共享k_（AB）的委托人的名称以密码方式绑定到密钥。 先前的两种攻击均未在修改后的协议上成功
* 该协议已改进到入侵者无法通过窃听或更改诚实方之间发送的消息来对其进行攻击的程度
* 但是，即使现在该协议仍不足以在正常操作条件下提供安全性

![9]()

### Third Attempt: Problem

* 问题源于最初与S共享的长期密钥加密密钥与为每个协议运行生成的会话密钥K_（AB）之间的质量差异。
* 使用会话密钥(Session keys)的原因：
  * 预期他们容易受到攻击（通过密码分析）
  * 不同会话中的通信应分开。 特别是，应该不可能重播先前会话中的消息
* 当在后续会话中重新使用旧密钥（或其他与安全性相关的数据）时，一整类攻击变得可能

**安全性假设4：入侵者能够获取协议的任何“足够旧”的先前运行中使用的会话密钥K_（AB）的值。** （以前的会话密钥都能获取到）

### Third Attempt: Attack 

* i 伪装成 s
* Replay:
* k_ab' 是一个在之前的会话中被a和b使用过的密钥
  * 通过安全性假设1，i 可以被认为能够知道用k_ab'加密过的信息
  * 通过安全性假设4，i 可以被认为知道k_ab'的值
  * 因此当a完成与b的协议，i能够解密接下来用k_ab'加密的后续信息，或者插入或者更改被k_ab'保护的信息的完整性

![10]()

* 即使i没有得到k_ab'的值，重播攻击仍然可以被视为成功的
  * i 已经成功的让a和b接受了一个老的会话密钥
  * 这个攻击可以让i重播在前一个会话区被k_ab'保护的信息
* 当然：只要a和b不检查密钥！
  * 委托人们不会想但会遵循这些协议
  * 可以使用各种技术来使委托人检查会话密钥是否已重播，e.g. the challenge–response method.

Definition: A nonce (“a number used only once”) is a  random value generated by one principal and returned to  that principal to show that a message is newly generated.

定义：随机数（“一个数字仅使用一次”）是由一个主体生成的随机值，并返回给该主体以表明消息是新生成的。

### Fourth Attempt 

* A将她的随机数N_A以及请求用一个新的密钥发给了S
* 如果会话密钥收到了相同的值，则A可以推断出密钥尚未重播（只要会话密钥和随机数以密码方式绑定在一起，使得只有S可以形成这样的推论，这种推论将是有效的。
* N_A只是一个数字
  * 在N_A中没有任何内容可以标识谁创建了它
  * 因此我们也要写N_A 或者认知更好的N_1 或N1

![11]()

* 如果B的加密密钥包含在A的消息的加密部分中，则A可以确保它是最新的
* 令人信服的是，A可能会将这种保证传递给B通过另一种方式
  * B产生了一个随机数N_B并且将它传递给了A通过被密钥K_AB保护
  * A使用密钥K_AB来回复给B（"-1"是为了避免回放信息4)
* 这确实是一个非常著名的安全协议
  * Needham Schroder with Conventional Keys(NSCK)
* 由Needham和Schroeder于1978年出版，它已成为一整套相关协议的基础
* 不幸的是，由于Denning和Sacco的著名攻击，此协议已经不在安全

### Fourth Attempt : Attack

* 问题是假设只有A才能对B的消息4做出正确答复
* 由于可以预期入侵者知道旧会话密钥的值，因此这种假设是不现实的
* i 通过伪造成a并且说明b使用老的密钥 k_ab'

![12]()

### Fifth Attempt 

* 想法：让我们放弃这样一个假设，即B和A都难以向S发送请求
* 现在，协议由B发起，后者先将其随机数N_B发送给A
* A添加了她的随机数N_A并将两者都发送给S，S现在可以在A和B的单独消息中返回K_AB，它们各自的接收者可以将其验证为最新

![13]()

### Fifth Attempt: Observations

* 看起来我们比以前的协议使用更少的消息可以实现更多的目标，但是实际上。 。
  * 在NSCK里，A可以验证B实际上已经收到了密钥
  * 这个密钥确认的属性是在消息4中使用了密钥而实现的
  * 假设{|N_B|}_K_AB不能被不知道K_AB的人所还原
  * 在我们最终的协议中，A和B都无法在成功运行协议的末尾推断出对方实际上已经收到K_AB

### Summary

* 只要使用的加密算法提供了机密性和完整性，并且服务器S正确运行，此协议就可以避免到目前为止我们看到的所有攻击。

* 在为该术语提供确切含义之前，断言该协议是安全是草率的！

* 必须始终相对于目标来考虑协议的安全性

  —>我们需要手段来规范协议和目标

## Notation: Messages

Roles(角色): A, B or Alice, Bob

Agents(代理人): a, b , i

Symmetric Keys(对称密钥): K, K_(AB),...;sk(A,S)

Symmetric Encryption(对称加密)： {|M|}_K

Public Keys(公共密钥): K,pk(A)

private Keys(私密密钥): inv(K), inv(pk(A))

Asymmetric Encryption(非对称加密):{M}_K

Signing(签收):{M}_inv(K)

Nonces（随机数）: NA, N1随机数用在请求或者挑战

Timestamps(时间戳记)：T代表着时间， 如： 用于密钥到期时间

Message concatenation(邮件串联): M1, M2, M3

### Notation: Communication

* Fundamental event 是主体之间的沟通

  ![14]()

* A 和 B叫做 roles

  可以由任何扮演角色的负责人实例化

* Communication is asynchronous通信是异步的

  Sender/receiver names “A ⟶ B” are not part of the message 

* 协议规定了委托人的行为

   或者，协议定义一组事件序列（跟踪)。

### Notation: Protocols

* 典型的协议描述结合了prose(正常文字)，数据类型规范，各种图表，特殊符号和消息序列，例如

  ![15]()

* 它们通常包括有关该协议的属性以及为何应保留的非正式声明
* What does a message A ⟶ B:M actually mean?
*  我们假设入侵者可以在所有通信路径中插入计算机，从而可以更改或复制部分消息，重播消息或散布虚假材料。 我们还假定每个主体都有一个安全的环境，可以在其中进行计算，例如由个人计算机提供的环境。 。 。”

### Protocol Execution(协议执行)

![16]()

* 生成随机数NA，将其与名称连接，并使用pk（B）加密
* Receive a message M:
  * 用inv（pk（A））解密M。 称其为M’，如果解密失败，则拒绝M’
  * 将邮件分为两个随机数NA'和NB。 如果不可能，请拒绝M
  * 检查NA’= NA； 如果没有，拒绝M
* 用pk（B）加密NB并发送到B

## Different Kind of Attacks(不同种类的攻击)

* Man in the middle  (or parallel sessions) attack: A ⟷ i ⟷ B
* Replay (or freshness) attack: 重播（或新鲜度）攻击：重用先前消息的一部分
* Masquerading attack 假装是另一方
* Reflection attack：反射攻击：将传输的信息发送回发起者
* Oracle attack：利用常规协议响应作为加密和解密“服务”
* Binding attack：在不同于原始意图的上下文中/出于不同目的使用消息
* Type flaw attack：替换不同类型的消息字段

**These attack types are not formally defined and there may be overlaps between these  types这些攻击类型未正式定义，这些类型之间可能存在重叠**

### Man-in-the-Middle Attack: Diffie Hellman

* Diffie Hellman Key Exchange 迪福 赫尔曼密钥交换
  * A和B在一个DH组(g,p)达成了一致
  * A产生了大x而且发送half-key(一半密钥) X = g^(x) mod p 给 B
  * B产生了大 y 而且发送half-key(一半密钥) Y = g^(y) mod p 给 A
  * A 和 B都计算密钥 k = Y^x mod p = X^y mod p

Security depends on the difficulty of computing the discrete logarithm of an  exponentiated number modulo a large prime number安全性取决于计算以大质数为模的指数值的离散对数的难度



* Diffie-Hellman（未验证半密钥）可能会受到攻击：

  1. a —> i (b):exp(g,x)
     1. i(a) —>b:exp(g,z)
     2. b —>i(a): exp(g,z)
  2. i(b) —> i(a):exp(g,z)

  a相信分享了密钥exp(exp(g,x),z)给了b

  b相信分享了exp(exp(g,y),z)给了a

  实际上是i 知道了两个密钥

* Prevention: authenticate the half keys, e.g., with digital signatures预防：例如使用数字签名对半键进行身份验证

  ![17]()

* 今天，许多协议都基于Diffie-Hellman，这不是一个坏主意！

### Type Flaw Attacks: The Otway-Rees Protocol (1/2) 类型缺陷攻击：奥特韦-里斯协议（1/2）

* Server-based protocol providing authenticated key distribution (with key  authentication and key freshness) but without entity authentication or key  confirmation 基于服务器的协议，提供经过身份验证的密钥分发（具有密钥身份验证和密钥新鲜度），但没有实体身份验证或密钥确认

  ![18]()

### Type Flaw Attacks: The Otway-Rees Protocol (2/2)

* ![19]()

i 将消息1的一部分重播为消息4（省略了步骤2和3）

![20]()

## Conclusion

* Abadi和Needham（1994，1995）提出的原则：

  * 每条消息都应说明其含义。
  * 明确指定要执行消息的条件。
  * 明确提及名字是否对含义至关重要
  * 明确为什么进行加密：机密性，消息身份验证,消息绑定
  * 明确您要假定的属性。
  * 当心时钟变化（时间戳）。

* Theses:

  * 没有明确目标（和假设）的协议是没有用的
  * 没有精密性证明的协议可能是错误的

* 假设/入侵者模型（遵循Dolev和Yao）

  * 可以控制网络
  * 可以参加协议
  * 可以使用他拥有的密钥撰写/分解消息
  * 不能破坏加密

  =>入侵者的最坏情况假设

* 目标：协议应实现的目标

  * 验证消息，将其绑定到其原始发件人
  * 确保消息的及时性（最近，最新……）
  * 确保某些项目（例如生成的密钥等）的保密性





