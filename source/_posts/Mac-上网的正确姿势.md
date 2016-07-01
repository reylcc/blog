---
title: Mac 上网的正确姿势
date: 2016-06-24 16:57:38
categories:
- SS
tags:
- SS
- Proxifier
---

我朝的网络环境不怎么乐观。作为程序员，怎么能忍受 Google 无法使用，怎么能忍受 Stack Overflow 的扯淡速度，怎么能忍受 Github 上每次拉取项目那 10KB/s 的速度？

## 关于常用方法的缺点：

### 各类 VPN + 客户端

* 每次各种需要连接断开烦死人，对于 Google 作为日常的人完全无法接受。
* 那些走国内中转的又都是小水管。

### ShadowsocksX

* 类似 git、gem 等均不走 ShadowsocksX（无论你是否在 ShadowsocksX 上设置全局代理）。

## 完美的姿势：

### Surge + Proxifier

好吧，Surge 这货在 iOS 上很出名，它的 Mac 版其实比较一般，依旧不能进行全局代理。但由于他本身提供了流量区分的规则，那么配合 Proxifier 就显得非常和谐了。Proxifier 捕获全局的流量全部抛给 Surge 的 socks5 端口，再由 Surge 进行流量的区分并视情况进行代理或直连。

### ShadowsocksX + Proxifier

这是也是一个很棒的解决方案，但这里需要使用 Proxifier 自己的规则，用 Profile 将各种流量进行区分后再进行直连或者转发。但是忧伤的是国内使用这种方案的人并不太多，所以并没有一个相对完善的 Profile 供你直接使用。关于这个问题，个人感觉比较好的解决方案是拿已有的比较完善的 Surge 的配置文件进行转换，好吧，程序员比较懒，写个转换的脚本就好，毕竟其自带的 GUI 对于此需求来说完全是反人类的。过几天写个脚本。

> 使用 ShadowsocksX + Proxifier 必须配置 Proxifier 的 Profile 增加各种基于域名的规则，否则其默认全局走代理，这就尴尬了，毕竟谁也无法接受上个京东、淘宝还得走代理。这个现象的原因是 ShadowsocksX 本身并不提供流量区分功能，所有流经 ShadowsocksX 的流量全被代理了。ShadowsocksX 自带的“全局”和“自动”代理其实是使用了操作系统提供的代理自动配置(PAC)，由操作系统决定哪些流量直连，哪些流量被代理，也就是转发给 ShadowsocksX 的 socks5 代理。