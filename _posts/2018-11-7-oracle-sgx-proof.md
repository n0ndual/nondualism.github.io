---
layout: post
title:  "oracle-sgx生成证据文件的格式和验证算法"
date:   2018-11-06 16:20:01
categories: thoughts
tags: oracle SGX wolfssl
---

* content
{:toc}

---

## 需求分析
 设计proof的验证步骤时要考虑两种应用场景：oracle服务使用者需要随时随地使用开源验证工具来验证proof，公链上的合约以尽可能的gas花销验证proof。

在公链上的验证算法需要满足四个要求：占用存储最小、计算代价最小、对第三方库依赖最少、安全可信。但第三方验证工具对文件大小和计算开销的要求不高。

## 难点：

### wolfssl
如果只使用wolfssl，那么依赖的第三方代码就是最少的。但是wolfssl的文档不全（免费GPL协议版），有一个关键方法（验证certificate chain）没有找到示例代码。

### openssl
使用openssl命令行工具的话，文档齐全，比较简单。但需要用c调用openssl命令行，效率有问题。如果用openssl c library的话，需要读很多代码，文档全但不友好。

### solidity的密码学函数库
solidity上也没有如“验证certificate chain”之类的高层方法。solidity上有一些第三方提供的“rsa验签”的方法，但据说花销已经很大。复用这些方法或许可以实现“验证certificate chain”的方法。但开发成本很高，而且gas花费也会很高。

## 解决方案:

### 生成两种类型的证据文件，精简版和完整版。
主要区别是：精简版不用验证certificate chain，把public key硬编码在验证算法中；完整版先验证certificate chain，然后从certificate chain中抽取出 public key。其他步骤都一样。

精简版用于发给公链上的合约验证，也可以用于做性能测试时获得比较好的性能。完整版用于第三方验证工具验证。普通用户啊，一般只使用精简版即可。

## 验证步骤
1、（Optional）verify cert chain，extract Report Public Key

2、verify IAS Report Signature using Report Key which is hardcoded or extracted by step1, extract Enclave Quote Body.

3、Decode base64-encoded Enclave Quote Body, extract the MRENCLAVE and HTTPS_DATA_HASH

4、check if the extracted MRENCLAVE is the same as the one hardcoded

5、check if the hash of the concatenation of Https Packages and Nounce equals to HTTPS_DATA_HASH

