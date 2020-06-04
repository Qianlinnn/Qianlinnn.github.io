# Anti-Forensics 反取证

## Computer forensics:

“The use of scientifically derived and proven methods toward the preservation, collection, validation, identification, analysis, interpretation, documentation and presentation of digital evidence derived from digital sources for the purpose of facilitating or furthering the reconstruction of events found to be criminal, or helping to anticipate unauthorized actions shown to be disruptive to planned operations.” – Brian Carrier

## Defining Anti-Forensics 定义反取证

* Anti-Forensics – Tools and techniques designed to blind or disrupt digital  forensic investigations. 旨在盲目或破坏数字法证调查的工具和技术。

* Goal: 
  * Blind the investigator 使调查者盲目
  * Disrupt information collection 破坏信息收集
  * Increase the time required to carry out analysis 增加执行分析所需的时间
  * Introduce doubt to the investigations findings 对调查结果提出疑问
  * Subvert the tools used during the investigation 颠覆调查期间使用的工具
  * Leave no evidence of anti-forensics techniques 不留任何取证技术证据

## Anti-Forensics Approaches

* Data destruction 数据销毁
* Data hiding 数据隐藏
* Reducing the footprint 减少足迹
* Anonymous computing/identities 匿名计算/身份
* Attacking the investigator  攻击调查员

## Data Destruction

* Approaches - Erase data (e.g. files) or metadata (e.g. timestamps)  方法-擦除数据（例如文件）或元数据（例如时间戳记）
  * Secure file shredders / media sanitisation 安全的文件粉碎机/介质消毒
    * SpyBot Shredder SpyBot碎纸机
      * Multi-pass overwriting of data 数据的多遍覆盖
      * NIST准则-http://tinyurl.com/kkuab38
    * System cleaners  系统清除器
      * Evidence Eliminator  证据消除器
      * CCleaner CCleaner
    * Meta-data tampering   元数据篡改
      * Timestamp – Delete or erase timestamp data 时间戳–删除或删除时间戳数据

## Data Hiding 资料隐藏

Data Hiding, also referred to as Data Obfuscation, is a form of data  masking where data is purposely scrambled/hidden to prevent  unauthorised access to sensitive materials.  It could be used as a countermeasure to forensic analysis 数据隐藏，也称为数据混淆，是一种数据掩蔽的形式，其中有意对数据进行加扰/隐藏以防止对敏感材料的未经授权的访问。 它可以用作取证分析的对策

* 2级数据隐藏：2 Levels of data hiding:  
  * Data in transit (Network & Internet Forensics)  传输中的数据（网络和互联网取证）
    * Encryption protocols (SSH, SSL/TLS, ToR)  加密协议（SSH，SSL / TLS，ToR）
  * Data at rest 静态数据

## Information Hiding methods

* Basic techniques 基本技巧
  * Codes 
  * Ciphers  密文
  * Encryption  加密
  * Steganography  隐写术
  * Passwords  
  * Alternative Data Streams 替代数据流

## Basic Techniques

* Modifying file extensions or magic numbers  修改文件扩展名或幻数
* Simple file modification to evade hash based signature  detection  简单的文件修改，以逃避基于哈希的签名检测
* Invisible text, created through the use of a word processor  (simple steganography)  通过使用文字处理器创建的不可见文本（简单隐写术）
* Setting files to hidden   将文件设置为隐藏
* Placing files in unexpected places (e.g. System32 folder) 将文件放置在意外的位置（例如System32文件夹）
* Hidden partitions 隐藏的分区

## Codes

* Typically work at the word or sentence level, replacing words  and phrases with alternatives while preserving the meaning of  the original message.  通常在单词或句子级别上工作，用单词替换其他单词和短语，同时保留原始消息的含义。
* Cryptolect – Used to allow conversation between a group of  people that prevents outsiders from eavesdropping Cryptolect –用于允许一群人之间的对话，以防止外人窃听
* Potentially more difficult to analyse and break than ciphers可能比密码更难分析和破解

## Ciphers

* Ciphers are used to provide confidentiality  密码用于提供机密性
*  Stream ciphers e.g. RC4 流密码，例如 RC4
  * Combine a key and a stream of pseudo random data with the plaintext  将密钥和伪随机数据流与明文合并
  * Lower resource requirements than block ciphers 资源要求比分组密码低
  * Require a new starting state each time, to avoid stream cipher attacks每次都需要一个新的开始状态，以避免流密码攻击
