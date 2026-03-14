tags:: [[Raspberry Pi]]
---

- ## 步骤
	- 开启树莓派 SSH Server .
	  logseq.order-list-type:: number
		- 参考: [[Raspberry Pi: 开启 SSH Server]]
	- 查看树莓派 IP 
	  logseq.order-list-type:: number
		- 参考: [[Raspberry Pi: 查看 IP]]
	- 给树莓派设置静态 IP.
	  logseq.order-list-type:: number
		- 参考: [[Raspberry Pi: 设置静态 IP]]
	- 使用 密码/密钥对 , SSH 连接树莓派.
	  logseq.order-list-type:: number
		- 普通 Terminal 连接:
			- `ssh <username>@<ip address>`
		- 可以打开图形窗口的 Terminal 连接 (基于  [[X Window System]] ): ==一般用不上==
			- `ssh -Y <username>@<ip address>`
			- ==这需要本地机器安装并启动 X Server==
- ## 使用密钥对连接
	- 参考: [Generate new SSH keypair](https://www.raspberrypi.com/documentation/computers/remote-access.html#generate-new-ssh-keypair)
- ## 常见问题
	- ### 默认密码问题
		- **参考** : [树莓派raspberry pi 4 SSH默认密码无法登录解决办法](https://blog.csdn.net/u012329294/article/details/123447208)
		- 由于安全问题, 最新版本的树莓派默认账号 `pi` 的密码, 不再是 `raspberry`
		- #### 方法一：烧录时设置
			- 在使用树莓派烧录工具时, 设置账号密码。
		- #### 方法二：编辑文件
			- 1. 根目录新建 `userconf` 文件。
			- 2. 编辑如下内容，即 `username:hash(password)` ，这一串hash就是raspberry。
			- ```sh
			  pi:$6$/4.VdYgDm7RJ0qM1$FwXCeQgDKkqrOU3RIRuDSKpauAbBvP11msq9X58c8Que2l1Dwq3vdJMgiZlQSbEXGaY5esVHGBNbCxKLVNqZW1
			   ```
- ## 参考
	- [Remote Access](https://www.raspberrypi.com/documentation/computers/remote-access.html)
	  logseq.order-list-type:: number