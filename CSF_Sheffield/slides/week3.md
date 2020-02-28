# Week3

## 背景：单向函数

* 一个函数f: X—>Y 是一个单向函数，如果：
  * 对x ∈X来说f很容易计算出所有的y∈Y
  * 但相反的过程很难计算f^(-1)

## one-way trapdoor function[单向陷门函数]([https://baike.baidu.com/item/%E5%8D%95%E5%90%91%E9%99%B7%E9%97%A8%E5%87%BD%E6%95%B0](https://baike.baidu.com/item/单向陷门函数))

* 一个单向陷门函数是一个单向函数
  * 给出额外信息(the trapdoor information)让人容易找到一个x∈X 从而f(x) = y

## Asymmetric(Public-key) Encryption 非对称（公钥）加密

* 一些示例算法：
  * RSA(Rivest-Shamir-Adleman)
    * 非常著名，而且广泛部署
    * 基于难以分解的大数
  * Elliptic Curve Cryptography 椭圆曲线密码学 
    *  著名的替代品，“轻量级”
    * 基于有限域上椭圆曲线的代数结构（寻找最短向量）
  * NTRUE加密
    * 基于将截断的多项式环中的某些多项式分解为系数非常小的两个多项式的商的困难
* 公钥加密是建立在两个密钥的基础上：e 和 d
  * 设计架构是为了给定一对(E_e, D_d)
    * 知道E_e,这是不可行的
    * 给定的c ∈ C 是找到一个m ∈ M, 其重E_e(m) = c
  * 这意味着从e推出d是不可行的
  * E_e组成了一个单向陷门函数，陷门是d
* 公钥e能当作公开信息

