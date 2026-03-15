tags:: [[Computer Network]] 
alias:: [[Network Mapper]]
---

- https://nmap.org/
- ## 用途
	- 主要用于扫描网络内的主机及其提供的服务等相关信息.
- ## 安装
	- ### brew
		- [brew - nmap](https://formulae.brew.sh/formula/nmap#default)
		- 执行 `brew install nmap`
	- ### apt
		- 执行 `apt install nmap` .
- ## 使用
	- ### 查看子网中的所有设备
		- ``` zsh
		  ➜  ~ sudo nmap -sn 192.168.5.0/24
		  
		  Password:
		  Starting Nmap 7.98 ( https://nmap.org ) at 2026-03-14 14:33 +0800
		  
		  Nmap scan report for zte.home (192.168.5.1)
		  Host is up (0.0097s latency).
		  MAC Address: xxxx (zte)
		  
		  Nmap scan report for 192.168.5.11
		  Host is up (0.12s latency).
		  MAC Address: xxxx (Raspberry Pi Trading)
		  
		  Nmap done: 256 IP addresses (2 hosts up) scanned in 3.14 seconds
		  ```