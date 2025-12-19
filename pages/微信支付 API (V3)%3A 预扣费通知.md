tags:: [[WeChat Pay API]], [[微信支付 - 委托代扣]]
---

- ## 文档
	- [预扣费通知 API](https://pay.weixin.qq.com/doc/v2/merchant/4011987402)
	- ==用于 [[微信支付 - 委托代扣]] ==
- ## 下发时间
	- [[微信支付 API (V3): 预扣费通知]] API , 需要在 `6 - 22点` 之间调用.
	- 否则, 会报如下错误:
		- ``` json
		  {
		    "code" : "INVALID_REQUEST",
		    "message" : "发送失败，需在6-22点之间方可发送"
		  }
		  ```
-