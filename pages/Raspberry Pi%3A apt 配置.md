tags:: [[Raspberry Pi]], [[apt]]
---

- ## 修改 apt 下载源
	- 备份原文件.
	  logseq.order-list-type:: number
		- ``` zsh
		  sudo cp /etc/apt/sources.list.d/raspi.sources /etc/apt/sources.list.d/raspi.sources.bak
		  sudo cp /etc/apt/sources.list.d/debian.sources /etc/apt/sources.list.d/debian.sources.bak
		  ```
	- 编辑 `raspi.sources`  .
	  logseq.order-list-type:: number
		- 执行 `sudo nano /etc/apt/sources.list.d/raspi.sources` .
		  logseq.order-list-type:: number
		- 填入:
		  logseq.order-list-type:: number
			- ``` zsh
			  Types: deb
			  URIs: https://mirrors.tuna.tsinghua.edu.cn/raspberrypi/debian/
			  Suites: trixie
			  Components: main
			  Signed-By: /usr/share/keyrings/raspberrypi-archive-keyring.pgp
			  ```
	- 编辑 `debian.sources` .
	  logseq.order-list-type:: number
		- 执行 `sudo nano /etc/apt/sources.list.d/debian.sources` .
		  logseq.order-list-type:: number
		- 填入:
		  logseq.order-list-type:: number
			- ``` zsh
			  # Debian 主源
			  Types: deb
			  URIs: https://mirrors.tuna.tsinghua.edu.cn/debian/
			  Suites: trixie trixie-updates
			  Components: main contrib non-free non-free-firmware
			  Signed-By: /usr/share/keyrings/debian-archive-keyring.pgp
			  
			  # Debian 安全更新源
			  Types: deb
			  URIs: https://mirrors.tuna.tsinghua.edu.cn/debian-security/
			  Suites: trixie-security
			  Components: main contrib non-free non-free-firmware
			  Signed-By: /usr/share/keyrings/debian-archive-keyring.pgp
			  ```
	- 执行 `sudo apt update` .
	  logseq.order-list-type:: number