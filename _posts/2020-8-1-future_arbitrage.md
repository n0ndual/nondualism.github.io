---
layout: post
title:  “Bitmex CEO套利策略学习"
date:   2020-08-02 12:20:01
categories: thoughts
tags: Bitmex bybit arbitrage BTC
---

* content
{:toc}

---

# Table of Contents

1.  [交易所是否应该鼓励套利？](#orgaac35b2)
2.  [国内交易所为什么不适合套利？](#orgd0e8aa0)
3.  [为什么BTC和USD之间有利率差？](#org25ba35b)
4.  [为什么买多比买空的人多？](#org5fcd5c4)
5.  [收益率曲线套利](#orgc208b0d)
6.  [为什么银行不从事数字货币交易？](#orge245b4f)
7.  [数字货币市场套利策略的盈利上限？](#orgc9b5fc6)
8.  [价差套利，spread trading](#orgf643d36)


<a id="orgaac35b2"></a>

# 交易所是否应该鼓励套利？

bitmex的CEO总是发博文，举办线下活动教授套利方法。<https://blog.bitmex.com/bitmex-arbitrage-lesson-1-webinar/>。 以下是他博客和视频中的观点。

期货交易所首先需要为交易者提供用于对冲风险的掉期期货。<https://blog.bitmex.com/bitmex-bitcoin-hedging-futures-reborn/>

套利者给交易所提供了流动性和深度。尤其在交易所的开始阶段，套利者可以很快地帮助交易所增大流动性和深度。

交易所的API设计需要考虑对套利者友好，吸引套利者。

以下是个人理解。对冲交易者使用期货对冲现货的风险，这是期货存在的价值。贪婪的韭菜希望用期货放大自己的杠杆。主要的用户是这两种。对于交易所来说，开始时流动性和深度可能不够，吸引不到这两种人，因为对手盘不够。如果对套利者非常友好的话，套利者会带来流动性，吸引更多前两种用户。更多的用户又会带来更多的套利者，交易所就发展起来了。

期货交易所吸引套利者，主要有两种方法：提供对套利者友好的API；对提供流动性的套利者提供负佣金。

如果套利者提供的流动性还不足够前两种，交易所自己可能要自己下场，做一些类似搬砖套利之类色事情，为市场提供流动性。

成功案例：

Bitmex 第一个，目前最大的期货交易所，专业套利者的选择。

Bybit，初期产品和各种参数都照抄Bitmex，算法有进一步优化。比Bitmex更稳定，自2018.11.14上线以来，从来没有过停机维护，号称永不停机。

目前对于套利者来说，可能只有这两家交易所可靠稳定。如果有其他可靠的交易所C，D，E&#x2026;，套利者自然愿意把一部分资金分散到这些交易所中。从这一点来看，交易所的生存空间还很大。真正地把基础技术设施做好，套利者会来。有了良好的流动性和低手续费，韭菜也会来。

预计未来还会有更多可靠的交易所出现，数字货币套利策略的未来可能还没开始。


<a id="orgd0e8aa0"></a>

# 国内交易所为什么不适合套利？

目前国内的几个交易所对套利都很不友好。是因为国内的交易所似乎意识不到套利者对生态的重要性？

国内的交易所只知道割韭菜，手续费设置的高。对提供流动性的套利者，不提供负佣金。如此，流动性更差，韭菜更不来。

国内交易所可能会想要操纵自家交易所价格，短期挣一波快钱，即使代价是伤害所有交易者，伤害信誉和长期利益。如果交易所中存在大量的套利者，而交易所操纵价格的难度会增加。如果全部套利者的实力强于交易所，交易所无法操纵价格。如果交易所的能力强于套利者，所有套利者遭受亏损，可能会远离该交易所。

国内的交易所要么完全不能信任，要么故意挤压套利空间，利润基本都下降一半左右。之前设想的通过把资金分散到N个交易所，以分散"交易所违约风险"的想法比较难实现。


<a id="org25ba35b"></a>

# 为什么BTC和USD之间有利率差？

btc抗通胀，usd会持续通胀贬值。

btc的潜力比usd高。

因此btc 每天利率0.03%，usd每天利率0.06%


<a id="org5fcd5c4"></a>

# 为什么买多比买空的人多？

做多的盈利上限是无穷大，做空的盈利上限是一倍。


<a id="orgc208b0d"></a>

# 收益率曲线套利

<https://blog.bitmex.com/basic-basis-trading-strategies/>

目前的套利策略属于收益率曲线套利。bitmex CEO博文中的最后一种，就是这种。


<a id="orge245b4f"></a>

# 为什么银行不从事数字货币交易？

<https://blog.bitmex.com/here-come-the-bankers/>

Trading Bitcoin requires a trading desk to have accounts on the leading Bitcoin exchanges. Exchanges, as we know, get hacked repeatedly. Insurance in the Bitcoin space, for good reason, does not exist. The desk needs to assign a probability of default on the exchange.

其中一个重要原因是，交易所违约风险，文章中黑bitfinex交易所的违约风险为35%。


<a id="orgc9b5fc6"></a>

# 数字货币市场套利策略的盈利上限？

<https://blog.bitmex.com/here-come-the-bankers/>

A 17.70% annual return is very achievable. I routinely speak about arbitrage opportunities that yield in excess of 50% per annum. However, you cannot put $65 million into any trades I describe without tremendous market impact.

bitmex ceo认为套利策略50%年收益是可实现的。但是这些策略能容纳的资金量是有限的。


<a id="orgf643d36"></a>

# 价差套利，spread trading

<https://blog.bitmex.com/bitmex-vs-cme-futures-guide/>

博文中说spread trading 是一种非常重要的套利策略。如果套利者能把细节都搞清楚，盈利空间很大。

博文中分析，芝加哥交易所CME和Bitmex之间的价差套利空间很大。



