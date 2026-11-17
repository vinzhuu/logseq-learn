tags:: [[Java Control Flow]]
---

- ## 语法
	- `For Statement` 语法：
		- ``` java
		  for (initialization; termination; increment) {
		      statement(s)
		  }
		  ```
	- `initialization` , `termination` 和 `increment` 三个表达式都是可选的：
		- `initialization` 表达式：循环开始时执行一次。
		  logseq.order-list-type:: number
			- 一般用于初始化循环 (initializes the loop)。
		- `termination` 表达式：结果为 `false` 时，则终止循环。
		  logseq.order-list-type:: number
		- `increment` 表达式：每次循环迭代后执行一次。
		  logseq.order-list-type:: number
			- 一般用于递增或递减一个值
	- 示例：
		- ``` java
		  for(int i=1; i<11; i++){
		  	System.out.println("Count is: " + i);
		  }
		  ```
- ## `initialization` 的变量作用域
	- `initialization` 表达式中声明的 **变量** 的作用域：从 **声明 (declaration)** 开始，到 **For 语句块** 结束。
		- 所以，`initialization` 中声明的变量，可以用于 `termination` ，`increment` 和 `statement(s)` 。
	- 一般使用 `i` , `j` , `k` 控制 for 循环。
- ## 无限循环
	- ``` java
	  // infinite loop
	  for ( ; ; ) {
	      // your code goes here
	  }
	  ```
- ## 参考
	- [Java 8 Tutorials - Learning the Java Language - Language Basics - The for Statement](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/for.html)
	  logseq.order-list-type:: number
-