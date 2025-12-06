tags:: [[PowerMock]]
---

- ## PowerMockRunner
	- ### 与 SpringRunner 一起使用
	  id:: 64422f3d-d7c9-45e6-b3a4-05684ba89223
		- 测试类上使用如下注解即可：
		- ``` java
		  @RunWith(PowerMockRunner.class)
		  @PowerMockRunnerDelegate(SpringRunner.class)
		  // 忽略一些类
		  @PowerMockIgnore({ "javax.management.*", "javax.net.ssl.*" })
		  ```
		-