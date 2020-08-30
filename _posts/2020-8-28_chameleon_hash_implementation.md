---
layout: post
title:  "chameleon hash的实现"
date:   2020-08-28 12:20:01
categories: thoughts
tags: chameleon hash redactable blockchain
---

* content
{:toc}

---
# Table of Contents

1.  [research timeline](#org34f1460)
    1.  [Chameleon hashing and signatures](#org475d940)
    2.  [Chameleon Hashing without Key Exposure](#orgbba0b2e)
    3.  [On the Key Exposure Problem in Chameleon Hashes](#org070bd2b)
    4.  [Identity-based chameleon hashing and signatures without key exposure](#orge1e5b85)
    5.  [Sanitizable Signatures](#org9e0ef99)
    6.  [Redactable Blockchain – or Rewriting History in Bitcoin and Friends](#orgb289c96)
2.  [可行算法总结：](#org6670049)
3.  [我们的实现方案：](#org74ceb64)
    1.  [实现过程：](#orga087051)

chameleon hash 的实现


<a id="org34f1460"></a>

# research timeline


<a id="org475d940"></a>

## Chameleon hashing and signatures

Krawczyk, Hugo, and Tal Rabin. "Chameleon hashing and signatures." (1998).

提出一种新hash和签名算法，不允许签名者伪造，允许接收者伪造，而且允许签名者否认自己的签名。论文主要目标是保护签名者，使他的消息的authenticity除了接收者之外，没有人可以知道。

首先，签名者计算的hash和签名只对特定的一个接收者有效。该接收者不能向第三方证明：某个签名者向自己发了某条消息。因为该接收者掌握着hash算法的trapdoor，可以伪造一个假的hash。

更重要的是，如果接收者伪造出一个假消息，签名者可以伪造出另一个假消息。这一点难理解，但很重要，这里详细说明。

签名者S的原始消息和hash是(m,r,h)，拥有trapdoor的接收者R可以伪造出(m', r', h)。此时R拿着(m',r',h)声称是S发给自己的，论文中假设的法官需要判定真假。而S此时可以拿出原版的(m,r, h)向法官证明，(m',r', h)是伪造的，但是这就等于S暴露了自己的真实消息。在这种情况下，如果S想自证清白，就必须暴露自己的原始消息。那么其他人就知道S的原始消息了。

因此论文中的方法，可以使S基于(m,r, h)和(m',r', h')伪造出另一个消息(m'',r'', h)。这样S拿出来的证据是另一个伪造的假消息，就不需要暴露自己的真实消息了。在该论文中这不算是个问题。算是签名者和接受者之间的一种互相约束。如果接受者伪造信息，那么签名者就获得了私钥，可以继续伪造信息。

但是在redactable blockchain应用中，意味着原始区块b 和 修订区块链b'都出现后，原始区块b的发送者就发送新的修订区块b''。新的b''对于其他节点看来，都是合法的。

而且该方法又导致了另一个问题，发送者可以通过(m, r, h)和(m', r', h')重构出接受者的trapdoor信息。接受者的私钥就暴露了。在区块链场景中，相当于原始区块b的发送者就拥有了trapdoor信息，可以修改未来的所有区块。

因此原版论文的方法有两个缺陷，是不能用的。


<a id="orgbba0b2e"></a>

## Chameleon Hashing without Key Exposure

Chen, Xiaofeng, Fangguo Zhang, and Kwangjo Kim. "Chameleon hashing without key exposure." International Conference on Information Security. Springer, Berlin, Heidelberg, 2004.

西安电子科技大学的陈晓峰教授挖了一个好坑，该论文应用很多。他指出了chameleon hash的trapdoor私钥暴露的问题，并且提出了一种新的方法，使得trapdoor不会暴露。

但是同样地，如果接收者伪造出一个假消息，签名者就可以继续伪造消息。同样地，在不关注应用的密码学研究中，这个可能不算是问题，反而算是优势。


<a id="org070bd2b"></a>

## On the Key Exposure Problem in Chameleon Hashes

Ateniese, Giuseppe, and Breno de Medeiros. "On the key exposure problem in chameleon hashes." International Conference on Security in Communication Networks. Springer, Berlin, Heidelberg, 2004.

Ateniese首先把之前的这两个工作做了理论分析，清晰定义了chameleon hash的两个属性。如果前文感觉比较难以理解(我也是开始没有完全理解)，从Ateniese的论文可以更清楚地理解。

Message Hiding: 如果接收者伪造一个消息m', 签名者者可以继续伪造m''，目的是保护签名者的消息不被泄漏。

Key Exposure Freeness: 如果原始信息m 和接收者伪造的消息m'都被公开，trapdoor信息，也就是接收者的私钥依然是安全的。

Ateniese分析了陈晓峰的论文同时满足上述两个属性，并且给出了几个新的同时满足上述两个属性的算法，增加了该类算法的种类。

而且Ateniese给出了一种奇特的只满足Key exposure Freeness，不满足 Message Hiding的算法。虽然在该论文中没有讲该算法有啥用，但在后续论文中，他使用了该算法。其实不满足message hiding，只满足key exposure freeness的算法正是在对原签名审核修订场景中需要的。

Ateniese还挖了一个坑，在identity-based的系统中是否有同时满足上述两个属性的算法？


<a id="orge1e5b85"></a>

## Identity-based chameleon hashing and signatures without key exposure

陈晓峰填了上述Ateniese挖的坑。

Identity-based system 不是目前主流的方式，不考虑了。


<a id="org9e0ef99"></a>

## Sanitizable Signatures

Ateniese, Giuseppe, et al. "Sanitizable signatures." European Symposium on Research in Computer Security. Springer, Berlin, Heidelberg, 2005.

这篇论文似乎显示出了Ateniese的一系列研究的目的。“可消毒/可净化签名”允许授权机构来受限修改一条签名消息。

该篇论文介绍了大量的应用场景，其最终方案是基于上述的只满足key exposure freeness，不满足Message Hiding的Chameleon Hash 算法。

因为在受限修改签名消息的场景中，原始消息m和修订消息m'都是合法的，但是不希望其他人能伪造出新的m''。

理论上，该方法在可修订区块链方面就可以使用了。


<a id="orgb289c96"></a>

## Redactable Blockchain – or Rewriting History in Bitcoin and Friends

第一篇"redactable blockchain"的论文也是Ateniese提出的。

这篇论文有一些让人迷惑，论文中有些观点似乎矛盾。首先他指出自己之前论文的chemeleon hash方法有缺陷，甚至not useful在这个场景中。但是他们在实现的原型中用的还是原来的方法。而且他提出了一些新的定义和新的方法，但没有实际使用。

Some of these constructions, e.g. the ones in [AdM04, CZK04, CTZD10, CZS + 10], do not suﬀer from the key exposure problem, as they satisfy the property that it should be unfeasible to ﬁnd collisions for a “fresh” label λ ∗ , even given access to an oracle that outputs collisions for arbitrary other labels λ = ̸ λ ∗ . 2 However, labeled chameleon hash functions are not useful for constructing online/oﬄine signatures and for the type of application considered in this paper.

To the best of our knowledge, the only construction of a chameleon hash function satisfying enhanced collision resistance is due to [AdM04]; the construction is ad-hoc and relies on the Nyberg-Rueppel signature scheme [NR94] (whose security can be shown under the Discrete Logarithm assumption in the generic group model [Sho97]).

Improved chameleon hash design (cf. Section 4). Traditional chameleon hashes have the key exposure problem as observed in [AdM04], except for the scheme proposed in [AdM04], but which relies on the generic group model. It was left as an open problem to ﬁnd similarly enhanced chameleon hashes in the standard model. We ﬁrst generalize the deﬁnition of chameleon hash to make it more relevant in practice and then provide new constructions in the standard model through a generic transformation.

For the sake of concreteness and practicality, we chose to work with the (public-coin) chameleon hash function introduced by Ateniese and de Medeiros [AdM04]; this construction satisﬁes enhanced collision resistance (cf. Deﬁnition 4) in the generic group model, based on the Discrete Logarithm assumption.

是否可以这样理解：这篇论文既研究了redactable blockchain应用，又在密码学算法方面有创新。虽然这个创新没有被应用在论文中的blockchain场景。

改论文提出的新的chemeleon hash 算法非常复杂，中间一个步骤需要零知识证明技术。新算法的证明过程非常复杂，使用game hopping 技术证明。新算法估计在实现方面也很难，论文没有提及实现。

作者自己原论文中的算法是否真的不适用，目前我还无法判断。但既然作者自己就基于他原论文中的方法实现，我们也可以用吧。

总之，这篇论文是读的这些论文中最不清晰的。


<a id="org6670049"></a>

# 可行算法总结：

只有两个可用算法，都是Ateniese提出的，一个是在《Chameleon Hashing without Key Exposure》中，一个是在《Redactable Blockchain》中提出。

《Chameleon Hashing without Key Exposure》中的算法有两个特点：不满足Message hiding 属性，满足key exposure freeness属性。该算法基于通用群模型假设，或者说离散对数难解假设，DL假设。

《Redactable Blockchain》中的新算法也满足上述两个特点，但作者给提了个新名字enhanced collision resistance属性/强防碰撞属性。该算法基于标准模型。

为什么要费力设计一种基于标准模型的非常复杂的算法？猜测：离散对数难解假设/DL假设，在量子计算下不成立？被广泛应用的密码学研究成果都是基于标准模型的？


<a id="org74ceb64"></a>

# 我们的实现方案：

李明磊可以先用github上的chemeleon hash库，基于1998年种子论文的算法。但该算法是不适合修订签名消息这个场景的。

我尝试实现《Chameleon Hashing without Key Exposure》论文中的算法，也就是《Redactable Blockchain》论文中实际用的算法。

该算法有专利，还在专利保护期，20年保护期的话，2024年到期。目前似乎没有开源的实现，我们实现一个，也是对区块链社区的重要贡献。

<a id="orga087051"></a>

## 实现过程：

一个密码学专家对程序员的忠告是，不要自己尝试实现密码学算法，用成熟的库函数。但是该算法的主要组件，都能从开源库，比如openssl中找到，只需要抓取一些函数修改、组合。所以我觉得能搞。

to-do

