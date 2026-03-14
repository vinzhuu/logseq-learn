tags:: [[微信 JS-SDK]]
---

- ## wx.config() 调用时机
	- `wx.config()` 是一个用于 **权限验证** 的函数 (传入一个对象).
	- `wx.config()` 是一个异步操作, 在调用任何 JS-SDK API 之前, 都必须先保证 `wx.config()` 已执行成功.
	- ==注意:==
		- 同一网页 URL , 需要且仅需要调用一次 `wx.config()` 
		  logseq.order-list-type:: number
		- 网页 URL 只要发生变化 (比如 [[SPA]] ), 就需要重新调用 `wx.config()` .
		  logseq.order-list-type:: number
		- 如何比较是否是 **同一网页 URL** :
		  logseq.order-list-type:: number
			- **比较用的 URL** = **原 URL** 去掉 **第一个 `#` 及其之后的字符**
			- (不管这个 `#` 是在路径中, 还是作为锚点)
- ## wx.config() 的回调函数
	- ### 注册 wx.config() 的回调函数
		- `wx.ready()` : 注册 `wx.config()` 执行成功时的回调函数 (传入一个函数).
		- `wx.error()` : 注册 `wx.config()` 执行失败时的回调函数 (传入一个函数).
	- ### 调用 wx.config() 后的逻辑
		- 调用逻辑:
			- 调用 `wx.config()` 之后, `wx.config()` 会异步执行.
			  logseq.order-list-type:: number
			- 如果在 `wx.config()` 执行完成前, 已经调用了 `wx.ready()/wx.error()` , 则会立即触发 `wx.ready()/wx.error()` 注册的回调函数.
			  logseq.order-list-type:: number
			- 如果在 `wx.config()` 执行完成前, 没有调用 `wx.ready()/wx.error()` , 则在后续调用 `wx.ready()/wx.error()` 时, 会立即触发 `wx.ready()/wx.error()` 注册的回调函数.
			  logseq.order-list-type:: number
		- 代码示例:
			- ``` js
			  // 可以这样
			  wx.ready(fn);
			  wx.error(errFn);
			  wx.config(cfg);
			  
			  // 也可以这样
			  wx.config(cfg);
			  wx.ready(fn);
			  wx.error(errFn);
			  ```
	- ### 关于 `wx.ready()`
		- 如果需要在页面加载时, 就调用 JS-SDK API : 可以放在 `wx.ready()` 注册的回调函数中.
		- 如果需要用户触发时, 才调用 JS-SDK API : 不要放在 `wx.ready()` 注册的回调函数中.
			- 但是, 由于 `wx.config()` 是异步操作, 为了避免用户触发时,  `wx.config()` 还没有执行完成, 这需要我们在用户触发的逻辑中, 判断 `wx.ready()` 函数是否已经执行:
				- 如果已经 `ready` , 则可以执行相应的逻辑
				  logseq.order-list-type:: number
				- 如果还未 `ready` , 则需要给用户一些提示 (比如 "初始化中, 请稍候再试" ).
				  logseq.order-list-type:: number
			- 另一种方案是:
				- 在 `ready` 之前, 直接禁用某些组件 (比如按钮), 同时也可以在页面上显示 "初始化中..." 之类.
				  logseq.order-list-type:: number
				- 在 `ready` 之后, 才启用这些组件, 用户触发操作后, 可以调用相应的 API.
				  logseq.order-list-type:: number
		- 所以最佳实践是:
			- ``` js
			  // 验证权限
			  wx.config(cfg);
			  
			  const button = document.getElementById("chooseImage");
			  button.disabled = true; // 初始禁用
			  button.innerText = "初始化中...";
			  
			  let wxIsReady = false;
			  wx.ready(() => {
			    wxIsReady = true;
			    
			    // 这里可以调用需要在页面加载时, 就调用的 API
			    
			    button.disabled = false;
			    button.innerText = "选择图片";
			  });
			  
			  wx.error(function(res){
			    console.log("error: " + res);
			  });
			  
			  button.onclick = () => {
			    if (!wxIsReady) {
			      showToast("功能初始化中，请稍候...");
			      return;
			    }
			    wx.chooseImage();
			  };
			  ```
	- ### 关于 `wx.error()`
		- #### 如何查看错误信息
			- 可以在通过设置 `wx.config()` 的 `debug` 参数为 `true` , 来查看错误日志信息.
			  logseq.order-list-type:: number
			- 也可以通过回调函数的 `res` 参数查看失败信息.
			  logseq.order-list-type:: number
			- ``` js
			  wx.error(function(res){
			    console.log("error: " + res);
			  });
			  ```
		- #### 验证失败如何处理
			- 比如 "签名过期" 就会导致验证失败.
			- 可以在 `wx.error()` 注册的回调函数中, 调用 `wx.config()` 重新进行权限验证.
				- 当然, 这只是兜底, 如果出现异常, 必然是有问题需要通过其他方式根本解决的.
