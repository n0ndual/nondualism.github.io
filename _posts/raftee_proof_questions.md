
# Table of Contents

1.  [为什么要使用UC框架来证明？](#orgf67ca5a)
    1.  [假设不用UC来证明：](#org6e2534f)
    2.  [使用UC的好处](#org80da046)
2.  [使用uc-emulates 还是 uc-realize?](#org7e2e502)
    1.  [先考虑 raftee uc-emulates 另一个协议raft<sub>cf</sub>](#orgad6a333)
        1.  [难点1：TEE初始化信息](#orgbcda0e2)
        2.  [引申问题：TLS<sub>IAS证书初始化过程是否必须是固定的</sub>？](#org58800e4)
        3.  [引申问题：客户端是否必须与raftee节点建立TLS连接？](#org6b39e99)
        4.  [难点2：客户端与raftee节点的通信过程](#orgde7c363)
        5.  [引申问题：S能否读取理想函数的中间状态？](#orga17ef8e)
        6.  [难点3：raftee节点之间的通信过程](#org6e9258f)
3.  [uc-emulates 和 uc-realize的对比和选择](#org195e3ba)
4.  [第2，3章构思](#org07f95af)
    1.  [是否需要section 2 先描述协议？](#org1e78e9a)
    2.  [是否需要先对协议进行一个overview？](#orgd3e69a4)
    3.  [问题1：如何初始化和验证？](#org8156023)
    4.  [问题2：enclave之间如何通信？](#org5642080)
    5.  [问题3：enclave的状态如何保存？](#org8c77523)
    6.  [问题4：enclave中的raft程序是否与F<sub>raft</sub> 完全一致？](#org8a979eb)
    7.  [Security Analysis](#org251ad40)
        1.  [raftee中的advarsary模型](#orgb1be9fe)
        2.  [Prot<sub>raftee</sub> UC-realize F<sub>raft</sub> 的过程](#org68092e9)
        3.  [F<sub>raft</sub> + S 的state machine safety 和 liveness Property](#org37cc386)
        4.  [raftee 也具有 state machine safety 和 liveness 两个性质](#org33c9e31)
        5.  [Intel SGX 的安全隐患](#orgd3f71a1)

raftee 证明中的问题：


<a id="orgf67ca5a"></a>

# 为什么要使用UC框架来证明？


<a id="org6e2534f"></a>

## 假设不用UC来证明：

A(advarsary)可以改通信内容，丢弃消息，A可以篡改logs，A可以篡改定时器，A可以造假证书，A可以尝试破坏TEE（虽然不成功）等等。
需要分析A的任意破坏行为，都无法破坏核心的raft的安全性。难点在于，如何证明上述任意的行为的任意组合，都无法破坏安全性。
证明过程中肯定包括了一些步骤，对A的所有可能的corruption从简单到复杂，一步步地分析和组合，等价于使用UC框架。


<a id="org80da046"></a>

## 使用UC的好处

拉近raftee协议和raft协议的距离，把复杂的证明简化。
重点是把构造raft协议中的一个S(simulator)，可以模拟raftee协议中的A的所有行为，使得Z(environment)无法区分自己是在与raftee+A交流，还是在于raft+S交流。
S的行为非常简单，相当于一个crash only的敌人。
直接应用raft协议的安全性证明，S无法破坏raft的安全性


<a id="org7e2e502"></a>

# 使用uc-emulates 还是 uc-realize?


<a id="orgad6a333"></a>

## 先考虑 raftee uc-emulates 另一个协议raft<sub>cf</sub>

目标：raftee协议模拟了raft<sub>cf协议</sub>


<a id="orgbcda0e2"></a>

### 难点1：TEE初始化信息

因为raftee中，Z能看到TEE初始化后的证书。那么，raft<sub>cf中的S必须模拟这些信息</sub>。
但是uc-emulates方式中，raft<sub>cf也只是一个普通协议</sub>，其中的Z可以直接向Pi索要这些信息。出问题了。
如果是UC-realize方式，ideal<sub>raft</sub> 是理想函数，Z只能从S中获取信息，S就可以模拟证书了。


<a id="org58800e4"></a>

### 引申问题：TLS<sub>IAS证书初始化过程是否必须是固定的</sub>？

是否需要一个global setup过程？是否可以动态？
可以假设是固定的，在一个session中随机生成证书并组建静态集群。同样，身份验证方面，不属于协议要考虑的部分。


<a id="org6b39e99"></a>

### 引申问题：客户端是否必须与raftee节点建立TLS连接？

如果建立TLS连接，可以验证raftee节点是否真实。那么，raft<sub>cf的S必须能够获取tls私钥</sub>，模拟客户端与Z的交互。
如果不用建立TLS连接，z直接把input给Pi，Pi把输入传给main machine。

客户端不属于协议的一部分，协议的安全性证明边界是：从Z给raftee的某个节点Pi一个input开始
真实的实现中，建立的TLS连接是为了验证raftee节点的身份，与协议本身无关。


<a id="orgde7c363"></a>

### 难点2：客户端与raftee节点的通信过程

在raftee中，A可以把客户端与raftee节点的通信发给Z。那么在raft<sub>cf中</sub>，S也必须能模拟这些信息。
两种模拟方式：
a，引入一个backdoor，就像Ftee论文中那样。缺点，有一个backdoor，会导致advarsary的行为更难模拟。
b，不考虑客户端与raftee节点的通信过程，或者说，客户端与raftee节点之间没有tls连接。


<a id="orga17ef8e"></a>

### 引申问题：S能否读取理想函数的中间状态？


<a id="org6e9258f"></a>

### 难点3：raftee节点之间的通信过程

如果raft<sub>cf是一个协议</sub>，S可以去破坏raft<sub>cf节点之间的通信</sub>，模拟A的行为。
如果把raft<sub>cf换成理想函数F</sub><sub>raft</sub>，S能否去改变F<sub>raft的中间过程</sub>，比如暂停/打断？


<a id="org195e3ba"></a>

# uc-emulates 和 uc-realize的对比和选择

\## 疑问1：理想函数ideal<sub>raft是否可以是并发的多个实例</sub>？

如果不能的话，直接否定了uc-realize的方式。
猜测：可以自行去建模。

\## 疑问2：S能否去打断或者改变ideal<sub>raft的中间过程</sub>。

如果不能的话，直接否定uc-realize.
猜测：可以自行去建模。

\## 模拟副作用的不同

raft<sub>cf中S模拟A的副作用</sub>，需要创建N个假的enclave，模拟假的证书。如果Z直接与Pi交流，读取其证书，那就否定了raft<sub>cf方案</sub>。
为了模拟tls通信内容，如果z直接与Pi交流，Pi之间必须用tls协议来通信。

F<sub>raft中的副作用</sub>，可以全部由S包办。S 创造N个假的enclave，S创造假的TLS通信。

\## 模拟corruption行为

raft<sub>cf</sub>，按照uc论文确定S可以改变Pi的输入输出带，所以可以很好的模拟各种corruption。

F<sub>raft</sub> 是否能改变理想函数的中间状态，影响理想函数的执行过程？似乎不确定。

首先，A的所有行为能被S模拟，让Z无法分辨。目的是说明，没有额外信息泄漏。
其次，S的所有行为，不会影响理想函数的执行。UC论文中，S只能与F的输出交流。S是否能影响输出？再查。
S必须能模拟A对协议的所有影响，而不影响F的执行。

\### uc-realizes

在现实世界中，

1，z可以与main machine交互，但不能与subroutine交互

2，z是否能看到中间通信过程？可以

3，z可以随时与A交流，z知道A的所有行动

4，z复杂提供输入？

在理想世界中，

1，z只能与S和ideal function 输入输出交流

2，z无法看到ideal function之间的交互

3，z基本只能通过S获取中间结果和状态

A is simulatable by S(simulator)

任意A 的任意行为，可以被S模仿


<a id="org07f95af"></a>

# 第2，3章构思


<a id="org1e78e9a"></a>

## 是否需要section 2 先描述协议？

需要，为第三章的形式化分析打下基础。
在第二章中，需要对 raftee的架构说明白，
给出F<sub>raft的形式化模型</sub>，使用public delayed output模型。
给出Prog<sub>raftee的伪代码</sub>。
给出Prot<sub>raftee的形式化模型</sub>。


<a id="orgd3e69a4"></a>

## 是否需要先对协议进行一个overview？

方便下文的描述。
是否需要加入advarsary，描述advarsary的能力？hybrid model，与原始的byzantine有区别。


<a id="org8156023"></a>

## 问题1：如何初始化和验证？

如何验证身份，初始化
使用GUC框架下的global F<sub>tee模型</sub>，给出形式化模型
static clusters


<a id="org5642080"></a>

## 问题2：enclave之间如何通信？

给出F<sub>sec</sub> 形式化模型


<a id="org8c77523"></a>

## 问题3：enclave的状态如何保存？

使用intel的data sealing feature.
data sealing key 从 F<sub>tee</sub> 的SK 派生出来。
使用monotonic counter来保护，避免脏数据攻击。


<a id="org8a979eb"></a>

## 问题4：enclave中的raft程序是否与F<sub>raft</sub> 完全一致？

给出Prog<sub>raftee</sub>
给出F<sub>raft</sub> 形式化模型。
几乎完全一致。
不依赖可信时钟，使用操作系统的不可靠时钟。
内部的raft协议不使用任何的密码学算法。
当节点丢失logs后，或者加载了脏数据后，变成不可投票节点。


<a id="org251ad40"></a>

## Security Analysis

简单介绍我们使用的方法，UC的证明过程。


<a id="orgb1be9fe"></a>

### raftee中的advarsary模型

具体描述其能力，无法完全形式化


<a id="org68092e9"></a>

### Prot<sub>raftee</sub> UC-realize F<sub>raft</sub> 的过程


<a id="org37cc386"></a>

### F<sub>raft</sub> + S 的state machine safety 和 liveness Property


<a id="org33c9e31"></a>

### raftee 也具有 state machine safety 和 liveness 两个性质


<a id="orgd3f71a1"></a>

### Intel SGX 的安全隐患

上述证明依赖的假设：intel sgx 三个技术的安全性
主要的隐患在于侧信道攻击，不具体描述，加几个引用