## proof 文件示例
```
------Https Request------
GET / HTTP/1.1
Host: www.github.com

------Https Response------
HTTP/1.1 200 OK
content-length: 0
request-id: 070d03189eaf45eb84b45e116841dad3
date: Wed, 07 Nov 2018 10:01:55 GMT
Connection: keep-alive


------Nounce------
2018-11-07-35897aeh2679831nf3
------Intel SGX Quote-----
AgABAOkTAAAHAAYAAAAAABw/ZWgOGQoiU8OfH2j4cyUAAAAAAAAAAAAAAAAAAAAABQUCBP8CAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABwAAAAAAAAAHAAAAAAAAAGOQ/NULusHORR/ZoVu8BTqIaX5sRdEBokihNakh7DFfAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACD1xnnferKFHD2uvYqTXdDA8iZ22kCD5xw7h38CMfOngAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAr8+9BjvuHGCbteXlrVokj8hYhi4tt/zxNp+9XsljubrKJtpQxvkNCDz57V0+25d3AK5Evaeu0ONE6c8yGOSSaqAIAALSjaQQsG38IAsW6TwN8whyvCNdPEAmiz3NnCg50E3Bb5kxj62LwB9eOyBSy4PSOjqd0+28SDyGb2Xd4fkW6lkHKMSNZOakuPQUKSagDI/N5oj719vvwW+oWIqaMQCuJH817WQTZy3x6akNNF0Zzc+cSxGYf38dccn/iaauN2wK9l2jtb3BmhPlW6kFFTdRrfxSTX6nhKyN9g10B3jO8vLx6QBFI6C4gxXfN8BhjelrN8VS1GRMLNqd0NZSOgJED+eDpdKuo5OP/mO1hWGMyV7siyvyxsCQyXAUTKLGrUfHI7ODWguLwEiU1SkmcInjX01zRUMTEDCjGxQJzfjfnzXdNVJpDdIYwuWpSmcnwfES2ftAM38u1vtVU/OEXXJIKbR42yeOgvogvKNaklWgBAADLL/u4rB7IBkRem+caV456NprBJrbVdrrYE/Tjc8p66aSAHPjZt2MyAhQ99toJRHhqEI/wTDJNp/EBOiX+CRpww2cG2J9nssJDkVyTCmF1nuOokTeEaZnf966YBVgWkbo85fOMthoIZozym5WADr4Q/QilZhcCkxe/IHtxQnj1EDisw94xaespTzGfb4QRwwsfC0CLbNC1AxUVeyUNtWiiBRI9TNOrSJUCgANBI6LwIK+IagLJJB0VsIgdjjYfvqX0f+wX8Xzsigl4wtdIDwRgpK6BRydc7oVzNmCfRhbb3M0pjWc++d+OMDH6x39v6ZCdab3KyFNoBSr2o6gldVUhmURrHE6ky3U1rZgbbA+FZwCV7LZsA5ycyZLpJ1VXodBbOBZ9j9dyWVGnahiyrRaM7oBkSGcXhytK3AL1bN/LNq3gBeqHdXrhS2HNtO12Cdi+JUULgvX81EqPs2HYhnDACM3IGpgKbPaqZ/cHoHTAAY+nVOUTJEHp
------Intel Attestation Service Report------
{"id":"1833330639229979318840324020560579123","timestamp":"2018-11-07T10:01:56.918946","version":3,"epidPseudonym":"Qm4bxt6GLIS4Jt6NdaXIFapJ9a/k1BuaypZRW/9A42tBzma0/3VxuH1EY4L19PaKM4Y+CwGVYEEY74U96gnO5D2Vmn66LdI5e8WjcGlicS96WlaQArr8PxTuot/OPhDDhIxsNleCU+0mAd2zcWK4zdfVI2HW6ljI4VvbggeakJc=","isvEnclaveQuoteStatus":"CONFIGURATION_NEEDED","platformInfoBlob":"15020065000008000005050204010100000000000000000000070000060000000200000000000013E9CCFBFB1E9B4BFB3CCA7C8659B7BE9D484E1D1935B4C384434144752149B78A2403FDA3EB15EC10EAFA9BA44D5C4DAC804D9A9BFDF2F9425A2D253FBA1C1A0CE3","isvEnclaveQuoteBody":"AgABAOkTAAAHAAYAAAAAABw/ZWgOGQoiU8OfH2j4cyUAAAAAAAAAAAAAAAAAAAAABQUCBP8CAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABwAAAAAAAAAHAAAAAAAAAGOQ/NULusHORR/ZoVu8BTqIaX5sRdEBokihNakh7DFfAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACD1xnnferKFHD2uvYqTXdDA8iZ22kCD5xw7h38CMfOngAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAr8+9BjvuHGCbteXlrVokj8hYhi4tt/zxNp+9XsljubrKJtpQxvkNCDz57V0+25d3AK5Evaeu0ONE6c8yGOSSa"}
------Intel Attestation Service Report Public Key------
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAqXot4OZuphR8nudFrAFi
aGxxkgma/Es/BA+tbeCTUR106AL1ENcWA4FX3K+E9BBL0/7X5rj5nIgX/R/1ubhk
KWw9gfqPG3KeAtIdcv/uTO1yXv50vqaPvE1CRChvzdS/ZEBqQ5oVvLTPZ3VEicQj
lytKgN9cLnxbwtuvLUK7eyRPfJW/ksddOzP8VBBniolYnRCD2jrMRZ8nBM2ZWYwn
XnwYeOAHV+W9tOhAImwRwKF/95yAsVwd21ryHMJBcGH70qLagZ7Ttyt++qO/6+KA
XJuKwZqjRlEtSEz8gZQeFfVYgcwSfo96oSMAzVr7V0L6HSDLRnpb6xxmbPdqNol4
tQIDAQAB
------Intel Attestation Service Report Signature------
fhUymoHzMnsjXuyQm1gVpfbvz78Q4QSUgrIn+lbrJMEdm0vgEAM/+NV+jaq01KQJ+z9AnRkIwlBf8IQc07XhDPQs6oRwJYIslgqr65YiCmY7pZF61LTah2IjSjigwjjYKFHajT4Mhul9/J+Glkrni0C4/nCeRcDTb5evbhHGw6GVgBGB46+Zfwcw02sudnUFX1KQjrgMU2IjmzEuvO9Q0uAtuxYVyfhsw6CLK/ph+9FB537QoaMl/p9f8T1DyKW72zKq1KBe1mYPQvZtZg4Q81JHSt9aL6S8HaxXfn7C7ACkpUAVxo+884Wo15SlQKsbKvlpl7iykkdf54XydnAlRA==
```
