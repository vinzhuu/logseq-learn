tags:: [[Flutter Layout]]
---

- ## What is Layout
	- 从广义上讲, **布局 (Layout)** 指的是 Widget 在屏幕上的 **尺寸 (Size)** 和 **位置 (Position)** .
- ## Constraints
	- 任何 Widget 的 Layout , 都受到其父元素的 **约束 (Constrain)** ,
	- 任何 Widget 的 Layout , 都由其与父元素之间的 **对话** 决定.
	- 它们之间的对话是这样的:
		- 父组件将 **约束 (Constraints)** 传递给子组件.
		  logseq.order-list-type:: number
			- 即 `minWidth / maxWidth` 和  `minHeight / maxHeight` .
		- 子组件根据约束确定自己 **期望的尺寸** , 并回传给父组件
		  logseq.order-list-type:: number
		- 父组件根据子组件 **期望的尺寸** 和 **对齐方式 (Alignment)** , 确定子组件的位置.
		  logseq.order-list-type:: number
	- 总结: `Constraints go down. Sizes go up. Parent sets the position.`
-
-
- ## 参考
	- [Flutter Docs - Layout](https://docs.flutter.dev/get-started/fundamentals/layout)
	  logseq.order-list-type:: number