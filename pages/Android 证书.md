tags:: [[Android]]
---

- ## Android 证书是干什么的
	- Android 应用打包发布时需要用到, 用于表明开发者身份.
- ## 如何生成 Android 证书
	- Android 证书的生成是自助和免费的，不需要审批或付费.
- ## 使用 keytool 生成证书
	- 安装 JDK 时, 也会安装 `keytool` 命令.
		- 比如 macOS 中,  `keytool` 命令会被安装在 `/Library/Java/JavaVirtualMachines/jdk1.8.0_341.jdk/Contents/Home/bin` 目录下, `/usr/bin/keytool` 也有此命令.
	- 生成步骤:
		- 执行命令并输入相关参数:
		  logseq.order-list-type:: number
			- ``` zsh
			  # testalias 是证书别名，建议使用英文字母和数字
			  # 36500 是证书的有效期, 单位天, 建议时间设置长一点，避免证书过期
			  # test.keystore 是证书文件路径
			  keytool -genkey -alias testalias -keyalg RSA -keysize 2048 -validity 36500 -keystore test.keystore
			  
			  Enter keystore password: 
			  Re-enter new password:
			  What is your first and last name?
			    [Unknown]:  Vincent Zhu                            
			  What is the name of your organizational unit?
			    [Unknown]:  Technology Department
			  What is the name of your organization?
			    [Unknown]:  Vincept
			  What is the name of your City or Locality?
			    [Unknown]:  Shenzhen
			  What is the name of your State or Province?
			    [Unknown]:  Guangdong
			  What is the two-letter country code for this unit?
			    [Unknown]:  CN
			  Is CN=Vincent Zhu, OU=Technology Department, O=Vincept, L=Shenzhen, ST=Guangdong, C=CN correct?
			    [no]:  y
			  
			  Enter key password for <sfb>
			          (RETURN if same as keystore password):  // 确认证书密码与证书文件密码一样（HBuilder|HBuilderX要求这两个密码一致），直接回车就可以
			  
			  Warning:
			  The JKS keystore uses a proprietary format. It is recommended to migrate to PKCS12 which is an industry standard format using "keytool -importkeystore -srckeystore sfb.keystore -destkeystore sfb.keystore -deststoretype pkcs12".
			  ```
		- 查看生成的证书文件:
		  logseq.order-list-type:: number
			- ``` zsh
			  keytool -list -v -keystore test.keystore
			  Enter keystore password:
			  
			  # 输出结果
			  Keystore type: PKCS12    
			  Keystore provider: SUN    
			  
			  Your keystore contains 1 entry    
			  
			  Alias name: test    
			  Creation date: 2019-10-28    
			  Entry type: PrivateKeyEntry    
			  Certificate chain length: 1    
			  Certificate[1]:    
			  Owner: CN=Tester, OU=Test, O=Test, L=HD, ST=BJ, C=CN    
			  Issuer: CN=Tester, OU=Test, O=Test, L=HD, ST=BJ, C=CN    
			  Serial number: 7dd12840    
			  Valid from: Fri Jul 26 20:52:56 CST 2019 until: Sun Jul 02 20:52:56 CST 2119    
			  Certificate fingerprints:    
			           MD5:  F9:F6:C8:1F:DB:AB:50:14:7D:6F:2C:4F:CE:E6:0A:A5    
			           SHA1: BB:AC:E2:2F:97:3B:18:02:E7:D6:69:A3:7A:28:EF:D2:3F:A3:68:E7    
			           SHA256: 24:11:7D:E7:36:12:BC:FE:AF:2A:6A:24:BD:04:4F:2E:33:E5:2D:41:96:5F:50:4D:74:17:7F:4F:E2:55:EB:26    
			  Signature algorithm name: SHA256withRSA    
			  Subject Public Key Algorithm: 2048-bit RSA key    
			  Version: 3
			  ```
			- 其中, `MD5` , `SHA1` 和 `SHA256` 可能需要用到.
		- logseq.order-list-type:: number
- ## 参考
	- [Android平台签名证书(.keystore)生成指南](https://ask.dcloud.net.cn/article/35777)
	  logseq.order-list-type:: number
	- logseq.order-list-type:: number