* Block ciphers e.g. Feistel 分组密码，例如 菲斯特尔
  * Operate on fixed length “blocks” of data   操作固定长度的“块”数据
  * Perform the same transformation each time,  may use block chaining where each block is XOR’d with the previous block  每次执行相同的转换，可以使用块链接，其中每个块与上一个块进行异或
  *  Usually slower than stream ciphers 通常比流密码慢

## Cryptanalysis - Breaking Ciphers 密码分析-破解密码

* Goals:
  * Decrypt a ciphered text解密密文
  * Obtain the key or determine the method to be appled to other ciphered  texts获取密钥或确定要应用于其他密文的方法
* Look for familiar patterns in documents, there may be clues in  the layout. e.g. Date, Salutation, etc. (e.g. yours sincerely)  在文档中寻找熟悉的图案，布局中可能有线索。 例如 日期，称呼等（例如，真诚的问候）
* Statistical analysis, look for vowels, double letters, common  short words e.g. the, and, at, etc  统计分析，查找元音，双字母，常用短词，例如 等等
*  Try to figure out the shift pattern or substution pattern尝试找出班次模式或替代模式

## Encryption

* Encryption may be applied at many levels 加密可以应用于多个级别
  * File level 文件等级 
  * Volume level  体积等级

  * Device level 设备等级
* Encrypted data looks very similar to compressed data 加密数据看起来与压缩数据非常相似
  * Encryption tools installed on a system provide a clue that  安装在系统上的加密工具提供了已使用加密的线索。
* Common tools include: 常用工具包括：
  * TrueCrypt 
  * VeraCrypt (TrueCrypt Fork/Replacement)
  * Bitlocker (Windows OS)
  * FileVault (Mac)

## Passwords

