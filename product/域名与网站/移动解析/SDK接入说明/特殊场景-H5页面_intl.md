This document describes the loading of the element HTTP_DNS in an HTML5 page.

### Code for Android

#### How It Works
The native Android system provides a system API to achieve network request blocking and custom logic injection in WebView. We can block various types of network requests in WebView, intercept the host of the URL request, call HttpDNS to resolve the host and obtain the IP to make up a new URL to request the network address.

#### Implementation Method
```
WebSettings webSettings = mWebView.getSettings();
// Use the default caching strategy; cache is used as long as it hasn't expired
webSettings.setCacheMode(WebSettings.LOAD_DEFAULT);
// Load the webpage image resources
webSettings.setBlockNetworkImage(false);
// Support for JavaScript scripts
webSettings.setJavaScriptEnabled(true);
// Support for zooming
webSettings.setSupportZoom(true);
mWebView.setWebViewClient(new WebViewClient() {
// Use this method for API 21 and later
@SuppressLint("NewApi")
@Override
public WebResourceResponse shouldInterceptRequest(WebView view, WebResourceRequest request) {
if (request != null && request.getUrl() != null && request.getMethod().equalsIgnoreCase("get")) {
String scheme = request.getUrl().getScheme().trim();
String url = request.getUrl().toString();
Logger.d("url a: " + url);
// HttpDNS resolves the network and image requests in the css file
if ((scheme.equalsIgnoreCase("http") || scheme.equalsIgnoreCase("https"))
&& (url.contains(".css") || url.endsWith(".png") || url.endsWith(".jpg") || url .endsWith(".jif"))) {
try {
URL oldUrl = new URL(url);
URLConnection connection = oldUrl.openConnection();
// Get the HttpDNS domain name resolution result
String ips = MSDKDnsResolver.getInstance().getAddrByName(oldUrl.getHost());
if (ips != null) { // Get the IP successfully via HttpDNS and perform URL replacement and HOST header setting
Logger.d("HttpDns ips are: " + ips + " for host: " + oldUrl.getHost());
String ip;
if (ips.contains(";")) {
ip = ips.substring(0, ips.indexOf(";"));
} else {
ip = ips;
}
String newUrl = url.replaceFirst(oldUrl.getHost(), ip);
Logger.d("newUrl a is: " + newUrl);
connection = (HttpURLConnection) new URL(newUrl).openConnection(); // Set the Host domain of the HTTP request header
connection.setRequestProperty("Host", oldUrl.getHost());
}
Logger.d("ContentType a: " + connection.getContentType());
return new WebResourceResponse("text/css", "UTF-8", connection.getInputStream());
} catch (MalformedURLException e) {
e.printStackTrace();
} catch (IOException e) {
e.printStackTrace();
}
}
}
return null;
}
// Use this method for API 11 to 20
public WebResourceResponse shouldInterceptRequest(WebView view, String url) {
if (!TextUtils.isEmpty(url) && Uri.parse(url).getScheme() != null) {
String scheme = Uri.parse(url).getScheme().trim();
Logger.d("url b: " + url);
// HttpDNS resolves the network and image requests in the css file
if ((scheme.equalsIgnoreCase("http") || scheme.equalsIgnoreCase("https"))
&& (url.contains(".css") || url.endsWith(".png") || url.endsWith(".jpg") || url
.endsWith(".jif"))) {
try {
URL oldUrl = new URL(url);
URLConnection connection = oldUrl.openConnection();
// Get the HttpDNS domain name resolution result
String ips = MSDKDnsResolver.getInstance().getAddrByName(oldUrl.getHost());
if (ips != null) {
// Get the IP successfully via HttpDNS and perform URL replacement and HOST header setting
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
// Set the Host domain of the HTTP request header
connection.setRequestProperty("Host", oldUrl.getHost());
}
Logger.d("ContentType b: " + connection.getContentType());
return new WebResourceResponse("text/css", "UTF-8", connection.getInputStream());
} catch (MalformedURLException e) {
e.printStackTrace();
} catch (IOException e) {
e.printStackTrace();
}
}
}
return null;
}
});
// Load web resources
mWebView.loadUrl(targetUrl);
}
```

### Code for iOS

#### How It Works
Network request blocking: iOS' native NSURLProtocol is used to block the network requests of WebView. It then filters the requests by the file name suffix of the request URLs. After getting the filtered URL, it takes out the domain name of the URL and then makes an HTTP_DNS request. Then, the resulting IP address is used to form the original file network request.

#### Implementation Method
HttpDNS resolution is performed in the method startLoading of the abstract class NSURLProtocol by replacing the domain name with the IP and then conducting URLConnection.

```
/**
 * Let the intercepted request execute and perform HttpDNS resolution here by replacing the domain name with the IP and then conducting URLConnection.
 */
- (void)startLoading
{
	  NSMutableURLRequest *newRequest;
    NSString *fileExtension = [[self.request URL] absoluteString];

	  // Perform URL domain name resolution in png, jpg or css format according to business needs
	  if ([fileExtension containsString:@".png"] || [fileExtension containsString:@".jpg"] || [fileExtension containsString:@".css"])
	  {
	      // The request header information is modified for sync/async request
	      newRequest = [[H5ContentURLProtocol convertToNewRequest:self.request isSynchronous:NO] mutableCopy];
	  } else {
	      newRequest = [self.request mutableCopy];
	  }

    [NSURLProtocol setProperty:@YES forKey:@"MyURLProtocolHandledKey" inRequest:newRequest];

	  self.connection = [NSURLConnection connectionWithRequest:newRequest delegate:self];
}
```
