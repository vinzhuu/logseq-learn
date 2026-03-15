tags:: [[Raspberry Pi Connect]]
---

- ## Connect 是 用户级服务
	- Connect 作为用户级服务运行, 而非 root 用户 .
		- 因此, Connect 仅在账户登录设备时有运行.
- ## 保持 Connect 常驻方法
	- 有如下几种方法:
		- 树莓派开启自动登录 (==貌似都是默认开启的==)
		  logseq.order-list-type:: number
			- `sudo raspi-config` > 选择 **System Options** > 选择 **Auto Login** .
				- **Would you like to automatically log in to the console?**   > 选择 **Yes** 开启 ==针对 Remote Shell==
				- **Would you like to automatically log in to the desktop?**   > 选择 **Yes** 开启 ==针对 Screen Sharing==
		- 启用用户驻留 (效果就是用户不登录, 也能运行用户级服务) ==仅针对 Remote Shell==
		  logseq.order-list-type:: number
			- 一些禁用自动登录的设备, 可能就要用到.
			- ``` zsh
			  # 为当前登录用户开启驻留
			  loginctl enable-linger
			  # 为当前登录用户关闭驻留
			  loginctl disable-linger
			  
			  # 为指定用户开启驻留
			  loginctl enable-linger pi
			  # 为指定用户关闭驻留
			  loginctl disable-linger pi
			  ```
			- 查看用户驻留状态
				- ``` zsh
				  # 查看指定用户驻留状态
				  loginctl show-user pi
				  ```
				- `Linger=yes` 即为开启.
- ## 参考
	- [Enable remote shell at all times](https://www.raspberrypi.com/documentation/services/connect.html#enable-remote-shell-at-all-times)
	  logseq.order-list-type:: number