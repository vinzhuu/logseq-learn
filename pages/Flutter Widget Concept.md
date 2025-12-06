tags:: [[Flutter]]
---

- ## Flutter's own UI Implementation
	- Flutter 有其自己用 Dart 实现的各类 UI 控件, 不必调用 **系统原生控件** .
	- 这有如下好处:
		- 开发者可以在 Flutter 控件的基础上扩展, 而不受 OS 扩展点的限制.
		  logseq.order-list-type:: number
		- 避免了 Flutter 代码 和 平台代码 之间来回切换带来的 **性能问题** .
		  logseq.order-list-type:: number
		- 不依赖具体的 OS , 保证 Flutter 应用在各个 OS 上外观和体验一致.
		  logseq.order-list-type:: number
- ## Everything is a Widget
	- 在 Flutter 中 , **万物皆组件** .
	- ==如下代码中, 所有实例化的类, 都是组件.==
		- ``` dart
		  import 'package:flutter/material.dart';
		  import 'package:flutter/services.dart';
		  
		  void main() => runApp(const MyApp());
		  
		  class MyApp extends StatelessWidget {
		    const MyApp({super.key});
		  
		    @override
		    Widget build(BuildContext context) {
		      return MaterialApp(
		        home: Scaffold(
		          appBar: AppBar(title: const Text('My Home Page')),
		          body: Center(
		            child: Builder(
		              builder: (context) {
		                return Column(
		                  children: [
		                    const Text('Hello World'),
		                    const SizedBox(height: 20),
		                    ElevatedButton(
		                      onPressed: () {
		                        print('Click!');
		                      },
		                      child: const Text('A button'),
		                    ),
		                  ],
		                );
		              },
		            ),
		          ),
		        ),
		      );
		    }
		  }
		  ```
- ## Composition
	- Flutter 中, Widget 通常由许多 **小型的, 单一用途** 其他 Widget 组合而成.
		- 组件之间基于 **组合 (composition)** 形成 **层次结构 (hierarchy)** .
		- 每个组件都嵌套在其父组件内, 并可以从父组件接收 **上下文 (context)** .
	- 即便是像 *内边距*  和 *对齐* 这样的基本功能, Flutter 也是通过包装相应的组件实现, 而不是配置组件的属性.
		- 比如, 要让一个组件居中, 是在其外部包一个 `Center` 组件, 而不是配置这个组件的某个属性值.
	- Flutter 使用这种组合的方法, 实现了一些 **实用组件** .
		- 比如 `Container` 就是由 `LimitedBox` 、 `ConstrainedBox` 等多个组件组合而成的.
		- 我们可以对这些实用组件再进行组合, 以 **二次封装** 自己的组件;
		- 或者, 阅读其源码, 了解其组合方式, 以其为灵感创建 **新组件** .
- ## Build a widget
	- ### Widget State
		- Flutter 中有两种组件:
			- `StatelessWidget` : 无状态组件, 即其没有随时间变化的 `class` 属性.
			  logseq.order-list-type:: number
				- 如 `Padding` ,  `Text` 和 `Icon` .
				- 我们大多数创建的也是这类组件.
			- `StatefulWidget` : 有状态组件, 即其有随时间变化的 `class` 属性.
			  logseq.order-list-type:: number
	- ### Build a StatelessWidget
		- 创建一个 无状态组件 , 我们需要:
			- 继承 `StatelessWidget` .
			  logseq.order-list-type:: number
			- 要实现 `build()` 方法 , 返回一个 `Widget` 对象.
			  logseq.order-list-type:: number
		- ``` dart
		  class PaddedText extends StatelessWidget {
		    const PaddedText({super.key});
		  
		    @override
		    Widget build(BuildContext context) {
		      return Padding(
		        padding: const EdgeInsets.all(8.0),
		        child: const Text('Hello, World!'),
		      );
		    }
		  }
		  ```
	- ### Build a StatefulWidget
		- 创建一个 有状态组件 , 我们需要:
			- 继承 `StatefulWidget` .
			  logseq.order-list-type:: number
			- 实现 `createState()` 方法, 返回一个继承自 `State<T>` 的对象.
			  logseq.order-list-type:: number
			- 继承自 `State<T>` 的类, 需要实现 `build()` 方法 , 返回一个 `Widget` 对象.
			  logseq.order-list-type:: number
		- 每当我们修改 `State<T>` 对象的属性时, 我们都应该调用 `setState()` 方法, 以通知框架再次调用 `State` 的 `build` 方法来更新用户界面.
		- ``` dart
		  class CounterWidget extends StatefulWidget {
		    @override
		    State<CounterWidget> createState() => _CounterWidgetState();
		  }
		  
		  class _CounterWidgetState extends State<CounterWidget> {
		    int _counter = 0;
		  
		    void _incrementCounter() {
		      setState(() {
		        _counter++;
		      });
		    }
		  
		    @override
		    Widget build(BuildContext context) {
		      return Text('$_counter');
		    }
		  }
		  ```
	- ### 总结
		- 不管是 `StatelessWidget` 还是 `StatefulWidget` , 最终渲染用户界面时, 都要调用 `build()` 方法.
-
- ## 参考
	- [Flutter Docs - Widgets](https://docs.flutter.dev/get-started/fundamentals/widgets)
	  logseq.order-list-type:: number
	- [Flutter Docs - Flutter architectural overview](https://docs.flutter.dev/resources/architectural-overview)
	  logseq.order-list-type:: number