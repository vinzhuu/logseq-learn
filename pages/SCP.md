tags:: [[File Transfer]]
alias:: [[Secure Copy Protocol]], [[Secure Copy]]
---

- SCP , 是 Secure Copy Protocol 或 Secure Copy 的简称.
	- 这里的 Protocol 只是习惯叫法, 并非真的协议.
	- 因为它没有明文协议标准, 它只是 Unix 早期的远程复制工具 [[RCP]] 的 [[SSH]] 安全版.
- 由于 SCP 设计有缺陷, [[OpenSSH]] 9.0 开始,  SCP 命令底层已改为使用 [[SFTP]] .
	-
	-