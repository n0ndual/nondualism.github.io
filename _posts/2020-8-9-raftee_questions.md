---
layout: post
title:  "raftee理论分析的细节问题"
date:   2020-8-9 12:20:01
categories: thoughts
tags: SGX raftee crs global
---

* content
{:toc}

---
# Table of Contents

1.  [客户端与raftee节点的通信，是否也需要形式化？](#org8b90823)
2.  [能不能写成F<sub>tee</sub>-hybrid model？](#org6fc9a8a)
3.  [形式化TEE时，用global model 还是 local model?](#org1ab8375)
4.  [我们的P<sub>raftee</sub> 是否需要 crs?](#org194eb1b)
5.  [P<sub>raftee</sub> 是否需要建模多轮通信？](#orgc395fe6)
6.  [如何确保sid/sessionid是独一无二的？](#org4b9f167)
7.  [协议的成员是否是动态可变的？](#org7d9c150)
8.  [协议的初始化过程](#org0b9b868)
    1.  [确定参与方，把所有的参与方都写入一个静态配置文件中，并且加入到信任列表中，一旦确定不能动态变化。](#org0b700fd)
    2.  [各参与方之间建立authenticated channel。](#org22e2d75)
    3.  [各参与方确认达成一个sessionid，作为该次运行的协议实例的唯一标识。](#org6f8b9e1)


<a id="org8b90823"></a>

# 客户端与raftee节点的通信，是否也需要形式化？

应该可以不管这部分。不是raftee协议的核心部分，不用过分严谨？


<a id="org6fc9a8a"></a>

# 能不能写成F<sub>tee</sub>-hybrid model？

比如P<sub>raftee调用F</sub><sub>tee</sub>, F<sub>tee</sub> 又调用F<sub>sec</sub>, F<sub>sec</sub> 又调用F<sub>raft</sub>，那么可以说P<sub>raftee是在F</sub><sub>tee模型下吗</sub>？

不符合UC框架的hybrid model的定义。混合模型必须是从最底层开始定义的。必须从底层开始证明，首先有一个P<sub>raft实现了F</sub><sub>raft才行</sub>，而我们的协议是完整的P<sub>raftee</sub> 才能实现F<sub>raft</sub>.

但有些项目论文用了F<sub>tee</sub> - hybrid model这个说法。似乎这个概念的定义比较模糊。


<a id="org1ab8375"></a>

# 形式化TEE时，用global model 还是 local model?

global model 是最贴合实际的intel sgx技术实现的。而local model反而不是现实。

一些论文指出，global model才能构造UC可组合的协议。用local model 不能组合。原因比较复杂，有些细节感觉不太重要，暂时不需要彻底搞清楚。

那么为什么有些基于TEE的论文，还要使用local model来建模？猜测：如果使用global model来建模，并且要证明基于global F<sub>tee的某个协议具有可组合性</sub>，证明非常复杂。如果使用local model建模，足以证明单个协议的安全性，即使不可UC组合对论文目标影响不大。

sealed<sub>glass</sub> proof 论文使用了local model, 他们的模型介于Pass的global 模型和 Barbosa的非UC框架下模型。他们证明了他们的协议的安全，并且他们的协议可以和其他不依赖TEE的协议组合。他们在证明UC可组合时，使用了CRS模型。

猜测：该篇文章不使用global model，是因为使用globalmodel 证明UC可组合性太麻烦。

我们的论文中，可以使用global model，只证明我们的协议的安全性，暂时不用关注可组合性。


<a id="org194eb1b"></a>

# 我们的P<sub>raftee</sub> 是否需要 crs?

是否需要可信初始化？根据一些相关论文，在TEE中实现一些协议（MPC，ZKP，commitment）还需要用到CRS。

经过仔细对比，我们的raftee可以不依赖crs。


<a id="orgc395fe6"></a>

# P<sub>raftee</sub> 是否需要建模多轮通信？

建模时，只需要专注于一轮通信，一次共识过程吗？

如果不考虑多轮，每个独立集群的一次启动，产生一个sessionid，之后的建模过程，只考虑输入一次input，一次共识后输出结果。原因：证明过程不用过分琐碎，一次共识是安全的，能推出多次共识也是安全的。只写出一次是省略了繁琐的部分，为了简洁。

如果需要考虑多轮，不仅需要sessionid, 还需要requestid。在形式化时，把每一轮通信用一个requestid标识。


<a id="org4b9f167"></a>

# 如何确保sid/sessionid是独一无二的？

这个问题似乎是非常复杂的。在理论分析时，只是假设每次初始化某个协议的一个实例时，会产生一个独一无二的sid。但是在实际实现某个协议时，究竟怎么产生的，一般论文都不提。猜测：可能也是需要可信初始化的过程，但不属于协议安全性分析的一部分，一般不讨论。

对我们的raftee协议来说，sid可以写死在enclave代码中。每次初始化一个实例，就要手动改一次sessionid。


<a id="org7d9c150"></a>

# 协议的成员是否是动态可变的？

UC框架中，考虑的各个参与方一般是确定的，可以看成是静态配置的集群。如果是动态可变的，是否安全可靠，未知。


<a id="org0b9b868"></a>

# 协议的初始化过程


<a id="org0b700fd"></a>

## 确定参与方，把所有的参与方都写入一个静态配置文件中，并且加入到信任列表中，一旦确定不能动态变化。


<a id="org22e2d75"></a>

## 各参与方之间建立authenticated channel。


<a id="org6f8b9e1"></a>

## 各参与方确认达成一个sessionid，作为该次运行的协议实例的唯一标识。

