tags:: [[Java]]
---

- ## 普通 try-catch-finally
	- ``` java
	  BufferedReader br = null;
	  try {
	    br = new BufferedReader(new FileReader("file.txt"));
	    throw new RuntimeException("try-block exception");
	  } finally {
	    br.close(); // 这里可能抛 IOException
	  }
	  ```
	- 执行流程：
		- try 块抛出 `RuntimeException`。
		  logseq.order-list-type:: number
		- finally 中的 `close()` 也抛出 `IOException`。
		  logseq.order-list-type:: number
			- Java 会直接把 finally 中抛出的异常 **覆盖** try 块的异常.
				- 这时, 我们将无法知道 try 块中发生了异常.
			- 或者，如果你手动捕获 try 块异常，再手动处理 finally 异常，你可以自己记录两者，但这是手动实现的。
- ## try-with-resources 的 Suppressed Exception 机制
	- Java 7 引入 try-with-resources 来自动关闭资源，并引入 **suppressed exception（被抑制的异常）** 机制：
		- ``` java
		  try (BufferedReader br = new BufferedReader(new FileReader("file.txt"))) {
		      // 使用资源
		  } catch (Exception e) {
		      System.out.println(e); // 主异常
		      for (Throwable t : e.getSuppressed()) {
		          System.out.println("Suppressed: " + t);
		      }
		  }
		  ```
	- 执行流程：
		- 执行 try 块，如果发生异常 `e1`，保存它。
		  logseq.order-list-type:: number
		- 自动调用 `br.close()`，如果 close() 也抛异常 `e2`：
		  logseq.order-list-type:: number
			- **e2 不会覆盖 e1**
			- 而是被 **添加到 e1 的 suppressed 异常列表**：
				- ```java
				  e1.addSuppressed(e2);
				  ```
			- catch 块捕获的仍然是 **e1**，`e2` 可以通过 `Throwable.getSuppressed()` 查看。
- ## 参考
	- 1.ChatGPT