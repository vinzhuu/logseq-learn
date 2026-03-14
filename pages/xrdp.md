tags:: [[RDP]]
---

- ## 官方资料
	- https://www.xrdp.org/
	- https://github.com/neutrinolabs/xrdp
- ## 啥是 xrdp
	- `xrdp` 是 Microsoft [[RDP]] (远程桌面协议) 的 **服务端** 的 一个 **开源实现** , 它允许以图形方式控制远程系统。
	- xrdp server 可以用如下客户端连接:
		- FreeRDP
		  logseq.order-list-type:: number
		- rdesktop
		  logseq.order-list-type:: number
		- KRDC
		  logseq.order-list-type:: number
		- NeutrinoRDP 
		  logseq.order-list-type:: number
		- Windows MSTSC
		  logseq.order-list-type:: number
		- Microsoft Remote Desktop Client (for Windows, macOS, iOS and Android) ==区别于 MSTSC==
		  logseq.order-list-type:: number
- ## 常用命令
	- ### 查看 xrdp 服务状态
		- `sudo systemctl status xrdp`
	-