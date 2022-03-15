##### 数据载荷

最终想要传递的信息

##### 报文

网络中交换与传输的数据单元

##### 头部

在数据载荷的前面添加的信息段

##### 尾部

在数据载荷的后面添加的信息段

##### 封装

对数据载荷添加头部和尾部，形成新的报文的过程

##### 解封装

去掉报文的头部和尾部，获取数据载荷的过程

##### 网关

提供协议转换、路由选择、数据交换等功能的网络设备

##### 路由器

为报文选择传递路径的网络设备

##### 终端设备

数据通信系统的端设备，作为数据的发送者或接收者

##### PDU

协议数据单元(Protocol Data Unit)

##### Break按键

Break键是电脑键盘上的一个键。Break键起源于19世纪的电报。在DOS时代，Pause/Break是常用键之一，但是近年来该键的使用频率逐年减少。在某些较旧的程序中，按这个键会使程序暂停，若同时按Ctrl，会使程序停止而无法执行。

因为Break可以中断程序，所以Break键也被称为Pause键。

在较小的笔记本电脑通常都没有Pause/Break。以下的方法可以代替Break：

Ctrl+Fn+F11、Fn+B或Ctrl+Fn+B（部分联想笔记本电脑）。
Ctrl+Fn+F11（三星电脑）
以下的方法可以代替Pause：

Fn+P、Ctrl+Fn+P或Alt+Fn+P（在部分的联想笔记本电脑）。
苹果标准键盘并没有Pause/Break，因为Mac OS X上并不需要使用。

##### IP协议号