* Passwords, Pass Phrases, Keys 密码，通行短语，密钥
* Strength dictated by length and character set 强度由长度和字符集决定
  * P = Permutations, L = Length, C = Character Set  P =排列，L =长度，C =字符集
  * P = LC (https://howsecureismypassword.net/ ) P = LC（https://howsecureismypassword.net/）
* Passwords may be retrieved from files, Windows SAM, Linux  /etc/passwords, and reused to encrypt data 可以从文件，Windows SAM，Linux / etc / passwords中检索密码，并重新用于加密数据
* Passwords can be cracked using John the ripper, Cain & Abel etc 使用开膛手约翰，该隐和亚伯等人可以破解密码

## Steganography 隐写术

* Main idea : Hide the message (from the fifth century BC)  主要思想：隐藏信息（来自公元前五世纪）
* Examples :
  * Shave the head of a slave, tattoo a message on the skull and wait  for the regrowth of hair to send it to the recipient. 剃掉一个奴隶的头，在头骨上纹身一条消息，然后等待头发再生长，将其发送给接收者。
  * Transmission of written messages with milk, revealed, then by a  flame. 用牛奶传递书面信息，然后通过火焰传递出来。
* Steganography is a technique where information or files are hidden  within another file in an attempt to hide data by leaving it in plain  sight.  隐写术是一种将信息或文件隐藏在另一个文件中的技术，目的是通过使数据或文件不被人们看到而隐藏数据。
* Hide a message in a text, for example, read only one word out of two.  隐藏文本中的消息，例如，仅读取两个单词中的一个。
* Detection is very difficult 检测非常困难  
  * Comparison with an original file may hold a clue to the fact that steganography  has been employed  与原始文件进行比较可能暗示使用了隐写术
* Compression can destroy the hidden message in some types of  steganography 压缩会破坏某些隐秘术中的隐藏消息
* Steganography are often used in conjunction with cryptography so that  the information is doubly protected; first it is encrypted and then hidden  so that an adversary has to first find the information and then decrypt it  (Kessler, 2001).隐秘术通常与加密术结合使用，以便对信息进行双重保护。 首先将其加密然后隐藏，以便对手必须首先找到信息，然后再对其解密（Kessler，2001）。
* Steganalysis is the discovery of the existence of information hidden  using steganography. Therefore, like cryptography and cryptanalysis, the  goal of steganalysis is to discover hidden information and to break the  security of its carriers. 隐写分析是发现使用隐写术隐藏的信息。 因此，像密码学和密码分析一样，隐匿分析的目标是发现隐藏信息并破坏其载体的安全性

## Common Steganography Programs常见的隐写术程序

* Steghide is a steganography program that is able to hide data in various kinds of  image- and audio-files. Support for JPEG, BMP, WAV and AU files.  Steghide是一种隐写术程序，能够隐藏各种图像和音频文件中的数据。 支持JPEG，BMP，WAV和AU文件。
* OutGuess is a universal steganography tool that allows the insertion of hidden  information into the redundant bits of data sources. Currently supports PPM,PNM  and JPEG image formats. OutGuess是一种通用的隐写术工具，允许将隐藏信息插入数据源的冗余位。 目前支持PPM，PNM和JPEG图像格式。
* JPHIDE and JPSEEK are programs which allow hiding a file in JPEG visual image.  The design objective was not simply to hide a file but rather to do this in such a way  that it is impossible to prove that the host file contains a hidden file.JPHIDE和JPSEEK是允许在JPEG可视图像中隐藏文件的程序。 设计目标不是简单地隐藏文件，而是以无法证明宿主文件包含隐藏文件的方式来做到这一点。
* Other GUI Steganography tools: Hiderman, OpenPuff, mp3stegz, Invisible  Secrets, OpenStego 其他GUI隐写术工具：Hiderman，OpenPuff，mp3stegz，Invisible Secrets，OpenStego

## Steganography – Legal Issues 隐秘术–法律问题

* Steganography relies on obfuscation to provide privacy (hide data) 隐秘术依靠混淆来提供隐私（隐藏数据）
  * If data is obfuscated correctly how can you determine its  existence?  如果正确混淆了数据，您如何确定其存在？
* How can law enforcement prove that steganography is being used?  执法部门如何证明正在使用隐写术？
* How can a suspect provide that steganography is not being used?  嫌疑人如何证明未使用隐写术？
* How can regulation be applied if the fact that a key exists cannot be  proven or disproven? 如果无法证明或拒绝存在密钥的事实，如何应用监管？

## Other Data Hiding Techniques 其他数据隐藏技术

* Windows – ADS - Alternative Data Streams  Windows – ADS-备用数据流
* ADS can “stream” or hide data behind  existing files without affecting the  functionality, size or other information. ADS可以“流化”或隐藏现有文件后面的数据，而不会影响功能，大小或其他信息。
  * Data can be embedded in the target  resource, that is not normally viewable 数据可以嵌入到通常无法查看的目标资源中

## Reducing the Footprint

* The previous techniques (Data destruction & hiding) are useful but  easily detected  先前的技术（数据销毁和隐藏）很有用，但很容易检测到
  * Statistical techniques 统计技术
  * Obvious signs 明显的迹象

* An alternative or complimentary approach is to minimise the  footprint
  * Memory injection  记忆注入
  * Live CD’s / USB sticks Live CD的/ U盘

  * Virtual Machines 虚拟机

  *  Anonymous ID and storage 匿名ID和存储

## Memory Injection  

* Code is injected into memory  代码已注入内存
  * e.g. by exploiting a buffer overflow 例如 通过利用缓冲区溢出
* Userland Exec
  * Loads process image without direct assistance from kernel  加载过程映像而无需内核的直接帮助
  * Process name remains unchanged, contents of process changed 流程名称保持不变，流程内容已更改
    * Hides code in process image from logging 从记录中隐藏过程映像中的代码
    * Bypasses access control 绕过访问控制
    * Process image/code can be read from network or removable disk 可以从网络或可移动磁盘读取过程映像/代码

## Live CDs/ USB sticks / Virtual Machines

* The majority of forensic investigations analyse the storage devices  from suspect machines 大多数法医调查会分析可疑机器中的存储设备
* Live CDs / USB sticks do not mount the storage device, or leave  behind any evidence   实时CD / USB记忆棒未装载存储设备，也不会或留下任何证据
* Virtual Machines can be easily securely deleted, purging all  evidence from the disk 可以轻松安全地删除虚拟机，从磁盘上清除所有证据

## Anonymous Identities & Storage 匿名身份和存储

* Webmail accounts can be set up with anonymity; 可以使用匿名方式设置Webmail帐户；
  * The storage provide for emails can be mounted as a file system via API calls   可以通过API调用将电子邮件提供的存储安装为文件系统
  * Mail boxes may be shared by user to exchange information in the drafts  folder. 用户可以共享邮箱以交换草稿文件夹中的信息。
* Cloud services provide access to anyone with a credit card   云服务为使用信用卡的任何人提供访问权限
  * Stolen cards  被盗卡
  * Prepaid cards预付卡
* EC2 instances may be used to form botnets, and carry out other malicious  activities  EC2实例可用于形成僵尸网络，并进行其他恶意活动

* S3 provides storage for data S3提供数据存储

* These services may be beyond the reach of an investigation   这些服务可能无法进行调查
* If combined with Live CDs/Proxies for the setup, they may be  untraceable 如果与Live CD /代理结合进行设置，则可能无法跟踪它们

## Attacking the Investigator  攻击调查员

*  Software and data can be crafted to disrupt the tools used in the  investigative process 可以精心设计软件和数据以破坏调查过程中使用的工具
  * Files that crash EnCase  使EnCase崩溃的文件

  * Disrupt/crash snort, tcpdump, wireshark  中断/崩溃snort，tcpdump，wireshark

  * Privilege escalation from evidence to investigators’ machines 特权从证据升级到调查人员的机器

  * Erasure of collective evidence  删除集体证据
  * Leak/obtain information about the analyst or investigator 泄漏/获取有关分析员或调查员的信息

## Anti-Forensics Recommendation 取证建议

* Improve the design of digital investigation tools, to make them less  vulnerable to attacks 改进数字调查工具的设计，使其更不容易受到攻击
  * Secure software development  安全的软件开发
* Save log files   保存日志文件
  * Prevent contamination, deletion  防止污染，删除
* Use key loggers to overcome encryption practices 使用按键记录器来克服加密做法
  * Legality of this is dubious 这是否合法？

## Investigating Alternate Data Streams 调查备用数据流

* ADS Tool can detect the presence  of hidden NTFS streams on a target  system.   ADS工具可以检测目标系统上是否存在隐藏的NTFS流。
* Alternate Data Streams (ADS) are  pieces of info hidden as metadata of  files on NTFS drives and can be  detected using tools such as ADS  Spy. 备用数据流（ADS）是隐藏为NTFS驱动器上文件元数据的信息，可以使用ADS Spy等工具进行检测

## Detecting Steganography 检测隐写术

* Steganalysis techniques can be classified in a similar way as cryptanalysis  methods, largely based on how much prior information is known: 隐写分析技术可以按照与密码分析方法类似的方式进行分类，主要基于已知的先验信息量：
  * Steganography-only attack: The steganography medium is the only item  available for analysis. 仅隐写术攻击：隐写术介质是唯一可用于分析的项目。

  * Known-carrier attack: The carrier and steganography media are both  available for analysis. 已知载体攻击：载体和隐写术介质均可用于分析。

  * Known-message attack: The hidden message is known. 已知消息攻击：隐藏的消息是已知的。

  * Chosen-steganography attack: The steganography medium and algorithm  are both known. 选择的隐写术攻击：隐写术媒介和算法都是已知的。

  * Chosen-message attack: A known message and steganography algorithm  are used to create steganography media for future analysis and  comparison. 选择消息攻击：使用已知的消息和隐写术算法创建隐写术媒体，以供将来分析和比较。

  * Known-steganography attack: The carrier and steganography medium, as  well as the steganography algorithm, are known 已知隐写术攻击：已知载体和隐写术媒介以及隐写术算法

## Steganography Detection 隐写术检测

* Gargoyle (formerly StegoDetect)  software (WetStone Technologies)  can be used to detect the presence  of steganography software.  Gargoyle is a commercial tool 石像鬼（以前是StegoDetect）软件（WetStone Technologies）可用于检测隐写软件的存在。 石像鬼是一种商业工具
* Stegdetect can find hidden  information in JPEG images using  such steganography schemes as F5,  Invisible Secrets, JPHide, and JSteg  (OutGuess 2003).Stegdetect可以使用F5，Invisible Secrets，JPHide和JSteg等隐写方案在JPEG图像中找到隐藏的信息（OutGuess 2003）。
* It shows the output from xsteg, a  graphical interface for stegdetect. 它显示xsteg的输出，xsteg是stegdetect的图形界面。
* Stegdectect is a non- commercial tool. Stegdectect是非商业工具。

## Conclusion

* Data can be hidden or obfuscated using a variety of techniques 可以使用多种技术隐藏或混淆数据
  * Simple techniques 简单的技巧

  * Complex techniques  复杂技术

  * Attempts to obfuscate data can be detected on computer systems  可以在计算机系统上检测到混淆数据的尝试
  * Data may be recoverable through cryptanalysis 数据可通过密码分析恢复
  * There are legal processes in place to assist the investigator in extreme  cases 在极端情况下，已制定法律程序来协助调查员

  * Encrypted data and steganography pose challenges to digital forensics 加密的数据和隐写术给数字取证带来挑战
* Adversaries will attempt to avoid detection by employing antiforensics approaches 对手将尝试通过采用反法医学方法来避免被发现
  * Overwriting / destroying data 覆盖/销毁数据
  * Restricting the flow evidence / minimising footprint  限制流动证据/最小化占地面积

  * Encrypting data加密数据
  * Using anonymous resources   使用匿名资源
  * Exploiting software vulnerabilities to mask the use of tools 利用软件漏洞掩盖工具的使用

  * Direct attacks against forensics tools 直接攻击取证工具