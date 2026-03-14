tags:: [[Protocol]]
alias:: [[Multicast DNS]]
---

- [官网](https://www.multicastdns.org/)
- ## 什么是 mDNS
	- mDNS 用于 [[Zeroconf]] 名称解析 (Zeroconf name resolution)
	- mDNS 基于 [[DNS]] 微调而来
- ## 原理
	- DNS: `设备 → DNS服务器 → 返回IP`
	- mDNS: `设备 → 局域网广播 → 目标设备自己回应`
- ## 保留域名
	- `.local` 是 mDNS 的保留域名.
	- 可以用 `ping <hostname>.local` 来查看与指定设备的连通性和 IP .
-