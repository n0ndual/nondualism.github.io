---
layout: post
title:  "基于SGX实现Machine learning"
date:   2020-07-25 12:20:01
categories: thoughts
tags: enclave SGX raftee
---

* content
{:toc}

---


# Table of Contents

1.  [Raftee 的安全性分析](#orgddee888)
    1.  [形式化模型：](#orgbce4fa2)
        1.  [基础部件](#org3b5c30a)
        2.  [raftee 形式化](#org4763d27)
    2.  [证明过程：](#org15d24b7)
        1.  [定理1：Prot<sub>raftee</sub> UC-realizes F<sub>raft</sub>](#org8887814)
        2.  [引理1： F<sub>raft</sub> + S 满足 state machine safety 属性](#org73dfff6)
        3.  [定理2： Prot<sub>raftee</sub> 满足 state machine safety 属性](#org9ec7615)


<a id="orgddee888"></a>

# Raftee 的安全性分析


<a id="orgbce4fa2"></a>

## 形式化模型：


<a id="org3b5c30a"></a>

### 基础部件

首先需要对基础部件进行形式化。

1.  F<sub>tee形式化了intel</sub> sgx处理器。

    需要写出来细节。参考两篇论文，融合起来做一些修改。
    参考论文： 《Formal Abstractions for Attested Execution Secure Processors》
    和 《Sealed-Glass Proofs: Using Transparent Enclaves to Prove and Sell Knowledge》

2.  F<sub>ds</sub> 形式化intel sgx的data sealing api。

    不用写出来，只定义理想函数F<sub>ds即可</sub>。
    没有可参考的，需要自己搞。

3.  F<sub>ke</sub> 和 F<sub>sec</sub> 对TLS协议的 key-exchange 和 加密信道进行形式化。

    不用写出来，只定义理想函数，说明TLS协议实现了这两个理想函数，引述相关论文即可。
    参考《Universally Composable Security Analysis of TLS》

4.  F<sub>raft</sub> 对Raft协议进行形式化

    有必要写出来，但没有现成的。可以简写，不完全地形式化。
    
    参考raft论文自己搞，简写，细节见原论文。


<a id="org4763d27"></a>

### raftee 形式化

对raftee 进行形式化，重点，必须严谨。

包括三部分：Prot<sub>raftee</sub> 是完整的协议；enclave中的program形式化为Prog<sub>raftee</sub>，Prot<sub>raftee</sub> 与Prog<sub>raftee交互</sub>；Prog<sub>raft</sub> 是Prog<sub>raftee的子程序</sub>，实现了raft协议的所有函数.

1.  Prot<sub>raftee</sub>:

    on input "init" from Z:
        初始化TEE，加载Prog<sub>raftee程序</sub>
        通过F<sub>tee</sub> 调用Prog<sub>raftee的init方法</sub>，生成tls证书
        把证书发给各个peer
        启动定时器：每隔T<sub>timeout时间后</sub>，通过F<sub>tee</sub> 调用Prog<sub>raftee</sub> 的 periodic方法。
    
    on input "new<sub>entry</sub>" from Z:
        通过F<sub>tee</sub> 调用 Prog<sub>raftee</sub> 中的"new<sub>entry</sub>"方法
        达成共识后，返回该entry的序列号。
    
    on input "restart" from Z:
        通过F<sub>tee</sub> 调用Prog<sub>raftee</sub> 中的"reload"方法，加载持久化的tls证书和日志
        解密日志，成功通过的话，启动定时器：每隔T<sub>timeout时间后</sub>，通过F<sub>tee</sub> 调用Prog<sub>raftee</sub> 的 periodic方法。
    
    on receive "tls<sub>cert</sub>" from P<sub>j</sub>：
        收到 peer 发来的证书后，通过F<sub>tee调用Prog</sub><sub>raftee</sub> 的add<sub>cert方法</sub>
        如果验证发现该证书是在TEE中生成，把该证书加入到信任列表。
        调用F<sub>ke</sub>，和 P<sub>j</sub> 进行key-exchange。
    
    on receive "tcp<sub>input</sub>" from P<sub>j</sub>:
        收到 peer 发来的ct<sub>tcp</sub><sub>data</sub> 数据包后，通过F<sub>tee</sub> 调用Prog<sub>raftee</sub> 的 "tcp<sub>input</sub>"
        收到F<sub>tee返回的</sub> ("tcp<sub>output</sub>", P<sub>k</sub>, tcp<sub>data</sub>) 后，
        发送("tcp<sub>in</sub>", tcp<sub>data</sub>)给 P<sub>k</sub>

2.  Prog<sub>raftee</sub>:

    on input "init" from F<sub>tee</sub>:
        生成tls 私钥，公钥，自签名证书
        返回 自签名证书 给 F<sub>tee</sub>.
    
    on input "new<sub>entry</sub>" from F<sub>tee</sub>:
        调用F<sub>raft</sub> 中的"new<sub>entry</sub>"方法。
        把结果返回给F<sub>tee</sub>.
    
    on receive "tls<sub>cert</sub>" from F<sub>tee</sub>：
        如果验证发现该证书是在TEE中生成，把该证书加入到信任列表。
        结果返回给F<sub>tee</sub>.
    
    on receive "tcp<sub>input</sub>" from F<sub>tee</sub>:
        解密tcp输入，pt<sub>tcp</sub><sub>input</sub> = SE<sub>key.decrypt</sub>(ct<sub>tcp</sub><sub>input</sub>).
        把 pt<sub>input</sub><sub>data</sub> 传给 F<sub>raft</sub>, 收到结果（"raft<sub>ouput</sub>", P<sub>k</sub>, raft<sub>output</sub>).
        加密，ct<sub>tcp</sub><sub>out</sub> = SE<sub>key.encrypt</sub>(raft<sub>output</sub>)
        发送("tcp<sub>output</sub>", P<sub>k</sub>, tcp<sub>data</sub>) 给 F<sub>tee</sub>
    
    on receive "reload" from F<sub>tee</sub>:
        解密ct<sub>logs</sub>, ct<sub>tls</sub><sub>cert</sub>
        加载cert，
        调用F<sub>raft的加载logs</sub>
        结果返回给F<sub>tee</sub>

3.  Prog<sub>raft</sub>:

    类似F<sub>raft</sub>，包含raft的所有子函数，简单写，引述raft论文


<a id="org15d24b7"></a>

## 证明过程：

主要参考论文：
《Universally Composable Security: A New Paradigm for Cryptographic Protocols》
《Formal Abstractions for Attested Execution Secure Processors》
《Sealed-Glass Proofs: Using Transparent Enclaves to Prove and Sell Knowledge》
《Teechain: A Secure Payment Network with Asynchronous Blockchain Access》


<a id="org8887814"></a>

### 定理1：Prot<sub>raftee</sub> UC-realizes F<sub>raft</sub>

1.  UC—realize的证明方法简介

    所有的部分都形式化以后，使用UC框架 相对简单了。
    在UC框架中分为现实世界和理想世界。
    在现实世界中的Prot<sub>raftee</sub>, 面临着A（byzantine advarsary）的攻击。
    在理想世界中的F<sub>raft</sub>（原始的raft协议），面临着假想的S （simulator，自己构造）的攻击。
    
    Z(environment 外部环境)无法区分它所观察到的是Prot<sub>raftee</sub>+A，还是 F<sub>raft</sub> + S，就意味着 Prot<sub>raftee</sub> UC-realizes F<sub>raft</sub>。

2.  证明重点：

    对于A的任意一种攻击，都对应于S的一种模拟攻击，使得Z无法分辨。
    
    分为三个步骤：H1, H2, H3，H4
    
    1.  H1
    
        S 模拟 A 对 init 函数的攻击
    
    2.  H2
    
        S 模拟 A 对 tls<sub>cert</sub> 的攻击
    
    3.  H3
    
        S 模拟 A 对 tcp<sub>msgs</sub> 的攻击
    
    4.  H4
    
        S 模拟了 A 对 reload<sub>logs</sub> 的攻击


<a id="org73dfff6"></a>

### 引理1： F<sub>raft</sub> + S 满足 state machine safety 属性

构造出来的S不会使F<sub>raft偏离协议</sub>，不会造假消息，只会停止运行，或者丢掉消息。

S 等于是一个 crash fault 敌人。

因此F<sub>raft</sub> + S 是安全的(不用证明，引用raft论文)，满足state machine safety 属性。


<a id="org9ec7615"></a>

### 定理2： Prot<sub>raftee</sub> 满足 state machine safety 属性

由定理1 和 引理1 可得。



