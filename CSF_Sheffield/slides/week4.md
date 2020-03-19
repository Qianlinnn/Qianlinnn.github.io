# Week 4:  Signatures and PKIs

## Motivation:

* 公钥密码术出生于1975年5月，是两个问题的孩子：密钥分发问题和签名问题。 该发现不是解决方案，而是认识到可以完全解决两个问题，每个问题从定义上看都无法解决，并且这两个问题的解决方案都在一个软件包中。

![1]()

对称钥匙就是每对用户之间都有单独的密钥，所以是n(n-1)/2

![2]()

非对称钥匙就是每个用户有个私钥。所以是n个



## The digital signature problem

* problem: 如何知道我们的数据来源于一个特定的实体呢
  * Public-key cryptography支持知道和向证明人证明 —> The non repudiation property不可否认属性

## Digital signature requirements

* 签名在authentication和non repudiation方面是基础的
* Nomenclature and set-up
  * M 是一个可以被用来标记的信息集
  * S 是标记的基本元素集合，如： n-bit 字符串
  * S_A:M —> S 就是一个对实体A的签名转换过程
  * V_A: M X S —> {true, false}是一个认证转换，并且是众所周知的
* S_A 和 V_A和构成了对A的数字签名方案的主要算法（转换）。

## Digital signature Scheme

![4]()

* Signing procedure(签署程序): A创造了一个m∈M的签名通过：
  * 计算 s = S_A(m)并且传输数据对(m,s)
* Verification procedure(验证程序) B验证了A的签名（m,s)通过：
  * 计算 u = V_A(m,s). B验证了A的签名如果u = ture
* 而对除了A以外的其他实体，很难找到有效的方法

## 实施数字签名(1/2)

* 可以基于（可逆）公共密钥加密方案(reversible public key encryption schemes)。
* 考虑到E_e: M —> C是一个公共密钥转换过程，更进一步的，假定M=C, 如果D_d是相对应E_e的解密过程，因为两者都是排列：D_d(E_e(m)) = E_e(D_d(m)) = m  对于所有的m ∈ M，一个这种模式的公共密钥加密叫做可逆的
* 建立一个数字签名模式：
  * 1 让M和C分别成为信息和签名空间
  * 让(e,d)成为一个公共密钥加密模式的钥匙对
  * 定义标记方程S_A成为D_d 如 s = D_d(m)
  * 将V_A按以下定义：
    * ![5]()

## 实施数字签名(2/2)

![6]()

* 为了防止伪造，标记信息通常是一个固定的结构，如：
  * 信息的名称是它的发件人
  * 加密哈希标记跟随着信息一起传送

对pairs(密钥对)另外加密以确保机密性

## The Essence of public key infrastructure(PKIs)(公钥基础设施的本质)

* 通过定义：
  * 一个公共密钥加密/签名模式需要一个(密钥分布)机制：
    * 它保证所使用的–公钥属于对应方。
    * 密钥管理基础结构称为公钥基础结构（PKI）
* 如果缺少此机制，则可以对任何公钥加密/签名方案进行中间人攻击（MITM）

## Public Key Infrastructures (PKIs)

* PKI是一种基础结构，允许实体识别哪个公钥属于谁（即将公钥绑定到主体）

* 为了加入PKI，Alice：

  * 生成自己的公钥/私钥对
  * 将她的公钥K_A送给每个人都信任的certification authority(认证机构)(CA)，并说“我是爱丽丝，K_A是我的公钥”。

* CA验证爱丽丝是她说的是谁，然后签署一份数字证书，声明:

   "K_A"是Alice的公钥

* 现在：

  * 任何实体，例如Bob现在可以检查证书以获取Alice的公钥，并将其视为有效。
  * Alice也刻意同样类似地得到Bob的公钥K_B

* 因此，CA可以帮助建立相互信任

## PKI services and components

![7]()

PKI服务：

* 链接公钥到了一个实体(certificates)
* 关键生命周期管理（密钥吊销，恢复，更新)

PKI 组件：

