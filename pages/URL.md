tags:: [[HTTP]]
---

- ## 几个概念的区别
	- URI (Universal Resource Identifier) : **统一资源标志符** ，用来唯一标识资源（抽象或物理）的一个字符串。
	- URL (Universal Resource Locator) : **统一资源定位符** ，一种 **定位资源** 的字符串。不仅标识了 Web 资源，还指定了操作或者获取方式，同时指出了主要访问机制和网络位置。
	- URN (Universal Resource Name) : **统一资源名称** ，用 **特定命名空间** 中的 **唯一名称或 ID** 来标识资源。使用URN可以在不知道其网络位置及访问方式的情况下讨论资源。
	- ==我的理解==
		- URL 和 URN 都是 URI 的一种实现（用子集不太妥当），都可以用来唯一标识一个资源。
		- URL 侧重表示资源的网络位置（逻辑上的位置，不一定与物理位置一致），而 URN 侧重表示这个资源唯一的一个名称。
			- eg: 如果世界上每一个人都住一栋房（且每栋房都只住一个人），且每个人都有一个唯一的身份证号。那么 **住址** 就是一种 URL，而 **身份证号** 就是一种 URN 。
		- 所以我们可以说：URL 是一种 UR ；URN 是一种 URI 。
		- 在平时的接口开发中，某个项目中的某个资源的名称可以作为 URN ，如 `/login.html` （完整的URL为 `http://www.example.com:8080/login.html`），但大家通常不把他称为 URN ，而叫做 URI 。
		- 为了防止混淆，一直叫 **URI** 准没错。
- ## URL的结构
	- 一个标准的URL必须包括：protocol、host、port、path、parameter、anchor
	- ```http
	  http://www.example.com:8080/news/index.html?boardID=5&ID=24618&page=1#name
	  ```
	- 协议部分 (protocol)
	  logseq.order-list-type:: number
		- URL的第一个字符串代表的是使用的何种协议，在 internet 中可以使用多种协议，比如 HTTP ， FTP 和 HTTPS 等等。
		  logseq.order-list-type:: number
	- 域名部分 (host)
	  logseq.order-list-type:: number
		- 用 `//` 作为协议与域名的分隔符，一个 URL 也可以使用 IP 地址作为这一部分的内容。
		  logseq.order-list-type:: number
	- 端口部分 (port)
	  logseq.order-list-type:: number
		- 用 `:` 作为端口与域名部分的分隔符。
		  logseq.order-list-type:: number
		- 端口号就是指定该数据应该被哪一个应用程序所接收。
		  logseq.order-list-type:: number
		- 端口号在 URL 中不是必须填写的，如果不写就选择默认端口号。
		  logseq.order-list-type:: number
	- 虚拟目录部分
	  logseq.order-list-type:: number
		- 从域名后的第一个 `/` 开始到最后一个 `/` 为止，是虚拟目录部分。
		  logseq.order-list-type:: number
		- 虚拟目录也不是一个URL必须的部分。
		  logseq.order-list-type:: number
		- 本例中的虚拟目录是 `/news/` .
	- 文件名部分
	  logseq.order-list-type:: number
		- 从域名后的最后一个 `/` 开始到 `?` 为止，是文件名部分
		  logseq.order-list-type:: number
		- 如果没有 `?` , 则是从域名后的最后一个 `/` 开始到 `#` 为止，是文件部分
		  logseq.order-list-type:: number
		- 如果没有 `?` 和 `#` ，那么从域名后的最后一个 `/` 开始到结束，都是文件名部分。
		  logseq.order-list-type:: number
		- 文件名部分不是一个 URL 必须的部分，如果省略该部分，则使用默认的文件名。
		  logseq.order-list-type:: number
		- 本例中的文件名是 `index.html` 。
	- 参数部分 (parameter)
	  logseq.order-list-type:: number
		- 从 `?` 开始到 `#` 为止之间的部分为参数部分，又称搜索部分、查询部分。
		  logseq.order-list-type:: number
		- 参数可以允许有多个参数，参数与参数之间用 `&` 作为分隔符。
		  logseq.order-list-type:: number
		- 本例中的参数部分为 `boardID=5&ID=24618&page=1` 。
	- 锚部分 (anchor)
	  logseq.order-list-type:: number
		- 从 `#` 开始到最后，都是锚部分。
		  logseq.order-list-type:: number
		- 锚部分也不是一个 URL 必须的部分。
		  logseq.order-list-type:: number
		- 本例中的锚部分是 `name` 。
		  logseq.order-list-type:: number
-
-