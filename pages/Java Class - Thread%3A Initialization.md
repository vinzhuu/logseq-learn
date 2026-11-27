tags:: [[Java Class - Thread]]
---

- ## 构造方法
	- 参见: [Java SE 8 - Thread#Constructor](https://docs.oracle.com/javase/8/docs/api/java/lang/Thread.html#constructor.detail)
	- Thread Class 有：
		- 8 个 public 构造方法
		  logseq.order-list-type:: number
		- 1 个非 public 构造方法。
		  logseq.order-list-type:: number
	- 所有构造方法，其实最终都在调用 `init` 方法。
- ## init 方法
	- ``` java
	  private void init(ThreadGroup g, Runnable target, String name,
	                    long stackSize, AccessControlContext acc,
	                    boolean inheritThreadLocals) {
	    // ...
	  }
	  ```
	-
- ## 参考
	- logseq.order-list-type:: number
	- logseq.order-list-type:: number