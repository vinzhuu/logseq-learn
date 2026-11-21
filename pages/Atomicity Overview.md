tags:: [[Atomicity]]
---

- ## 原子性 (Atomicity)
	- > Atomicity is the performing of a sequence of steps, called actions, so that they appear to be done as a single, indivisible step, known in operating system and architecture literature as an atomic action and in database management literature as a transaction. 
	  -- 引自 [Chapter 9 Atomicity: All-or-Nothing and Before-or-After (第 5 页)](https://ocw.mit.edu/courses/res-6-004-principles-of-computer-system-design-an-introduction-spring-2009/de2b7c59e413f58e51eac60acd52efef_atomicity_open_5_0.pdf)
	- 执行一系列 **步骤 (Step)** (这些步骤也可以称为 **Action**) ，使它们看起来像是作为 **一个单独 (Single)、不可分割 (Indivisible) 的步骤** 完成的。
- ## 原子动作 (Atomic Action)
	- 上述整体步骤：
		- 在 **操作系统 和 计算机体系结构 ( [[Computer Architecture]] )** 领域，被称为 **原子动作 (Atomic Action)** 。
		- 在 **数据库管理** 领域，被称为 **事务 (Transaction)** 。
	- ==下文将 CS 领域的所有这类整体步骤，都统称为 **原子动作 (Atomic Action)**==
- ## All-or-nothing Atomicity & Before-or-after Atomicity
	- 存在两种原子性：
		- `All-or-nothing Atomicity` ，用于 **故障恢复 (recovery from failures)**
		  logseq.order-list-type:: number
			- 当一个故障导致某个设计正确的 **原子动作 (Atomic Action)** 在执行过程中失败时，在 **调用者看来** ，这个 **原子动作 (Atomic Action)** ：
				- 要么已经成功完成；
				  logseq.order-list-type:: number
				- 要么完全没有产生任何作用。
				  logseq.order-list-type:: number
					- 通过设计机制，使故障不会导致外部观察到 **不完整的操作结果** 。
			- ==注意，这里说 “在调用者看来” 是想表达：==
				- **需要执行的动作** 或者 **故障恢复** 不一定立即执行了，但是 **调用者** 可以立即看到 **执行的结果** 。
		- `Before-or-after Atomicity` ，用于 **协调并发活动 (coordination of concurrent activities)**
		  logseq.order-list-type:: number
			- 当多个 **原子动作 (Atomic Action)** 并发执行时，在每个 **原子动作 (Atomic Action)** 看来，其他 **原子动作 (Atomic Action)** ：
				- 要么完全发生在它之前；
				  logseq.order-list-type:: number
				- 要么完全发生在它之后。
				  logseq.order-list-type:: number
			- ==即各个 **原子动作 (Atomic Action)** 达到 **串行** 的效果 (虽然实际执行时不一定是串行)==
				- 参见: [[Sequential Execution]]
	- | 对比 | All-or-nothing atomicity | Before-or-after atomicity |
	  | ---- | ---- | ---- |
	  | 解决的问题 | 异常、崩溃导致 **原子动作** 只完成一部分 | 多个 **原子动作** 交错执行，互相干扰 |
	  | 是否要求实际串行 | 不要求 | 可以实际并发，只要效果符合串行执行 |
	  | 无并发时是否仍有意义 | 有，**单线程执行** 也可能中途失败 | 没有并发，就不会出现问题 |
- ## 各语境下的原子性
	- > Designers of database management systems customarily are concerned only with actions that
	  are both all-or-nothing and before-or-after, and they describe such actions as transactions. In
	  addition, they use the term atomic primarily in reference to all-or-nothing atomicity. On the
	  other hand, hardware processor architects customarily use the term atomic to describe an action
	  that exhibits before-or-after atomicity.
	  -- 引自 [Sidebar 9.1: Actions and transactions](https://ocw.mit.edu/courses/res-6-004-principles-of-computer-system-design-an-introduction-spring-2009/de2b7c59e413f58e51eac60acd52efef_atomicity_open_5_0.pdf?utm_source=chatgpt.com)
	- | 具体语境 | 强调哪种原子性 | 备注 |
	  | ---- | ---- | ---- |
	  | 数据库事务 ACID 中的 A | All-or-nothing atomicity | 虽然数据库事务本身也关注 Before-or-after atomicity，但这属于 **事务的隔离性** 的讨论范围，一般不纳入 **事务的原子性** 中来讨论。 |
	  | 数据库事务 ACID 中的 I 设为 **Serializable**  | Before-or-after atomicity | 在数据库事务中 Before-or-after atomicity 由 **隔离性** 保证 |
	  | 并发编程 | Before-or-after atomicity | |
	  | 硬件处理器架构 (hardware processor architects) | Before-or-after atomicity | |
- ## 参考
	- [Chapter 9 Atomicity: All-or-Nothing and Before-or-After](https://ocw.mit.edu/courses/res-6-004-principles-of-computer-system-design-an-introduction-spring-2009/de2b7c59e413f58e51eac60acd52efef_atomicity_open_5_0.pdf)
	  logseq.order-list-type:: number