* CA:
  * 创建证书并将其发布在路径中(directory)。
  * 在路径中维护证书吊销列表（CRL）。
  * CRL由单个客户端或验证服务积极检查。CRL checked actively by single clients or by validation services.
  * 备份某些密钥（用于密钥恢复或托管）
* Directory(路径)
  * 使用户证书和CRL可用。Makes user certificates and CRLs available
  * 必须唯一标识用户（需要新的/准确的用户数据）Must identify users uniquely (needs fresh/accurate user 
  * 必须高度可用Must be highly available.
* Registration Authority(RA)注册机构
  * 管理注册用户和颁发证书的过程。
  * 确保正确的用户识别
* Clients: PKI的不同用途，例如 身份验证（单向，两向或三向），签名的文档和交易。

## Certificates

* A certificate 是将身份绑定到密钥的令牌(token)

* Example: 颁发机构CA，标记了一个身份到主体的证书(ALice),对应的公钥就是K_Alice,以及发布或到期时间等信息

  ​	![8]()

* 要验证证书，实体Bob必须获得发行者的公钥，并使用它来解密哈希并检查证书中的数据。

* 为了说明证书和证明，让我们考虑一个具体的示例：X.509。

## X.509

* TU-T X.500系列建议书的一部分，该标准定义了身份验证服务的框架。
* X.509中定义的证书结构（证书格式和证书验证）和身份验证协议可用于多种情况，例如 在IPSEC和SSL / TLS中
* 它基于公钥加密（建议使用RSA），哈希和数字签名。
* X.509方案的核心是与每个用户关联的公钥证书，该证书由CA创建，并由CA或用户放置在目录中。

## X.509 components

* Serial Number (SN) 序列号（SN）在此颁发者颁发的证书中必须唯一。 即，对（发布者名称，序列号）必须唯一
* Signature Algorithm Identifier (AI)算法的签名算法标识符（AI）和任何参数，用于对证书进行签名
* Issuer name (CA)颁发者名称（CA）是创建并签署此证书的CA的X.500名称。如果X.500名称已用于不同实体，则为可选的字符串发行者唯一标识符。

![9]()

* Period of validity (T_A)有效期
* Subject name 是证书所引用的用户的名称（即，其公钥经过认证的用户）。 如果X.500名称已被不同实体重用，则可选的位字符串主题唯一标识符。
* Subject public-key info (A_p)(主体公钥信息)识别算法，其参数和使用者的公钥
* Signature(签名)包含其他字段的哈希码，并使用CA的私钥加密。

### The X.509 Certificate

* The certificate of user A issued (并且标记为 K_CA(-1))b CA is:
  * ![10]()
* 为了验证 CA = <<A>>, 并且验证生成的用户公共密钥，Bob会为特定的签名算法获取的公共密钥，并解密签名。
* 然后，Bob使用签名字段中的信息重新计算其他字段中的哈希值。 如果它与解密后的签名相匹配，则在发行人的公钥正确的情况下，签名有效。
* 然后，Bob检查有效期，以确保证书是最新的。

### Trust models: Direct Trust

* Direct Trust(直接信任): 

  * 如果所有用户都订阅相同的CA，则该CA具有共同的信任。
  * 所有用户证书可以放在同一目录中，以供所有用户访问。

  ![11]()

### Trust models: Hierarchical Trust(分层信任)

* Direct trust:对于广大的用户社区来说，拥有多个CA更为实用，每个CA都会向部分用户安全地提供其公共密钥。
* Trust Tree:
  * 信任来自许多根证书。
  * 这些证书可以本身对证书进行认证，也可以对在某个链上仍对其他证书进行认证的证书进行认证。
  * 通过从其证明者向后追溯到其他证明者来验证叶证书的有效性，直到找到直接受信任的根证书为止。

![12]()

### Hierarchical models and Cross-Certification 层次模型和交叉认证

* 假设A和B分别从CA X_1和X_2获得了证书。 如果A无法安全地知道X_2的公钥，则A无法验证B的证书。
* Cross-certification: 如果CA已经交换了自己的公钥，则A可以通过一系列证书获得B的公钥。
* A从目录中获得X_1签名的X_2证书。 因此，A可以持有X_2的公钥（并通过X_1在证书上的签名进行验证）。
* 然后A返回目录并获得X_2签名的B证书，A现在可以使用X_2公钥的受信任副本进行验证
* X.509建议在层次结构中排列CA

### Trust models: Web of Trust 信任模型：信任网络

信任网络：

* direct and hierarchical trust  涵盖了直接和分级信任
* 增加了在旁观者眼中信任的想法（这是现实世界的观点），并且更多的信息会更好。

A certificate is trusted directly, or trusted in some  chain going back to a directly trusted root  certificate (the meta-introducer), or by some  group of introducers.证书是直接受信任的，或者在某个链中可以信任，可以追溯到直接受信任的根证书（元引入者），也可以由某些引入者信任。

### Web of Trust: PGP 信任网：PGP

* Pretty Good Privacy (PGP): 相当好的隐私（PGP）：一种加密程序，广泛用于为电子邮件提供隐私并以数字方式对文件签名
* 它为用户的公共密钥使用基于证书的密钥管理基础结构。
* PGP证书（和密钥管理）在几个重要方面不同于X.509证书
  * PGP密钥可能具有多个签名（甚至是“自签名”)。
  * 每个用户都为他/她认识的人创建并签署证书（因此，不需要中央基础结构）。
  * 每个签名中都包含“信任”概念，并且单个密钥的签名可能具有不同的信任级别（并且证书的用户根据信任级别进行操作）
