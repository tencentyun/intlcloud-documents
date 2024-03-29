﻿该文档说明 H5 页面内元素 HTTP_DNS 的加载。

## Android 部分代码

### 原理
Android 原生系统提供了系统 API 以实现 WebView 中的网络请求拦截与自定义逻辑注入，我们可以通过上述拦截 WebView 的各类网络请求，截取 URL 请求的 host，然后调用 HTTPDNS 解析该 host，通过得到的 IP 组成新的 URL 来请求网络地址。

### 实现方法
```java
WebSettings webSettings = mWebView.getSettings();
// 使用默认的缓存策略，cache 没有过期就用 cache
webSettings.setCacheMode(WebSettings.LOAD_DEFAULT);
// 加载网页图片资源
webSettings.setBlockNetworkImage(false);
// 支持 JavaScript 脚本
webSettings.setJavaScriptEnabled(true);
// 支持缩放
webSettings.setSupportZoom(true);
mWebView.setWebViewClient(new WebViewClient() {
	// API 21 及之后使用此方法
	@SuppressLint("NewApi")
	@Override
	public WebResourceResponse shouldInterceptRequest(WebView view, WebResourceRequest request) {
		if (request != null && request.getUrl() != null && request.getMethod().equalsIgnoreCase("get")) {
			String scheme = request.getUrl().getScheme().trim();
			String url = request.getUrl().toString();
			Logger.d("url a: " + url);
			// HTTPDNS 解析 css 文件的网络请求及图片请求
			if ((scheme.equalsIgnoreCase("http") || scheme.equalsIgnoreCase("https"))
			&& (url.contains(".css") || url.endsWith(".png") || url.endsWith(".jpg") || url .endsWith(".jif"))) {
				try {
					URL oldUrl = new URL(url);
					URLConnection connection = oldUrl.openConnection();
					// 获取 HTTPDNS 域名解析结果
					String ips = MSDKDnsResolver.getInstance().getAddrByName(oldUrl.getHost());
					if (ips != null) {
						// 通过 HTTPDNS 获取 IP 成功，进行 URL 替换和 HOST 头设置
						Logger.d("HttpDns ips are: " + ips + " for host: " + oldUrl.getHost());
						String ip;
						if (ips.contains(";")) {
							ip = ips.substring(0, ips.indexOf(";"));
						} else {
							ip = ips;
						}
						String newUrl = url.replaceFirst(oldUrl.getHost(), ip);
						Logger.d("newUrl a is: " + newUrl);
						connection = (HttpURLConnection) new URL(newUrl).openConnection();
						// 设置 HTTP 请求头 Host 域
						connection.setRequestProperty("Host", oldUrl.getHost());
					}
					Logger.d("ContentType a: " + connection.getContentType());
					return new WebResourceResponse("text/css", "UTF-8", connection.getInputStream());
				}
				catch (MalformedURLException e) {
					e.printStackTrace();
				}
				catch (IOException e) {
					e.printStackTrace();
				}
			}
		}
		return null;
	}
	// API 11 至 API20 使用此方法
	public WebResourceResponse shouldInterceptRequest(WebView view, String url) {
		if (!TextUtils.isEmpty(url) && Uri.parse(url).getScheme() != null) {
			String scheme = Uri.parse(url).getScheme().trim();
			Logger.d("url b: " + url);
			// HTTPDNS 解析 css 文件的网络请求及图片请求
			if ((scheme.equalsIgnoreCase("http") || scheme.equalsIgnoreCase("https"))
			&& (url.contains(".css") || url.endsWith(".png") || url.endsWith(".jpg") || url
			.endsWith(".jif"))) {
				try {
					URL oldUrl = new URL(url);
					URLConnection connection = oldUrl.openConnection();
					// 获取 HTTPDNS 域名解析结果
					String ips = MSDKDnsResolver.getInstance().getAddrByName(oldUrl.getHost());
					if (ips != null) {
						// 通过 HTTPDNS 获取 IP 成功，进行 URL 替换和 HOST 头设置
						Logger.d("HttpDns ips are: " + ips + " for host: " + oldUrl.getHost());
						String ip;
						if (ips.contains(";")) {
							ip = ips.substring(0, ips.indexOf(";"));
						} else {
							ip = ips;
						}
						String newUrl = url.replaceFirst(oldUrl.getHost(), ip);
						Logger.d("newUrl b is: " + newUrl);
						connection = (HttpURLConnection) new URL(newUrl).openConnection();
						// 设置 HTTP 请求头 Host 域
						connection.setRequestProperty("Host", oldUrl.getHost());
					}
					Logger.d("ContentType b: " + connection.getContentType());
					return new WebResourceResponse("text/css", "UTF-8", connection.getInputStream());
				}
				catch (MalformedURLException e) {
					e.printStackTrace();
				}
				catch (IOException e) {
					e.printStackTrace();
				}
			}
		}
		return null;
	}
// 加载 web 资源
mWebView.loadUrl(targetUrl);
})
```

## iOS 部分代码

### 原理
拦截网络请求：使用 iOS 原生的 NSURLProtocol，拦截 webview 的网络请求，并根据网络请求 URL 的文件名后缀进行过滤，拿到过滤后的 URL 以后，截取 URL 的域名，然后进行 HTTP_DNS 请求，最后用返回的 IP 地址拼接原文件网络请求的 URL。

### 实现方法
在 NSURLProtocol 抽象类方法 startLoading 中进行 HTTPDNS 解析，将域名替换成 IP 后进行 URLConnection。

```
/**
 *  让被拦截的请求执行，在此处进行 HTTPDNS 解析，将域名替换成 IP 后进行 URLConnection
 */
- (void)startLoading
{
	  NSMutableURLRequest *newRequest;
    NSString *fileExtension = [[self.request URL] absoluteString];

	  //根据业务需求，进行 png，jpg，css 等格式的 URL 域名解析
	  if ([fileExtension containsString:@".png"] || [fileExtension containsString:@".jpg"] || [fileExtension containsString:@".css"])
	  {
	      // 修改了请求的头部信息，同步/异步请求
	      newRequest = [[H5ContentURLProtocol convertToNewRequest:self.request isSynchronous:NO] mutableCopy];
	  } else {
	      newRequest = [self.request mutableCopy];
	  }

    [NSURLProtocol setProperty:@YES forKey:@"MyURLProtocolHandledKey" inRequest:newRequest];

	  self.connection = [NSURLConnection connectionWithRequest:newRequest delegate:self];
}
```





