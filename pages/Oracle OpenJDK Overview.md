tags:: [[Oracle OpenJDK]]
---

- ## GA Release, Early-access Release & Reference Implementation
	- ### 区别
		- | 名称 | 所属维度 | 含义 |
		  | ---- | ---- | ---- | ---- |
		  | Early-Access Release (EA) / Release-Candidate (RC) | JDK 发布阶段 | 正式发布前 **供用户试用和测试** 的构建, 不建议用于 **生产环境** | 
		  | General-Availability Release (GA) | JDK 发布阶段 | 已经正式面向 **普通用户** 和 **生产环境** 发布 |
		  | Reference Implementation (RI) | Java SE 规范体系 | 用来证明 Java SE 规范可以被完整实现的 **官方参考实现** , 仅供参考, 不可用于 **生产环境** |
	- ### 关于 GA
		- GA 也还是不要用于生产环境吧.
		- 因为 Oracle OpenJDK 的 一个 Release Family 的维护时间很短, **新的安全修复** , 可能不会应用到旧的 Release Family .
		- 这就导致使用 旧 Release Family 的用户, 无法应用新的 **新的安全修复** .
			- 除非, 用户一直保持使用最新的 Release Family .
	- ### 关于 EA
		- EA 功能可能随时被修改或移除.
		  logseq.order-list-type:: number
		- EA 功能可能永远不会进入 GA
		  logseq.order-list-type:: number
	- ### 大致发布流程
		- ``` zsh
		  不断发布 EA Build
		          ↓
		  某个构建被确定为 Java SE 的 RI , 锁定代码
		          ↓
		  如果发现必须修复的问题
		          ├─ 修改代码并产生新构建
		          └─ 相应更新 RI, 锁定代码
		          ↓
		  到达预定发布日期
		          ↓
		  最终构建宣布为 GA
		  ```
- ## 历史上发布过的 GA Release
	- 参见: [Archived OpenJDK General-Availability Releases](https://jdk.java.net/archive/)
	- 官方不建议在 **生产环境** 使用历史 GA 版本, 因为历史 GA 版本没有安全补丁.
	- 所以要使用 Oracle OpenJDK Build , 应下载安装最新的 GA 版本.
- ## 参考
	- AI
	  logseq.order-list-type:: number
	- [OpenJDK JDK 27 Release-Candidate Builds](https://jdk.java.net/27/)
	  logseq.order-list-type:: number
	- [JDK 26.0.2.1 Release Notes](https://jdk.java.net/26/release-notes)
	  logseq.order-list-type:: number