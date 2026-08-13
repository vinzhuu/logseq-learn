tags:: [[DESIGN.md]]
---

- ## DESIGN.md 的作用
	- `DESIGN.md` 是一种 [[Design System Document]] , 用于 **结构化** 描述 **visual identity (视觉标识)** .
		- 让 [[AI Agent]] 可以生成一致的 UI .
- ## README.md, AGENTS.md & DESIGN.md
	- | 文件 | 谁会读它 |  它定义了哪些内容 |
	  | ---- | ---- | ---- | ---- |
	  |  [[README.md]] | Humans  人类 | 这个项目是什么 |
	  | [[AGENTS.md]] | Coding agents  编码代理 | 如何构建该项目 |
	  | [[DESIGN.md]] | Design agents  设计代理 | 项目的外观与风格 |
- ## DESIGN.md 的来源
	- 来自 [[Stitch]] 项目, 借鉴了 [[DTCG Design Tokens Format]] .
- ## 规范格式
	- ==具体规范参见: [[DESIGN.md Spec]]==
	- 包含两部分:
		- `YAML front matter` : Machine-readable design token (机器可读的 [[Design Token]] )
		  logseq.order-list-type:: number
		- `Markdown body` : Human-readable design rationale (人类可读的设计原理说明)
		  logseq.order-list-type:: number
	- 即 `YAML front matter` 提供 **Design Token**  , `Markdown body` 则提供 **Design Token** 的说明.
- ## 示例
	- ``` yaml
	  ---
	  name: DevFocus Dark
	  colors:
	    primary: "#2665fd"
	    secondary: "#475569"
	    surface: "#0b1326"
	    on-surface: "#dae2fd"
	    error: "#ffb4ab"
	  typography:
	    body-md:
	      fontFamily: Inter
	      fontSize: 16px
	      fontWeight: 400
	  rounded:
	    md: 8px
	  ---
	  
	  # Design System
	  
	  ## Overview
	  A focused, minimal dark interface for a developer productivity tool.
	  Clean lines, low visual noise, high information density.
	  
	  ## Colors
	  - **Primary** (#2665fd): CTAs, active states, key interactive elements
	  - **Secondary** (#475569): Supporting UI, chips, secondary actions
	  - **Surface** (#0b1326): Page backgrounds
	  - **On-surface** (#dae2fd): Primary text on dark backgrounds
	  - **Error** (#ffb4ab): Validation errors, destructive actions
	  
	  ## Typography
	  - **Headlines**: Inter, semi-bold
	  - **Body**: Inter, regular, 14–16px
	  - **Labels**: Inter, medium, 12px, uppercase for section headers
	  
	  ## Components
	  - **Buttons**: Rounded (8px), primary uses brand blue fill
	  - **Inputs**: 1px border, subtle surface-variant background
	  - **Cards**: No elevation, relies on border and background contrast
	  
	  ## Do's and Don'ts
	  - Do use the primary color sparingly, only for the most important action
	  - Don't mix rounded and sharp corners in the same view
	  - Do maintain 4:1 contrast ratio for all text
	  ```
- ## 如何生成 DESIGN.md
	- 有如下方式生成 `DESIGN.md` :
		- 描述风格, 让 Agent 生成
		  logseq.order-list-type:: number
			- 比如, 给 Agent 这样的提示词: `A playful coffee shop ordering app with warm colors, rounded corners, and a friendly feel` , 让它生成  `DESIGN.md` (Stitch 会自动生成, 其他 Agent 可能需要说明让它生成 `DESIGN.md`)
		- 提供品牌素材, 让 Agent 生成
		  logseq.order-list-type:: number
			- 比如, 已经有网站, 图片等素材了, 让 Agent 读取, 来生成 `DESIGN.md` .
		- 人类手写.
		  logseq.order-list-type:: number
			- 适合专业人员.
		- 提供已有代码库, 让 Agent 总结.
		  logseq.order-list-type:: number
			- 使用 **提示词** 或 **Skill** (比如 [[Stitch Design Skills]] )
			- 具体参见: [Import from your codebase](https://stitch.withgoogle.com/docs/design-md/get-instructions/)
- ## 支持 DESIGN.md 的 Agent
	- 目前只有 [[Stitch]] 原生支持 `DESIGN.md` .
	- 其他 Agent 需要在如 [[AGENTS.md]] 之类的文档中指示 Agent 去读取.
- ## 参考
	- [Github Repo - DESIGN.md - README.md](https://github.com/google-labs-code/design.md)
	  logseq.order-list-type:: number
	- [Stitch - DESIGN.md - What is DESIGN.md?](https://stitch.withgoogle.com/docs/design-md/overview/)
	  logseq.order-list-type:: number
-