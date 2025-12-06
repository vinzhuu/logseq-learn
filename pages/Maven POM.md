alias:: [[POM]]
tags:: [[Maven]]
---

- ## 官方资料
	- [Maven POM 参考手册](https://maven.apache.org/pom.html)
- ---
- ## `<dependencyManagement>`
	- 参考：[Dependency Management](https://maven.apache.org/guides/introduction/introduction-to-dependency-mechanism.html#dependency-management)
	- `<dependencyManagement>` 的优先级 高于 传递依赖 ( transitive dependencies ) 。
	- 当前项目的 `<dependencyManagement>` 的优先级 高于 父项目的 `<dependencyManagement>` 。
	- ### Importing Dependencies
		- `<dependencyManagement>` 除了可以引入具体依赖的管理，还可以通过 `<scope>import</scope>` 引入 pom 类型的依赖中的 `<dependencyManagement>`
- ## `<version>RELEASE</version>`
	- 参考:
		- Maven doc - [version-order-specification](https://maven.apache.org/pom.html#version-order-specification)
		- stackoverflow - [How do I tell Maven to use the latest version of a dependency?](https://stackoverflow.com/questions/30571/how-do-i-tell-maven-to-use-the-latest-version-of-a-dependency#comment8744781_30571)
		- stackoverflow - [Maven RELEASE and LATEST version "numbers"](https://stackoverflow.com/questions/45567787/maven-release-and-latest-version-numbers)
	- > The usage of '`final`', '`ga`', and '`release`' qualifiers is discouraged. Use no qualifier instead.
	- 表示使用当前依赖的最新的发行版本
	- Maven 已不推荐使用。
- ## `<repositories>`
	- 指定项目拉取依赖的仓库。
	- `<id>` 需与 `settings.xml` 文件中的 `<servers>` 中 `<server>` 的 `<id>` 一致。
	- ``` xml
	  <repositories>
	    <repository>
	      <id>nexus</id>
	      <name>Nexus Repository</name>
	      <url>http://example.com/repository/maven-public/</url>
	      <releases>
	        <enabled>true</enabled>
	        <updatePolicy>always</updatePolicy>
	        <checksumPolicy>warn</checksumPolicy>
	      </releases>
	      <snapshots>
	        <enabled>true</enabled>
	        <updatePolicy>always</updatePolicy>
	        <checksumPolicy>warn</checksumPolicy>
	      </snapshots>
	    </repository>
	  </repositories>
	  ```
- ## `<distributionManagement>`
	- 指定项目上传依赖的仓库。
	- `<id>` 需与 `settings.xml` 文件中的 `<servers>` 中 `<server>` 的 `<id>` 一致。
	- ``` xml
	  <distributionManagement>
	    <repository>
	      <id>maven-releases</id>
	      <url>http://example.com/repository/maven-releases/</url>
	    </repository>
	    <snapshotRepository>
	      <id>maven-snapshots</id>
	      <url>http://example.com/repository/maven-snapshots/</url>
	    </snapshotRepository>
	  </distributionManagement>
	  ```
	-