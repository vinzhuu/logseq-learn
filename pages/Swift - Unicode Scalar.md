tags:: [[Swift Type]], [[Unicode]] 
---

- ## 前置知识
	- 参见: [[Unicode Concept]]
- ## Unicode Scalar Value (Unicode 标量值)
	- Swift 原生的 `String` , 在底层采用 `Unicode Scalar Value` 构建.
	- `Unicode Scalar Value` 是用来描述一个 Unicode 码点的 `21-bit` 数字.
		- 例如 :
			- `U+0061` 表示 `LATIN SMALL LETTER A` , 即 `a` .
			- `U+1F425` 表示 `FRONT-FACING BABY CHICK` , 即 `🐥` .
- ## 为什么是 21 位
	- Unicode 码点范围是: `U+0000` ~ `U+10FFFF`
	- `10FFFF` = 1,114,111
		- 2^20  = 1,048,576  ==不够，还差一点==
		- 2^21 = 2,097,152 ==足够覆盖，且有余裕==
	- 在 Swift 中使用 `UInt32` 类型来存储:
		- 只用到了低 `21 位` , 其余 `11 位` 始终为 `0` .
- ## Unicode 标量类型: `Unicode.Scalar`
	- Swift 中使用 `Unicode.Scalar` 表示 Unicode 标量类型
	- ``` swift
	  // 代理项
	  let surrogate = Unicode.Scalar(0xD800);
	  print(surrogate == nil); // true
	  
	  // 非代理项
	  let unicode = Unicode.Scalar(0x1F468);
	  print(unicode!); // 👨
	  ```
	- 不是所有 **Unicode 码点** 都代表一个字符, **代理项** 不能代表一个字符.
		- 所以, 在 Swift 中为了保证安全, **代理项** 的码点值, 无法被创建为一个 `Unicode.Scalar` 对象.
		- 所以, 可以说: `全量 Unicode Scalar` = `Unicode 全量码点` - `Unicode 代理项码点` .
- ## Extended Grapheme Clusters (扩展字形簇)
	- 可以使用多个 `Unicode Scalar` 表示组合字符:
	- ``` swift
	  let eAcute: Character = "\u{E9}"                         // é
	  let combinedEAcute: Character = "\u{65}\u{301}"          // e followed by ́
	  // eAcute is é, combinedEAcute is é
	  
	  let precomposed: Character = "\u{D55C}"                  // 한
	  let decomposed: Character = "\u{1112}\u{1161}\u{11AB}"   // ᄒ, ᅡ, ᆫ
	  // precomposed is 한, decomposed is 한
	  ```
- ## 参考
	- [Swift Language Guide - Strings and Characters](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/stringsandcharacters)
	  logseq.order-list-type:: number
	- GPT
	  logseq.order-list-type:: number