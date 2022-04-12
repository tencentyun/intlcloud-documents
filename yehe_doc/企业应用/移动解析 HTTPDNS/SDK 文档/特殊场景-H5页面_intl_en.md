This document describes how to load elements on HTML5 pages by using HTTPDNS.

## Sample Code for Android

### How it works
The Android system provides APIs to block network requests and inject custom logic in WebView. You can get the host of a URL request by blocking various types of network requests from WebView, call HTTPDNS to resolve the host, and then request the network address by using the new URL formed with the obtained IP.

### Implementation method
```java
WebSettings webSettings = mWebView.getSettings();
// Adopt the default cache policy, i.e., the cache will always be used before it expires
webSettings.setCacheMode(WebSettings.LOAD_DEFAULT);
// Load web image resources
webSettings.setBlockNetworkImage(false);
// Support JavaScript scripts
webSettings.setJavaScriptEnabled(true);
// Support zoom
webSettings.setSupportZoom(true);
mWebView.setWebViewClient(new WebViewClient() {
	// Use this method for API 21 or later
	@SuppressLint("NewApi")
	@Override
	public WebResourceResponse shouldInterceptRequest(WebView view, WebResourceRequest request) {
		if (request != null && request.getUrl() != null && request.getMethod().equalsIgnoreCase("get")) {
			String scheme = request.getUrl().getScheme().trim();
			String url = request.getUrl().toString();
			Logger.d("url a: " + url);
			// HTTPDNS resolves the network and image requests of CSS files
			if ((scheme.equalsIgnoreCase("http") || scheme.equalsIgnoreCase("https"))
			&& (url.contains(".css") || url.endsWith(".png") || url.endsWith(".jpg") || url .endsWith(".jif"))) {
				try {
					URL oldUrl = new URL(url);
					URLConnection connection = oldUrl.openConnection();
					// Get the HTTPDNS query result
					String ips = MSDKDnsResolver.getInstance().getAddrByName(oldUrl.getHost());
					if (ips != null) {
						// Get the IP successfully through HTTPDNS, replace the URL, and set the host header
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
						// Set the host field of the HTTP request header
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
	// Use this method for API 11–20
	public WebResourceResponse shouldInterceptRequest(WebView view, String url) {
		if (!TextUtils.isEmpty(url) && Uri.parse(url).getScheme() != null) {
			String scheme = Uri.parse(url).getScheme().trim();
			Logger.d("url b: " + url);
			// HTTPDNS resolves the network and image requests of CSS files
			if ((scheme.equalsIgnoreCase("http") || scheme.equalsIgnoreCase("https"))
			&& (url.contains(".css") || url.endsWith(".png") || url.endsWith(".jpg") || url
			.endsWith(".jif"))) {
				try {
					URL oldUrl = new URL(url);
					URLConnection connection = oldUrl.openConnection();
					// Get the HTTPDNS query result
					String ips = MSDKDnsResolver.getInstance().getAddrByName(oldUrl.getHost());
					if (ips != null) {
						// Get the IP successfully through HTTPDNS, replace the URL, and set the host header
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
						// Set the host field of the HTTP request header
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
// Load web resources
mWebView.loadUrl(targetUrl);
})
```

## Sample Code for iOS

### How it works
Network request interception: intercept a network request from WebView by using the iOS' native NSURLProtocol, filter by the filename extension of the network request URL, extract the domain from the obtained URL, make an HTTPDNS request, and finally concatenate the returned IP address into the URL of the original file network request.

### Implementation method
Perform HTTPDNS query in the `startLoading` method of the `NSURLProtocol` abstract class and replace the domain with the IP for `URLConnection`.

```
/**
 * Run the intercepted request, perform HTTPDNS query, and replace the domain with the IP for `URLConnection`
 */
- (void)startLoading
{
	  NSMutableURLRequest *newRequest;
    NSString *fileExtension = [[self.request URL] absoluteString];

	  // Resolve domains for URLs of PNG, JPG, or CSS files based on your business needs
	  if ([fileExtension containsString:@".png"] || [fileExtension containsString:@".jpg"] || [fileExtension containsString:@".css"])
	  {
	      // Modify the header information of the sync/async request
	      newRequest = [[H5ContentURLProtocol convertToNewRequest:self.request isSynchronous:NO] mutableCopy];
	  } else {
	      newRequest = [self.request mutableCopy];
	  }

    [NSURLProtocol setProperty:@YES forKey:@"MyURLProtocolHandledKey" inRequest:newRequest];

	  self.connection = [NSURLConnection connectionWithRequest:newRequest delegate:self];
}
```





