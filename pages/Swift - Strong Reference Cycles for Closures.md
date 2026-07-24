tags:: [[Swift Reference Counting]]
---

- 如果将 **闭包** 赋值给 `Class` 实例的属性, 并且该 **闭包** 通过 **引用该实例或其成员** 来捕获该实例:
	- 那就会在 **闭包** 和 **实例** 之间产生 **强引用循环 (Strong Reference Cycle)** .
- ## Capture List
	-