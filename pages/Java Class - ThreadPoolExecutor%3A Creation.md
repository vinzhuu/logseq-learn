tags:: [[Java Class - ThreadPoolExecutor]]
---

- ## 创建 ThreadPoolExecutor 实例
	- ### 方式一：直接调用 ThreadPoolExecutor 的构造方法
		- 参见: [[Java Class - ThreadPoolExecutor: Init & Run]]
	- ### 方式二：调用 Executors 工具类的静态方法
		- `Executors` 工具类提供了若干静态方法，可以创建 `ThreadPoolExecutor` 实例 (不过它方法返回值类型是 `ExecutorService`)。
			- 内部其实也是调用 `ThreadPoolExecutor` 的构造方法，一些字段给了默认值。
		- 参见: [[Java Class - Executors: Create ExecutorService]]
	- ### 最佳实践
		-
- ## 参数最佳实践
	-