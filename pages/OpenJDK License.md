tags:: [[OpenJDK]], [[License]]
---

- ## OpenJDK 使用的 License
	- 一般称为: [[GPLv2]] + Classpath Exception
- ## OpenJDK 使用的 License原文
	- OpenJDK 网站: [GNU General Public License, version 2, with the Classpath Exception](https://openjdk.org/legal/gplv2+ce.html)
	  logseq.order-list-type:: number
	- OpenJDK 源码: [OpenJDK LICENSE](https://github.com/openjdk/jdk/blob/master/LICENSE)
	  logseq.order-list-type:: number
- ## OpenJDK 使用的 License 与 GPLv2 原文的区别
	- | 段落 | 位置 | GPLv2 原文 | OpenJDK LICENSE |
	  | -----------| ----------- | ----------- | ----------- |
	  | 开头的版权声明 | `Copyright (C) 1989, 1991 Free Software Foundation, Inc.` 文本下的内容 | `<https://fsf.org/>` | `59 Temple Place, Suite 330, Boston, MA 02111-1307 USA` |
	  | Preamble | `Preamble` 标题后的第一个段落中说的 **可替换的 License**   | `GNU Lesser General Public License` | `GNU Library General Public License` |
	  | How to Apply These Terms to Your New Programs | `one line to give ...`   | `one line to give the program's name and an idea of what it does.` | `One line to give the program's name and a brief idea of what it does.` |
	  | How to Apply These Terms to Your New Programs | `Copyright (C) ...`   | `Copyright (C) yyyy  name of author` | `Copyright (C) <year> <name of author>` |
	  | How to Apply These Terms to Your New Programs | `if not, ...`   | `if not, see <https://www.gnu.org/licenses/>.` | `if not, write to the Free Software Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA 02111-1307 USA` |
	  | How to Apply These Terms to Your New Programs | 引号问题   | show w / show c / Gnomovision 都使用 `' 包裹 (一个 backtick 和 一个单引号) | show w / show c / Gnomovision 都使用一对单引号包裹 |
	  | How to Apply These Terms to Your New Programs | `signature of ...`   | `signature of Moe Ghoul, 1 April 1989` 和 `Moe Ghoul, President of Vice` | `signature of Ty Coon, 1 April 1989` 和 `Ty Coon, President of Vice` |
	  | How to Apply These Terms to Your New Programs | `If this is what you want to do, use the ...`   | `use the GNU Lesser General Public License instead of this Licens` | `use the GNU Library General Public License instead of this License` |
	  | 新增段落 | Exception | - | 添加了 "CLASSPATH" EXCEPTION TO THE GPL |
	- ==总结就是:==
		- 非关键文本修改
		  logseq.order-list-type:: number
			- 将 `GNU Lesser General Public License` 换成 `GNU Library General Public License` .
			  logseq.order-list-type:: number
				- `GNU Library General Public License` 是 `GNU Lesser General Public License` 的旧名称.
					- 参见: [[LGPL 的旧名称]]
				- OpenJDK LICENSE 一直保留着旧名称, 而未修改.
			- 其它非关键文本修改 (地址改网址, 修改人名等).
			  logseq.order-list-type:: number
				- 实际上, 包括 `GNU Library General Public License` 在内的所有文本修改, 都是因为 OpenJDK 使用的是 GPLv2 的历史版本 .
					- 参见: [[GPLv2 的历史版本]]
				- OpenJDK LICENSE 一直保留 GPLv2 历史旧文本, 而未修改.
		- 添加 "CLASSPATH" EXCEPTION TO THE GPL 段落.
		  logseq.order-list-type:: number
- ## Classpath Exception
	- OpenJDK 的 Classpath Exception 在 [[GNU Classpath Exception]] 原文的基础上, 在开头额外加了一段描述:
		- `Certain source files distributed by Oracle America ...`
		- 大致是在说: 只有在开头有如下描述的 **源文件 (source file)** , 才遵守 Classpath Exception
			- > Oracle designates this particular file as subject to the "Classpath" exception as provided by Oracle in the LICENSE file that accompanied this code.
	- Classpath Exception 正文内容, 与 [[GNU Classpath Exception]]  一致.
- ## 参考
	- [GNU General Public License, version 2, with the Classpath Exception](https://openjdk.org/legal/gplv2+ce.html)
	  logseq.order-list-type:: number