tags:: [[Logstash]]
---

- ## 配置文件结构
	- ``` conf
	  # This is a comment. You should use comments to describe
	  # parts of your configuration.
	  input {
	    ...
	  }
	  
	  filter {
	    ...
	  }
	  
	  output {
	    ...
	  }
	  ```
	- 三大元素
		- input: 指定数据来源
		- output: 指定数据去向
		- filter: 对数据进行处理
			- 如果配置了多个 filter , 将会按配置的先后顺序执行 .
-