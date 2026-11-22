tags:: [[Java Class - Thread]]
---

- ## 线程使用步骤
	- 步骤如下：
		- 创建 Thread 实例，指定要执行的任务。
		  logseq.order-list-type:: number
		- 启动 Thread 实例，执行已指定的任务。
		  logseq.order-list-type:: number
- ## 启动 Thread 实例，执行已指定的任务
	- ### 启动 Thread 实例：start()
		- https://docs.oracle.com/javase/8/docs/api/java/lang/Thread.html#start--
		- 调用 Thread 实例的 `start()` 方法，即可让线程真正开始执行。
			- 线程会自动执行 Thread 实例的 `run()` 方法。
	- ### 执行已指定的任务：run()
		- https://docs.oracle.com/javase/8/docs/api/java/lang/Thread.html#run--
		- Thread 中 `run()` 相关代码如下：
			- ``` java
			  class Thread implements Runnable {
			      private Runnable target;
			  
			      public Thread(Runnable target) {
			          this.target = target;
			      }
			  
			      @Override
			      public void run() {
			          if (target != null) {
			              target.run();
			          }
			      }
			  }
			  ```
		- `Thread` 实现了 `Runnable` ， 所以才需要实现 `run()` 方法。
			- `run()` 方法内部：其实就是调用 `Runnable` 类型的成员变量 `target` 的 `run()` 方法。
- ## 创建 Thread 实例：Thread 的构造方法
	- 创建 Thread 实例，只需要调用 Thread 类的任一构造方法即可。
		- 参见: [[Java Class - Thread: Initialization]]
	- 但是，我们创建 Thread 实例，通常是需要它去执行某个任务的。
		- 所以，如果不给 Thread 实例指定任务，我们创建的 Thread 实例将没有意义。
- ## 指定要执行的任务
	- 参照 `run()` 方法代码可知，指定要执行的任务，可以采用如下方式之一：
	- ### 方案一：Provide a Runnable object
		- 即：直接调用 Thread 的构造方法，传入要执行的任务 `target`
		- ==注意：==
			- Thread 类只有构造方法可以设置 `target` ，不存在实例方法可以设置 `target` 。
			- 所以，不要想着创建实例时不指定 `target` ，之后再指定。
		- 一般我们就是用如下构造函数，只需要传入一个参数：“实现 `Runnable` 接口” 的类的实例。(参见: [[Java Interface - Runnable]] )
			- ``` java
			  public Thread(Runnable target) {
			    init(null, target, "Thread-" + nextThreadNum(), 0);
			  }
			  ```
		- 示例：
			- ``` java
			  public class Main {
			  	public static void main(String args[]) {
			          // 直接调用 Thread 的构造方法，传入要执行的任务 `target`
			  		Thread thread = new Thread(new MyRunnable());
			  		thread.start();
			  	}
			  }
			  
			  class MyRunnable implements Runnable {
			  	@Override
			  	public void run() {
			  		System.out.println("MyRunnable");
			  	}
			  }
			  ```
	- ### 方案二：Subclass Thread
		- 即：定义一个子类继承 Thread 类，重写 `run()` 方法为我们要执行的任务，然后调用子类的 **无参构造方法** 创建子类的实例。
		- ==注意：==
			- 重写 `run()` 方法，一般直接写任务代码，不会再去调用 `target` ，除非我们要实现一些特殊逻辑。
			  logseq.order-list-type:: number
			- 调用子类的 **无参构造方法** 时，其实也隐式调用了 Thread 类的 **无参构造方法** ，Thread 类的 **无参构造方法** ，不会给 `target` 属性再赋值。
			  logseq.order-list-type:: number
				- 我们也没有必要再给 `target` 属性赋值，因为我们重写的 `run()` 方法不再调用 `target`，除非我们要实现一些特殊逻辑。
		- 示例：
			- ``` java
			  public class Main {
			  	public static void main(String args[]) {
			  		MyThread myThread = new MyThread();
			  		myThread.start();
			  	}
			  }
			  
			  class MyThread extends Thread {
			  	@Override
			  	public void run() {
			  		System.out.println("MyThread");
			  	}
			  }
			  ```
	- ### 最佳实践
		- 没有特殊情况，无脑选择 **方案一：Provide a Runnable object** 。
			- 方案一明显比方案二更灵活、更清晰明了：任务是任务，线程是线程。
		- 个人认为，方案二属于极其糟糕的设计。
			- 明明可以通过组合 `Runnable` 属性达到目的，却非要定义子类去继承 `Thread` 。
				- 违背了 [[合成复用原则]] (组合优于继承)。
			- 只是通过子类扩展 `Thread` 的功能也就罢了，本可以通过 父类 (即 `Thread`) 的构造方法指定要执行的任务，却非要重写 `Thread` 的 `run()` 方法。
				- 违背了 [[里氏替换原则]] 。
			-
- ## 参考
	- [Java Tutorials - Defining and Starting a Thread](https://docs.oracle.com/javase/tutorial/essential/concurrency/runthread.html)
	  logseq.order-list-type:: number
	- logseq.order-list-type:: number