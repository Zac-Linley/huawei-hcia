## 11.1 什么是VLAN

### 11.1.1 传统以太网的问题

<img src="https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/VLAN原理与配置2022-03-20-15-09-59.png" alt="VLAN原理与配置2022-03-20-15-09-59" width="" height="">

广播域：
- 如图是一个典型的交换网络，网络中只有终端计算机和交换机。在这样的网络中，如果某一台计算机发送了一个广播帧，由于交换机对广播帧执行泛洪操作，结果所有其他的计算机都会收到这个广播帧。
- 把广播帧所能到达的整个访问范围称为二层广播域，简称广播域(Broadcast Domain)。显然，一个交换网络其实就是一个广播域。

网络安全问题和垃圾流量问题：
- 如图：如果PC1向PC2发送了一个单播帧。此时SW1、SW3、SW7的MAC地址表中存在关于PC2的MAC地址表项，但SW2和SW5不存在关于PC2的MAC地址表项。那么，SW1和SW3将对该单播帧执行点对点的转发操作，SW7将对该单播帧执行丢弃操作，SW2和SW5将对该单播帧执行泛洪操作。最后的结果是，PC2虽然收到了该单播帧，但网络中的很多其他非目的主机，同样收到了不该接收的数据帧。

?> 显然，**广播域越大，网络安全问题和垃圾流量问题就越严重**。

### 11.1.2 虚拟局域网（VLAN，Virtual LAN）

通过在交换机上部署VLAN，可以将一个规模较大的广播域在逻辑上划分成若干个不同的、规模较小的广播域，由此可以有效地提升网络的安全性，同时减少垃圾流量，节约网络资源。

<img src="https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/VLAN原理与配置2022-03-20-15-16-24.png" alt="VLAN原理与配置2022-03-20-15-16-24" width="" height="">

VLAN的特点：
- 一个VLAN就是一个广播域，所以在同一个VLAN内部，计算机可以直接进行二层通信；而不同VLAN内的计算机，无法直接进行二层通信，只能进行三层通信来传递信息，即广播报文被限制在一个VLAN内。
- VLAN的划分不受地域的限制。

VLAN的好处：
- 灵活构建虚拟工作组：用VLAN可以划分不同的用户到不同的工作组，同一工作组的用户也不必局限于某一固定的物理范围，网络构建和维护更方便灵活。
- 限制广播域：广播域被限制在一个VLAN内，节省了带宽，提高了网络处理能力。
- 增强局域网的安全性：不同VLAN内的报文在传输时是相互隔离的，即一个VLAN内的用户不能和其它VLAN内的用户直接通信。
- 提高了网络的健壮性：故障被限制在一个VLAN内，本VLAN内的故障不会影响其他VLAN的正常工作。

## 11.2 VLAN的基本概念

### 11.2.1 如何实现VLAN

<img src="https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/VLAN原理与配置2022-03-20-15-18-48.png" alt="VLAN原理与配置2022-03-20-15-18-48" width="700" height="">

### 11.2.2 VLAN标签

报文中添加标识VLAN信息的字段使交换机能够分辨不同VLAN的报文。
VLAN标签，又称VLANTag，简称Tag。

<img src="https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/VLAN原理与配置2022-03-20-15-19-49.png" alt="VLAN原理与配置2022-03-20-15-19-49" width="600" height="">

