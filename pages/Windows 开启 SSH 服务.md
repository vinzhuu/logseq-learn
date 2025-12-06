tags:: [[Windows]], [[SSH]]
---

- 执行如下命令进行安装和启动
	- ``` powershell
	  ::安装
	  Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0 
	   
	  :: 启动 SSH
	  Start-Service sshd
	  
	  :: 设置开机自启
	  Set-Service -Name sshd -StartupType Automatic
	  
	  :: 配置防火墙
	  New-NetFirewallRule -Name "OpenSSH-Server" -DisplayName "OpenSSH Server (TCP/22)" -Direction Inbound -Action Allow -Protocol TCP -LocalPort 22
	  ```
- 执行如下命令测试连接
	- `ssh 用户名@主机IP`
	-