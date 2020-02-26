# Cryptography
Cryptography is an enabling technology
密码学是一门 使能技术：使能技术是指一项或一系列的、应用面广、具有多学科特性、为完成任务，而实现目标的技术。

# Clarifying notation
* Cryptography: the science of secret writing 
  密码学：秘密写作的科学
* Steganography(隐写术): the science of hiding messages in other messages or images
  隐写术是将信息隐藏在其他信息或图像里得科学
* Cryptanalysis: The science of analyzing a cryptographic system to break/circumvent its protection
  密码分析：分析密码系统以破坏/规避其保护的科学

## A general cryptographic schema

![1](https://github.com/Qianlinnn/personal-study-zone/raw/master/CSF_Sheffield/img/week2/1.png)

encryption: 加密  decryption:解密
* Symmetric encryption(对称加密)
    * Key1 = Key2(非常容易彼此衍化)
* Asymmetric encryption(public key)
    * Key1 != Key2(互相不容易彼此衍化)
    * 公共密钥Key1 能够被发布，而不会损坏private key(Key2)
* 如果知道密钥得话，加密和解密应该都简单
* 安全取决于密钥得私密性，而不是加密/解密算法

## Encryption & Decryption(加密和解密)
* 我们介绍了
    * 一个有限的集合A， 被叫做alphabet
    * The message space 𝑀 ⊆ 𝐴∗ and M ∈ 𝑀 is a plaintext (message)
      信息空间*M*是A得子集 且M属于*M*是未加密的纯文本
    * The ciphertext space C, whose alphabet may differ from X 
      密文空间𝐶，其字母可能不同于*M*。
    * K denoting the key space of keys
      K代表密钥的密钥空间
* 此外：
    * 每一个*e*∈K决定了一个双射函数(bijective function)从M到C，用E_e表示
        * E_e是一个加密函数
    * 对每一个d ∈ K, D_d代表了从C到M的双射函数(一一对应)
        * D_d是一个解密函数
    * 应用E_e(or D_d)的过程叫做加密和解密
* 加密方案(密码)是由一组集合{E_e|e ∈ K}和对应的集合{D_d|d ∈ K}例如，对每一个e ∈ K,都有一个 d ∈ K ,它们的关系是![2](https://github.com/Qianlinnn/personal-study-zone/raw/master/CSF_Sheffield/img/week2/2.png)
如：
          𝐷_𝑑 = (𝐸_𝑒(𝑚)) = 𝑚, for all 𝑚 ∈ *M*

    * 密钥*e*和*d* 组成了一个密钥对， 有时候用(*e*,*d*)表示
        * 它们可以是相同的(如 对称加密模式的对称密钥)
    * 构建一个加密模式要求一个固定的消息空间*M*, 一个密文空间*C*，和一个钥匙空间*K*, 以及加密转换{𝐸_𝑒|𝑒 ∈ 𝐾}和一个对应的解密转换{𝐷_𝑑|𝑑 ∈ 𝐾} 
    
    ![3](https://github.com/Qianlinnn/personal-study-zone/raw/master/CSF_Sheffield/img/week2/3.png)
 
## Codes
* 代表完整信息的字符串符号
* 最简单和最早的密码学之一
* 是通过一本"code-book"来翻译的
* 如今仍然被使用
## Mono-Alphabetic Substitution Ciphers(单字母替代密码)
* 最简单的密码(该方法已经出现超过2000年了)
* 令𝐾为字母上所有排列的集合。
* 对每一个𝑒 ∈ K， 我们定义了一个加密转换E_e在字符串 m = m_1m_2...m_n∈*M* 当作
        
        E_e(m) = e(m_1)e(m_2)...e(m_n) = c_1c_2...c_n = c
* 为了解密c，计算所有的反排列 d = e^(-1)and
        
        D_d(c) = d(c_1)d(c_2)...d(c_n) = m
        
* E_e是一个简单替换密码或者单字母替换密码
 
## Examples of Substitution Cipher
* D(KHOOR ZRUOG) = HELLO WORLD
   * Caesar cipher [凯撒密码](https://baike.baidu.com/item/%E6%81%BA%E6%92%92%E5%AF%86%E7%A0%81)
* D(Zl anzr vf Nqnz) = My name is Adam
   * [ROT13](https://zh.wikipedia.org/wiki/ROT13)
        * 移动字母13位，只有字母受影响
* D(2-25-5 2-25-5) = BYE BYE
   * Alphanumeric
   * Substitute numbers for letters
    
* Security of Substitution Ciphers
   * Key spaces are typically huge(密钥空间非常巨大)
       * 26个字母 ——> 26!个可能的密钥
   * Trivial to crack using frequency analysis(letters, diagraphs,etc.)使用频率分析（字母，有向图等）可轻松破解
   * 英语的频率基于数据挖掘书籍/文章具体频率如下图所示(意思是我们可以统计一本书里的各个单词的出现频率来根据这个表来从密文逆推出明文)
    
   ![4](https://github.com/Qianlinnn/personal-study-zone/raw/master/CSF_Sheffield/img/week2/4.png)   
   
   * 很容易应用，除了一些短的，非典型的文本
   * 需要更多复杂性来掩盖统计规律(sophistication 复杂性)

## Polyalphabetic Substitution Ciphers(多字母替代密码)
* 创意(Leon Alberti)
    * 使用映射族隐蔽分发
    
* 多字母替代密码是在字母表A上具有块长度𝑡的块密码，其中：
    * 密钥空间K是由A上所有排列的集合 t排列组合而成
    * 加密是通过key e = (p_1,...,p_t)l来加密m = m_1...m_t，公式表示为E_e(m) = p_1(m1)...p_t(m_t)
    * 对e的解密密钥是 ![5](https://github.com/Qianlinnn/personal-study-zone/raw/master/CSF_Sheffield/img/week2/5.png)

* Vigenere Cipher [维吉尼亚密码](https://zh.wikipedia.org/wiki/%E7%BB%B4%E5%90%89%E5%B0%BC%E4%BA%9A%E5%AF%86%E7%A0%81)
    * 密钥由有序的数字e = e_1,...,e_t给出：其中：
        
        ![6](https://github.com/Qianlinnn/personal-study-zone/raw/master/CSF_Sheffield/img/week2/6.png)
      在一个大小为n的字母表上定义一个排列
      
    * Example: English(n=26), with k = 3, 7, 10
        
            m = THI SCI PHE RIS CER TAI NLY NOT SEC URE
        
       then
            
            E_e(m) = WOS VJS SOO UPC FLB WHS QSI QVD VLM XYO
            
            加密方式是k有个几个数，就设置k个字母为一组，然后分别对当前得字母往后移动k_i个位置，就得到了加密得密文
            
* One-time pads(Vernam Cipher) 一次性密码本 弗纳姆演算法
    * 一次性密码本是一个定义在{0，1}得密码
* 一个信息m_1...m_n 是被一个二进制密钥字符串k_1...k_n加密的
   
   ![7](https://github.com/Qianlinnn/personal-study-zone/raw/master/CSF_Sheffield/img/week2/7.png)
   
    Example： 
        
      c = m ⊕ k = (010111)_2 ⊕ (110010)_2 = (100101)_2
      
    ⊕ 代表的是对应的位数相加，但不会影响到下一位去加1

* 因为每一个密钥顺序都是等可能的，因此纯文本也是   
* 如果不重用密钥，则无条件（信息理论）安全！
* 莫斯科与华盛顿之间的通讯先前已通过这种方式获得保障
* 问题：安全地交换和同步长密钥(如何安全的传递下次的密钥)

* Transposition Cipher 换位密码：一种早期的加密方法，与明文的字母保持相同，区别是顺序被打乱了。
* 对于块长度t， 让k成为{1,...t}的排列的集合，对每一个e ∈ K 和 m ∈ M

        E_e(m) = m_e(1) m_e(2)... m_e(t)
        
* 所有这些转换的集合称为换位密码
* 为了解密 c = c_1 c_2 ... c_t计算

    ![8](https://github.com/Qianlinnn/personal-study-zone/raw/master/CSF_Sheffield/img/week2/8.png)

其中d是逆排列
* 字母是不变的
    * 应用频率分析以揭示密文是否为换位
    * 通过对双元音，三元音，单词等进行频率分析来解密
    
* Example
  
  ![9](https://github.com/Qianlinnn/personal-study-zone/raw/master/CSF_Sheffield/img/week2/9.png)
 
 该示例中C是加密文字，图表是明文，加密方法是将明文按照列的方向由左向右进行抄写。解密方法就是知晓排列模式，按从左到右的顺序往下读
 下面的密码棒同理，按照上面所述的方法去左右到右解读，翻译为：这个密码棒(scytale)是换位密码
 
# Composite Ciphers: 复合密码
 
* Ciphers based on either subsitutions or transpositions are insecure
  
   基于替换字母或改变位置是不安全的

* 密码可以被组合：
    * Two substitution 
    
      两次替换字母： 实际上只有一种“更复杂”的替代
    * Two transpositions: 
    
      两次交换位置： 实际上只有一次位置替换
    * Substitution followed by a transposition makes a new harder cipher 
      
      换位后的替换能制造一个更难的密码
* Product ciphers chain combinations of substitutions and transpositions 
  制造置换和换位的密码链组合
    "S-Boxes"混淆了输入位
    "P-Boxes"通过S-Box输入分散了位置
    
  ![10](https://github.com/Qianlinnn/personal-study-zone/raw/master/CSF_Sheffield/img/week2/10.png)
  
* Substitution:Each binary bit of the ciphertext should depend on several parts of the key, obscuring the connections between the two
  密文的每个二进制位应取决于密钥的几个部分，从而使两者之间的连接更加模糊
    * Nonlinear operation
      
      非线性操作
        * Not easily invertible 
          
          不容易取逆
    * Substitutes message bits according to a lookup table 
    
      根据查询表替换消息位
    * Introduces confusion to the cipher: 
      
      对密码引入混乱
* Permutation: Each plaintext digit (bit) affects many ciphertext digits, or each ciphertext digit is affected by many plaintext digits
  
  排列：每个明文数字（位）影响许多密文数字，或者每个密文数字受许多明文数字影响
    * Linear operation 
    
     线性操作
    * Diffuses substituted bits across S-Box inputs 
      
      通过S-Box输入扩大替换位
* Target is to have all bits substituted as soon as possible (in less number of  rounds)
  
  目标是尽快替换所有位置(在尽量少的回合数)
    * Otherwise, performance and cost issues in practice
      
      否则，实践中的性能和成本问题

* One bit change in input should have an impact on every output bit
  
  改变输入一位会对每个输出位造成影响
    * So, it should be a completely different ciphertext
      
      因此，它应该是一个完全不同的密文
      
## Symmetric Cryptography 对称的密码学
* Stream Ciphers 流密码
* Block Ciphers 块密码

### Stream Ciphers 串流加密法
* A stream cipher is one where the block-length is 1 
  
  流密码是块长度为1的密码
* Plaintext digits are combined with a pseudorandom cipher digit stream  (keystream)
  
  纯文本数字与伪随机密码流（密钥流）组合

* Each plaintext digit is encrypted one at a time with the corresponding digit of the keystream in order to give a digit of the ciphertext stream
  
  每个明文数字用密钥流的相应数字一次加密一次，以给出密文流的数字

* Remember Vigenere cipher维吉尼亚密码(substitution)

![11](https://github.com/Qianlinnn/personal-study-zone/raw/master/CSF_Sheffield/img/week2/11.png)

### Block ciphers [区块加密法/分组加密](https://zh.wikipedia.org/wiki/%E5%88%86%E7%BB%84%E5%AF%86%E7%A0%81)
* A block cipher is an encryption scheme that breaks up the plaintext message into strings (blocks) of a fixed length t and encrypts one block at a time
  
  分组密码是一种加密方案，它将明文消息分解为固定长度为t的字符串（块）并一次加密一个块
    * Take a number of bits and encrypt them as a single unit, padding the plaintext so that it is  a multiple of the block size
      
      取多个位并将其加密为一个单元，对明文进行填充，使其为块大小的倍数
* 64/128 bits are common block sizes
  
  64/128位是常见的块尺寸

* Different design strategies(structures) exists
  不同的设计策略(结构)存在
 
 ![12](https://github.com/Qianlinnn/personal-study-zone/raw/master/CSF_Sheffield/img/week2/12.png)
 
* 为区块加密设计结构
    * Feistel Network[费斯妥密码具体见构造细节部分](https://zh.wikipedia.org/wiki/%E8%B4%B9%E6%96%AF%E5%A6%A5%E5%AF%86%E7%A0%81)
    * Substitution-Permutation Network(SPN) 置换排列网络
  
  **上述两个是常见的设计策略**
    * Addition-Rotation-XOR(ARX) 加法-异或运算
    * Adhoc[拉丁文，表示特定制作的](https://zh.wikipedia.org/wiki/Ad_hoc)
    
费斯妥密码如图

![13](https://github.com/Qianlinnn/personal-study-zone/raw/master/CSF_Sheffield/img/week2/13.png)

SPN

![14](https://github.com/Qianlinnn/personal-study-zone/raw/master/CSF_Sheffield/img/week2/14.png)

## Data Encryption Standard(DES)[数据加密标准](https://baike.baidu.com/item/%E6%95%B0%E6%8D%AE%E5%8A%A0%E5%AF%86%E6%A0%87%E5%87%86)
* 1993 NIST Standard
* Feistel network
* Block cipher, encrypting 64-bit blocks,uses 56-bit keys
    * Expressed as 64 bit numbers(8 bits parity checking-key scheduling)
      表示为64位数字（8位奇偶校验–密钥调度）
* First cryptographic standard 第一个加密标准
    * 1977 US federal standard(US Bureau of Standards) 
    * 1981 ANSI private sector standard
* Heavily used in banking applications 在银行应用里广泛使用
    * Extensions like Triple-DES (TDES) used to overcome short  key-length 诸如Triple-DES（TDES）之类的扩展用于克服较短的密钥长度
    * TDES is the only secure version now TDES是目前唯一的安全版本
    
**Note: [TDES三重数据加密法详细说明](https://zh.wikipedia.org/wiki/3DES)**
      
![15](https://github.com/Qianlinnn/personal-study-zone/raw/master/CSF_Sheffield/img/week2/15.png)

Half Block一半块(32位)， Subkey子密钥(48位)

![16](https://github.com/Qianlinnn/personal-study-zone/raw/master/CSF_Sheffield/img/week2/16.png)

## Security of DES
* 人们长期以来一直对DES的安全性提出质疑。 人们一直在猜测密钥长度，迭代次数和S盒的设计。 S盒特别神秘-所有这些常量，没有任何明显的原因或目的。 尽管IBM声称内部工作是经过17年的密集密码分析工作的结果，但有些人还是担心NSA(国家安全局)在该算法中嵌入了一个活板门，因此他们将有一种轻松的方式来解密消息。 Bruce Schneier, Applied
Cryptography, p278
* 国家安全局还向IBM提供了技术建议。 引述Konheim的话说：“我们将S-box送到了华盛顿。 他们回来了，都是不同的。 我们进行了测试，结果通过了。” 人们指出这是NSA在DES中放过陷阱的证据
* 并不知道安全性有保证还是有损害
* 主要的攻击：详尽搜索
    * 一百万美元的计算机使用7个小时 in 1993
    * 7天，基于10,000美元的FPGA机器 in 2006
* 数学攻击
    * 目前还不知道
    * 但是可以使用（线性）密码分析将密钥空间从256减少到243
* Triple-DES 三重DES：使用三个加密阶段
    * 目前还不知道
    * 通过2^112次暴力查找操作
* DES不应用于新应用程序（至少应为TDES）
* 继承者 Advanced Encryption Standard(AES)
    
## Advanced Encryption Standard(AES) [高级加密标准](https://zh.wikipedia.org/wiki/%E9%AB%98%E7%BA%A7%E5%8A%A0%E5%AF%86%E6%A0%87%E5%87%86)
* SPN(置换排列网络)
* 128-bit block size, 128/192/256-bit key sizes(key scheduling)

   AES的区块长度固定为128比特，密钥长度可以是128，192或256比特
* NIST Standard cipher for encryption(2001)   
  美国国家标准与技术研究院于2001年发布的加密标准密码

* Widely-used in many applications
  在许多应用广泛使用
  
![17](https://github.com/Qianlinnn/personal-study-zone/raw/master/CSF_Sheffield/img/week2/17.png)

## Lightweight cipher example: present cipher(轻量级密码示例: x现在的密码)
* SPN
* 64-bit block size, 80/128-bit key sizes 区块长度64比特，密钥生成器长度是80/128
* ISO standard lightweight cipher for  encryption 用于加密的ISO标准轻量级密码

![18](https://github.com/Qianlinnn/personal-study-zone/raw/master/CSF_Sheffield/img/week2/18.png)

## Cryptographic Hashes: Requirements 加密哈希： 要求
* Motivation： Create a data "fingerprint"
  动机： 创造一个数据指纹
* A hash function h(x)( in the general sense) has the properties:
  一个哈希函数(一般意义)具有以下性质
    * Compression: h maps an input x of an arbitrary bit length to an output h(x) of fixed bit length n
      
      压缩： h将任意位长的输入x映射到固定位长的输出h(x)
    * Polynomial time computable
      
      多项式时间可计算
* Example (longitudinal redundancy check):
  
* 示例（纵向冗余检查）：  

     * Given 𝑚𝑚 blocks of 𝑛-bit input 𝑏_1, … , 𝑏_𝑚, form the 𝑛 -bit checksum 𝑐 from the bitwise xor of
every block, i.e., (for 1 ≤ 𝑖 ≤ 𝑛)

     给定n位输入b1,...bn的代码块m个， 从每个块的按位异或形成n位效验之和c
      
    ![19](https://github.com/Qianlinnn/personal-study-zone/raw/master/CSF_Sheffield/img/week2/19.png)
    
     * Cryptographic techniques can be seen as a refinement of checksum techniques to  handle an active forger 
       加密技术可以看作是对校验和技术的改进，可以处理活跃的伪造者

* ℎ(𝑥) is a cryptographic hash function h(x)是一个加密的哈希函数
    * one-way(or pre-image resistant)单向的
        * 给定一个y，想要通过h(x) = y来反向推出x是很难的
    * 同样:
        * 2nd-premiage resistance
            * 在计算上不可能找到与任何指定输入具有相同输出的第二个输入 如给定了x, 那么不存在 x* != x， 使得 h(x*) != h(x)
            
        * Collision resistance(耐碰撞)
            * For a given message  x 1 it is hard to find a second message  x2≠x1 with  H(x1)=H(x2) .
    * Hash value also called message digest or modification detection code  (abbreviated as MDC)
      哈希值也称为消息摘要或修改检测代码  
## Application: Message Integrity(应用程序， 消息完整性)
   * 消息或者数据完整性是指自该数据被授权方创建，转移或者存储后， 该数据不能被未经授权的方式修改   
   * 消息完整性：修改检测代码提供可检查的指纹
        * 需要二次原像抗性和经过身份验证的MDC
        * Typical application: Signed hashes

## Application: Password Files(应用： 密码文件)
   * 对密码p， 在密码文件里存储了h(p)
   * 要求只有一个原像抗性
   * 经常于其他salts 组合，保存为(s, h(s,p))
  
## Constructing a Cryptographic Hash Function
* 可以使用块链接技术（Rabin 1978）
    * 将信息分成固定大小的块,b_1,...,b_n
    * 使用对称的加密算法 e.g. DES
                        
    ![20](https://github.com/Qianlinnn/personal-study-zone/raw/master/CSF_Sheffield/img/week2/20.png)

* 现代算法（例如SHA-1 / 2/3，MD4，MD5等）更加复杂，并使用专门设计的功能
    * 许多冲突结果（例如Crypto 2004）动摇了对其性能的信心
    * 基于哈希的现代应用程序仍然“看起来”安全，例如，尚无前映像攻击（SHA-1除外）
    
    
    
  
    
        
   
    
    
     
 





        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        