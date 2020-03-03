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



