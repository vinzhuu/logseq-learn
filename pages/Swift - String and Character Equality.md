tags:: [[Swift Type]]
---

- ## 如何比较 String
	- 比较两个 `String` 是否相等:
		- 就是比较两个 `String` 的每个 **用户感知字符 (Extended Grapheme Clusters)** 是否相等.
	- 比较两个 **用户感知字符 (Extended Grapheme Clusters)** 是否相等:
		- 就是比较它们是否具有相同的 **语言意义** 和 **外观** .
- ## 注意
	- 同一 **用户感知字符 (Extended Grapheme Clusters)** 的 预组形式 和 分解形式, 被视为相等. (参见: [[Unicode Concept]] )
	  logseq.order-list-type:: number
		- ``` swift
		  // "Voulez-vous un café?" using LATIN SMALL LETTER E WITH ACUTE
		  let eAcuteQuestion = "Voulez-vous un caf\u{E9}?"
		  
		  // "Voulez-vous un café?" using LATIN SMALL LETTER E and COMBINING ACUTE ACCENT
		  let combinedEAcuteQuestion = "Voulez-vous un caf\u{65}\u{301}?"
		  
		  if eAcuteQuestion == combinedEAcuteQuestion {
		      print("These two strings are considered equal") // These two strings are considered equal
		  }
		  ```
	- 两个 **用户感知字符 (Extended Grapheme Clusters)**  视觉上相似, 并不意味着它们具有相同的 **语言意义** .
	  logseq.order-list-type:: number
		- ``` swift
		  // 英文字母: A
		  let latinCapitalLetterA: Character = "\u{41}"
		  
		  // 俄语字母: А
		  let cyrillicCapitalLetterA: Character = "\u{0410}"
		  
		  if latinCapitalLetterA != cyrillicCapitalLetterA {
		      print("These two characters aren't equivalent.") // These two characters aren't equivalent.
		  }
		  ```
- ## Prefix and Suffix
	- `String` 的 `hasPrefix(_:)` 方法: 比较字符串是否含有某个前缀.
	- `String` 的 `hasSuffix(_:)` 方法: 比较字符串是否含有某个后缀.
	- ``` swift
	  let hello: String = "hello, world";
	  print(hello.hasPrefix("he")); // true
	  print(hello.hasPrefix("hell")); // true
	  print(hello.hasSuffix("ld")); // true
	  ```
- ## 参考
	- [Swift Language Guide - Strings and Characters](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/stringsandcharacters)
	  logseq.order-list-type:: number
	-