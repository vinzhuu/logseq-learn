tags:: [[微信支付 API]]
---

- ## 接口规范
	- **请求方式**: HTTPS + POST .
	  logseq.order-list-type:: number
	- **出参入参**: 都为 XML 格式, 根节点名为 `xml` .
	  logseq.order-list-type:: number
	- **字符编码**: 只支持 UTF-8 使用 1 至 3 个字节编码的字符 (包括常用汉字).
	  logseq.order-list-type:: number
- ## 签名算法
	- ### 作用
		- 用于 **商户** 调用 **微信 API** 时传参.
		  logseq.order-list-type:: number
		- 用于 **商户** 验证 **微信 API 的返回值** 和 **微信异步通知的传参** .
		  logseq.order-list-type:: number
	- ### 签名规则
		- 将所有 **参数值非空** 的参数, 按 `key1=value1&key2=value2…` 格式拼接, 得到 `stringA` .
		  logseq.order-list-type:: number
			- 其中 **键值对** 按 **参数名 ASCII 码从小到大排序 (即字典序)** .
			  logseq.order-list-type:: number
			- **微信 API 的返回值** 和 **微信异步通知的传参** 中的 `sign` 字段, 是不参与签名的.
			  logseq.order-list-type:: number
			- 微信 API 字段并非固定, 可能会有变化, 所以不能写死哪些字段参与签名, 应将所有 **非 sign** 字段纳入签名计算.
			  logseq.order-list-type:: number
			- 参数值采用原值, 不要进行 URL 编码.
			  logseq.order-list-type:: number
		- `stringSignTemp` = `${stringA}&key=${APIv2 密钥}`
		  logseq.order-list-type:: number
		- `signValue` = `签名算法(${stringSignTemp}).toUpperCase()` 
		  logseq.order-list-type:: number
			- 签名算法为 `MD5` 或 `HMAC-SHA256` .
		- 最终追加一个 `sign` 字段, 值为 `signValue` .
		  logseq.order-list-type:: number
- ## 签名校验工具
	- [微信支付接口签名校验工具](https://pay.weixin.qq.com/doc/v2/tool/sign_verify)
- ## 参考
	- [协议规则](https://pay.weixin.qq.com/doc/v2/merchant/4011986811)
	  logseq.order-list-type:: number
	- [安全规范](https://pay.weixin.qq.com/doc/v2/merchant/4011985891)
	  logseq.order-list-type:: number