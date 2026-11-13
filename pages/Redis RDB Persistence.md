tags:: [[Redis Persistence]]
---

- 将 Redis 中当前的全量数据快照，以二进制的形式存到文件中。
	- save：同步保存操作，会阻塞 Redis 主线程；
	- bgsave：fork 出一个子进程，子进程执行。
-