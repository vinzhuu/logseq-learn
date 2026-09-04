tags:: [[Oracle JDK]]
---

- ## Release Family
	- `Release Family` : 即 具有 **相同 Java 主版本号** 的一组发行版 .
		- 如: JDK 26 系列, JDK 21 系列.
- ## Release Family 的 Support Timeline
	- 参见: [Java Release Support Timeline](https://ops.java/releases#support-timeline)
	- 可以查看各个 `Release Family` 的
		- GA 版本的发布时间
		  logseq.order-list-type:: number
		- 支持生命周期的结束时间 (End Of Support Life , EOSL).
		  logseq.order-list-type:: number
	- 只有标有 `LTS` 的才是长期支持版本.
- ## CPU Release 与 PSU Release
	- 参考: [JDK Releases](https://ops.java/releases)
	- ### CPU Release
		- CPU, 即 `Critical Patch Update` , 关键补丁更新.
		- 包括:
			- 漏洞修复 (vulnerability fixes): 针对所有 **受相关漏洞影响** 且 **仍在维护期内** 的 Release Family .
			  logseq.order-list-type:: number
			- 常规维护 (general maintenance): 针对所有 LTS 的 Release Family .
			  logseq.order-list-type:: number
				- 包括: 提供新平台支持.
				- 包括: 普通的 Bug 修复.
					- 如果某次发布 CPU 时, 也要发布 PSU;
					- 则 **普通的 Bug 修复** 不会放到 CPU, 而是放到 PSU.
	- ### PSU Release
		- PSU, 即 `Patch Set Update` , 补丁集更新 .
		- 与 CPU 同一天发布, 包含:
			- 漏洞修复 (vulnerability fixes).
			  logseq.order-list-type:: number
			- 额外的功能修复 (additional functional fixes).
			  logseq.order-list-type:: number
- ## Feature Release
	-
- ## Security Alert
	-
- ## Security Baseline
	- 参考: [Security Baselines](https://ops.java/security/baselines/)
	- ### 什么是 Security Baseline
		- Security Baseline, 就是每个 `Release Family` 中被视为安全的 **最低版本号** .
			- 这可以用来确定某个 JDK 版本是否最新, 且包含 **最新的安全修复 (latest security fixes)** .
	- ### 各 Release Family 的 Security Baseline
		- 可以在 [Security Baseline](https://javadl-esd-secure.oracle.com/update/baseline.version) 页面, 查看每个 Release Family 的 Security Baseline .
			- 一行就是一个 Release Family 的 Security Baseline .
	- ### Security Baseline 的取值
		- 如果 Release Family 仍未到达 **支持生命周期终点** , 则取 **该 Release Family 的最新发布版本** .
		- 如果 Release Family 已经到达 **支持生命周期终点** , 则取 **一个不存在的版本** .
			- 如果 最终更新版本 (last update version) 小于 99, 则取 99 .
			  logseq.order-list-type:: number
			- 如果 最终更新版本 (last update version) 大于 99 , 则取 **最终更新版本** + 10 .
			  logseq.order-list-type:: number
			- ==由于用户使用的版本永远不会大于 Security Baseline , 所以可以提示用户使用的版本不安全==
		- 注意:
			- `1.7.0_513` 我们无法在 [Java SE 7 Archive Downloads](https://www.oracle.com/java/technologies/javase/javase7-archive-downloads.html) 下载, 但可以在  [Release Notes for JDK 7 and JDK 7 Update Releases](https://www.oracle.com/java/technologies/javase/7-support-relnotes.html) 看到 .
			  logseq.order-list-type:: number
			- `1.6.0_221` 我们无法在 [Java SE 6 Downloads](https://www.oracle.com/java/technologies/javase-java-archive-javase6-downloads.html) 下载, 但可以在 [Java SE 6 Advanced and Java SE 6 Support (formerly known as Java SE for Business 6) Release Notes](https://www.oracle.com/java/technologies/javase/6-relnotes.html) 看到.
			  logseq.order-list-type:: number
- ## 参考
	- [JDK Releases](https://ops.java/releases)
	  logseq.order-list-type:: number
-