* 在PGP环境中，任何用户都可以充当证书颁发机构。
  * Digital signatures as form of introduction数字签名作为介绍的形式：当任何用户签署他人的密钥时，他或她都会成为该密钥的介绍者
  * 随着这一过程的进行，它建立了信任网络
* Any PGP user can validate another user’s public key  certificate, but such a certificate is only valid to  another user if he recognizes the validator as a  trusted introducer.任何PGP用户都可以验证另一个用户的公钥证书，但是只有当另一个用户将验证者识别为可信的介绍者时，该证书才对该一个用户有效。
  * 即 您相信我的观点，即只有当您认为我是值得信赖的介绍者时，其他人的密钥才有效
  * 否则，我对其他键的有效性的看法不重要。

### PKI – Key/Certificate Revocation PKI –密钥/证书吊销

* Certificate Revocation List (CRL) signed and maintained by CA CA签署和维护的证书吊销列表（CRL）
  * 发表在目录上
  * 客户端可以主动检查自己（也使用本地缓存），或者使用验证服务来集中收集和检查CRL。
  * 每个CA维护该CA颁发的所有吊销但未过期的证书的列表（同时发给用户和其他CA）
* 撤销原因：
  * 假定用户的私钥已被泄露。
  * 用户不再由CA认证。
  * 假定CA的证书已被盗用。
* X.509：
  * 每个证书均包含有效期。
  * 通常，新证书会在旧证书过期之前颁发。

### X.509 Certificate Revocation X.509证书吊销

每个CRL包括

* the issuer’s name, 发行人的名字，
* the date the CRL was created CRL的创建日期
* the date the next CRL is scheduled to be  issued 计划发布下一个CRL的日期
* an entry for each revoked certificat 每个已撤销证书的条目

每次证书验证都需要咨询CRL

![13]()

### PKI – Key Recovery PKI –密钥恢复

* 如果丢失的密钥或者知道密钥的人无法或不愿意透露它，该如何恢复？
* 三种选择：密钥或密码系统很弱，或者可以将密钥副本放置在某处。
* A key escrow system is a system in which a third party can recover a  cryptographic key密钥托管系统是第三方可以恢复加密密钥的系统
  * For business对于业务（例如恢复备份密钥）
  * or law enforcement或执法部门（用于加密需要授权机构访问的通信的密钥的恢复，例如，加密的信件或电话消息)。

### Conclusion

* Digital signature schemes 数字签名方案
  * 提供：
    * authentication 认证
    * non-repudiation  不可否认
  * Help to solve the “key distribution” problem  帮助解决“密钥分配”问题
  * Can be implemented using reversible public-key crypto systems  (e.g., RSA)可以使用可逆公钥加密系统（例如RSA）实现








