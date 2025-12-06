tags:: [[Feign]]
---

- ## 问题点
	- OpenFeign 和 Netflix Feign 的关系？
	  logseq.order-list-type:: number
- ## 学习路线
	- [[Spring Cloud OpenFeign]]
	  logseq.order-list-type:: number
- ## 常见问题
	- ### 关于 MethodType
		- 在接口层，定义如下方法；如果 @FeignClient 标注的类继承这个接口，在执行时，会报错；
		- 因为 OpenFeign 不支持一个方法定义多种 Method 类型
		- ```java
		  @RequestMapping(path = "/refreshAll", method = { RequestMethod.GET, RequestMethod.POST })
		  ```
-