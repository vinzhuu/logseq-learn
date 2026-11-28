tags:: [[Intellij IDEA]]
---

- ## 如何查看某个类的 Hierarchy
	- 选中指定类, 按 `Control + H` .
- ## Hierarchy Scope
	- 可以自定义展示的类的范围.
		- 只看 JDK 中主要的类: `lib:java..*`
		  logseq.order-list-type:: number
		- 查看 JDK 中所有的类:
		  logseq.order-list-type:: number
			- ``` zsh
			  lib:java..*||lib:javax..*||lib:jdk..*||lib:com.sun..*||lib:sun..*||lib:org.ietf.jgss..*||lib:org.w3c.dom..*||lib:org.xml.sax..*||lib:netscape.javascript..*||lib:org.jcp.xml.dsig.internal..*||lib:com.apple..*||lib:apple..*
			  ```
-