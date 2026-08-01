tags:: [[Swift Subscript]]
---

- ## 声明 Subscript
	- 声明 `Subscript` 的语法, 相当于 `Instance Method` 的语法 和 `Computed Property` 的语法的结合.
		- 参见: [[Swift Instance Method]] 和 [[Swift Computed Property]]
		- **函数体** 部分, 与 `Computed Property` **函数体** 的语法完全一致.
		- **函数体** 之外的部分, 除了如下内容之外, 与 `Instance Method` 的语法完全一致:
			- 没有 `func` 关键字 .
			  logseq.order-list-type:: number
			- 方法名称必须是 `subscript` .
			  logseq.order-list-type:: number
			- 不能声明 `in-out Parameter` .
			  logseq.order-list-type:: number
	- ``` swift
	  subscript(index: Int) -> Int {
	      get {
	          // Return an appropriate subscript value here.
	      }
	      set(newValue) {
	          // Perform a suitable setting action here.
	      }
	  }
	  
	  // 只有 get 时的简写 (只读, 禁止赋值)
	  subscript(index: Int) -> Int {
	      // Return an appropriate subscript value here.
	  }
	  ```
- ## 使用 Subscript
	- 语法: 在 **实例名称** 后面的 `[]` 中传入 **一个或多个值** .
		- 如果声明了 `set` , 则可以使用 `[]` 语法赋值;
		- 如果没有声明 `set` , 则禁止使用 `[]` 语法赋值;
	- 示例:
		- ``` swift
		  struct TimesTable {
		      let multiplier: Int
		      subscript(index: Int) -> Int {
		          return multiplier * index
		      }
		  }
		  let threeTimesTable = TimesTable(multiplier: 3)
		  print("six times three is \(threeTimesTable[6])")
		  // Prints "six times three is 18".
		  ```
- ##  Subscript Overloading (下标重载)
	- 我们可以为 **单个类型** 定义 **多个下标** , 这被称为 `subscript overloading`
		- 调用时, 可以根据传递给下标的 **索引值类型** , 来选择使用哪个 **下标**.
- ## 多个参数
	- 虽然下标一般都是只接收一个参数, 但其实, 下标 也可以接受 **多个参数** .
	- ``` swift
	  struct Matrix {
	      let rows: Int, columns: Int
	      var grid: [Double]
	      init(rows: Int, columns: Int) {
	          self.rows = rows
	          self.columns = columns
	          grid = Array(repeating: 0.0, count: rows * columns)
	      }
	      func indexIsValid(row: Int, column: Int) -> Bool {
	          return row >= 0 && row < rows && column >= 0 && column < columns
	      }
	      subscript(row: Int, column: Int) -> Double {
	          get {
	              assert(indexIsValid(row: row, column: column), "Index out of range")
	              return grid[(row * columns) + column]
	          }
	          set {
	              assert(indexIsValid(row: row, column: column), "Index out of range")
	              grid[(row * columns) + column] = newValue
	          }
	      }
	  }
	  ```
- ## 参考
	- [Swift Guide - Subscripts#Subscript Syntax](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/subscripts#Subscript-Syntax)
	  logseq.order-list-type:: number