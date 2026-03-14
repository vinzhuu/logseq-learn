tags:: [[Deep Linking]] 
---

- ## Deep Linking 是啥
	- **Deep Linking** 是这样一种技术:
		- 通过 **Link (链接, 并非特指 http/https 链接)** 向系统表达 "意图" , 系统会将这个 "意图" 交给目标 APP 处理 .
		- 系统只是起到一个导航的作用, 目标 APP 可以自行决定如何处理:
			- 可以是跳转到目标 APP 的某个页面.
			  logseq.order-list-type:: number
				- 这个跳转到的目标页面也可以立即自行触发一些逻辑: 比如 再次发生跳转 (这样就可以实现多次跳转了, 哈哈哈)
			- 也可以是不跳转页面, 只触发一个后台操作.
			  logseq.order-list-type:: number
		- 其实, **Deep Linking** 就是可以做到 "通过系统中转, 实现 APP 之间的简单通信" .
	- ==但是, Deep Linking 大多数时候, 还是用来进行页面跳转的.==
- ## 跳转类型
	- APP 的跳转, 可以分为如下类型:
		- 不同应用之间的跳转.
		  logseq.order-list-type:: number
			- 需要代码显式调用系统中 Deep Linking 相关 API .
		- 应用内部的跳转.
		  logseq.order-list-type:: number
			- 实现方式可以和 Deep Linking 一致, 只是无需调用系统 API , 交由系统处理.
			- APP 内部定义规则, 自行处理跳转即可.
	- ==系统原生应用之间的跳转, 与第三方应用之间的跳转, 没有本质区别.==
		- 只是系统原生应用的跳转可能拥有某些特权
- ## 页面分类
	- APP 中的页面可以分为如下几类 (既可以是 **源页面** , 也可以是 **目标页面** ):
		- APP 原生页面
		  logseq.order-list-type:: number
		- APP 中的 WebView 页面.
		  logseq.order-list-type:: number
		- 浏览器网页.
		  logseq.order-list-type:: number
	- 但其实, 在系统层面, 做这种区分是没有必要的.
		- 因为系统只会管你这个 Link , 由哪个 APP 发起, 并交由哪个 APP 处理.
		- 而不会管你从哪个具体的页面跳转, 要跳转到哪个具体的页面.
		- 要跳转到哪个页面, 完全由目标 APP 控制, 可以是任何一种页面.
- ## 参考
	- ChatGPT
	  logseq.order-list-type:: number