tags:: [[美团联盟]]
---

- ## 事前准备
	- ``` zsh
	  媒体 ID	
	  媒体 AppKey 
	  媒体 AppSecret
	  推广位 SID
	  ```
- ## API 请求头
	- ### 公共请求头
		- ``` crystal
		  S-Ca-App
		  S-Ca-Timestamp
		  
		  Content-MD5
		  S-Ca-Signature-Headers
		  S-Ca-Signature
		  ```
		- `S-Ca-App` : 媒体 AppKey
		- `S-Ca-Timestamp` : 时间戳毫秒值.
			- 2 分钟内有效, 用于防重放.
		- `Content-MD5` : `Base64.encodeBase64(MD5(${请求体字符串}.getbytes("UTF-8")))`
			- `POST`, `PUT` 方式必填, `GET` 方式不填.
			- 用于校验请求体是否被篡改.
	- ### 需要参与签名的请求头
		- 包括: 除了 `S-Ca-Signature` , `S-Ca-Signature-Headers` 和 `Content-MD5` 之外的所有请求头 ( ==建议加入自定义请求头== ) .
	- ### S-Ca-Signature-Headers
		- `S-Ca-Signature-Headers` 就是所有 **需要参与签名的请求头** , 使用 `,` 分隔.拼接成的字符串.
		- 示例: `S-Ca-Timestamp,S-Ca-App,My-Header1,My-Header2`
	- ### S-Ca-Signature
		- ``` java
		  // 媒体 SecretKey
		  String secretKey = "xxx";
		  
		  // 待签名字符串
		  String stringToSign = 
		    HTTPMethod + "\n" +             
		    Content-MD5 + "\n" +
		    Headers + 
		    Url;
		  
		  Mac hmacSha256 = Mac.getInstance("HmacSHA256");
		  byte[] keyBytes = secretKey.getBytes("UTF-8");
		  hmacSha256.init(new SecretKeySpec(keyBytes, 0, keyBytes.length, "HmacSHA256"));
		  
		  // 最终 S-Ca-Signature 的值
		  String sign = new String(Base64.encodeBase64(hmacSha256.doFinal(stringToSign.getBytes("UTF-8")),"UTF-8"));
		  ```
		- `HTTPMethod` : 就是请求方式, 如 `POST` , `GET`等 , 需要全大写.
		- `Content-MD5` : 即 `Content-MD5` 请求头的值.
			- `Content-MD5` 如果为空, 也需要换行符 `\n` .
		- `Headers` 和 `Url` 见下文.
	- ### Headers
		- `Headers` 就是所有 **需要参与签名的请求头** , 拼接成的字符串.
		- 格式如下:
			- 对所有 **需要参与签名的请求头** , 按 HeaderKey 的 **字典顺序** , 根据如下格式进行拼接:
			- ``` java
			  "${HeaderKey1}:${HeaderValue1}\n" +
			  "${HeaderKey2}:${HeaderValue2}\n" +
			  ...
			  "${HeaderKeyN}:${HeaderValueN}\n" +
			  ```
			- 如果某个 HeaderValue 是空字符串, 则拼接为: `"${HeaderKey}:\n"`
		- 如果没有 **需要参与签名的请求头** , 则返回空字符串.
	- ### Url
		- `Url = Path + ? + Query`
			- 如果没有 `Query` 参数, 则 `Url = Path`
		- `Path` : 即 Url 路径 Host 和 Port 之后, `?` 之前的部分.
			- 比如 `https://media.meituan.com/cps_open/common/api/v1/get_referral_link?name=1` 的 Path 就是 `/cps_open/common/api/v1/get_referral_link` .
		- `Query`:
			- 所有的 Query 字段, 按 Key 的 **字典顺序** , 根据如下格式进行拼接:
			- ``` java
			  "${Key1}=${Value1}&" +
			  "${Key2}=${Value2}&" +
			  ...
			  "${KeyN}=${ValueN}" +
			  ```
			- 如果某个 Value 是空字符串, 则拼接为: `${Key}&` (去掉了 `=` )
- ## API 公共错误码
	- 参考: [API公共错误码](https://media.meituan.com/pc/index.html#/help?path=API%E5%85%AC%E5%85%B1%E9%94%99%E8%AF%AF%E7%A0%81)
	- ``` crystal
	  # 服务业务相关:
	  -1: 接口不可用，请联系相关负责人
	  0: 成功
	  1: 参数错误，请参考接口文档或联系相关负责人
	  2: 请求处理异常，请稍后再试
	  
	  # 4xx 认证等非服务业务相关:
	  400: 鉴权不通过
	  401: 不允许的请求方式
	  402: 请求过于频繁，请稍后再试
	  403: 请求次数超过授权额度
	  
	  # 未知异常:
	  999: 系统出现异常，请稍后再试
	  ```
-