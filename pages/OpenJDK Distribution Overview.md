tags:: [[OpenJDK Distribution]]

- ## 什么是 Downstream of OpenJDK
	- 即基于 [[OpenJDK]] 源码得到的下游 JDK 产物.
	- 一般可以分为两类 ( ==非官方定义, 只是本人的总结== ):
		- `OpenJDK Build` :
		  logseq.order-list-type:: number
			- 不修改 OpenJDK 源码, 直接构建 (有问题也是等源码修复了, 再重新构建)
		- `OpenJDK Distribution` :
		  logseq.order-list-type:: number
			- 修改 OpenJDK 源码, 再做构建 (有问题可能会先自己修复, 后面上游源码修复了, 再做合并)
- ## OpenJDK Build
	- `OpenJDK Build` 目前由 [[Oracle]] 直接从 OpenJDK 源码构建得到 .
		- 所以一般也称为 : [[Oracle OpenJDK Build]]
- ## OpenJDK Distribution
	- **OpenJDK Distribution** 就是对 OpenJDK 源码进行 **修改、构建、测试、打包** 后, 提供给用户的 **JDK 二进制发行版** .
	- **OpenJDK Distribution** 一般会用 **Prebuilt** 这个词来形容:
	  id:: 6a8db2b3-48d7-44c9-ad5e-bc9a1d3b379c
		- 这是为了强调: "给的不是 OpenJDK 源码, 而是已经构建完成、可以直接运行的 JDK" .
	- ==广义上, 也可以将 OpenJDK Build 视为 OpenJDK Distribution. ==
- ## OpenJDK Distribution 对 OpenJDK 源码做了哪些改动
	- 大致有如下调整:
		- 系统集成与平台适配 ==属于较大改动==
		  logseq.order-list-type:: number
			- 比如: 动态链接系统原生库, 适配特定编译器或内核
		- 功能增减与定制
		  logseq.order-list-type:: number
			- 比如: [[Oracle JDK]] 会增加它自己闭源的部署组件（WebStart、插件）和第三方字体/光栅化器.
			- 比如: [[Alibaba Dragonwell]] 增加了 Wisp (协程相关能力) 和 Elastic-Heap 等功能.
			- 比如: 移除不常用或存在法律风险的旧加密算法
		- 安全与紧急修复 ==属于最频繁的改动==
		  logseq.order-list-type:: number
			- 比如: 将 OpenJDK 后面的版本已经修复的问题, 移植到发行版上, 这样被称为 [[Backport]] .
			- 比如: 发行版自己动手修复 OpenJDK 现在还未修复的问题,
		- 性能调优与增强
		  logseq.order-list-type:: number
			- 比如: 优化 [[JVM]] 与 [[GC]] 性能.
		- 元数据与品牌标识
		  logseq.order-list-type:: number
			- 比如: 修改 `java -version` 输出的供应商信息.
			- 比如: 修改源码中的默认 `java.vendor`、`java.vm.vendor` 等系统属性.
		- 构建与打包策略
		  logseq.order-list-type:: number
			- 比如: 在发行版的 `src.zip` 中包含所有依赖库的源码, 以方便开发者调试.
- ## 为什么需要 OpenJDK Distribution
	-
- ## 有哪些 OpenJDK Distribution
	- Oracle 官方:
	  logseq.order-list-type:: number
		- [[Oracle JDK]]
	- 开源社区: 
	  logseq.order-list-type:: number
		- [[Eclipse Temurin]]
	- 商业公司:
	  logseq.order-list-type:: number
		- [[Amazon Corretto]]
		  logseq.order-list-type:: number
		- [[Liberica JDK]]
		  logseq.order-list-type:: number
		- [[Azul Zulu]]
		  logseq.order-list-type:: number
		- [[Alibaba Dragonwell]]
		  logseq.order-list-type:: number
		- [[BiSheng JDK]]
		  logseq.order-list-type:: number
		- [[Tencent Kona]]
		  logseq.order-list-type:: number
		- [[Red Hat Build of OpenJDK]]
		  logseq.order-list-type:: number
		- [[Microsoft Build of OpenJDK]]
		  logseq.order-list-type:: number
- ## Oracle JDK & Oracle OpenJDK Build
	-
- ## OpenJDK Distribution 的 License
	- GPLv2 with Classpath Exception
- ## JDK 产品
	- **参考:**
		- [【方向盘】逐渐碎片化的Java生态圈：Oracle JDK、OpenJDK、阿里Dragonwell、华为毕昇](https://developer.aliyun.com/article/1108370)
		- [Java Is Still Free 3.0.0 (Oct 2021)](https://medium.com/@javachampions/java-is-still-free-3-0-0-ocrt-2021-bca75c88d23b)
		- [What is the difference between Azul OpenJDK, Zulu OpenJDK and OpenJDK?](https://stackoverflow.com/a/61337953)
	- [[Oracle JDK]] : Oracle 官方 JDK ，并不完全免费 (8u211 以下版本 (比如JDK 8u202) 不升级就不收费，升级但不商用也不收费) 。
	-
	-
- ## 参考
	- AI
	  logseq.order-list-type:: number
	- [Best Oracle Java Alternatives in 2026: Comparison of OpenJDK Distributions](https://bell-sw.com/blog/oracle-java-alternatives-comparison-of-openjdk-distributions/)
	  logseq.order-list-type:: number
-