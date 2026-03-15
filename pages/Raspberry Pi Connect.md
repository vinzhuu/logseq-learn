tags:: [[Raspberry Pi]]
---

- ## 学习路线
	- [[Raspberry Pi Connect: Concept]]
	  logseq.order-list-type:: number
	- [[Raspberry Pi Connect: 连接树莓派]]
	  logseq.order-list-type:: number
- ## 常用命令
	- ### 更新
		- ``` zsh
		  sudo apt update
		  # rpi-connect
		  sudo apt install --only-upgrade rpi-connect
		  # rpi-connect-lite 
		  sudo apt install --only-upgrade rpi-connect-lite 
		  ```
	- ### 退出登录
		- ``` zsh
		  rpi-connect signout
		  ```
	- ### 卸载
		- ``` zsh
		  sudo apt remove --purge rpi-connect
		  ```
	- ### 诊断问题
		- ``` zsh
		  rpi-connect doctor
		  ```