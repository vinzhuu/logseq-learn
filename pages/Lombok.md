tags:: [[Java Library]]
---

- ## 官方网站
	- [Lombok 官网](https://projectlombok.org/)（需要关掉代理才能访问）。
	- [Lombok 文档](https://projectlombok.org/features/all)
- ## 概述
	- Lombok 是一个 Java 库，它可以插入 **编辑器** 和 **构建工具** 。
	- Lombok 可以在代码编译时生成 getter 、setter 、 hashCode、 equals 、 toString 等方法，而在编写时我们只需要加几个注解就可以，代码足够清爽。
	- 但这样也有弊端：也就是无法从源码中直接看到相应的方法。
- ## 如何使用
	- 导入依赖。
	  logseq.order-list-type:: number
		- ```xml
		   <dependency>
		       <groupId>org.projectlombok</groupId>
		       <artifactId>lombok</artifactId>
		   </dependency>
		   ```
	- 安装 `Lombok` 插件（ IDEA 2020.3 开始内置Lombok插件(bundled)）
	  logseq.order-list-type:: number
		- ![image-20220325210906474.png](../assets/image-20220325210906474_1733645231427_0.png)
	- 使用 `Lombok` 的注解即可。
	  logseq.order-list-type:: number
	- 由于 `Lombok` 插件已集成在 IDE 中，所以直接运行项目 `Lombok` 插件会为我们处理那些注解。
	  logseq.order-list-type:: number
- ## 注解
	- 参见: [Lombok 文档](https://projectlombok.org/features/all)
	- ### @Data
		- `@Data` = `@ToString` + `@EqualsAndHashCode` + `@Getter` on all fields + `@Setter` on all non-final fields + `@RequiredArgsConstructor`
	- ### @RequiredArgsConstructor
		- 生成构造方法，参数有以下几种 (参数的顺序，就是参数声明的顺序)：
			- 声明时未初始化的 final 属性。
			  logseq.order-list-type:: number
			- 标记为 @NonNull，且声明时没有初始化的属性。
			  logseq.order-list-type:: number
				- 同时，在构造方法内部，会判断传入的参数是否是 null ，如果是，则会抛出 `NullPointerException` 。
		- ==注意：如果没有参数满足上述任一条件，则将会生成一个无参构造方法。==
	- ### Log
		- #### @Slf4j
			- 相当于 `private static final org.slf4j.Logger log = org.slf4j.LoggerFactory.getLogger(LogExample.class);`
-