- ## wx.config() 参数说明
	- ### 参数预览
		- ``` js
		  wx.config({
		    debug: true, // 开启调试模式,调用的所有api的返回值会在客户端 alert 出来，若要查看传入的参数，
		                 // 可以在 pc 端打开，参数信息会通过 log 打出，仅在 pc 端时才会打印。
		    
		    appId: '', // 必填，网页域名所绑定的公众号/服务号的唯一标识
		    
		    timestamp: 1, // 必填，生成签名的时间戳(秒)
		    nonceStr: '', // 必填，生成签名的随机串
		    signature: '',// 必填，签名
		    
		    jsApiList: [], // 必填，需要使用的JS接口列表
		    openTagList: [] // 可选，需要使用的开放标签列表，例如['wx-open-launch-app']
		  });
		  ```
	- ### timestamp, nonceStr 与 signature
		- ### 1. 获取 jsapi_ticket
			- 参见: [[微信服务端 API: JS-SDK ticket]]
		- ### 2. 准备 noncestr, timestamp 和 url
			- `noncestr` : 随机字符串
			- `timestamp` : 10 位时间戳 (秒)
			- `url` : 当前网页 URL 去掉第一个 `#` 及其后面的内容 (不管 `#` 是否在路径中)
				- 可以通过 `alert(location.href.split('#')[0])` 获取.
				- ==传给后端需注意:==
					- 如果 `url` 字段要通过 Query Params 传给后端, 前端记得要进行 URL 编码, 后端记得要进行解码.
					- 如果 `url` 字段要通过 请求体 传给后端, 就前端就无需进行 URL 编码.
		- ### 3.计算 signature
			- 准备好如下几个字符串:
			  logseq.order-list-type:: number
				- `jsapi_ticket`
				  logseq.order-list-type:: number
				- `noncestr`
				  logseq.order-list-type:: number
				- `timestamp`
				  logseq.order-list-type:: number
				- `url`
				  logseq.order-list-type:: number
			- 以上字段, 按如下格式组合成 **待签名字符串** .
			  logseq.order-list-type:: number
				- 按 **字段名** 的 ASCII 码升序, 以 `key1=value1&key2=value2…` 格式拼接
				  logseq.order-list-type:: number
				- 所有 **字段名** 和 **字段值** 都采用原始值, 不进行 URL 编码.
				  logseq.order-list-type:: number
				- 如 `jsapi_ticket=sM4AOVdWfPE4DxkXGEs8VMCPGGVi4C3VM0P37wVUCFvkVAy_90u5h9nbSlYy3-Sl-HhTdfl2fzFy1AOcHKP7qg&noncestr=Wm3WZYTPz0wzccnW&timestamp=1414587457&url=http://mp.weixin.qq.com?params=value`
			- 对以上 **待签名字符串** 进行 `sha1` 签名计算, 得到最终结果.
			  logseq.order-list-type:: number
			- 此处可校验签名: [微信 JS 接口签名校验工具](https://mp.weixin.qq.com/debug/cgi-bin/sandbox?t=jsapisign)
	- ### jsApiList
		- 当前 URL 需要用到的,  JS-SDK API 列表.
		- 枚举值参见: [附录 | 所有JS接口列表](https://developers.weixin.qq.com/doc/service/guide/h5/jssdk.html#63)
	- ### openTagList
		- 当前 URL 需要用到的, 开放标签列表.
		- 枚举值参见: [附录-所有开放标签列表](https://developers.weixin.qq.com/doc/service/guide/h5/opentag.html#%E9%99%84%E5%BD%95-%E6%89%80%E6%9C%89%E5%BC%80%E6%94%BE%E6%A0%87%E7%AD%BE%E5%88%97%E8%A1%A8)
	- ### signature 生成示例
		- 来自: [服务端 Demo](https://www.weixinsxy.com/jssdk/sample.zip)
		- ``` java
		  import java.util.UUID;
		  import java.util.Map;
		  import java.util.HashMap;
		  import java.util.Formatter;
		  import java.security.MessageDigest;
		  import java.security.NoSuchAlgorithmException;
		  import java.io.UnsupportedEncodingException;  
		  
		  class Sign {
		      public static void main(String[] args) {
		          String jsapi_ticket = "jsapi_ticket";
		  
		          // 注意 URL 一定要动态获取，不能 hardcode
		          String url = "http://example.com";
		          Map<String, String> ret = sign(jsapi_ticket, url);
		          for (Map.Entry entry : ret.entrySet()) {
		              System.out.println(entry.getKey() + ", " + entry.getValue());
		          }
		      };
		  
		      public static Map<String, String> sign(String jsapi_ticket, String url) {
		          Map<String, String> ret = new HashMap<String, String>();
		          String nonce_str = create_nonce_str();
		          String timestamp = create_timestamp();
		          String string1;
		          String signature = "";
		  
		          //注意这里参数名必须全部小写，且必须有序
		          string1 = "jsapi_ticket=" + jsapi_ticket +
		                    "&noncestr=" + nonce_str +
		                    "&timestamp=" + timestamp +
		                    "&url=" + url;
		          System.out.println(string1);
		  
		          try
		          {
		              MessageDigest crypt = MessageDigest.getInstance("SHA-1");
		              crypt.reset();
		              crypt.update(string1.getBytes("UTF-8"));
		              signature = byteToHex(crypt.digest());
		          }
		          catch (NoSuchAlgorithmException e)
		          {
		              e.printStackTrace();
		          }
		          catch (UnsupportedEncodingException e)
		          {
		              e.printStackTrace();
		          }
		  
		          ret.put("url", url);
		          ret.put("jsapi_ticket", jsapi_ticket);
		          ret.put("nonceStr", nonce_str);
		          ret.put("timestamp", timestamp);
		          ret.put("signature", signature);
		  
		          return ret;
		      }
		  
		      private static String byteToHex(final byte[] hash) {
		          Formatter formatter = new Formatter();
		          for (byte b : hash)
		          {
		              formatter.format("%02x", b);
		          }
		          String result = formatter.toString();
		          formatter.close();
		          return result;
		      }
		  
		      private static String create_nonce_str() {
		          return UUID.randomUUID().toString();
		      }
		  
		      private static String create_timestamp() {
		          return Long.toString(System.currentTimeMillis() / 1000);
		      }
		  }
		  ```
- ## 参考
	- [服务号 JS-SDK](https://developers.weixin.qq.com/doc/service/guide/h5/jssdk.html)
	  logseq.order-list-type:: number