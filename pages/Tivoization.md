tags:: [[CS Glossary]]
---

- ## Tivoization 的含义
	- 这个词源自 **TiVo** 这家公司:
		- **TiVo** 使用 GPL 软件, 允许用户获得相应的源码.
		- 但 **TiVo** 的设备, 会通过 **数字签名等机制** 阻止用户运行修改后软件版本.
		- 所以, 大家把这种行为称为 **Tivoization** , 可以翻译为 `TiVo 式限制` .
	- 所以 Tivoization 的含义就是:
		- > 给你修改软件的自由，但用 **硬件/签名机制** 阻止你运行修改后的软件 .
- ## Tivoized Blob & Tivoized Device
	- Tivoization 行为中的硬件被称为 [[Tivoized Device]] , 软件被称为 [[Tivoized Blob]] .
- ## Tivoization 与 Open Source & Free Software
	- [[Tivoized Blob]] 的 **源码** 虽然是自由的, 但是 **可执行文件** 却不是自由的.
	- 这或许符合 [[Open Source Definition]] , 但不符合 [[Free Software]] 标准.
- ## GPLv3 禁止 Tivoization 行为
	- 禁止 Tivoization 正是 [[GPLv3]] 最重要的新增内容之一.
	- 但可惜的是, Linux 并没有采用 [[GPLv3]] .
		- 所以, 有很多安卓设备, 使用 **Tivoized Linux 可执行文件** (即 安卓系统) .
- ## 参考
	- [GNU - Proprietary Tyrants](https://www.gnu.org/proprietary/proprietary-tyrants.html#content)
	  logseq.order-list-type:: number
	- [GNU - Tivoization](https://www.gnu.org/philosophy/tivoization.html)
	  logseq.order-list-type:: number