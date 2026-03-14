tags:: [[Raspberry Pi]], [[SSH]]
---

- ## 安装系统时开启
	- 参考 [[Raspberry Pi: 安装系统]]
- ## Desktop 开启
	- 进入 `Preferences > Control Centre > Interfaces` .
	  logseq.order-list-type:: number
	- 勾选 `SSH`
	  logseq.order-list-type:: number
- ## Terminal 开启
	- 树莓派 Terminal 执行 `sudo raspi-config` .
	  logseq.order-list-type:: number
	- 选择 `Interfacing Options` .
	  logseq.order-list-type:: number
	- 选择 `SSH` .
	  logseq.order-list-type:: number
	- 选择 `Yes` 开启.
	  logseq.order-list-type:: number
- ## 创建 SSH 文件
	- 创建名为 `ssh` 的空文件.
	  logseq.order-list-type:: number
		- 两种方式:
			- SD 卡连接我们已有的设备, 在 SD 卡中创建 `ssh` 文件.
			  logseq.order-list-type:: number
			- 键/鼠/显示器 连接树莓派, 创建 `ssh` 文件: `sudo touch /boot/firmware/ssh`
			  logseq.order-list-type:: number
	- 重启树莓派: `sudo reboot`
	  logseq.order-list-type:: number
- ## 参考
	- [Enable the SSH server](https://www.raspberrypi.com/documentation/computers/remote-access.html#enable-the-ssh-server)
	  logseq.order-list-type:: number