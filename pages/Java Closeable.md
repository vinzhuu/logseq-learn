tags:: [[Java IO]]
---

- ## Closeable 与 AutoCloseable
	- Java 由 `Closeable` 与 `AutoCloseable` 两个关闭资源相关的接口, `Closeable` 继承了 `AutoCloseable` .
	- ### AutoCloseable
		- 实现了 `AutoCloseable` 接口的对象, 如果使用 `try-with-resources` , 则会在使用完毕后自动关闭:
			- ``` java
			  try (BufferedReader br = new BufferedReader(new FileReader("file.txt"))) {
			      System.out.println(br.readLine());
			  } catch (IOException e) {
			      e.printStackTrace();
			  }
			  // br.close() 会在 try 块结束时自动调用
			  ```
			- 自定义实现类:
			- ``` java
			  class MyResource implements AutoCloseable {
			      @Override
			      public void close() {
			          System.out.println("Resource closed");
			      }
			  }
			  
			  try (MyResource r = new MyResource()) {
			      System.out.println("Using resource");
			  }
			  ```
	- ### Closeable
		- 由于 `Closeable` 继承了 `AutoCloseable` , 所以也拥有 `AutoCloseable` 的上述性质.
		- 但 `Closeable` 的 close 方法, 抛出专门的 `IOException` , 专门用于 I/O 相关类.
	- ### 实现时需注意
		- 参考: [Java SE 8 API - AutoCloseable](https://docs.oracle.com/javase/8/docs/api/java/lang/AutoCloseable.html)
		- #### 关于抛出异常
			- 如果 实现类 调用 `close()` 方法, 可能会出现异常, 则尽量抛出具体的异常 (而非 `Exception` ) .
			  logseq.order-list-type:: number
			- 如果 实现类 调用 `close()` 方法要抛出异常 (这里指的并非是关闭资源相关代码抛出的异常), 先执行真正关闭资源相关的代码, 再抛出异常, 避免资源因为异常而一直没被释放.
			  logseq.order-list-type:: number
			- 如果 能够保证 实现类 调用 `close()` 方法几乎不会出现异常, 则尽量不要抛出异常, 这样调用者就不用关心异常捕获的问题.
			  logseq.order-list-type:: number
				- ``` java
				  class MyResource implements AutoCloseable {
				      // close 方法没有像 AutoCloseable 那样抛出异常
				      @Override
				      public void close() {
				          // 不会失败，所以不抛异常
				          System.out.println("Resource closed safely");
				      }
				  }
				  ```
			- 如果某个异常被抑制可能会带来问题, 就不要在 close() 中抛出它.
			  logseq.order-list-type:: number
				- 因为 `try-with-resources` 的 [[Java Suppressed Exception]] 机制会导致调用方无法直接捕获 try 块内部的异常.
				- 如果这个异常是 `InterruptedException` ( [[Java InterruptedException]] ) 等不处理就会有问题的异常, 就可能会导致程序出错.
		- #### 关于幂等性
			- `Closeable` 的 `close()` 方法要求 [[幂等性]] , 即多次调用不会产生副作用.
			- 而 `AutoCloseable` 的 `close()` 方法则不要求 [[幂等性]] , 多次调用可能会有副作用 (比如, 每次都会打印日志).
				- 但为了安全, 仍然强烈建议 `AutoCloseable` 的 `close()` 方法也保证  [[幂等性]] .
- ## Java 自动关闭资源的机制
	- ### finalize() 方法
		- Java 早期 `FileInputStream` , `FileOutputStream` 等方法中, 有 `finalize()` 方法,
			- 当 GC 回收流对象时，会调用它的 `finalize()` , `finalize()` 方法内部会调用 `close()` 方法 .
		- 但是, GC 触发的时机不可预测, 所以并不可靠, 所以在Java 9 之后被标记为 `deprecated` .
	- ### Cleaner
		- 现代 JDK 采用 `Cleaner` 机制来代替 `finalize()`.
			- 当流对象被 GC 回收时，Cleaner 线程会在后台调用 `close0()` (native 方法) 关闭资源.
		- 但是 `Cleaner` 是异步执行的, 并不能做到及时关闭.
- ## 为什么必须显式调用 close() 方法
	- 外部流资源 (如 文件流, 网络流) 并不受 JVM 管理, 而是由操作系统管理.
	- 所以, JVM 进行垃圾回收时, 如果没有 `finalize()` 和 `Cleaner` 等机制显式关闭资源, JVM 根本无法关闭资源.
	- 操作系统确实能够在程序退出后, 释放资源占用.
		- 但是这并没有手动调用 `close()` 方法安全.
		- 何况, 很多服务器程序都是处于长期运行状态, 并不会被关闭.
	- ==所以存在这样的问题:==
		- 如果一个流对象没有执行 `close()` 方法就被垃圾回收了, 而程序还在执行中, 此时 :
			- 如果没有  `finalize()` 和 `Cleaner` 等机制, 这个资源将永远无法被释放 (除非程序退出).
- ## 最佳实践
	- 一定要在资源使用完成后调用 `close()` 方法.
- ## 参考
	- ChatGPT
	  logseq.order-list-type:: number
	- logseq.order-list-type:: number