十进制 | 十六进制 | 关键字 | 协议 | 引用
--- | --- | --- | --- | ---
0 | 0x00 | HOPOPT | IPv6逐跳选项 | 
1 | 0x01 | ICMP | 互联网控制消息协议（ICMP） | 
2 | 0x02 | IGMP | 因特网组管理协议（IGMP） | 
3 | 0x03 | GGP | 网关对网关协议 | 
4 | 0x04 | IPv4 | IPv4?(封装) /?IP-within-IP 封装协议（IPIP） | 
5 | 0x05 | ST | 因特网流协议 | ","
6 | 0x06 | TCP | 传输控制协议（TCP） | 
7 | 0x07 | CBT | 有核树组播路由协议 | 
8 | 0x08 | EGP | 外部网关协议 | 
9 | 0x09 | IGP | 内部网关协议（任意私有内部网关（用于思科的IGRP）） | 
10 | 0x0A | BBN-RCC-MON | BBN RCC 监视 | 
11 | 0x0B | NVP-II | 网络语音协议 | 
12 | 0x0C | PUP | XeroxPUP（英语：帕罗奥多通用报文） | 
13 | 0x0D | ARGUS | ARGUS | 
14 | 0x0E | EMCON | EMCON | 
15 | 0x0F | XNET | Cross Net Debugger | IEN 158
16 | 0x10 | CHAOS | Chaos | 
17 | 0x11 | UDP | 用户数据报协议（UDP） | 
18 | 0x12 | MUX | 多路复用 | IEN 90
19 | 0x13 | DCN-MEAS | DCN Measurement Subsystems | 
20 | 0x14 | HMP | Host Monitoring Protocol | 
21 | 0x15 | PRM | Packet Radio Measurement | 
22 | 0x16 | XNS-IDP | XEROX NS IDP | 
23 | 0x17 | TRUNK-1 | Trunk-1 | 
24 | 0x18 | TRUNK-2 | Trunk-2 | 
25 | 0x19 | LEAF-1 | Leaf-1 | 
26 | 0x1A | LEAF-2 | Leaf-2 | 
27 | 0x1B | RDP | 可靠数据协议（英语：Reliable Data Protocol） | 
28 | 0x1C | IRTP | Internet Reliable Transaction Protocol | 
29 | 0x1D | ISO-TP4 | ISO Transport Protocol Class 4 | 
30 | 0x1E | NETBLT | Bulk Data Transfer Protocol | 
31 | 0x1F | MFE-NSP | MFE Network Services Protocol | 
32 | 0x20 | MERIT-INP | MERIT Internodal Protocol | 
33 | 0x21 | DCCP | Datagram Congestion Control Protocol | 
34 | 0x22 | 3PC | Third Party Connect Protocol | 
35 | 0x23 | IDPR | Inter-Domain Policy Routing Protocol | 
36 | 0x24 | XTP | Xpress Transport Protocol | 
37 | 0x25 | DDP | Datagram Delivery Protocol | 
38 | 0x26 | IDPR-CMTP | IDPR Control Message Transport Protocol | 
39 | 0x27 | TP++ | TP++ Transport Protocol | 
40 | 0x28 | IL | IL Transport Protocol | 
41 | 0x29 | IPv6 | IPv6 封装 | 
42 | 0x2A | SDRP | Source Demand Routing Protocol | 
43 | 0x2B | IPv6-Route | IPv6路由拓展头 | 
44 | 0x2C | IPv6-Frag | IPv6分片扩展头 | 
45 | 0x2D | IDRP | Inter-Domain Routing Protocol | 
46 | 0x2E | RSVP | 资源预留协议 | 
47 | 0x2F | GRE | 通用路由封装（GRE） | ","
48 | 0x30 | DSR | 动态源路由（英语：Dynamic Source Routing） | 
49 | 0x31 | BNA | BNA | 
50 | 0x32 | ESP | 封装安全协议（ESP） | 
51 | 0x33 | AH | 认证头协议（AH） | 
52 | 0x34 | I-NLSP | Integrated Net Layer Security Protocol | TUBA
53 | 0x35 | SWIPE | SwIPe | IP with Encryption
54 | 0x36 | NARP | NBMA Address Resolution Protocol | 
55 | 0x37 | MOBILE | IP Mobility?(Min Encap) | 
56 | 0x38 | TLSP | 传输层安全性协议（使用Kryptonet密钥管理） | 
57 | 0x39 | SKIP | Simple Key-Management for Internet Protocol | 
58 | 0x3A | IPv6-ICMP | 互联网控制消息协议第六版（ICMPv6） | ","
59 | 0x3B | IPv6-NoNxt | IPv6无负载头 | 
60 | 0x3C | IPv6-Opts | IPv6目标选项扩展头 | 
61 | 0x3D |  | 任意的主机内部协议 | 
62 | 0x3E | CFTP | CFTP | 
63 | 0x3F |  | 任意本地网络 | 
64 | 0x40 | SAT-EXPAK | SATNET and Backroom EXPAK | 
65 | 0x41 | KRYPTOLAN | Kryptolan | 
66 | 0x42 | RVD | MIT远程虚拟磁盘协议 | 
67 | 0x43 | IPPC | Internet Pluribus Packet Core | 
68 | 0x44 |  | Any distributed file system | 
69 | 0x45 | SAT-MON | SATNET Monitoring | 
70 | 0x46 | VISA | VISA协议 | 
71 | 0x47 | IPCV | Internet Packet Core Utility | 
72 | 0x48 | CPNX | Computer Protocol Network Executive | 
73 | 0x49 | CPHB | Computer Protocol Heart Beat | 
74 | 0x4A | WSN | Wang Span Network | 
75 | 0x4B | PVP | Packet Video Protocol | 
76 | 0x4C | BR-SAT-MON | Backroom SATNET Monitoring | 
77 | 0x4D | SUN-ND | SUN ND PROTOCOL-Temporary | 
78 | 0x4E | WB-MON | WIDEBAND Monitoring | 
79 | 0x4F | WB-EXPAK | WIDEBAND EXPAK | 
80 | 0x50 | ISO-IP | 国际标准化组织互联网协议 | 
81 | 0x51 | VMTP | Versatile Message Transaction Protocol | 
82 | 0x52 | SECURE-VMTP | Secure Versatile Message Transaction Protocol | 
83 | 0x53 | VINES | VINES | 
84 | 0x54 | TTP | TTP | 
84 | 0x54 | IPTM | Internet Protocol Traffic Manager | 
85 | 0x55 | NSFNET-IGP | NSFNET-IGP | 
86 | 0x56 | DGP | Dissimilar Gateway Protocol | 
87 | 0x57 | TCF | TCF | 
88 | 0x58 | EIGRP | 增强型内部网关路由协议（EIGRP） | 
89 | 0x59 | OSPF | 开放式最短路径优先（OSPF） | 
90 | 0x5A | Sprite-RPC | Sprite RPC Protocol | 
91 | 0x5B | LARP | Locus Address Resolution Protocol | 
92 | 0x5C | MTP | Multicast Transport Protocol | 
93 | 0x5D | AX.25 | AX.25 | 
94 | 0x5E | IPIP | IP-within-IP 封装协议 | 与4号协议重复
95 | 0x5F | MICP | Mobile Internetworking Control Protocol | 
96 | 0x60 | SCC-SP | Semaphore Communications Sec. Pro | 
97 | 0x61 | ETHERIP | Ethernet-within-IP 封装协议 | 
98 | 0x62 | ENCAP | 封装头部 | 
99 | 0x63 |  | 任意的加密模式 | 
100 | 0x64 | GMTP | GMTP | 
101 | 0x65 | IFMP | Ipsilon Flow Management Protocol | 
102 | 0x66 | PNNI | PNNI over IP | 
103 | 0x67 | PIM | Protocol Independent Multicast | 
104 | 0x68 | ARIS | IBM's ARIS (Aggregate Route IP Switching) Protocol | 
105 | 0x69 | SCPS | 空间通信协议规范（英语：Space Communications Protocol Specifications） | SCPS-TP
106 | 0x6A | QNX | QNX | 
107 | 0x6B | A/N | Active Networks | 
108 | 0x6C | IPComp | IP负载压缩协议（英语：IP Payload Compression Protocol） | 
109 | 0x6D | SNP | Sitara Networks Protocol | 
110 | 0x6E | Compaq-Peer | Compaq Peer Protocol | 
111 | 0x6F | IPX-in-IP | 封装于IP的IPX | 
112 | 0x70 | VRRP | 虛擬路由器備援協定、共用位址冗餘協定（没在IANA注册） | VRRP:
113 | 0x71 | PGM | 实际通用多播 | 
114 | 0x72 |  | Any 0-hop protocol | 
115 | 0x73 | L2TP | 第二层隧道协议第三版 | 
116 | 0x74 | DDX | D-II Data Exchange (DDX) | 
117 | 0x75 | IATP | Interactive Agent Transfer Protocol | 
118 | 0x76 | STP | Schedule Transfer Protocol | 
119 | 0x77 | SRP | SpectraLink Radio Protocol | 
120 | 0x78 | UTI | Universal Transport Interface Protocol | 
121 | 0x79 | SMP | Simple Message Protocol | 
122 | 0x7A | SM | Simple Multicast Protocol | （，存于互联网档案馆）
123 | 0x7B | PTP | Performance Transparency Protocol | 
124 | 0x7C | IS-IS over IPv4 | 负载于IPv4的IS-IS | and
125 | 0x7D | FIRE | Flexible Intra-AS Routing Environment | 
126 | 0x7E | CRTP | Combat Radio Transport Protocol | 
127 | 0x7F | CRUDP | Combat Radio User Datagram | 
128 | 0x80 | SSCOPMCE | Service-Specific Connection-Oriented Protocol in a Multilink and Connectionless Environment | （，存于互联网档案馆）
129 | 0x81 | IPLT |  | 
130 | 0x82 | SPS | Secure Packet Shield | 
131 | 0x83 | PIPE | Private IP Encapsulation within IP | （，存于互联网档案馆）
132 | 0x84 | SCTP | Stream Control Transmission Protocol | 
133 | 0x85 | FC | 光纤通道 | 
134 | 0x86 | RSVP-E2E-IGNORE | Reservation Protocol (RSVP) End-to-End Ignore | 
135 | 0x87 | Mobility Header | IPv6移动IP扩展头 | 
136 | 0x88 | UDPLite | UDP-Lite | 
137 | 0x89 | MPLS-in-IP | 封装于IP协议的多协议标签交换 | 
138 | 0x8A | manet | MANET?Protocols | 
139 | 0x8B | HIP | Host Identity Protocol | 
140 | 0x8C | Shim6 | Site Multihoming by IPv6 Intermediation | 
141 | 0x8D | WESP | 包装过的封装安全协议（ESP） | 
142 | 0x8E | ROHC | Robust Header Compression | 
143-252 | 0x8F-0xFC | 未分配 |  | 
253-254 | 0xFD-0xFE | 用于实验和测试 |  | 
255 | 0xFF | 保留 |  | 


##### 命令行格式约定


格式 | 意义
--- | ---
粗体 | 命令行关键字（命令中保持不变、必须照输的部分）采用加粗字体表示。
斜体 | 命令行参数（命令中必须由实际值进行替代的部分）采用斜体表示。
[ ] | 表示用“[ ]”括起来的部分在命令配置时是可选的。
{ x \| y \| ... } | 表示从两个或多个选项中选取一个。
[ x \| y \| ... ] | 表示从两个或多个选项中选取一个或者不选。
{ x \| y \| ... } * | 表示从两个或多个选项中选取多个，最少选取一个，最多选取所有选项。
[ x \| y \| ... ] * | 表示从两个或多个选项中选取多个或者不选。
&<1-n> | 表示符号&的参数可以重复1～n次。
\# | 由“#”开始的行表示为注释行。
 
