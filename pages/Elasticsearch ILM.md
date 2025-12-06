tags:: [[Elasticsearch]]
---

- ## 一句话解释
	- ILM, 即 `Index Lifecycle Management` , 索引生命周期管理 .
- ## Five Lifecycle Phases
	- 参考: [Index lifecycle](https://www.elastic.co/guide/en/elasticsearch/reference/7.17/ilm-index-lifecycle.html)
	- Hot: 索引可以被更新、可以被查询
	- Warm: 索引不可被更新、但可以被查询
	- Cold: 索引不可被更新、但可以被不频繁地查询 (能够接受查询比较慢)
	- Frozen: 索引不可被更新、但可以被极少地查询 (能够接受查询极慢)
	- Delete: 索引不再需要，并可以被安全地移除
- ## API
	- kibana 貌似不支持详细的生命周期配置，建议直接使用 API
	- ## 创建生命周期策略
		- 创建一个 **7d 后删除** 的生命周期策略
		- ``` json
		  PUT _ilm/policy/生命周期策略名称
		  {
		    "policy": {
		      "phases": {
		        "delete": {
		          "min_age": "7d",
		          "actions": {
		            "delete": {}
		          }
		        }
		      }
		    }
		  }
		  ```