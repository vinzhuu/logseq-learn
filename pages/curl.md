tags:: [[URL Tool]], [[URL Tool]] 
---

- ## 官方资料
	- https://curl.se/
	- https://everything.curl.dev/
- ## 第三方资料
	- [阮一峰](https://www.ruanyifeng.com/blog/2011/09/curl.html)
	- [catonmat.net - curl cookbook](https://catonmat.net/cookbooks/curl)
- ---
- ## 一句话解释
	- curl 即 **Client for URLs** , 是一个 *使用各种协议传输数据* 的命令行工具。
- ## curl是啥
	- curl 是常用的命令行工具，用来请求 Web 服务器。
	- 它的功能非常强大，命令行参数多达几十种。如果熟练的话，完全可以取代 Postman 这一类的图形界面工具。
- ## curl命令
	- get 请求中有多个参数时，必须用 `""` 包裹。否则只能识别第一个参数：
	- ```shell
	  curl "http://ws.webxml.com.cn/WebServices/WeatherWS.asmx/getWeather?theCityCode=%E6%B7%B1%E5%9C%B3&theUserID="
	  ```
-