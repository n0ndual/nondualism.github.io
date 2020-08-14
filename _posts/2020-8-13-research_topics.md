---
layout: post
title:  "2020年区块链研究热点"
date:   2020-8-13 12:20:01
categories: thoughts
tags: blockchain 2020 research
---

* content
{:toc}

---

# Table of Contents

1.  [intro](#org9c2c73b)
    1.  [重视监管技术](#org8831979)
    2.  [跨链技术是实现审核的基础](#org6a8eeb8)
    3.  [重视数据存储/链上链下数据协同](#org8fa9425)
    4.  [其他](#orgdf22012)
    5.  [下文结构](#orgf81da64)
2.  [跨链](#orgaf8d6ff)
    1.  [相关课题](#org08497d3)
        1.  [中兴-区块链系统互联互通关键技术研究](#orga60b95d)
        2.  [北京市2020年度区块链领域储备课题](#orgae716b7)
        3.  [北京市自然科学基金面上项目指南](#org31cba84)
        4.  [国家重点研发计划"云计算和大数据"重点专项-"以链治链"监管架构与关键技术研究](#orgcbbaaa2)
        5.  [国家重点研发计划"云计算和大数据"重点专项-支持异构多链互通的新型跨链体系研究](#orgfbf1825)
    2.  [研究方向](#orgfc8c5b1)
        1.  [异构联盟链之间的高性能去中心化跨链技术](#org25092ba)
        2.  [不存在单点依赖的跨链原子性事务处理机制](#org8c1d3ab)
        3.  [可监管的高性能存储侧链以及存储侧链与主链的数据协同](#org6ad6ac7)
        4.  [密态内容跨链监管方法](#orgec64278)
3.  [共识机制](#orgeca4325)
    1.  [相关课题](#orgc5a1955)
        1.  [北京市2020年度区块链领域储备课题](#org12e1803)
        2.  [北京市自然科学基金面上项目指南](#orgf7dc6f0)
    2.  [研究方向](#org31703b8)
        1.  [可检测作恶可追责可受限回滚的共识机制](#orgc00b366)
        2.  [基于TEE的高性能区块链共识算法](#org4356eea)
        3.  [基于多种TEE的高可信共识算法](#org48c19bb)
4.  [智能合约](#org1031ee4)
    1.  [相关课题](#org8020f49)
        1.  [北京市2020年度区块链领域储备课题](#orga8f873b)
        2.  [北京市自然科学基金面上项目指南](#org1a0b99d)
    2.  [研究方向](#orgdb57803)
        1.  [提高fabric智能合约的安全性和性能](#orgf2752bc)
        2.  [基于TEE的可监管的机密智能合约](#org2500650)
5.  [隐私保护与安全监管](#org3514ff6)
    1.  [相关课题](#org4def44a)
        1.  [北京市2020年度区块链领域储备课题](#org30e3dd1)
        2.  [北京市自然科学基金面上项目指南](#org933f5c7)
    2.  [研究方向](#org85c87bc)
        1.  [真实身份可监管、且保护隐私的区块链身份标识](#orgff6371d)
        2.  [可监管的区块链匿名交易](#orgdfc7df7)
        3.  [基于可信计算协议的可监管的链上秘密分享机制](#orgbe844a0)
        4.  [基于区块链和TEE的可监管的多方安全计算平台](#org1855f54)
6.  [链上链下数据协同](#org68dcc53)
    1.  [相关课题](#org9340378)
        1.  [北京市自然科学基金面上项目指南](#orgf87ef2c)
        2.  [广东省重点领域研发计划 2020 年度“区块链与金融科技”重点专项](#org4ce08e3)
        3.  [陕西省重点研发计划项目指南-基于区块链的数据存储安全关键技术研究](#org7fec7f7)
    2.  [研究方向](#org5fb6de5)
        1.  [基于TEE的可监管的机密智能合约](#org2d3a3e3)
        2.  [基于专用存储链和全同态加密技术的高性能数据协同机制](#orgb8d3e45)
        3.  [高性能存储侧链](#org85bc86c)
7.  [可信数据上链/软硬件结合](#org56db4e5)
    1.  [相关课题](#orgda53550)
        1.  [北京市2020年度区块链领域储备课题](#org2363ab1)
        2.  [陕西省重点研发计划项目指南-基于区块链的数据链信息去中心化融合共享技术研究](#orge419e7c)
    2.  [研究方向](#orge6e59cb)
        1.  [领域特定的移动设备联盟链客户端](#orga366f10)
        2.  [全自主可控的区块链软硬件一体机](#orga243bfe)
        3.  [全自主可控的区块链移动设备客户端](#orgc6307d7)
        4.  [基于TEE的可信数据采集移动终端](#org16767a3)
8.  [区块链新型体系架构研究](#org97cecb6)
    1.  [相关课题](#orge1fc84b)
        1.  [北京市自然科学基金面上项目指南](#org2281c79)
    2.  [研究方向](#org0553890)
        1.  [提供SQL接口的高性能区块链架构](#org0ee09d1)
        2.  [面向大数据分析的高性能存储链架构](#orgfceb268)
9.  [监管](#org6ff21ce)
    1.  [相关课题](#org7f14de2)
        1.  ["以链治链"监管架构与关键技术研究](#org8aaec38)
        2.  [北京市自然科学基金面上项目指南](#orgd329b11)
        3.  [国家重点研发计划"云计算和大数据"重点专项-联盟链监管关键技术](#org3ecdd5b)
    2.  [研究方向：](#orgc42197b)
        1.  [链上数据的受限回滚机制和可信擦除证明](#org4928cec)
        2.  [基于可信计算协议的密态内容审计方法](#org4dc8bd2)
        3.  [基于秘密共享协议的匿名可追踪方法](#org1099525)
        4.  [适用于监管链的共识算法](#org9446be9)
        5.  [异构联盟链跨链监管机制](#org2c0c37b)
        6.  [可受限回滚且不可篡改的区块链架构](#org628c683)
        7.  [向监管开放的链上隐私交易技术](#orgb83d4cf)
10. [军科委项目后续](#orgf1f95d5)
    1.  [向监管开放的链上情报共享](#org3b4723b)
    2.  [基于TEE的防拜占庭攻击的共识算法](#org5e3482e)
    3.  [高性能存储测链设计以及侧链与主链的跨链数据协同](#org0844f3a)
    4.  [自主可控的可信区块链移动终端](#org0e185e6)

区块链研究课题:


<a id="org9c2c73b"></a>

# intro


<a id="org8831979"></a>

## 重视监管技术

今年的多个项目申报指南中，区块链方面最突出的特点是对监管技术的重视。有三种内容需要进行监管：联盟链参与者的真实身份；链上的交易金额，包括匿名交易；链上的密态内容审核，交易和智能合约中的密态内容；

一些研究课题的重点是设计监管链，监管方法；一些课题重点在于设计向监管开放的联盟链。

最难的挑战是设计向监管开放的各种链上隐私保护技术。比如可监管的身份匿名方案，可监管的密态内容，可受限回滚可复原的区块链架构。这些研究方向不太符合密码学研究的主流方向，密码学发展至今一直重视“可否认性”，各种主流协议基本都满足"可否认性"或者“不可操纵性”，而不是“不可否认”或者“可监管”。细节可参考：<https://nondualism.github.io/2020/08/08/why_crs/> 第一部分。
对于监管需要的研究不是密码学界研究重点，严谨程度要求不高，难度不大，大家的起点可能差不多。这算是一点好处吧。


<a id="org6a8eeb8"></a>

## 跨链技术是实现审核的基础

区块链监管技术的实现，必须依赖跨链技术。跨链技术也是各个项目申报指南中的热点问题。随着跨链技术的发展，目前的技术要求也更高。首先，需要能对各类区块链架构进行安全性分析，对不同链应用不同的跨链技术。其次，需要研究各种异构区块链的跨链，能抽出共性的特征，设计统一的跨链方案。最后，要求跨链方案不能存在单点依赖，跨链事务处理具有原子性。比如我们之前的那种依赖一个链下跨链服务器的方法不能满足要求了。


<a id="org8fa9425"></a>

## 重视数据存储/链上链下数据协同

随着区块链落地项目越来越多，可能出现了某些链数据量已经很大，或者可能出现了需要把大数据上链的场景。也有可能有些单位使用区块链的方法不对，导致存储的垃圾过多。总之最近这些课题比较重视数据存储问题，主要提法是"链上链下数据协同"或者“基于区块链的数据存储安全”。
姚前最近谈到ipfs，认为ipfs是未来重要的研究方向，可以用来解决区块链的存储瓶颈。据此猜测可能已经有些人在研究怎么把ipfs改造成适合联盟链和大数据分析场景的一种存储链。前两年我们也讨论过怎么能让ipfs符合监管要求，现在似乎是个好的推进时机。

姚前谈ipfs <https://www.tuoluocaijing.cn/article/detail-10017620.html>


<a id="orgdf22012"></a>

## 其他

其他一些一直受关注尚未解决的问题，包括共识机制、智能合约、软硬件结合。


<a id="orgf81da64"></a>

## 下文结构

分为跨链、共识、智能合约、隐私保护、链上链下数据协同、软硬件结合、新体系结构、监管。对于每个topic，先引述了相关项目指南，然后是设想的一些研究方向。从难度/可行性，实用价值，学术价值三方面分析。有些内容在各部分中重复。

最后分析军科委项目后续可考虑的研究方向。


<a id="orgaf8d6ff"></a>

# 跨链


<a id="org08497d3"></a>

## 相关课题


<a id="orga60b95d"></a>

### 中兴-区块链系统互联互通关键技术研究

合作方向和主要内容: 针对各类区块链系统，需要分析其互联互通涉及到的关键技术，并给出相应 的算法，协议和方案实现及专利。 预期成果： 能够提出通用的互联互通的协议及其实现，并申请相应的专利。


<a id="orgae716b7"></a>

### 北京市2020年度区块链领域储备课题

区块链技术支撑服务平台关键技术研发与应用，聚焦数据标识技术、跨链技术和监管技术，实现根据业务需求选择模块组件快速建链和跨链互联，降低区块链开发使用门槛，强化数据协同和监管，更好地支撑应用落地；


<a id="org31cba84"></a>

### 北京市自然科学基金面上项目指南

区块链应用技术取得了较大发展，但是在性能、安全、隐私、互操 作、监管等方面仍然存在很多技术瓶颈，亟需在新型体系架构、共 识机制、链上链下数据协同、隐私保护、安全监管、合约可信性等 方面取得突破。2020 年资助方向：

1.  区块链跨链互操作机制研究


<a id="orgcbbaaa2"></a>

### 国家重点研发计划"云计算和大数据"重点专项-"以链治链"监管架构与关键技术研究

针对区块链目前的发展趋势和面临的监管挑战，研究区块链“以链治链”监管体系架构和关键技术；研究区块链平台的安全测评方法和接入标准，以评估接入链的安全强度和准入许可；研究跨链监管体系设计，包括跨链监管的安全需求和安全机制、跨监管机构协统计数等；研究支持“以链治链”监管架构的共性关键技术，包括跨链监管技术、分布式监管机制、节点权限分级机制、智能合约自动化监管技术等；研究支持“以链治链”监管架构的核心算法，包括监管链的共识算法、密态内容审计方法、匿名可追踪方法、链上数据的受限回滚和可信擦除的证明等；研究监管链与接入链的一致性要求，包括接入链信息巡查和数据处理结果的正确性和完整性的证明等。


<a id="orgfbf1825"></a>

### 国家重点研发计划"云计算和大数据"重点专项-支持异构多链互通的新型跨链体系研究

&#x2026;&#x2026;研究安全高效的跨链数据传输与验证机制，定义跨链数据的格式规范，保证数据在区块链间的可信传递；研究跨事务处理机制，设计不存在单点依赖的跨链资产流通与合约调用协议，保证在异常情况下资产流通与合约调用的原子性；研究跨链治理机制，设计跨链体系的准入机制、权限控制、奖惩机制与监管审计方案；对跨链体系进行安全性分析，研究针对该体系的各类攻击及防范措施；在供应链金融等场景下开展试验测试。


<a id="orgfc8c5b1"></a>

## 研究方向


<a id="org25092ba"></a>

### 异构联盟链之间的高性能去中心化跨链技术

实现多种不同架构（fabric、fisco、superchain、tendermint等）的联盟链之间的互联互通。课题中重视的一种场景是，有一条监管链，监管链与各种异构链进行跨链监管。

设计一套方案不难，但没有完美的解决方案。因为首先目前单条链本身的安全性就不够。其次，跨链最重要的目标包括：事务原子性、不存在单点依赖、应对子链分叉的异常。这几个目标可能是无法同时达到的。

工程量较大。可能需要对跨链技术熟悉的程序员，几个人月的时间吧。

实用价值大，但是跨链的最终形态应该会形成一些国家规范，目前的研究只能是探索阶段，最终不一定会被采用。学术价值小。


<a id="org8c1d3ab"></a>

### 不存在单点依赖的跨链原子性事务处理机制

前一个方向的子问题。
目前对跨链技术的高标准要求。对于一些链来说可能是做不到的。对另一些链，有可能需要对链底层做较多修改。设计方案需要解决不少问题，而且可能最终不可能有满足所有目标的方案。工程实现复杂。


<a id="org6ad6ac7"></a>

### 可监管的高性能存储侧链以及存储侧链与主链的数据协同

高性能存储侧链：联盟链版的，可内容审核，改共识机制的ipfs。通过存储侧链与主链进行协同，可以降低主链的存储压力。

设计工作有一些困难，怎么把ipfs变成一个适合联盟链场景的链，需要研究。比如ipfs依赖经济激励，联盟链中是否能用经济激励？用什么共识算法？是否需要引入CA？

工程量较大，但对程序员的要求一般。

实用价值较高，未来区块链项目落地时，存储链（或存储方案）+ 业务主链 可能会成为很多项目的标配。

学术价值一般，算是一个新问题，但使用的都是存储和分布式计算领域的老技术。


<a id="orgec64278"></a>

### 密态内容跨链监管方法

密态内容跨链监管，基于可信计算协议或者TEE两种方式，都可行。设计方案需要花一些时间调研相关工作，对比各种方法。

工程实现比较难，需要对密码学方向的，或者学习能力比较强的程序员才能做。而且要改造链底层。


<a id="orgeca4325"></a>

# 共识机制


<a id="orgc5a1955"></a>

## 相关课题


<a id="org12e1803"></a>

### 北京市2020年度区块链领域储备课题

面向业务灵活适配的共识机制和算法研究，提供面向业务需求的可拔插的多共识算法模块支持，提高区块链性能；


<a id="orgf7dc6f0"></a>

### 北京市自然科学基金面上项目指南

区块链应用技术取得了较大发展，但是在性能、安全、隐私、互操 作、监管等方面仍然存在很多技术瓶颈，亟需在新型体系架构、共 识机制、链上链下数据协同、隐私保护、安全监管、合约可信性等 方面取得突破。2020 年资助方向：

1.  区块链共识机制研究


<a id="org31703b8"></a>

## 研究方向


<a id="orgc00b366"></a>

### 可检测作恶可追责可受限回滚的共识机制

在共识的安全性方面，有课题特别强调“监管链的共识算法”。可能需要考虑监管链的特征来设计一种共识机制。暂时理解为监管链的共识机制需要满足"可检测作恶"、“可追责”、“可受限回滚”几种特征。

可以通过在联盟链共识中也引入pos的机制，表达多个监管机构之间的权重的不同？也可以在TEE中做pbft，增强安全性？

需要先调研具体的需求，才能更深入思考如何设计共识机制。实用价值和研究价值一般，似乎主要是为了满足监管目标。


<a id="org4356eea"></a>

### 基于TEE的高性能区块链共识算法

raftee算法。


<a id="org48c19bb"></a>

### 基于多种TEE的高可信共识算法

解决raftee算法依赖intel sgx一种tee的弱点。难度较大，实用价值待定，研究价值较大。


<a id="org1031ee4"></a>

# 智能合约


<a id="org8020f49"></a>

## 相关课题


<a id="orga8f873b"></a>

### 北京市2020年度区块链领域储备课题

智能合约关键技术研究与应用，提升智能合约执行性能和安全性；


<a id="org1a0b99d"></a>

### 北京市自然科学基金面上项目指南

区块链应用技术取得了较大发展，但是在性能、安全、隐私、互操 作、监管等方面仍然存在很多技术瓶颈，亟需在新型体系架构、共 识机制、链上链下数据协同、隐私保护、安全监管、合约可信性等 方面取得突破。2020 年资助方向：

1.  区块链智能合约可信性研究


<a id="orgdb57803"></a>

## 研究方向


<a id="orgf2752bc"></a>

### 提高fabric智能合约的安全性和性能

百度超级链已经做了这类工作，fabric的智能合约有很多改进空间。需要熟悉fabric底层的程序员来做，工程量一般。实用价值一般，实际落地项目并不关心智能合约是否真的安全。学术价值小。


<a id="org2500650"></a>

### 基于TEE的可监管的机密智能合约

已有很多研究在做这类工作，百度超级链可能已经实现了“基于TEE的机密智能合约”这部分，但"可监管"是一个新的要求。

设计方案需要一些时间调研相关工作，选择合适的密码学方法。实现有难度，需要有密码学基础知识或者学习能力强的程序员。工程量约几个人月。

实用价值一般，未来可能有前途，但目前业界对隐私保护需求不大，动力不足。而这个研究在解决保护隐私的同时要求向监管开放，应用场景目前可能很有限。学术价值小。


<a id="org3514ff6"></a>

# 隐私保护与安全监管


<a id="org4def44a"></a>

## 相关课题


<a id="org30e3dd1"></a>

### 北京市2020年度区块链领域储备课题

区块链安全与隐私保护关键技术和工具研发，提高区块链身份和数据的安全性和隐私保护水平；


<a id="org933f5c7"></a>

### 北京市自然科学基金面上项目指南

区块链应用技术取得了较大发展，但是在性能、安全、隐私、互操 作、监管等方面仍然存在很多技术瓶颈，亟需在新型体系架构、共 识机制、链上链下数据协同、隐私保护、安全监管、合约可信性等 方面取得突破。2020 年资助方向：

1.  区块链安全与隐私保护研究
2.  区块链安全监管研究


<a id="org85c87bc"></a>

## 研究方向


<a id="orgff6371d"></a>

### 真实身份可监管、且保护隐私的区块链身份标识

我们之前的DID，以及目前其他DID技术难落地的一个重要原因是，没有把公钥与真实的身份证ID对应。我们之前一些调研报告中设想过一个方案，用户加入联盟链时，可以要求他提交kyc材料，我们的验证服务调用第三方的KYC验证，生成一个zkp技术保护的公民身份证明文件。然后他凭借该zkp证明文件才能参与到联盟链上。

这种方案可以满足监管要求的可追溯、可审核、保护用户隐私等要求。工程量较大，需要做一些验证服务，需要对链底层做较大改造。

实用价值较大。但是未来可能会有国家的数字身份证，也可能这类项目由其他单位来做。我们实现的方案是否能有很多落地机会不一定。研究价值小，有一篇这个思路的国外论文。


<a id="orgdfc7df7"></a>

### 可监管的区块链匿名交易

在匿名交易技术的基础上，满足可监管的需求。可以基于门限签名技术，或者TEE技术。需要改动底层链，工程难度较大。

实用价值前景看好，未来对于联盟链上的匿名交易，监管要求肯定会个更高。联盟链与公链上的匿名交易使用的技术方案会有很大不同。研究价值小，“可监管”不是密码学研究的主流。


<a id="orgbe844a0"></a>

### 基于可信计算协议的可监管的链上秘密分享机制

未来对区块链的监管可能更严格，如果上链数据被检测到是密文，那么必须同时提供一份证据文件。该证据文件证明了原始数据通过了一个“内容审查程序”的审查，不包含违法内容。

实用价值较大，未来联盟链的监管会更严格，这种技术可能会有很多的应用。研究价值小，“内容审核”不是密码学主流研究关注的。


<a id="org1855f54"></a>

### 基于区块链和TEE的可监管的多方安全计算平台

某些项目指南中提到了对多方安全计算也要进行审核，是一个新的更高的要求。

实用价值前景看好，未来国家对隐私保护要求更高，可能会要求进行安全多方计算的各方接受审核，那么该技术有价值。


<a id="org68dcc53"></a>

# 链上链下数据协同


<a id="org9340378"></a>

## 相关课题


<a id="orgf87ef2c"></a>

### 北京市自然科学基金面上项目指南

区块链应用技术取得了较大发展，但是在性能、安全、隐私、互操 作、监管等方面仍然存在很多技术瓶颈，亟需在新型体系架构、共 识机制、链上链下数据协同、隐私保护、安全监管、合约可信性等 方面取得突破。


<a id="org4ce08e3"></a>

### 广东省重点领域研发计划 2020 年度“区块链与金融科技”重点专项

区块链隐私安全与链上链下数据协同技术研究

研究基于可信硬件或可信执行环境下的数据 存储计算技术，达成链上链下数据的高效协同；


<a id="org7fec7f7"></a>

### 陕西省重点研发计划项目指南-基于区块链的数据存储安全关键技术研究

研究内容：针对大数据环境下海量敏感数据集中存储带来 的数据监管薄弱、用户隐私泄露等问题，构建基于区块链的去 中心化敏感数据管理平台，解决数据存储过程中的单点失效及权力集中问题，实现数据存储的安全性；研究基于区块链的轻 量级数据加密技术和敏感海量数据挖掘机制，解决数据管理过 程中的成本及安全问题，实现密态数据的可搜索、可溯源、可 审计以及可控制；研究具有激励机制的分布式文件存储系统， 提出支持非结构化的数据安全共享机制，实现链上密态数据共 享的公平性和高效性。


<a id="org5fb6de5"></a>

## 研究方向


<a id="org2d3a3e3"></a>

### 基于TEE的可监管的机密智能合约

重复部分。该方案既是保护隐私的技术，也是解决存储量过大的技术。


<a id="orgb8d3e45"></a>

### 基于专用存储链和全同态加密技术的高性能数据协同机制

纯密码学方案。用户把原始数据使用全同态加密技术加密后，上传到存储链上，再基于主链与其他用户共享或交易数据。

难度一般。改造ipfs实现存储链，同态加密技术相对简单一些。

实用价值较大。研究价值小。


<a id="org85bc86c"></a>

### 高性能存储侧链

重复部分。既与跨链有关，又与数据协同有关。


<a id="org56db4e5"></a>

# 可信数据上链/软硬件结合


<a id="orgda53550"></a>

## 相关课题


<a id="org2363ab1"></a>

### 北京市2020年度区块链领域储备课题

区块链软硬件结合关键技术研究，提升源头上链数据的安全性和真实性；


<a id="orge419e7c"></a>

### 陕西省重点研发计划项目指南-基于区块链的数据链信息去中心化融合共享技术研究

针对数据链技术应用发展中面临的信息去中心 化安全流转、实时可信共享等需求，研究基于区块链的去中心 化数据链信息安全流转和融合共享技术问题，重点突破基于区 块链技术的多平台协作共识机制、数据链态势分布式形成与安 全共享策略、多层级数据链态势信息分布式融合处理模型等关 键技术，搭建动态可信的去中心化数据链信息共享服务平台， 并结合无人集群智能协同数据链态势信息共享、网络协同智能 制造物联网等场景完成等效示范验证。


<a id="orge6e59cb"></a>

## 研究方向


<a id="orga366f10"></a>

### 领域特定的移动设备联盟链客户端

对于特定领域的应用，需要定制的区块链移动设备客户端。比如溯源应用中，各环节的参与人员，需要使用移动设备对某些数据签名上链。

工程难度一般。定制一个fabric客户端，移植到移动设备上。


<a id="orga243bfe"></a>

### 全自主可控的区块链软硬件一体机

可能是各家正在进行或者已经完成的研究课题。此处只是列出来作对比。


<a id="orgc6307d7"></a>

### 全自主可控的区块链移动设备客户端

移动智能设备，能否全自主可控？基于华为的自主可控的移动芯片和设备？

工程难度一般。实用价值较大，未来可信数据上链需要这样的联盟链移动终端设备，可能成为一些落地项目标配。


<a id="org16767a3"></a>

### 基于TEE的可信数据采集移动终端

真正的实现源头上链数据的安全性和真实性。

实用价值大，应该是区块链技术的最终形态。研究价值大。

工程难度大，目前缺少一些关键芯片。或者需要把几个芯片集成到一起，有难度。


<a id="org97cecb6"></a>

# 区块链新型体系架构研究


<a id="orge1fc84b"></a>

## 相关课题


<a id="org2281c79"></a>

### 北京市自然科学基金面上项目指南

区块链应用技术取得了较大发展，但是在性能、安全、隐私、互操 作、监管等方面仍然存在很多技术瓶颈，亟需在新型体系架构、共 识机制、链上链下数据协同、隐私保护、安全监管、合约可信性等 方面取得突破。2020 年资助方向：

1.  区块链新型体系架构研究


<a id="org0553890"></a>

## 研究方向


<a id="org0ee09d1"></a>

### 提供SQL接口的高性能区块链架构

LedgerDB，目前可能有些过时了。实用价值一般。研究价值小。


<a id="orgfceb268"></a>

### 面向大数据分析的高性能存储链架构

基于ipfs被改造成适用于联盟链场景的存储链的前提，同时改进它的使用接口。提供面向大数据分析的接口，研究能否提供兼容HFS的接口，直接被hadoop，spark等大数据分析框架调用，这样就打通了区块链和大数据。

实用价值较大。难度较大，不需要学习密码学知识，需要较强的系统软件知识。工程量较大，可能需要十个人月左右吧。研究价值一般。

存储量与跨链、链上链下数据协同有关，再考虑面向大数据分析的接口，算是一种新型体系结构吧。


<a id="org6ff21ce"></a>

# 监管


<a id="org7f14de2"></a>

## 相关课题


<a id="org8aaec38"></a>

### "以链治链"监管架构与关键技术研究

针对区块链目前的发展趋势和面临的监管挑战，研究区块链“以链治链”监管体系架构和关键技术；研究区块链平台的安全测评方法和接入标准，以评估接入链的安全强度和准入许可；研究跨链监管体系设计，包括跨链监管的安全需求和安全机制、跨监管机构协统计数等；研究支持“以链治链”监管架构的共性关键技术，包括跨链监管技术、分布式监管机制、节点权限分级机制、智能合约自动化监管技术等；研究支持“以链治链”监管架构的核心算法，包括监管链的共识算法、密态内容审计方法、匿名可追踪方法、链上数据的受限回滚和可信擦除的证明等；研究监管链与接入链的一致性要求，包括接入链信息巡查和数据处理结果的正确性和完整性的证明等。


<a id="orgd329b11"></a>

### 北京市自然科学基金面上项目指南

区块链应用技术取得了较大发展，但是在性能、安全、隐私、互操 作、监管等方面仍然存在很多技术瓶颈，亟需在新型体系架构、共 识机制、链上链下数据协同、隐私保护、安全监管、合约可信性等 方面取得突破。2020 年资助方向：

1.  区块链安全监管研究


<a id="org3ecdd5b"></a>

### 国家重点研发计划"云计算和大数据"重点专项-联盟链监管关键技术

面向联盟链的监管需求，以安全多方计算、零知识证明和跨链技术为基础，以隐私保护为前提，研究面向联盟链的分布式、穿透式全维度监管技术体系架构；研究智能合约的数据痕迹追踪技术，实现智能合约数据与区块链交易关联关系分析，实现智能合约内容的安全验证；研究基于多方门限签名的分布式链上监管决策体系，实现对链上违法违规信息的取证、认定与处理；研究多方隐私交易技术，实现对监管方友好并兼顾隐私保护的区块链账本交易技术；研究新型区块结构，实现异构联盟链自适应监管技术，根据不同的区块结构，自适应调整数据监测与数据屏蔽算法策略；研究新型区块结构，在区块内容不被篡改、可追溯、可复原的前提下，实现关键信息的智能屏蔽。


<a id="orgc42197b"></a>

## 研究方向：


<a id="org4928cec"></a>

### 链上数据的受限回滚机制和可信擦除证明

虽然违反区块链技术的原意，但不是不能做。受限回滚机制可以通过密码学协议或者TEE的方法。可信擦除肯定需要依赖某种硬件技术。

设计一套方案难度一般。工程难度较大，对链底层的改造较大，还需要依赖硬件技术。研究价值小，不是区块链主流的研究方向。

实用价值一般。主要是为了符合监管的要求。


<a id="org4dc8bd2"></a>

### 基于可信计算协议的密态内容审计方法

重复部分。

可以通过协议或者TEE的方式来做，难度较大，对链底层改动较大。

研究价值小.

实用价值一般，主要为了符合监管要求。


<a id="org1099525"></a>

### 基于秘密共享协议的匿名可追踪方法

重复内容。


<a id="org9446be9"></a>

### 适用于监管链的共识算法

重复内容。


<a id="org2c0c37b"></a>

### 异构联盟链跨链监管机制

重复内容。


<a id="org628c683"></a>

### 可受限回滚且不可篡改的区块链架构

重点是探索如何让一个“可回滚”的链同时还是“不可篡改”的。

需要设计一套方案，并进行理论分析。可能需要对一些概念进行更细的定义，论证其不矛盾。

设计方案难度一般。工程难度一般，对链底层熟悉的程序员几个月能完成。


<a id="orgb83d4cf"></a>

### 向监管开放的链上隐私交易技术

重复内容。


<a id="orgf1f95d5"></a>

# 军科委项目后续

综合上述分析，以下题目是难度可接受的研究方向


<a id="org3b4723b"></a>

## 向监管开放的链上情报共享

与军事应用结合较紧密

符合当前的研究热点

与之前课题联系性一般，能勉强连上。


<a id="org5e3482e"></a>

## 基于TEE的防拜占庭攻击的共识算法

与之前课题连续性强

raftee就能用


<a id="org0844f3a"></a>

## 高性能存储测链设计以及侧链与主链的跨链数据协同

与之前课题连续性强

史老师关注存储


<a id="org0e185e6"></a>

## 自主可控的可信区块链移动终端

与之前课题连续性一般

不需要集成TEE芯片

在自主可控的国产设备上实现fabric客户端即可
