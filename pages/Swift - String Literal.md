tags:: [[Swift Type]]
---

- ## Single-line String Literals
	- ``` swift
	  let someString = "Some string literal value"
	  ```
- ## Special Characters
	- ### Escaped special characters
		- `\0` (null character)
		- `\\` (backslash)
		- `\t` (horizontal tab)
		- `\n` (line feed)
		- `\r` (carriage return)
		- `\"` (double quotation mark)
		- `\'` (single quotation mark)
	- ### Unicode scalar value
		- `\u{n}` (n 为 1-8 位的 16 进制数)
		- ``` swift
		  let wiseWords = "\"Imagination is more important than knowledge\" - Einstein"
		  // "Imagination is more important than knowledge" - Einstein
		  let dollarSign = "\u{24}"        // $,  Unicode scalar U+0024
		  let blackHeart = "\u{2665}"      // ♥,  Unicode scalar U+2665
		  let sparklingHeart = "\u{1F496}" // 💖, Unicode scalar U+1F496
		  ```
- ## Multiline String Literals
	- 使用 **三个双引号** 可以定义多行字符串 .
	- ### 缩进
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
	- ### 行尾 \
		- ``` swift
		  let softWrappedQuotation = """
		  The White Rabbit put on his spectacles.  "Where shall I begin, \
		  please your Majesty?" he asked.
		  
		  "Begin at the beginning," the King said gravely, "and go on \
		  till you come to the end; then stop."
		  """
		  ```
		- 每一行末尾的 `\` 不是字符串的一部分，只是用来表明最终字符串不换行 (声明时换行只是让代码更可读)。
	- ### 双引号转义
		- 多行字符串中可以直接使用 `"` , 但如果要在多行字符串中使用 `"""` , 则需要至少转义其中的一个引号。
		- ``` swift
		  let threeDoubleQuotationMarks = """
		  Escaping the first quotation mark \"""
		  Escaping all three quotation marks \"\"\"
		  """
		  ```
- ## 参考
	- [Swift Language Guide - Strings and Characters](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/stringsandcharacters)
	  logseq.order-list-type:: number