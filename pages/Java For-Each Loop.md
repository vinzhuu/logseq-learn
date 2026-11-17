tags:: [[Java Control Flow]]
---

- ## Iterable
	- 所有实现了 `Iterable` (参见: [[Java Iterable & Iterator]]) 的类，才可以使用 [[Java For-Each Loop]] 语法进行迭代.
- ## 语法
	- Enhanced For Statement 语法：
		- ``` java
		  for (element: iterable) {
		    statement(s)
		  }
		  ```
	- 示例：
		- ``` java
		  int[] numbers = {1,2,3,4,5,6,7,8,9,10};
		  for (int item : numbers) {
		    System.out.println("Count is: " + item);
		  }
		  ```
- ## 最佳实践
	- 一般能用 `Enhanced For Statement` , 就不要用普通的 `For Statement` ( [[Java For Loop]] ) .
- ## 参考
	- [Java 8 Tutorials - Learning the Java Language - Language Basics - The for Statement](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/for.html)
	  logseq.order-list-type:: number
	- logseq.order-list-type:: number