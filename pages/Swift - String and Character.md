tags:: [[Swift Type]]
---

- ## String Literals
	- ### Single-line String Literals
		- ``` swift
		  let someString = "Some string literal value"
		  ```
	- ### Special Characters
		- #### Escaped special characters
			- `\0` (null character)
			- `\\` (backslash)
			- `\t` (horizontal tab)
			- `\n` (line feed)
			- `\r` (carriage return)
			- `\"` (double quotation mark)
			- `\'` (single quotation mark)
		- #### Unicode scalar value
			- `\u{n}` (n 为 1-8 位的 16 进制数)
			- ``` swift
			  let wiseWords = "\"Imagination is more important than knowledge\" - Einstein"
			  // "Imagination is more important than knowledge" - Einstein
			  let dollarSign = "\u{24}"        // $,  Unicode scalar U+0024
			  let blackHeart = "\u{2665}"      // ♥,  Unicode scalar U+2665
			  let sparklingHeart = "\u{1F496}" // 💖, Unicode scalar U+1F496
			  ```
	- ### Multiline String Literals
		- 使用 **三个双引号** 可以定义多行字符串 .
		- #### 缩进
			- ``` swift
			  let apples = 3
			  let oranges = 5
			  let quotation = """
			         Even though there's whitespace to the left,
			      the actual lines aren't indented.
			              Except for this line.
			          Double quotes (") can appear without being escaped.
			  
			          I still have \(apples + oranges) pieces of fruit.
			      """
			  print(quotation)
			  
			  // 最终字符串
			     Even though there's whitespace to the left,
			  the actual lines aren't indented.
			          Except for this line.
			      Double quotes (") can appear without being escaped.
			  
			      I still have \(apples + oranges) pieces of fruit.
			  ```
			- 实际的字符串的值，每一行将会参照结尾 `"""` (closing quotation marks) 的缩进位置去掉缩进。
		- #### 末尾 \
			- ``` swift
			  let softWrappedQuotation = """
			  The White Rabbit put on his spectacles.  "Where shall I begin, \
			  please your Majesty?" he asked.
			  
			  "Begin at the beginning," the King said gravely, "and go on \
			  till you come to the end; then stop."
			  """
			  ```
			- 每一行末尾的 `\` 不是字符串的一部分，只是用来表明最终字符串不换行 (声明时换行只是让代码更可读)。
		- #### 双引号转义
			- 多行字符串中可以直接使用 `"` , 但如果要在多行字符串中使用 `"""` , 则需要至少转义其中的一个引号。
			- ``` swift
			  let threeDoubleQuotationMarks = """
			  Escaping the first quotation mark \"""
			  Escaping all three quotation marks \"\"\"
			  """
			  ```
- ## String Interpolation
	- 使用 `\(变量名)` 和 `\(表达式)` 在字符串中插入 变量 或 表达式 **当前的值** 。
	- ``` swift
	  let apples = 3
	  let oranges = 5
	  let appleSummary = "I have \(apples) apples."
	  let fruitSummary = "I have \(apples + oranges) pieces of fruit."
	  ```
- ## Extended String Delimiter
	- ### 避免特殊字符的特殊效果
		- 使用 `#"...."#` 可以避免触发 **特殊字符** 的特殊效果, 而是直接将其字面量作为字符串的一部分.
			- ==注意, 字符串首尾的 `#` 可以只有一个, 也可以有多个.==
		- 包括:
			- 转义字符.
			  logseq.order-list-type:: number
			- 字符串插值.
			  logseq.order-list-type:: number
			- 三双引号: `"""`
			  logseq.order-list-type:: number
		- ``` swift
		  // 这里没有换行符, 直接 \n 字符串
		  let lines = #"Line 1\nLine 2"#
		  
		  // 这里 """ 不是作为多行字符串的结束标识, 而是作为字符串的一部分
		  let threeMoreDoubleQuotationMarks = #"""
		  Here are three more double quotes: """
		  """#
		  ```
	- ###  允许特殊效果
		- 如果需要触发 **特殊字符** 的特殊效果, 则必须在转义字符 `\` 后, 加上与首尾 `#` 数量相同的 `#`
			- ``` swift
			  // Line 1 
			  // Line 2
			  #"Line 1\#nLine 2"#
			  
			  // Line 1\#nLine 2
			  ##"Line 1\#nLine 2"##
			  
			  // Line 1 
			  // Line 2
			  ##"Line 1\##nLine 2"##
			  ```
	- ### 多个 `#`
		- 如下情况, 字符串首尾需要多个 `#` .
			- 字符串内部有一个或多个连续的 `#`
			  logseq.order-list-type:: number
				- ``` swift
				  // 报错
				  let s1 = #"He said "#Hello""#;
				  // 正常
				  let s2 = ##"He said "#Hello""##;
				  
				  // 报错
				  let s3 = ##"He said "##Hello""##;
				  // 正常
				  let s4 = ###"He said "##Hello""###;
				  ```
			- 将转义字符 `\` 后的 `#` 视为普通字符.
			  logseq.order-list-type:: number
				- ``` swift
				  // 这样会被处理为插值
				  #"\#(value)"#
				  
				  // 这样会被处理为普通字符
				  ##"\#(value)"##
				  ```
- ## Empty String
	- ### Initialize an Empty String
		- ``` swift
		  var emptyString = ""               // empty string literal
		  var anotherEmptyString = String()  // initializer syntax
		  // these two strings are both empty, and are equivalent to each other
		  ```
	- ### isEmpty
		- ``` swift
		  if emptyString.isEmpty {
		      print("Nothing to see here")
		  }
		  // Prints "Nothing to see here".
		  ```
-
- ---
- ## 参考
	- [Swift Language Guide - Strings and Characters](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/stringsandcharacters)
	  logseq.order-list-type:: number