tags:: [[Digital Certificate]]
---

- ## 步骤
	- 本地生成 **密钥对** .
	  logseq.order-list-type:: number
	- 用 "私钥 + 身份信息" 生成 **CSR** (证书请求) .
	  logseq.order-list-type:: number
		- CSR 中包含:
			- 公钥
			  logseq.order-list-type:: number
			- 申请者信息
			  logseq.order-list-type:: number
			- 用私钥做的签名
			  logseq.order-list-type:: number
		- ==一般内容以 `BEGIN CERTIFICATE REQUEST` 开头==
	- CA 验证 CSR 信息.
	  logseq.order-list-type:: number
		- CA 使用公钥验签, 证明申请者拥有私钥.
	- CA 生成证书.
	  logseq.order-list-type:: number
		- ==一般内容以 `BEGIN CERTIFICATE` 开头==