![1](https://github.com/Qianlinnn/personal-study-zone/raw/master/CSF_Sheffield/img/week3/1.png)

* 当爱丽丝（Alice）可以确定授权信息e时，公钥加密为她提供了一个向鲍勃（Bob）保密的渠道

![2](https://github.com/Qianlinnn/personal-study-zone/raw/master/CSF_Sheffield/img/week3/2.png)

## 非对称（公钥）加密

* 是以他的发明者名字命名的：Rivest, Shamir, Adleman, 1978
* 被Diffie and Hellman挑战了1976次后才发表
* 安全性来自难以分解的大量数字
  * 密钥是一对大（≥100位数）质数对的函数
* 最受欢迎的公钥算法
* 需要一些基本数论才能体会

## 数论： 质数

* 数 N = {0, 1, 2, ...}        Z = {0,1, -1,...} 	Primes = {2,3,5,7,...}

* 每一个n ∈ N 都有一个独特的质数因子集合

  * 60 = (2^2) * 3 * 5

* 乘以数字很简单，分解数字得到因子数很难

  * 我们不能将大多数大于1024位的数字分解为因数

    

## 数论： Division/Remainder/Modulo

* Divisors： a != 0 divides b (written a|b) if  ∃ m, ma = b

  * examples: 3|6 3 !| 7

* ∀𝑎, 𝑛. ∃𝑞, 𝑟. 𝑎 = 𝑞 × 𝑛 + 𝑟 where 0 ≤ 𝑟< n

  * 这里r是一个余数，而且我们写a mod n = r

  * 如:

    ​	6 = 2*3 + 0   —> 6 mod 3 = 0

* a,b ∈ Z 是一个全等模 n, 如果 a mod n = b mod n

  * 我们把这个写作  We write this as 𝑎 ≡ 𝑏(mod𝑛)  
  * Example: Example: 7 ≡ 10(mod3)

## 数论: GCD

* 对于 a,b ∈ N,  gcd(a,b)带包了最大的公约数
  * 如 60 = 2^2 *3 *5, 14 = 2 * 7, gcd(60,14) = 2
* a, b ∈ N是相互互为质数得如果 gcd(a,b) = 1
* GCD能用欧几得里算法很快算出

![3](https://github.com/Qianlinnn/personal-study-zone/raw/master/CSF_Sheffield/img/week3/3.png)

## 数论： 逆

* 假定a, b ∈ Z 是互为相对素数，那会有一个c ∈ Z 满足 bc mod a = 1, i.e., 我们可以计算 b^(-1) mod a

* 证明：

  * 根据扩展的欧几里得算法，存在𝑥，𝑦∈𝑍其中

    1 = a * x + b * y

  * 现在考虑 module a的两边，  如果a |ax, 我们会有 mod a =1

* 举例： 4 ^(-1) mod 7

  ![4](https://github.com/Qianlinnn/personal-study-zone/raw/master/CSF_Sheffield/img/week3/4.png)

## RSA 算法

* 产生一个 公共/私人 密钥对：
  * 生成两个大的不同的素数 p 和 q
  * 计算 n = pq 且 𝛷 = (𝑝 − 1)(𝑞 − 1)
  * 选取一个e, 1 < e < 𝛷 , 与𝛷 相对互质
  * 计算唯一整数d， 1 < d < 𝛷 ,其中 (e*d) mod(𝛷 ) = 1
  * 返回一个公共密钥(n,e)和一个私人密钥d
* 用密钥(n, e)加密
  * 用整数as∈{0，…，− 1}表示消息
  * 计算 c = (m^e) mod n
* 用密钥d解密：
  * 计算 m  = (c^d) mod n



## RSA example

![5](https://github.com/Qianlinnn/personal-study-zone/raw/master/CSF_Sheffield/img/week3/5.png)



## RSA security

* 给定（n,e)计算密钥d
  * 跟求因子一样难
  * 如果我们可以分解n = pq, 那我们就可以计算出 𝛷 =(p-1)(q-1),因此 𝑑≡ (𝑒^−1)mod 𝛷
* 没有已知的多项式时间算法
  * 但是考虑到分解的进展，𝑛应该至少具有1024位。
* 计算m, 给定c, 和(n,e)
  * 计算e次方根
  * 没有证据表明是否一定要计算d, i.e. 如 去分解n
* 数论上的进展可能会使RSA不安全
* 这对我们的现代IT（安全）基础架构意味着什么？

## 对称和非对称加密

* 实际操作的注意项
  * 通常对称加密会计算的不那么复杂(刚快)
  * 真实世界系统经常建立在
    * 非对称密钥对作为长期密钥
    * symmetric session key 对称会话密钥 
    * 长期密钥被用来加密会话密钥

## 推荐：对称和非对称加密

* 对称
  * 56bits可通过蛮力破解，例如against DES
  * NIST: 直到2013年，至少具有128位的三重DES（具有112个）和AES被认为是安全的
  * BSI：到2021年，至少具有128位的AES被认为是安全的
  * 通常建议使用256位AES
* 非对称
  * 1024位RSA密钥被认为等效于80位对称密钥
  * NIST：2048 RSA被认为在2030年之前都是安全的
  * BSI：3072 RSA被认为在2021年之前是安全的
  * 椭圆曲线密码学使用较短的密钥（例如256位）显得安全
  * 假设没有相关的数学突破

## 攻击加密：攻击加密系统的示例

* 加密方案并非牢不可破
* 为了实现安全的系统，了解一个攻击系统的方式将很有帮助
* 警告：以下幻灯片仅简要介绍了攻击加密系统的主题（使用一些选定的示例攻击）

​	

## 攻击加密： Ciphertext-only Attack(COA)纯密文攻击

* 攻击者只能访问的攻击
  * 密文
  * 并且通常尝试获取对纯文本的访问
* 方法：
  * 蛮力(测试大多数或者大部分的组合)
    * 可以基于预先计算的数据（例如，哈希表或更有效的彩虹表）
  * 统计分析
* 加密算法的标准化流程
  * 审核过程通常需要几年
  * 对大量密文进行详尽的测试，以统计是否偏离随机噪声

## Attacking Crypto: Known Plaintext Attack (KPA)  攻击加密：已知的纯文本攻击（KPA)

* 发动的攻击只能是攻击者能访问的：
  * 纯文本（可能是消息的一部分）
  * 纯文本的密文（或包含纯文本的消息）
  * 并尝试获得对加密的密钥得到进入权限
* 选择明文攻击
  * 攻击者可以为任意明文生成密文
* 今天的情况
  * 目前尚不知道现代密码（例如AES）会容易受到KPA的影响
  * PKZIP流密码的旧版本容易遭受KPA的攻击

## Attacking Crypto: Birthday Attack

* 理念：
  * 利用生日悖论
    * 在一个有23人的房间中，两个人在同一天生日的概率大于0.5
    * 在100人的房间中，概率为0.9999997
  * 重新讨论哈希码
    * 哈希是将可变长度的消息m映射到固定长度的哈希码的函数
    * 对于长度为l的哈希码，可能有(2^I)个哈希码
      * 通常：m比l长得多，因此将一个以上的m映射到相同的哈希码
    * 生日悖论：
      * 如果生成2^(I/2)消息，则发生碰撞的可能性大于0.5

## Attacking Crypto: Random Number Generator Attack: 攻击加密：随机数生成器攻击

* 观察结果
  * 许多密码方案的安全性都取决于强大的随机数生成器，
    * 即无法与将“噪声”与不可预测的随机数序列区分开
  * 人类不利于生成随机数（请考虑密码...）
  * 计算机：许多伪随机数生成器（PRNG）都可以轻松预测
    * 例如，请勿将java.util.Random用于安全性至关重要的实现
  * 用于与安全相关的实现的随机生成器应包括来自物理测量和/或硬件设备的熵
* 知名的案例：
  * Netscape种子
    * Netscape的SSL实施的早期版本使用PRNG，该PRNG使用以下三个输入作为种子：时间，进程ID和父进程ID
  * Java类SecureRandom可能会在Android上的比特币实现中用于ECDSA的k个随机数值生成冲突（2013年）

## Attacking Crypto: Other Attacks

* Chosen-ciphertext attack 
* Chosen-key attack 
* Denial-of-Service (DoS) 
* Man-in-the-middle (MiM) attack 
* Meet-in-the-middle attack 
* Replay attack

## 物理攻击

![6](https://github.com/Qianlinnn/personal-study-zone/raw/master/CSF_Sheffield/img/week3/6.png)

## probing(探测)

* 加强加密实施
  * 特殊技术，使攻击者难以到达加密芯片的电路，电线
  * 应该以某种方式进行设计，以便即使在多重探测的情况下，攻击也仍然足够困难
    * 取决于应用程序和所需的安全级别

## Fault Injection(故障注入)

* 单个和多个比特攻击
* 复杂度随着被攻击比特数量的增加而增加
* 可以考虑使用传感器来提供低级别的安全性
* 更好：在实施过程中牢记故障

## Side-Channel Attacks(侧通道攻击)

* Power Analysis(功率分析)
* Timing 时间安排
* Electromagnetic emission: EM probes 电磁发射：电磁探针

![7](https://github.com/Qianlinnn/personal-study-zone/raw/master/CSF_Sheffield/img/week3/7.png)

* Power Analysis

  * Simple power analysis（SPA）简单功率分析
    * 随时间可视化电源轨迹来阐述功率分析
  * Differential power analysis(差分功率分析)
    * Advanced form of power analysis (功率分析的高级形式)
    * 攻击者可以通过对从多个密码操作中收集的数据进行统计分析，来计算密码计算中的中间值
  * Multiple order attacks: 多阶攻击
    * 二阶，高阶等
    * 包括多个数据源和不同的时间偏移
    * 更困难的攻击

  ## 对策

  * SPA:
    * 避免条件分支泄漏秘密
    * 隐藏冗余操作
  * DPA
    * 最有效和广泛使用：隐藏
      * 使用随机且变化的值使秘密蒙蔽
      * 隐藏统计信息中的秘密

  

  ## Reverse Engineering: 逆向工程

  * 尝试了解电路及其行为

  * 对策
    * 使其难以进入
    * 使用特殊逻辑隐藏电路行为

  ## Conclusion

  * 正确实施加密很难
  * 乍看之下很多安全的实现实际上都是不安全的
  * 通常很难对密码方案的“心脏”进行攻击



[GCD最大公约数递归定理的证明](https://blog.csdn.net/mowayao/article/details/26944181)

其中课后练习题答案练习题第二题的第一小问可以参考这个答案

a|b 代表b能被a整除

[RSA算法原理](https://www.zhihu.com/question/33645891/answer/57512229)


