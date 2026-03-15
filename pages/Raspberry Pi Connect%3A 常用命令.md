tags:: [[Raspberry Pi Connect]]
---

- ## 启停看
	- ``` zsh
	  # 开启
	  rpi-connect on
	  # 关闭
	  rpi-connect off
	  # 重启
	  rpi-connect restart
	  # 查看
	  rpi-connect status
	  ```
- ## 更新
	- ``` zsh
	  sudo apt update
	  # rpi-connect
	  sudo apt install --only-upgrade rpi-connect
	  # rpi-connect-lite 
	  sudo apt install --only-upgrade rpi-connect-lite 
	  ```
- ## 退出登录
	- ``` zsh
	  rpi-connect signout
	  ```
- ## 卸载
	- ``` zsh
	  sudo apt remove --purge rpi-connect
	  ```
- ## 诊断问题
	- ``` zsh
	  rpi-connect doctor
	  ```
-