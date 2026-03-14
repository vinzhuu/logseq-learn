alias:: [[设计原则]]
---

- ## 七大设计原则
	- 单一职责原则 (Single Responsibility Principle, SRP)
	  logseq.order-list-type:: number
	- 开闭原则 (Open-Closed Principle, OCP)
	  logseq.order-list-type:: number
	- 里氏替换原则 (Liskov Substitution Principle, LSP)
	  logseq.order-list-type:: number
	- 接口隔离原则 (Interface Segregation Principle, ISP)
	  logseq.order-list-type:: number
	- 依赖倒置原则 (Dependency Inversion Principle, DIP)
	  logseq.order-list-type:: number
	- 迪米特法则 (Law of Demeter, LoD)
	  logseq.order-list-type:: number
	- 合成复用原则 (Composite Reuse Principle, CRP)
	  logseq.order-list-type:: number
	- 其中，前五项被合称为 **SOLID 原则** ，由 [Robert C. Martin](https://en.wikipedia.org/wiki/Robert_C._Martin) 在论坛与他人讨论整理得出，后来他在 [架构整洁之道 Clean Architecture](https://weread.qq.com/web/reader/480322f072021a3248038c8k32932b102423295c76ac7d9) 也有对 SOLID 的讲解。
- ## 单一职责原则
	- Single Responsibility Principle, SRP
	- > 即 **一个类应该只有一个职责，那么也就有且仅有一个引起它变化的原因**
	- 并不是一个类只能有一个函数，而是说这个类中的函数所做的工作是高度相关的！！！
	- 当然，**职责** 的粒度，就因项目而异了。
- ## 开闭原则
	- Open-Closed Principle, OCP
	- > 对扩展开放，对修改关闭。
	- 当软件需要变化时，应该尽可能通过扩展来实现变化，而不是修改原有的代码。
- ## 里氏替换原则
	- Liskov Substitution Principle, LSP
	- > 子类可以扩展父类的功能，但不能改变其原有含义。
	- 也就是说，程序中所有用到父类的地方，可以使用子类代替；所以父类已经实现的方法，最好不要去重写。
- ## 接口隔离原则
	- Interface Segregation Principle, ISP
	- > 类不应该依赖它不需要的接口
	- 如果依赖的接口中有自己用不到的方法，则说明这个接口应该进行拆分。
- ## 依赖倒置原则
	- Dependency Inversion Principle, DIP
	- > 程序应该依赖于抽象，而不是具体实现。
- ## 迪米特法则
	- Law of Demeter, LoD
	- > 对于依赖的类的内部实现，我们知道的越少越好，所有的逻辑都应尽可能封装在依赖的类中。
- ## 合成复用原则
	- Composite Reuse Principle, CRP
	- > 尽量使用 合成或聚合 关系，尽可能减少继承关系。
	-
- ---
- ## 参考
	- [软件设计模式——七大设计原则](https://hjk.life/posts/design-patterns-principles/)
	  logseq.order-list-type:: number
	- [设计模式原则](https://thinkkeep.github.io/design-patterns/zh/uml/design-principle.html)
	  logseq.order-list-type:: number
	- [设计模式——七大原则](https://it-blog-cn.com/blogs/design_mode/seven_principle.html)
	  logseq.order-list-type:: number
	- [架构整洁之道 Clean Architecture](https://weread.qq.com/web/reader/480322f072021a3248038c8k32932b102423295c76ac7d9)
	  logseq.order-list-type:: number