tags:: [[Distributed Transaction]]
alias:: [[2PC]]
---

- ## 存在的问题
	- 性能问题：在提交或回滚事务前，所有资源都被锁定。
	  logseq.order-list-type:: number
	- 单点问题：在 TM 下发 Commit / Rollback 指令前，如果 TM 故障，将导致所有事务参与者卡住。
	  logseq.order-list-type:: number
	- 不一致风险：在 TM 下发 Commit / Rollback 指令后，如果部分节点接收到指令，部分节点因为网络等问题没接收到指令，将导致数据不一致。
	  logseq.order-list-type:: number
		- 因为没接受到指令的节点，显然无法根据现有信息推断其他节点执行的是 Commit 还是 Rollback。
-