- 如图所示，SW1识别出某个帧是属于哪个VLAN后，会在这个帧的特定位置上添加⼀个标签。这个标签明确地标明了这个帧是属于哪个VLAN的。其他交换机（如SW2）收到这个带标签的数据帧后，就能轻⽽易举地直接根据标签信息识别出这个帧属于哪个VLAN。
- [IEEE 802.1Q](https://zh.wikipedia.org/wiki/IEEE_802.1Q)定义了这种带标签的数据帧的格式。满⾜这种格式的数据帧称为IEEE 802.1Q数据帧，也称VLAN数据帧。

### 11.2.3 VLAN数据帧 :id=vlandate

<img src="https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/VLAN原理与配置2022-03-20-15-23-58.png" alt="VLAN原理与配置2022-03-20-15-23-58" width="" height="">

**TPID（标签协议标识符）**
- <u>取值为0x8100时表示IEEE 802.1Q的VLAN数据帧</u>。如果不⽀持802.1Q的设备收到这样的帧，会将其丢弃。
- 各设备⼚商可以⾃定义该字段的值。当邻居设备将TPID值配置为⾮0x8100时，为了能够识别这样的报⽂，实现互通，必须在本设备上修改TPID值，确保和邻居设备的TPID值配置⼀致。

**PRI（Priority优先级）**
- 取值范围为0～7，值越⼤优先级越⾼。当⽹络阻塞时，交换机优先发送优先级⾼的数据帧。

**CIF（Canonical Format Indicator标准格式指示符）**
- 表示MAC地址在不同的传输介质中是否以标准格式进⾏封装，⽤于兼容以太⽹和令牌环⽹
- CFI取值为0表示MAC地址以标准格式进⾏封装，为1表示以⾮标准格式封装。
- 在以太⽹中，CFI的值为0。

**VLAN ID（VLAN标识符）**
- 取值范围是0～4095。由于0和4095为协议保留取值，所以VLAN ID的有效取值范围是1～4094。

?> 计算机⽆法识别Tagged数据帧，因此计算机处理和发出的都是Untagged数据帧；为了提⾼处理效率，交换机内部处理的数据帧⼀律都是Tagged帧。

### 11.2.4 VLAN的实现

<img src="https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/VLAN原理与配置2022-03-20-17-53-30.png" alt="VLAN原理与配置2022-03-20-17-53-30" width="" height="">

## 11.3 VLAN的划分方式

<img src="https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/VLAN原理与配置2022-03-20-17-54-30.png" alt="VLAN原理与配置2022-03-20-17-54-30" width="" height="">

### 11.3.1 基于接⼝划分 :id=baseonport 

⽹络管理员预先**给交换机的每个接⼝配置不同的PVID**，当⼀个数据帧进⼊交换机时，如果没有带VLAN标签，该数据帧就会被打上接⼝指定PVID的标签，然后数据帧将在指定VLAN中传输。

<img src="https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/VLAN原理与配置2022-03-20-17-55-46.png" alt="VLAN原理与配置2022-03-20-17-55-46" width="" height="">

**划分原则：**
- 将VLAN ID配置到交换机的物理接⼝上，从某⼀个物理接⼝进⼊交换机的、由终端计 算机发送的Untagged数据帧都被划分到该接⼝的VLAN ID所表明的那个VLAN。

**特点：**
- 这种划分原则简单⽽直观，实现容易，是⽬前实际的⽹络应⽤中最为⼴泛的划分VLAN的⽅式。
- 当计算机接⼊交换机的端⼝发⽣了变化时，该计算机发送的帧的VLAN归属可能会发⽣变化。

**缺省VLAN，PVID (Port VLAN ID)**
- 每个交换机的接⼝都应该配置⼀个PVID，到达这个端⼝的Untagged帧将⼀律被交换机划分到PVID所指代的VLAN。
- 默认情况下，PVID的值为1

### 11.3.2 基于MAC地址划分

⽹络管理员预先**配置MAC地址和VLAN ID映射关系表**，当交换机收到的是Untagged帧时，就依据该表给数据帧添加指定VLAN的标签，然后数据帧将在指定VLAN中传输。

<img src="https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/VLAN原理与配置2022-03-20-17-57-46.png" alt="VLAN原理与配置2022-03-20-17-57-46" width="" height="">

**划分原则：**
- 交换机内部建⽴并维护了⼀个MAC地址与VLAN ID的对应表。当交换机接收到计算机发送的Untagged帧时，交换机将分析帧中的源MAC地址，然后查询MAC地址与VLAN ID的对应表，并根据对应关系把这个帧划分到相应的VLAN中。
**特点：**
- 这种划分实现稍微复杂，但灵活性得到了提⾼。
- 当计算机接⼊交换机的端⼝发⽣了变化时，该计算机发送的帧的VLAN归属不会发⽣变化（因为计算机的MAC地址没有变）。
- 但这种类型的VLAN划分安全性不是很⾼，因为恶意计算机很容易伪造MAC地址。

### 11.3.3 其他划分方式

1. 基于IP⼦⽹划分

⽹络管理员预先**配置IP地址和VLAN ID映射关系表**，当交换机收到的是Untagged帧，就依据该表给数据帧添加指定VLAN的标签，然后数据帧将在指定VLAN中传输。

2. 基于协议划分

⽹络管理员预先**配置以太⽹帧中的协议域和VLAN ID的映射关系表**，如果收到的是Untagged帧，
就依据该表给数据帧添加指定VLAN的标签，然后数据帧将在指定VLAN中传输。

3. 基于策略划分

⽹络管理员预先**配置策略**，如果收到的是Untagged帧，且匹配配置的策略时，给数据帧添加指定VLAN的标签，然后数据帧将在指定VLAN中传输。

?> **配置策略**:
多种组合的划分⽅式，包括接⼝、MAC地址、IP地址等

## 11.4 以太网二层接口类型

<img src="https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/VLAN原理与配置2022-03-20-18-04-05.png" alt="VLAN原理与配置2022-03-20-18-04-05" width="300" height="">

### 11.4.1 Access接口

⼀般⽤于和不能识别Tag的⽤户终端（如⽤户主机、服务器等）相连，或者在不需要区分不同VLAN成员时使⽤。
只收发无标记帧；只能加入一个VLAN.

<img src="https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/VLAN原理与配置2022-03-20-20-29-38.png" alt="VLAN原理与配置2022-03-20-20-29-38" width="" height="">

**Access接口接收数据帧：**
- 当Access接口从链路上收到一个Untagged帧，交换机会在这个帧中添加上VID为PVID的Tag，然后对得到的Tagged帧进行转发操作（泛洪、转发、丢弃）。
- 当Access接口从链路上收到一个Tagged帧，交换机会检查这个帧的Tag中的VID是否与PVID相同。如果相同，则对这个Tagged帧进行转发操作；如果不同，则直接丢弃这个Tagged帧。

**Access接口发送数据帧：**
- 当一个Tagged帧从本交换机的其他接口到达一个Access接口后，交换机会检查这个帧的Tag中的VID是否与PVID相同：如果相同，则将这个Tagged帧的Tag进行剥离，然后将得到的Untagged帧从链路上发送出去；如果不同，则直接丢弃这个Tagged帧。

> **#VID** VLAN标识符（[见11.2.3 VLAN数据帧](md/VLAN原理与配置.md#vlandate)）</br>
> **#PVID** 缺省VLAN（[见11.3.1 基于接⼝划分](md/VLAN原理与配置.md#baseonport)）

### 11.4.2 Trunk接口

⼀般⽤于连接交换机、路由器、AP以及可同时收发Tagged帧和Untagged帧的终端。
允许多个VLAN的数据通过。
<img src="https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/VLAN原理与配置2022-03-20-20-42-07.png" alt="VLAN原理与配置2022-03-20-20-42-07" width="" height="">

**Trunk接口接收数据帧：**
- 当Trunk接口从链路上收到一个Untagged帧，交换机会在这个帧中添加上VID为PVID的Tag，然后查看PVID是否在**允许通过的VLAN ID列表**中。如果在，则对得到的Tagged帧进行转发操作；如果不在，则直接丢弃得到的Tagged帧。
- 当Trunk接口从链路上收到一个Tagged帧，交换机会检查这个帧的Tag中的VID是否在允许通过的VLAN ID列表中。如果在，则对这个Tagged帧进行转发操作；如果不在，则直接丢弃这个Tagged帧。

**Trunk接口发送数据帧：**
- 当一个Tagged帧从本交换机的其他接口到达一个Trunk接口后，如果这个帧的Tag中的VID不在允许通过的VLAN ID列表中，则该Tagged帧会被直接丢弃。
- 当一个Tagged帧从本交换机的其他接口到达一个Trunk接口后，如果这个帧的Tag中的VID在允许通过的VLAN ID列表中，则会比较该Tag中的VID是否与接口的PVID相同：
  - 如果相同，则交换机会对这个Tagged帧的Tag进行剥离，然后将得到的Untagged帧从链路上发送出去；
  - 如果不同，则交换机不会对这个Tagged帧的Tag进行剥离，而是直接将它从链路上发送出去。

### 11.4.3 Access接口与Trunt接口举例

> 举例展示了不同VLAN如何通过一个共用端口通信，而不会互相影响。

<img src="https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/VLAN原理与配置2022-03-20-20-47-53.png" alt="VLAN原理与配置2022-03-20-20-47-53" width="" height="">

### 11.4.4 Hybrid接口

- 既可以⽤于连接不能识别Tag的⽤户终端（如⽤户主机、服务器等），也可以⽤于连接交换机、路由器以及可同时收发Tagged帧和Untagged帧的终端、AP。**华为设备默认的接⼝类型是Hybrid。**
- Hybrid接⼝仅允许VLAN ID在允许通过列表中的数据帧通过。
- Hybrid接⼝可以允许多个VLAN的帧带Tag通过，且允许从该类接⼝发出的帧根据需要配置某些VLAN的帧带Tag、某些VLAN的帧不带Tag。
- **与Trunk最主要的区别就是，能够⽀持多个VLAN的数据帧，不带标签过。**

<img src="https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/VLAN原理与配置2022-03-20-20-51-39.png" alt="VLAN原理与配置2022-03-20-20-51-39" width="" height="">

**Hybrid接口接收数据帧：**
- 当Hybrid接口从链路上收到一个Untagged帧，交换机会在这个帧中添加上VID为PVID的Tag，然后查看PVID是否在**Untagged或Tagged VLAN ID列表**中。如果在，则对得到的Tagged帧进行转发操作；如果不在，则直接丢弃得到的Tagged帧。
- 当Hybrid接口从链路上收到一个Tagged帧，交换机会检查这个帧的Tag中的VID是否在Untagged或Tagged VLAN ID列表中。如果在，则对这个Tagged帧进行转发操作；如果不在，则直接丢弃这个Tagged帧。

**Hybrid接口发送数据帧：**
- 当一个Tagged帧从本交换机的其他接口到达一个Hybrid接口后，如果这个帧的Tag中的VID既不在Untagged VLAN ID列表中，也不在Tagged VLAN ID列表中，则该Tagged帧会被直接丢弃。
- 当一个Tagged帧从本交换机的其他接口到达一个Hybrid接口后，如果这个帧的Tag中的VID在Untagged VLAN ID列表中，则交换机会对这个Tagged帧的Tag进行剥离，然后将得到的Untagged帧从链路上发送出去。
- 当一个Tagged帧从本交换机的其他接口到达一个Hybrid接口后，如果这个帧的Tag中的VID在Tagged VLAN ID列表中，则交换机不会对这个Tagged帧的Tag进行剥离，而是直接将它从链路上发送出去。

!> 华为设备特有的接口类型。

### 11.4.5 Hybrid接口举例

> 举例展示了不同VLAN的客户端不能相互访问，但是却都可以访问同一个VLAN的服务器。

<img src="https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/VLAN原理与配置2022-03-20-20-57-18.png" alt="VLAN原理与配置2022-03-20-20-57-18" width="" height="">

### 11.4.6 小结

<img src="https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/VLAN原理与配置2022-03-20-21-00-22.png" alt="VLAN原理与配置2022-03-20-21-00-22" width="" height="">

<img src="https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/VLAN原理与配置2022-03-20-21-00-38.png" alt="VLAN原理与配置2022-03-20-21-00-38" width="300" height="">

## 11.5 VLAN的应用

### 11.5.1 VLAN的规划

**VLAN分配原则**
- 按业务规划
- 按部门规划
- 按应用规划

**VLAN分配技巧**

为了提高VLAN ID的连续性，可以采用VLAN ID和子网关联的方式进行分配。

**VLAN规划示例**
- 假设某园区有三栋楼，分别为行政楼、教学楼、办公楼；每栋楼各有1台接入交换机，核心交换机在行政楼；行政楼内有办公室、财务部和教室；办公楼内有办公室和财务部；教学楼内有办公室和教室。
- VLAN规划如下

<img src="https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/VLAN原理与配置2022-03-20-21-04-21.png" alt="VLAN原理与配置2022-03-20-21-04-21" width="400" height="">

### 11.5.2 基于接口的VLAN划分

某商务楼内有多家公司，为了降低成本，多家公司共用网络资源，各公司分别连接到一台二层交换机的不同接口，并通过统一的出口访问Internet。

<img src="https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/VLAN原理与配置2022-03-20-21-06-36.png" alt="VLAN原理与配置2022-03-20-21-06-36" width="300" height="">

为了保证各公司业务的独立和安全，可将每个公司所连接的接口划分到不同的VLAN，实现公司间业务数据的完全隔离。可以认为每个公司拥有独立的网络，每个VLAN就是一个“虚拟工作组”。

### 11.5.3 基于MAC的VLAN划分

某个公司的网络中，网络管理者将同一部门的员工划分到同一VLAN。为了提高部门内的信息安全，要求只有本部门员工的主机才可以访问特定网络资源。

<img src="https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/VLAN原理与配置2022-03-20-21-08-00.png" alt="VLAN原理与配置2022-03-20-21-08-00" width="400" height="">

为了保证非本部门员工不能访问网络资源，可在SW1上配置基于MAC地址划分VLAN。这样，新的主机接入网络，就无法访问公司的网络资源。

## 11.6 VLAN的配置

### 11.6.1 VLAN的基础配置命令

#### 11.6.1.1 创建VLAN并进入VLAN视图，如果VLAN已存在，直接进入该VLAN的视图

> [!cmd]
> **vlan** _vlan-id_ </br>
> **vlan batch** { _vlan-id1_ \[ **to** _vlan-id2_ \] } &<1-10>

| 参数 | 参数说明 | 取值 |
| :-- | :-- | :-- |
| _vlan-id_ | 指定VLAN ID。 | 整数形式，取值范围是1～4094。 |
| **batch** | 指定批量创建VLAN。 | \- |
| _vlan-id1_ **to** _vlan-id2_ | 指定批量创建的VLAN ID，其中：</br>_vlan-id1_ 表示第一个VLAN的编号。</br> _vlan-id2_ 表示最后一个VLAN的编号。</br> _vlan-id2_ 的取值必须大于等于 _vlan-id1_，它与 _vlan-id1_ 共同确定一个VLAN范围。</br> 如果不指定**to** _vlan-id2_ 参数，则只创建 _vlan-id1_ 所指定的VLAN。 | _vlan-id1_ 和 _vlan-id2_ 是整数形式，取值范围是1～4094。 |

创建编号是100的VLAN并进入VLAN100视图。如果该VLAN100已存在，则直接进入该VLAN100视图。

```shell
<HUAWEI> system-view
[HUAWEI] vlan 100
[HUAWEI-vlan100]
```

#### 11.6.1.2 查看VLAN的相关信息

> [!cmd]
> **display vlan** \[ { _vlan-id_ | **vlan-name** _vlan-name_ } \[ **verbose** \] \]</br>
> **display vlan** \[ _vlan-id1_ \[ **to** _vlan-id2_ \] | **brief** | **summary** \]

| 参数 | 参数说明 | 取值 |
| --- | --- | --- |
| _vlan-id_ | 查看编号是 _vlan-id_ 的VLAN的信息。 | 整数形式，取值范围是1～4094。 |
| _vlan-id1_ \[ **to** _vlan-id2_ \] | 查看编号是 _vlan-id1_ \[ **to** _vlan-id2_ \]的VLAN段的信息。</br>其中：</br> _vlan-id1_ 表示第一个VLAN的编号。</br>- **to** _vlan-id2_ 表示最后一个VLAN的编号。_vlan-id2_ 的取值必须大于等于 _vlan-id1_ 的取值，它和 _vlan-id1_ 共同确定一个范围。如果不指定**to** _vlan-id2_ 参数，则只查看编号为 _vlan-id1_ 的VLAN。 | _vlan-id1_ 为整数形式，取值范围是1～4094。</br> _vlan-id2_ 为整数形式，取值范围是1～4094。 |
| **summary** | 查看所有VLAN的汇总信息。 | \- |
| **verbose** | 查看指定VLAN的详细信息。如果不指定**verbose**，显示VLAN的简要信息。 | \- |
| **vlan-name** _vlan-name_ | 显示指定VLAN名称的VLAN信息。 | 字符串形式，区分大小写，不支持空格，取值范围是1～31。</br>当输入的字符串两端使用双引号时，可在字符串中输入空格。 |
| **brief** | 显示VLAN的简要信息。 | \- |

#### 11.6.1.3 查看VLAN中包含的接口信息

> [!cmd]
> **display port vlan** \[ _interface-type interface-number_ | **active** \] <sup>*</sup>

| 参数 | 参数说明 | 取值 |
| --- | --- | --- |
| _interface-type interface-number_ | 显示VLAN中包含指定接口类型和编号的接口信息。</br>如果不指定接口，则显示VLAN中包含的所有接口信息。 | \- |
| **active** | 显示VLAN中包含动态表项的接口信息。 | \- |

#### 11.6.1.4 配置接口的链路类型

> [!cmd]
> **port link-type** { **access** | **hybrid** | **trunk** }

| 参数 | 参数说明 | 取值 |
| --- | --- | --- |
| **access** | 配置接口的链路类型为Access。 | \- |
| **hybrid** | 配置接口的链路类型为Hybrid。 | \- |
| **trunk** | 配置接口的链路类型为Trunk。 | \- |

配置接口GE0/0/1的链路类型为Trunk。

```shell
<HUAWEI> system-view
[HUAWEI] interface gigabitethernet 0/0/1
[HUAWEI-GigabitEthernet0/0/1] port link-type trunk
```

#### 11.6.1.5 配置接口的缺省VLAN并同时加入这个VLAN

> [!cmd]
> **port default vlan** _vlan-id_ \[ **step** _step-number_ \[ **increased** | **decreased** \] \]

| 参数 | 参数说明 | 取值 |
| --- | --- | --- |
| _vlan-id_ | 配置缺省VLAN的编号。 | 整数形式，取值范围是1～4094。 |
| **step** _step-number_ \[ **increased** \| **decreased** \] | 指定将端口组成员接口加入到以 _vlan-id_ 为起始VLAN，以 _step-number_ 为步长的VLAN中。</br>**increased**表示以VLAN ID递增的方式将接口加入到VLAN中，**decreased**表示以VLAN ID递减的方式将接口加入到VLAN中。</br>例如， _vlan-id_ 取值是10，_step-number_ 取值是20，选择以**increased**方式将接口加入到VLAN中，则端口组的成员接口1加入到VLAN10中，成员端口2加入到VLAN30中，以此类推。 | _step-number_ 是整数形式，取值范围是1～4093。 |

> 关于**step** _step-number_ \[ **increased** \| **decreased** \]说明：
> - 此参数只有在端口组视图下可以使用。
> - 选择**step**方式，_vlan-id_ 的取值必须保证所有接口加入的VLAN是可以使用的。
> - 如果不指定此参数，则端口组中的所有成员接口加入到同一个VLAN，即VLAN _vlan-id_ 。

配置接口GE0/0/1的接口类型为Access，缺省VLAN为VLAN3（VLAN3已经存在）。

```shell
<HUAWEI> system-view
[HUAWEI] interface gigabitethernet 0/0/1
[HUAWEI-GigabitEthernet0/0/1] port link-type access
[HUAWEI-GigabitEthernet0/0/1] port default vlan 3
```

#### 11.6.1.6 设置Trunk类型接口的缺省VLAN

> [!cmd]
> **port trunk pvid vlan** _vlan-id_

| 参数 | 参数说明 | 取值 |
| --- | --- | --- |
| _vlan-id_ | 指定Trunk类型接口的缺省VLAN编号。 | 整数形式，取值范围是1～4094。 |

配置接口GE0/0/1的缺省VLAN为VLAN5。

```shell
<HUAWEI> system-view
[HUAWEI] interface gigabitethernet 0/0/1
[HUAWEI-GigabitEthernet0/0/1] port link-type trunk
[HUAWEI-GigabitEthernet0/0/1] port trunk pvid vlan 5
```

#### 11.6.1.7 配置Trunk类型接口加入的VLAN

> [!cmd]
> **port trunk allow-pass vlan** { { _vlan-id1_ \[ **to** _vlan-id2_ \] }&<1-10> | **all** }

| 参数 | 参数说明 | 取值 |
| --- | --- | --- |
| _vlan-id1_ \[ **to** _vlan-id2_ \] | 指定Trunk类型接口加入的VLAN，其中：</br>_vlan-id1_ 表示第一个VLAN的编号。</br> **to** _vlan-id2_ 表示最后一个VLAN的编号。_vlan-id2_ 的取值必须大于等于 _vlan-id1_ 的取值。 | _vlan-id1_ 为整数形式，取值范围是1～4094。</br>_vlan-id2_ 为整数形式，取值范围是1～4094。 |
| **all** | 指定Trunk接口加入所有VLAN。 | \- |
| _vlan-id3_ | 指定端口组中成员接口与VLAN绑定的起始VLAN。 | 整数形式，取值范围是1～4094。 |
| **step** _step-number_ | 指定VLAN ID递增或递减的步长。</br>此参数用于实现以 _vlan-id3_ 为起始VLAN、 _step-number_ 为步长、递增或递减的方式将端口组下成员接口与VLAN一一绑定，便于用户配置。如：</br>端口组下有10个成员接口，通过命令**port trunk allow-pass vlan**设置 _vlan-id3_ 为1、 _step-number_ 为1、选择递增方式成功配置后，成员口1加入的VLAN ID为1、成员口2加入的VLAN ID为2，以此类推，成员口10加入的VLAN ID为10。 | 整数形式，取值范围是1～4093。 |
| **increased** | 指定以 _vlan-id3_ 为起始VLAN、 _step-number_ 为步长、递增的方式将端口组下成员接口与VLAN一一绑定。 | 缺省情况下，二层接口与VLAN以递增的方式绑定。 |
| **decreased** | 指定以 _vlan-id3_ 为起始VLAN、 _step-number_ 为步长、递减的方式将端口组下成员接口与VLAN一一绑定。</br>选择递减方式， _vlan-id3_ 的取值必须大于等于端口组下的成员接口数。 | \- |

配置接口GE0/0/1属于VLAN10～VLAN30。

```shell
<HUAWEI> system-view
[HUAWEI] interface gigabitethernet 0/0/1
[HUAWEI-GigabitEthernet0/0/1] port link-type trunk
[HUAWEI-GigabitEthernet0/0/1] port trunk allow-pass vlan 10 to 30
```

#### 11.6.1.8 设置Hybrid类型接口的缺省VLAN ID

> [!cmd]
> **port hybrid pvid vlan** _vlan-id_

| 参数 | 参数说明 | 取值 |
| --- | --- | --- |
| _vlan-id_ | 指定Hybrid类型接口的缺省VLAN编号。 | 整数形式，取值范围是1～4094。 |

配置接口GE0/0/1的缺省VLAN为VLAN5。

```shell
<HUAWEI> system-view
[HUAWEI] vlan 5
[HUAWEI-vlan5] quit
[HUAWEI] interface gigabitethernet 0/0/1
[HUAWEI-GigabitEthernet0/0/1] port link-type hybrid
[HUAWEI-GigabitEthernet0/0/1] port hybrid pvid vlan 5
```

#### 11.6.1.9 配置Hybrid类型接口加入的VLAN，这些VLAN的帧以Tagged方式通过接口

> [!cmd]
> **port hybrid tagged vlan** { { _vlan-id1_ \[ **to** _vlan-id2_ \] }&<1-10> | **all** }

| 参数 | 参数说明 | 取值 |
| --- | --- | --- |
| _vlan-id1_ \[ **to** _vlan-id2_ \] | 指定Hybrid类型接口加入的VLAN，其中：</br> _vlan-id1_ 表示第一个VLAN的编号。</br> **to** _vlan-id2_ 表示最后一个VLAN的编号。 _vlan-id2_ 的取值必须大于等于 _vlan-id1_ 的取值。 | _vlan-id1_ 为整数形式，取值范围是1～4094。</br>_vlan-id2_ 为整数形式，取值范围是1～4094。 |
| **all** | 指定Hybrid接口加入所有VLAN。 | \- |
| _vlan-id3_ | 指定端口组中成员接口与VLAN绑定的起始VLAN。 | 整数形式，取值范围是1～4094。 |
| **step** _step-number_ | 指定VLAN ID递增或递减的步长。</br>此参数用于实现以 _vlan-id3_ 为起始VLAN、 _step-number_ 为步长、递增或递减的方式将端口组下成员接口与VLAN一一绑定，便于用户配置。如：</br>端口组下有10个成员接口，通过命令**port hybrid tagged vlan**设置 _vlan-id3_ 为1、 _step-number_ 为1、选择递增方式成功配置后，成员口1加入的VLAN ID为1、成员口2加入的VLAN ID为2，以此类推，成员口10加入的VLAN ID为10。 | 整数形式，取值范围是1～4093。 |
| **increased** | 指定以 _vlan-id3_ 为起始VLAN、 _step-number_ 为步长、递增的方式将端口组下成员接口与VLAN一一绑定。 | 缺省情况下，二层接口与VLAN以递增的方式绑定。 |
| **decreased** | 指定以 _vlan-id3_ 为起始VLAN、_step-number_ 为步长、递减的方式将端口组下成员接口与VLAN一一绑定。</br>选择递减方式， _vlan-id3_ 的取值必须大于等于端口组下的成员接口数。 | \- |

配置接口GE0/0/1属于VLAN3～VLAN5，并且接口GE0/0/1在发送以上这些VLAN的帧时不将帧中的Tag剥掉。

```shell
<HUAWEI> system-view
[HUAWEI] interface gigabitethernet 0/0/1
[HUAWEI-GigabitEthernet0/0/1] port link-type hybrid
[HUAWEI-GigabitEthernet0/0/1] port hybrid tagged vlan 3 to 5
```

#### 11.6.1.10 配置Hybrid类型接口加入的VLAN，这些VLAN的帧以Untagged方式通过接口

> [!cmd]
> **port hybrid untagged vlan** { { _vlan-id1_ \[ **to** _vlan-id2_ \] }&<1-10> | **all** }

| 参数 | 参数说明 | 取值 |
| --- | --- | --- |
| _vlan-id1_ \[ **to** _vlan-id2_ \] | 指定Hybrid类型接口加入的VLAN，其中：</br>_vlan-id1_ 表示第一个VLAN的编号。</br>**to** _vlan-id2_ 表示最后一个VLAN的编号。 _vlan-id2_ 的取值必须大于等于 _vlan-id1_ 的取值。 | _vlan-id1_ 为整数形式，取值范围是1～4094。</br>_vlan-id2_ 为整数形式，取值范围是1～4094。 |
| **all** | 指定Hybrid接口所属的所有VLAN。 | \- |
| _vlan-id3_ | 指定端口组中成员接口与VLAN绑定的起始VLAN。 | 整数形式，取值范围是1～4094。 |
| **step** _step-number_ | 指定VLAN ID递增或递减的步长。</br>此参数用于实现以 _vlan-id3_ 为起始VLAN、 _step-number_ 为步长、递增或递减的方式将端口组下成员接口与VLAN一一绑定，便于用户配置。如：</br>端口组下有10个成员接口，通过命令**port hybrid untagged vlan**设置 _vlan-id3_ 为1、 _step-number_ 为1、选择递增方式成功配置后，成员口1加入的VLAN ID为1、成员口2加入的VLAN ID为2，以此类推，成员口10加入的VLAN ID为10。 | 整数形式，取值范围是1～4093。 |
| **increased** | 指定以 _vlan-id3_ 为起始VLAN、 _step-number_ 为步长、递增的方式将端口组下成员接口与VLAN一一绑定。 | 缺省情况下，二层接口与VLAN以递增的方式绑定。 |
| **decreased** | 指定以 _vlan-id3_ 为起始VLAN、 _step-number_ 为步长、递减的方式将端口组下成员接口与VLAN一一绑定。</br>选择递减方式， _vlan-id3_ 的取值必须大于等于端口组下的成员接口数。 | \- |

配置接口GE0/0/1属于VLAN3～VLAN5，并且接口GE0/0/1在发送以上这些VLAN的帧时将帧中的Tag剥掉。

```shell
<HUAWEI> system-view
[HUAWEI] interface gigabitethernet 0/0/1
[HUAWEI-GigabitEthernet0/0/1] port link-type hybrid
[HUAWEI-GigabitEthernet0/0/1] port hybrid untagged vlan 3 to 5
```

#### 11.6.1.11 使能接口的MAC VLAN功能

> [!cmd]
> **mac-vlan enable**

使能接口GE0/0/1的MAC VLAN功能。

```shell
<HUAWEI> system-view
[HUAWEI] interface gigabitethernet 0/0/1
[HUAWEI-GigabitEthernet0/0/1] port link-type hybrid
[HUAWEI-GigabitEthernet0/0/1] mac-vlan enable
```

#### 11.6.1.12 配置MAC地址与VLAN关联

> [!cmd]
> **mac-vlan mac-address** _mac-address_ \[ _mac-address-mask_ | _mac-address-mask-length_ \] \[ **priority** _priority_ \]

| 参数 | 参数说明 | 取值 |
| --- | --- | --- |
| _mac-address_ | 指定与VLAN关联的MAC地址。 | 格式为H-H-H。其中H为4位的十六进制数，可以输入1～4位，如00e0、fc01。当输入不足4位时，表示前面的几位为0，如：输入e0，等同于00e0。MAC地址不可设置为0000-0000-0000、FFFF-FFFF-FFFF和组播地址。 |
| _mac-address-mask_ | 指定MAC地址掩码。 | 格式为H-H-H，其中H为1至4位的十六进制数，缺省值是FFFF-FFFF-FFFF。 |
| _mac-address-mask-length_ | 指定MAC地址掩码长度。 | 整数形式，取值范围是1～48，缺省值是48。 |
| **priority** _priority_ | 指定MAC地址对应VLAN的802.1p优先级。 | 整数形式，取值范围是0～7，值越大优先级越高。缺省值是0。 |
| **all** | 指定与VLAN关联的所有MAC地址。 | \- |

配置MAC地址22-33-44与VLAN100关联。

```shell
<HUAWEI> system-view
[HUAWEI] vlan 100
[HUAWEI-vlan100] mac-vlan mac-address 22-33-44
```

### 11.6.2 VLAN的配置案例
</br>
<img src="https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/VLAN原理与配置2022-03-20-21-11-41.png" alt="VLAN原理与配置2022-03-20-21-11-41" width="" height="">