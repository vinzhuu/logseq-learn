tags:: [[Raspberry Pi]], [[RDP]] 
---

- ## Microsoft Remote Desktop Client + xrdp server
	- 连接步骤:
		- 服务端: Microsoft RDP 协议的开源实现, xrdp
		  logseq.order-list-type:: number
			- 树莓派执行 `sudo apt-get install xrdp` 安装 [[xrdp]] .
			- 若安装出现如下问题：
			- ```sh
			  E: Failed to fetch http://raspbian.raspberrypi.org/raspbian/pool/main/x/xterm/xterm_366-1_armhf.deb  404  Not Found [IP: 93.93.128.193 80]
			  E: Unable to fetch some archives, maybe run apt-get update or try with --fix-missing?
			  ```
			- 则先执行 `sudo apt-get update` 更新, 再执行上述安装命令即可.
		- 客户端: Microsoft Remote Desktop Client (for Windows, macOS, iOS and Android).
		  logseq.order-list-type:: number
			- Microsoft Remote Desktop Client  可以使用 `mstsc -admin` 打开.
-