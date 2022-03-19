## 9.1 VPR概述
### 9.1.1 通用路由平台

<img src="https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/华为VRP系统基础2022-03-19-13-31-55.png" alt="华为VRP系统基础2022-03-19-13-31-55" width="300" height="">

VRP(Versatile Routing Platform)的功能：
- 实现统一的用户界面和管理界面
- 实现控制平面功能，并定义转发平面接口规范
- 实现各产品转发平面与VRP控制平面之间的交互
- 屏蔽各产品链路层对于网络层的差异

### 9.1.2 文件系统

<img src="https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/华为VRP系统基础2022-03-19-13-33-15.png" alt="华为VRP系统基础2022-03-19-13-33-15" width="" height="">

指对储存器中文件、目录的管理，功能包括查看、创建、重命名和删除目录，拷贝、移动、重命名和删除文件等。
- 配置文件是命令行的集合。用户将当前配置保存到配置文件中，以便设备重启后，这些配置能够继续生效。另外，通过配置文件，用户可以非常方便地查阅配置信息，也可以将配置文件上传到别的设备，来实现设备的批量配置。
- 补丁是一种与设备系统软件兼容的软件，用于解决设备系统软件少量且急需解决的问题。在设备的运行过程中，有时需要对设备系统软件进行一些适应性和排错性的修改，如改正系统中存在的缺陷、优化某功能以适应业务需求等。
- 文件的管理方式包括：
  - 通过Console或者telnet等直接登陆系统管理
  - 通过FTP、TFTP或SFTP登录设备进行管理


### 9.1.3 存储设备

<img src="https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/华为VRP系统基础2022-03-19-13-34-15.png" alt="华为VRP系统基础2022-03-19-13-34-15" width="700" height="">

存储设备包括：SDRAM、Flash、NVRAM 、SD Card、USB
- SDRAM是系统运行内存，相当于电脑的内存；
- NVRAM非易失存储器，日志写入FLASH操作是耗时耗CPU的操作，因此采用缓存机制，即日志产生后，先存入缓存，定时器超时或缓存满后再写入Flash；
- Flash与SD Card属于非易失存储器，配置文件与系统文件存放于flash或SD Card中，具体设备参考产品文档；
- SD Card是外置的SD存储卡，用来扩展。USB是接口，用于外接大容量存储设备，主要用于设备升级，传输数据；
- 补丁文件和PAF文件由维护人员上传可自行指定放置。

### 9.1.4 设备初始化过程

<img src="https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/华为VRP系统基础2022-03-19-13-35-34.png" alt="华为VRP系统基础2022-03-19-13-35-34" width="500" height="">

设备上电后，首先运行BootROM软件，初始化硬件并显示设备的硬件参数，然后运行系统软件，最后从默认存储路径中读取配置文件进行设备的初始化操作。
- BootROM（Boot Read-Only Memory）是一组固化到设备内主板上ROM芯片中的程序，它保存着设备最重要的基本输入输出的程序、系统设置信息、开机后自检程序和系统自启动程序。
- 开机界面提供了系统启动的运行程序和正在运行的VRP版本及其加载路径等信息。

## 9.2 VRP管理

### 9.2.1 常见管理方式

> 用户对设备的管理方式主要有命令行方式和WEB网管方式两种，用户需要同过相应的方式登录到设备后才能对设备进行管理。

**WEB管理方式**
- Web网管方式通过图形化的操作界面，实现对设备直观方便地管理与维护，但是此方式仅可实现对设备部分功能的管理与维护。
- Web网管方式可以通过HTTP和HTTPS方式登录设备。
**命令行管理方式**
- 命令行方式需要用户使用设备提供的命令行对设备进行管理与维护，此方式可实现对设备的精细化管理，但是要求用户熟悉命令行。
- 命令行方式可以通过Console口、Telnet或SSH方式登录设备。

### 9.2.2 VRP用户界面

> 用户通过命令行方式登录设备时，系统会分配一个用户界面来管理、监控设备和用户间的当前会话；
> 
> 设备系统支持的用户界面有Console用户界面和虚拟终端VTY(Virtual Type Terminal)用户界面。

**Console用户界面**
- Console用户界面用来管理和监控通过Console口登录的用户。
- 用户终端的串行口可以与设备Console口直接连接，实现对设备的本地访问。
**VTY用户界面**
- VTY用户界面用来管理和监控通过VTY方式登录的用户。
- 用户通过终端与设备建立Telnet或STelnet连接后，即建立了一条VTY通道，通过VTY通道实现对设备的远程访问。

