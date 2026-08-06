tags:: [[CloudBase 云函数]], [[CloudBase 云托管]]
---

- ## 普通云函数 & HTTP 云函数
	- 通读: [[CloudBase 云函数: Overview]]
- ## 云托管
	- 通读: [[CloudBase 云托管: Overview]]
- ## 云托管函数框架
	- 通读: [[CloudBase 云托管函数框架: Overview]]
- ## 开发上的区别: 普通云函数, HTTP 云函数, 云托管 & 云托管函数框架
	- **普通云函数** : 相当于只写一个函数.
	- **HTTP 云函数** : 相当于写一个我们 **无法完全控制的** Web 容器应用.
	- **云托管** : 相当于写一个我们 **可以控制的完整的** 容器应用 (不一定非得是 Web 应用).
	- **云托管函数框架** : 相当于用 [[CloudBase Functions Framework]] 写一个我们 **可以控制** 的容器应用.
		- 使用 [[CloudBase Functions Framework]] , 可以让我们像编写 **普通云函数** 一样开发业务逻辑, 而无需像 **云托管** 那样写一个完整的应用.
- ## 如何选择: 普通云函数, HTTP 云函数, 云托管 & 云托管函数框架
	- 参考:
		- [普通云函数 VS HTTP 云函数](https://docs.cloudbase.net/cloud-function/quickstart/select-types)
		  logseq.order-list-type:: number
		- [云托管函数框架](https://docs.cloudbase.net/cbrf/intro)
		  logseq.order-list-type:: number
		- [云托管函数框架 VS 云托管 VS 云函数](https://docs.cloudbase.net/cbrf/vs)
		  logseq.order-list-type:: number
		- [技术选型指南](https://docs.cloudbase.net/run/introduction#%E6%8A%80%E6%9C%AF%E9%80%89%E5%9E%8B%E6%8C%87%E5%8D%97)
		  logseq.order-list-type:: number
	- 大致可以按如下指标选择:
		- 费用:
		  logseq.order-list-type:: number
			- `普通云函数` < `HTTP 云函数` < `云托管 / 云托管函数框架`
		- 性能 (响应速度与并发处理能力):
		  logseq.order-list-type:: number
			- `普通云函数` < `HTTP 云函数` < `云托管 / 云托管函数框架`
		- 灵活度:
		  logseq.order-list-type:: number
			- `普通云函数` < `HTTP 云函数` < `云托管函数框架` <  `云托管 (非函数框架)`
		- 支持长连接 (WebSocket、SSE):
		  logseq.order-list-type:: number
			- `HTTP 云函数`
			  logseq.order-list-type:: number
			- `云托管 / 云托管函数框架`
			  logseq.order-list-type:: number
		- 支持并发:
		  logseq.order-list-type:: number
			- `HTTP 云函数`
			  logseq.order-list-type:: number
			- `云托管 / 云托管函数框架`
			  logseq.order-list-type:: number
		- 支持实例常驻:
		  logseq.order-list-type:: number
			- `云托管 / 云托管函数框架`
-