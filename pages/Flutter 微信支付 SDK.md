tags:: [[Flutter]], [[微信支付]]
---

- 参见 [fluwx](https://pub.dev/packages/fluwx)
-
- ## 测试代码
	- ``` dart
	  // 使用 `weixin-java-pay` 创建的支付串
	  Map result = {"xx": "yy"};
	  fluwx.pay(
	    which: Payment(
	      appId: result['appid'].toString(),
	      partnerId: result['partnerId'].toString(),	
	      prepayId: result['prepayId'].toString(),
	      packageValue: result['packageValue'].toString(),
	      nonceStr: result['noncestr'].toString(),
	      timestamp: int.parse(result['timestamp']),
	      sign: result['sign'].toString(),
	    ));
	  ```