### 9.2.3 VRP用户级别

VRP提供基本的权限控制，可以实现不同级别的用户能够执行不同级别的命令，限制不同用户对设备的操作。
用户的级别与命令级别对应，不同级别的用户登录后，只能使用等于或低于自己级别的命令。

缺省情况下，命令级别按0～3级进行注册，用户级别按0～15级进行注册，用户级别和命令级别对应关系如表所示。

<img src="https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/华为VRP系统基础2022-03-19-13-39-22.png" alt="华为VRP系统基础2022-03-19-13-39-22" width="" height="">

### 9.2.4 WEB网管方式登录

> 以华为AR系列路由器为例，PC终端打开浏览器软件，在地址栏中输入“[https://192.168.1.1](https://192.168.1.1/)”，按下回车键，显示AR Web管理平台登录界面。
> 

<img src="https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/华为VRP系统基础2022-03-19-13-40-40.png" alt="华为VRP系统基础2022-03-19-13-40-40" width="300" height="">

<img src="https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/华为VRP系统基础2022-03-19-13-40-47.png" alt="华为VRP系统基础2022-03-19-13-40-47" width="" height="">

?> 路由器的缺省用户名为`admin`，缺省密码为`Admin@huawei`

### 9.2.5 命令行方式—本地登录

设备登录的两种方式分为两种：本地登录和远程登录。

<img src="https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/华为VRP系统基础2022-03-19-13-44-54.png" alt="华为VRP系统基础2022-03-19-13-44-54" width="600" height="">

本地登录包括：
- 当用户需为第一次上电的设备进行配置时，可通过Console口本地登录设备。
- 控制口（Console Port）是一种通信串行端口，符合RS232串口标准的RJ45接口，由设备的主控板提供。
- 目前大多数台式电脑提供的COM口都可以与Console口连接。笔记本电脑一般不提供COM口，需要使用USB到RS232的转换接口。
- 用户终端的串行端口可以与设备Console口直接连接，然后通过PuTTY工具本地登录实现对设备的本地配置。
- Console口登录是设备默认开启的功能，不需要对设备做预配置。

**使用PuTTY本地登录VRP**

PuTTY工具是一个Telnet、SSH、串行接口等的连接软件，[下载地址](https://www.putty.org/)

- 本地登录时，终端设备采用串口与华为设备Console口连接，所以采用“Serial”连接类型，COM端口根据终端设备实际端口选取，**速率固定为9600**。
- 完成设置以后，点击“Open”按钮即可与VRP建立连接。

<img src="https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/华为VRP系统基础2022-03-19-13-47-52.png" alt="华为VRP系统基础2022-03-19-13-47-52" width="500" height="">

### 9.2.6 命令行方式—远程登录

- 远程登录指终端远程登录到网络设备上，并且可以集中管理维护网络设备。
- 远程登录包括SSH和Telnet两种方式。
- 设备默认不开启SSH登录功能，需要用户先通过Console口登录，配置上SSH登录必须的参数之后，才可以使用SSH登录功能。

<img src="https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/华为VRP系统基础2022-03-19-14-02-06.png" alt="华为VRP系统基础2022-03-19-14-02-06" width="300" height="">
</br>
<img src="https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/华为VRP系统基础2022-03-19-14-02-13.png" alt="华为VRP系统基础2022-03-19-14-02-13" width="500" height="">

## 9.3 熟悉命令行

### 9.3.1 命令行结构

每条命令有最多一个命令字，若干个关键字和参数，形成一条命令，参数必须由参数名和参数值组成。
命令字、关键字、参数名、参数值之间，需要用空格分隔开。

<img src="https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/华为VRP系统基础2022-03-19-14-03-39.png" alt="华为VRP系统基础2022-03-19-14-03-39" width="500" height="">

- 命令字：规定了系统应该执行的功能，如display（查询设备状态），reboot（重启设备）等命令字
- 关键字：特殊的字符构成，用于进一步约束命令，是对命令的拓展，也可以用于表达命令构成逻辑而增设的补充字符串。
- 参数列表：是对命令执行功能的进一步约束。包括一个或一对参数和参数值。

例如:`display ip interface GE0/0/0`，查看接口信息的命令
- 命令字：`display`
- 关键字：`ip`
- 参数名：`interface`
- 参数值：`GE0/0/0`

### 9.3.2 命令行视图

设备提供了多样的配置和查询命令，为便于用户使用这些命令，VRP系统按功能分类将命令分别注册在不同的命令行视图下。

<img src="https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/华为VRP系统基础2022-03-19-14-05-52.png" alt="华为VRP系统基础2022-03-19-14-05-52" width="600" height="">

- 用户视图：用户视图应为登录系统后的第一个视图。在用户视图中不提供**除查询和工具命令之外**的其他命令。用户视图中，唯一可进入的视图是系统视图；
- 系统视图：系统视图中提供全局的配置命令；如果系统存在下一级配置视图，则在系统视图中须提供进入下一级配置视图的命令。
- 其他视图：用户可以进行接口参数和协议参数配置。

<img src="https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/华为VRP系统基础2022-03-19-14-06-27.png" alt="华为VRP系统基础2022-03-19-14-06-27" width="700" height="">

```shell
命令行举例：
<Huawei>system-view #用户首先进入用户视图，通过命令进入系统视图
[Huawei]interface GigabitEthernet0/0/1 #在系统视图进入接口视图
[Huawei-GigabitEthernet0/0/1]ipaddress 192.168.1.1 24 #配置IP地址
[Huawei-GigabitEthernet0/0/1]quit #退回到上一个视图
[Huawei]ospf1 #在系统视图进入协议视图
[Huawei-ospf-1]area 0 #在协议视图进入OSPF区域视图
[Huawei-ospf-1-area-0.0.0.0]return #返回用户视图
```

### 9.3.3 编辑命令行

**功能键**
- <kbd>Ctrl</kbd>+<kbd>A</kbd>	把光标移动到当前命令行的最前端
- <kbd>Ctrl</kbd>+<kbd>E</kbd>	把光标移动到当前命令行的末尾
- <kbd>Ctrl</kbd>+<kbd>C</kbd>	停止当前命令的运行
- <kbd>Ctrl</kbd>+<kbd>Z</kbd>	回到用户视图
- <kbd>Ctrl</kbd>+<kbd>]</kbd>	终止当前连接或切换连接
- <kbd>Ctrl</kbd>+<kbd>X</kbd>	删除光标左侧的所有字符
- <kbd>Ctrl</kbd>+<kbd>Y</kbd>	删除光标所在位置右侧的所有字符
- <kbd>↑</kbd>/ <kbd>Ctrl</kbd>+<kbd>P</kbd>	调用上一条历史命令
- <kbd>↓</kbd>/ <kbd>Ctrl</kbd>+<kbd>N</kbd>	调用下一条历史命令


**不完整关键字输入**

```markdown
<Huawei>d cu
<Huawei>di cu
<Huawei>dis cu
<Huawei>d c
        ^
Error:Ambiguouscommand found at '^' position.
<Huawei>dis c
            ^
Error:Ambiguouscommand found at '^' position.
```

`display current-configuration`命令，可以输入`d cu`、`di cu`或`dis cu`等都可以执行此命令，但不能输入`d c`或`dis c`等，因为以`d c`、`dis c`开头的命令**不唯一**。
    

**Tab键的使用**
- 如果与之匹配的关键字唯一，按下<Tab>键，系统自动补全关键字，补全后，反复按<Tab>关键字不变。

```shell
[Huawei] info- #按下Tab键
[Huawei] info-center
```

- 如果与之匹配的关键字不唯一，反复按<Tab>键可循环显示所有以输入字符串开头的关键字。

```shell
[Huawei] info-center log  #按下Tab键
[Huawei] info-center logbuffer #继续按Tab键循环翻词
[Huawei] info-center logfile
[Huawei] info-center loghost
```

- 如果没有与之匹配的关键字，按Tab键后，关键字不变。

```shell
[Huawei] info-center loglog #输入错误的关键字，按下Tab键
[Huawei] info-center loglog
```


### 9.3.4 使用命令行在线帮助

- 完全帮助

当用户输入命令时，可以使用命令行的完全帮助获取全部关键字和参数的提示。

```shell
<Huawei>?
Userviewcommands:
	arp-ping    ARP-ping
	autosave    <Group>autosave command group
	backup      Backup information
	cd          Change current directory
	clear       Clear
	clock       Specify the system clock
...
```

- 部分帮助

当用户输入命令时，如果只记得此命令关键字的开头一个或几个字符，可以使用命令行的部分帮助获取以该字符串开头的所有关键字的提示。

```shell
<Huawei>d?
	debugging    <Group>debugging command group
	delete       Delete a file
	dialer       Dialer
	dir          List files on a file system
	display      Display information
```

### 9.3.5 解读命令行的错误信息

```shell
[Huawei] sysname
                 ^
Error:Incomplete command found at ‘^’ position.  #箭头所指地方提示命令不完整，需要进一步补齐
[Huawei] router if 1.1.1.1
                ^
Error: Unrecognized command found at ‘^’ position.  #箭头所指地方提示该命令不能识别，需要确认命令正确性
[Huawei] a
         ^
Error:Ambiguous command found at ‘^’ position. #箭头所指的命令不明确，有多个a开头的关键字
[Huawei-GigabitEthernet0/0/0]ospfcost 800000   
                                      ^
Error: Wrong parameter found at '^' position. #箭头所指的参数值越界
```

### 9.3.6 自定义快捷键

自定义快捷键共有4个，<kbd>Ctrl</kbd>+<kbd>G</kbd><kbd>Ctrl</kbd>+<kbd>L</kbd><kbd>Ctrl</kbd>+<kbd>O</kbd><kbd>Ctrl</kbd>+<kbd>U</kbd>。
用户可以根据自己的需要将这4个快捷键与任意命令进行关联，当使用快捷键时，系统自动执行它所对应的命令。

```shell
<Huawei>system-view
[Huawei]hotkey ctrl_l "display tcp status"
```

### 9.3.7 使用undo命令行

在命令前加undo关键字，即为undo命令行。undo命令行一般用来恢复缺省情况、禁用某个功能或者删除某项配置。以下为参考案例：
- 使用undo命令行恢复缺省情况

```shell
<Huawei> system-view
[Huawei] sysname Server
[Server] undo sysname
[Huawei]
```

- 使用undo命令禁用某个功能

```shell
<Huawei> system-view
[Huawei] ftp server enable
[Huawei] undo ftp server
```

- 使用undo命令删除某项设置

```shell
[Huawei]interface g0/0/1
[Huawei-GigabitEthernet0/0/1]ipaddress 192.168.1.1 24
[Huawei-GigabitEthernet0/0/1]undo ipaddress
```


## 9.4 基本配置命令

### 9.4.1 常见文件系统操作命令

```shell
<Huawei>pwd #查看当前目录
<Huawei>dir #显示当前目录下的文件信息
<Huawei>more #查看文本文件的具体内容（txt等格式）
<Huawei>mkdir #创建目录
<Huawei>rename old-name new-name #重命名目录
<Huawei>cd #改变当前路径
<Huawei>cd.. #回到上一层
<Huawei>rmdir #删除目录
<Huawei>execute #批量处理文件
<Huawei>copy source-filename destination-filename #拷贝文件
<Huawei>move source-filename destination-filename #移动文件
<Huawei>zip #压缩文件
<Huawei>delete #删除文件
<Huawei>reset #彻底删除文件
<Huawei>Reset recycle-bin #清空回收站
<Huawei>fixdisk #修复异常的储存设备
<Huawei>format #格式化储存设备
<Huawei>undelete #恢复删除文件
```

### 9.4.2 系统基础配置命令

> 请参考 [命令行格式约定](http://localhost:3000/#/_glossary?id=%e5%91%bd%e4%bb%a4%e8%a1%8c%e6%a0%bc%e5%bc%8f%e7%ba%a6%e5%ae%9a)

> [!cmd]
> - **display version** #查看系统信息
> - **display clock** #查看系统时间
> - **clock timezone** _time-zone-name_ {**add**|**minus**} _offset_ #修改时区
> - **clock datetime** _HH:MM:SS YYYY-MM-DD_ #修改时间
> - **system-view** #进入系统视图
> - **sysname** _R1_ #修改设备名称
> - **header** {**login**|**shell**} {**information** _text_|**file** _file-name_} #配置登陆前信息（设置密码后才会显示）
> - **display saved-configuration** [**last**|**time**|**configuration**] #查看保存的配置文件信息	（在任意视图）
> - **display startup** #查看下次启动时使用的配置文件
> - **compare configuration** #比较配置信息(比较当前和下次启动的)
> - **save** #保存配置（在任意视图）
> - **display currrent-configuration** #查看当前配置信息
> - **authentication-mode {aaa|password|none}** #设置登录用户界面的验证方式
> - **set authentication password** [**cipher** _password_] #设置本地验证的密码console
> - **idle-timeout** _minutes_ [_seconds_] #设置超时时间（在console口下）
> - **display this** #查看当前配置结果（在任意接口下）
> - **reboot** #重启设备
> - **command-privilege level** _level_ **view** _view-name command-key_ #设置指定视图内的命令的级别
