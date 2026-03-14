tags:: [[Elasticsearch]]
---

- ## 概念
	- ### Elasticsearch 和 Enterprise Search
		- Enterprise Search 是 Elasticsearch 的一个商业化模块，需要购买许可证。
		- 不带 Enterprise Search 模块的 Elasticsearch 是开源免费的。
		  id:: 64aed07e-da86-41ab-98f5-8404121f24f1
		- Enterprise Search 提供了一些高级功能。
	- ### 内置 JDK
		- Elasticsearch 使用 Java 开发，自 7.0 版本起有内置的 JDK ，所以不用额外安装 JDK 也能运行。
		- 但其实也可以指定使用系统安装的 JDK 。
		- 使用内置的 JDK 会更方便，而使用系统安装的 JDK 会更灵活，也可以被多个程序共用，以统一版本和节省空间。
	- ### JDK 版本
		- 参考 [Elasticsearch 与 JDK 版本的兼容关系](https://www.elastic.co/support/matrix/#matrix_jvm) 可知：
			- 从 Elasticsearch 8.0.x 版本之后，不再兼容 Oracle JDK 1.8 ，至少需要 Oracle JDK 17 。
			- Elasticsearch 7.17.x 是最后与 Oracle JDK 1.8 兼容的版本。
			-