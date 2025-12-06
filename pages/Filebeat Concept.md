tags:: [[Filebeat]]
---

- ## 架构
	- 参考: [Filebeat overview](https://www.elastic.co/guide/en/beats/filebeat/7.17/filebeat-overview.html)
	- ![image.png](../assets/image_1704253415448_0.png)
	- Filebeat 启动时, 针对配置的每一个 location , 会启动一个 input 去监控日志数据.
	  logseq.order-list-type:: number
	- 针对每一个 input 又会启动一个 harvester 收集日志数据. 
	  logseq.order-list-type:: number
	- harvester 收集的日志数据将会汇入 libbeat (参见 [[Beats Concept]] ) .
	  logseq.order-list-type:: number
	- libbeat 会将数据输出到配置的 output .
	  logseq.order-list-type:: number
- ## 重启 Filebeat
	- 重启 Filebeat 时，如果需要 Filebeat 重新读取数据，需要删除 `rm data/registry` 目录，因为这个目录存储了 Filebeat 读取数据的状态.
	-