tags:: [[C#]]
---

- https://learn.microsoft.com/en-us/dotnet/
- `.NET` 不是一门编程语言, 而是一个运行 `C#` 程序的平台或技术体系.
	- 可以这样类比:
		- ``` zsh
		  .NET               Java 平台/生态
		    ↓                    ↓
		  .NET SDK            JDK
		  .NET Runtime        Java Runtime
		  CLR                 JVM
		  C#                  Java
		  ASP.NET Core        Spring 等 Web 框架
		  ```
	- 类比支持多语言:
		- ``` zsh
		  C#  ──┐
		  F#  ──┼──→ IL / CIL ──→ CLR ──→ 机器码
		  VB  ──┘
		  
		  Java   ─┐
		  Kotlin ─┼──→ JVM Bytecode ──→ JVM ──→ 机器码
		  Scala  ─┘
		  ```
-