## Overview
At present, domain name hijacking happens frequently during domain name resolution, which brings many OPS and security challenges. To address this problem, the HttpDNS service is introduced. To ensure DNS access, the function is divided into two levels: HttpDNS and LocalDNS. If HttpDNS is successfully performed, the value of HttpDNS is directly returned; otherwise, the value of LocalDNS is returned; if both cases fail, a null value is returned.
You can get the Zhiying Analysis SDK for Android in the following way:
[Get the latest version of SDK from Github >>](https://github.com/tencentyun/httpdns-android-sdk)

## Access 
### Step 1: Configure AndroidMainfest
```
    <uses-permission android:name="android. permission. ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android. permission. ACCESS_WIFI_STATE" />
    <uses-permission android:name="android. permission. CHANGE_WIFI_STATE" />
    <uses-permission android:name="android. permission. READ_PHONE_STATE" />
    <uses-permission android:name="android. permission. INTERNET" />
    <! -- DNS receives the network switching broadcast -->
    <receiver
        android:name="com.tencent.msdk.dns. HttpDnsCache$ConnectivityChangeReceiver"
        android: label="NetworkConnection" >
        <intent-filter>
            <action android:name= “android.net. conn. CONNECTIVITY_CHANGE" />
        </intent-filter>
</receiver>
```

### Step 2: Access the HttpDNS library
Copy the `HttpDnsLibs\httpdns_xxxx.jar` library file to the corresponding location of the project libs, and copy the `HttpDnsLibs\dnsconfig.ini` configuration file to the app's `Android\assets` directory;
> **Note:**
Before copying the `dnsconfig.ini` file, modify the relevant configuration in this file first, but do not change the original encoding format of the file.
The specific modification method is as follows:
> 
| Modification item | Modification field | Modification method |
|---------|---------|---------|
| Switch for external and internal vendor | IS_COOPERATOR | true |
| Switch for external vendor test | IS_COOPERATOR_TEST | For a test environment, enter "true"; for a production environment, enter "false"; it must be "false" after official launch |
| Vendor-reported appId | COOPERATOR_APPID | Obtained by registering at Tencent Cloud's official website |
| Switch for HttpDNS SDK log | IS_DEBUG | true: log turned on; false: log turned off |
| Server-assigned ID | DNS_ID | Obtained by registering at Tencent Cloud's official website |
| Server-assigned key | DNS_KEY | Obtained by registering at Tencent Cloud's official website |

### Step 3: Access dependent libraries
> **Note:**
> Ignore this step for apps that already have accessed Tencent Beacon.

Copy the `HttpDnsLibs\\ beacon_android_vxxxx.jar` library to the corresponding location in the game libs.

### Step 4: Call HttpDNS Java API
Call the command as follows:
```
// Initialize Beacon: If you already have accessed MSDK, IMSDK or Tencent Beacon, you don't need to initialize this API.
try {
// ***Note: The business' own Beacon appKey needs to be entered here.
UserAction.setAppKey("0I000LT6GW1YGCP7");
UserAction.initUserAction(MainActivity.this);
} catch (Exception e) {
	Logger.e("init beacon error:" + e.getMessage());
}

/**
* Initialize HttpDNS: If you already have accessed MSDK, you need to initialize HttpDNS after initializing the MSDK.
* @param Activity   Pass in the current Activity
*/
MSDKDnsResolver.getInstance(). init (MainActivity.this);

/**
* Set openId; for businesses that have already accessed MSDK, pass in the MSDK openId; for other businesses, pass in "NULL".
* Note: The return value of this API is Boolean. When calling in Unity or Cocos, please pay attention to the return type.
* @param String openId
*/
MSDKDnsResolver.getInstance().WGSetDnsOpenId("10000");


/**
* HttpDNS sync resolution API; it queries the cache first; if a result exists, it returns the result; otherwise, it performs a sync domain name resolution request for resolving
* Complete and return the latest resolution result; an empty object is returned if the resolution fails
* @param domain   Domain name (such as www.qq.com), note: for domain, you can only pass in a domain name rather than an IP, and the returned result needs to be made non-null
* Judge
* @return Set of the resolved IP results corresponding to the domain name
*/
	String ips = MSDKDnsResolver.getInstance(). getAddrByName(domain);
```

## Precautions
- It is recommended to call the getAddrByName(domain) API in a child thread when calling the HttpDNS sync API.
- If the client's business is already bound with the Host (such as its HTTP service or CDN service), then, after replacing the domain name in the URL with the IP returned by HttpDNS, you also need to specify the Host field in the HTTP header.
 - Take URLConnection as an example: 
```
		URL oldUrl = new URL(url); 
        URLConnection connection = oldUrl.openConnection(); 
        // Get the HttpDNS domain name resolution result 
        String ips = MSDKDnsResolver.getInstance().getAddrByName(oldUrl.getHost()); 
        if (ips != null) { // Get the IP successfully via HttpDNS and perform URL replacement and HOST header setting 
            String ip; 
            if (ips.contains(";")) { 
                ip = ips.substring(0, ips.indexOf(";")); 
            } else { 
                ip = ips; 
            } 
            String newUrl = url.replaceFirst(oldUrl.getHost(), ip); 
            connection = (HttpURLConnection) new URL(newUrl).openConnection(); // Set the Host domain name of the HTTP request header 
            connection.setRequestProperty("Host", oldUrl.getHost()); 
        } 
```
 - Take curl as an example:
If you want to access `www.qq.com` and the IP address resolved by HttpDNS is 192.168.0.111, then you can call it by this method: 
```
curl -H "Host:www.qq.com" http://192.168.0.111/aaa.txt.
```

## Practice Scenario
### Unity Access Instructions
#### 1. Initialize HttpDns and Beacon APIs.
> **Note:**
If you already have accessed Beacon, you don't need to initialize it.

```
private static AndroidJavaObject m_dnsJo;
	private static AndroidJavaClass sGSDKPlatformClass;
	public static void Init() {
		AndroidJavaClass jc = new AndroidJavaClass("com.unity3d.player.UnityPlayer");
		if (jc == null)
			return;
			
		AndroidJavaObject joactivety = jc.GetStatic<AndroidJavaObject>("currentActivity");
		if (joactivety == null)
			return;
		AndroidJavaObject context = joactivety.Call<AndroidJavaObject>("getApplicationContext");
		// Initialize HttpDNS
		AndroidJavaObject joDnsClass = new AndroidJavaObject("com.tencent.msdk.dns.MSDKDnsResolver");
		Debug.Log(" WGGetHostByName ===========" + joDnsClass);
		if (joDnsClass == null)
			return;
		m_dnsJo = joDnsClass.CallStatic<AndroidJavaObject>("getInstance");
			Debug.Log(" WGGetHostByName ===========" + m_dnsJo);
		if (m_dnsJo == null)
			return;
		m_dnsJo.Call("init", context);
	}
```

#### 2. Call the HttpDNS API to resolve the domain name。
```
// This operation is recommended to be processed in a child thread
public static string GetHttpDnsIP( string strUrl ) {
		string strIp = string.Empty;
		// Resolve to get the IP configuration set
		strIp = m_dnsJo.Call<string>("getAddrByName", strUrl);
		Debug.Log( strIp );
		if( strIp != null )
		{
		    // Take the first one
			string[] strIps = strIp.Split(';');
			strIp = strIps[0];
		}
		return strIp;
	}
```
### Loading of the Element HTTP_DNS in an HTML5 Page
How it works:
The native Android system provides a system API to achieve network request blocking and custom logic injection in WebView. We can block various types of network requests in WebView, intercept the host of the URL request, call HttpDNS to resolve the host and obtain the IP to make up a new URL to request the network address.
Implementation method:
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
&& (url.contains(".css") || url.endsWith(".png") || url.endsWith(".jpg") || url 
.endsWith(".gif"))) { 
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
.endsWith(".gif"))) { 
try { 
URL oldUrl = new URL(url); 
URLConnection connection = oldUrl.openConnection(); 
// Get the HttpDNS domain name resolution result 
String ips = MSDKDnsResolver.getInstance().getAddrByName(oldUrl.getHost()); 
if (ips != null) { 
// Get IP successfully through HTTPDNS, perform URL replacement and HOST header settings 
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
### OkHttp + HttpDns Scenario
```
    // The scheme is for reference only
    String url = "http://www.qq.com";
    Uri uri = Uri.parse(url);
    String ip = MSDKDnsResolver.getInstance().getAddrByName("www.qq.com"); // HttpDNS resolves the domain name
    if (ip != null) {
	    if (ip.contains(";")) {
	        ip = ip.substring(0, ip.indexOf(";"));
	}
    } else {
	    return;
    }
    String mURL = uri.toString().replaceFirst(uri.getHost(), ip);

    // OkHttp GET Method
    try {
	    String mGetURL = mURL; // Encapsulate according to the business's own server address
	    Request request = new Request.Builder().url(mGetURL).build();
	    OkHttpClient client = new OkHttpClient();
	    Response response = client.newCall(request).execute();
	    String mGetResult = response.body().string();
	    System.out.println("OkHttp Get Method result:" + mGetResult);
    } catch (Exception e) {
	    e.printStackTrace();
    }

    // OkHttp POST Method
    try {
        String mPostURL = mURL; // Encapsulate according to the business's own server address
	    MediaType mType = MediaType.parse("application/json; charset=utf-8");
	    // Encapsulate the request parameters according to the business' actual conditions
	    JSONObject jsonData = new JSONObject();
	    jsonData.put("os", "Android");
	    jsonData.put("api_version", 23);
	    jsonData.put("version", "0.0.1");
	    ......
	    String data = jsonData.toString();
	    RequestBody body = RequestBody.create(mType, data);
	    Request request = new Request.Builder().url(mPostURL).post(body).build();
	    OkHttpClient client = new OkHttpClient();
	    Response response = client.newCall(request).execute();
	    String mPostResult = response.body().string();
	    System.out.println("OkHttp POST Method result:" + mPostResult);
    } catch (Exception e) {
	    e.printStackTrace();
    }
```

### HTTPS Scenario
#### Ordinary HTTPS Scenario
```
  String url = "https://IP obtained after domain name resolution by HttpDNS/d?dn=&clientip=1&ttl=1&id=128"; // The business' own request connection
	HttpsURLConnection connection = (HttpsURLConnection) new URL(url).openConnection();
	connection.setRequestProperty("Host", "Originally resolved domain name");
	connection.setHostnameVerifier(new HostnameVerifier() {
	@Override
	public boolean verify(String hostname, SSLSession session) {
		return HttpsURLConnection.getDefaultHostnameVerifier().verify("Originally resolved domain name", session);
	}
	});
	connection.setConnectTimeout(mTimeOut); // Set the connection timeout
	connection.setReadTimeout(mTimeOut); // Set the read stream timeout
	connection.connect();
```

#### HTTPS SNI (Single-IP Multi-HTTPS Certificate) Scenario
```
	 String url = "https://" + ip + "/pghead/xxxxxxx/140"; // Encapsulate the request URL of the business with the IP obtained from HttpDNS
		HttpsURLConnection sniConn = null;
		try {
			sniConn = (HttpsURLConnection) new URL(url).openConnection();
			// Set the Host domain of the HTTP request header
			sniConn.setRequestProperty("Host", "Originally resolved domain name");
			sniConn.setConnectTimeout(3000);
			sniConn.setReadTimeout(3000);
			sniConn.setInstanceFollowRedirects(false);
			// Customize the SSLSocketFactory to bring the request domain name ***key step
			SniSSLSocketFactory sslSocketFactory = new SniSSLSocketFactory(sniConn);
			sniConn.setSSLSocketFactory(sslSocketFactory);
			// Verify whether the hostname matches the server authentication scheme
			HostnameVerifier hostnameVerifier = new HostnameVerifier() {
				@Override
				public boolean verify(String hostname, SSLSession session) {
					return HttpsURLConnection.getDefaultHostnameVerifier().verify("Originally resolved domain name", session);
				}
			};
			sniConn.setHostnameVerifier(hostnameVerifier);
			int code = sniConn.getResponseCode();// Network block
			if (code >= 300 && code < 400) {
				// The locations of the temporary redirects and permanent redirects are case-sensitive
				String location = sniConn.getHeaderField("Location");
				if (location == null) {
					location = sniConn.getHeaderField("location");
				}
				if (!(location.startsWith("http://") || location.startsWith("https://"))) {
					URL originalUrl = new URL(url);
					location = originalUrl.getProtocol() + "://" + "Originally resolved domain name" + location;
				}
				showSniHttpsDemo(location, "Originally resolved domain name");
			} else {
				// The business processes the server response result itself
				DataInputStream dis = new DataInputStream(sniConn.getInputStream());
				int len;
				byte[] buff = new byte[4096];
				StringBuilder response = new StringBuilder();
				while ((len = dis.read(buff)) != -1) {
					response.append(new String(buff, 0, len));
				}
				dis.close();
				Log.d("WGGetHostByName", "response: " + response.toString());
			}
		} catch (Exception e) {
			Log.w("WGGetHostByName", e.getMessage());
		} finally {
			if (sniConn != null) {
				sniConn.disconnect();
			}
		}
		
Customize the SSLSocketFactory:
    class SniSSLSocketFactory extends SSLSocketFactory {
	private HttpsURLConnection conn;

	public SniSSLSocketFactory(HttpsURLConnection conn) {
		this.conn = conn;
	}

	@Override
	public Socket createSocket() throws IOException {
		return null;
	}

	@Override
	public Socket createSocket(String host, int port) throws IOException, UnknownHostException {
		return null;
	}

	@Override
	public Socket createSocket(String host, int port, InetAddress localHost, int localPort) throws IOException, UnknownHostException {
		return null;
	}

	@Override
	public Socket createSocket(InetAddress host, int port) throws IOException {
		return null;
	}

	@Override
	public Socket createSocket(InetAddress address, int port, InetAddress localAddress, int localPort) throws IOException {
		return null;
	}

	@Override
	public String[] getDefaultCipherSuites() {
		return new String[0];
	}

	@Override
	public String[] getSupportedCipherSuites() {
		return new String[0];
	}

	@Override
	public Socket createSocket(Socket socket, String host, int port, boolean autoClose) throws IOException {
		String mHost = this.conn.getRequestProperty("Host");
		if (mHost == null) {
			mHost = host;
		}
		Log.i("WGGetHostByName", "customized createSocket host is: " + mHost);
		InetAddress address = socket.getInetAddress();
		if (autoClose) {
			socket.close();
		}
		SSLCertificateSocketFactory sslSocketFactory = (SSLCertificateSocketFactory) SSLCertificateSocketFactory.getDefault(0);
		SSLSocket ssl = (SSLSocket) sslSocketFactory.createSocket(address, port);
		ssl.setEnabledProtocols(ssl.getSupportedProtocols());

		if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.JELLY_BEAN_MR1) {
			Log.i("WGGetHostByName", "Setting SNI hostname");
			sslSocketFactory.setHostname(ssl, mHost);
		} else {
			Log.d("WGGetHostByName", "No documented SNI support on Android <4.2, trying with reflection");
			try {
				java.lang.reflect.Method setHostnameMethod = ssl.getClass().getMethod("setHostname", String.class);
				setHostnameMethod.invoke(ssl, mHost);
			} catch (Exception e) {
				Log.w("WGGetHostByName", "SNI not useable", e);
			}
		}
		// verify hostname and certificate
		SSLSession session = ssl.getSession();
		HostnameVerifier mHostnameVerifier = HttpsURLConnection.getDefaultHostnameVerifier();
		if (!mHostnameVerifier.verify(mHost, session))
			throw new SSLPeerUnverifiedException("Cannot verify hostname: " + mHost);
		Log.i("WGGetHostByName",
				"Established " + session.getProtocol() + " connection with " + session.getPeerHost() + " using " + session.getCipherSuite());
		return ssl;
	}
    }

```

### Use Case of Proxy
Please check whether an HTTP proxy is used locally. If yes, it is recommended not to use HttpDNS for domain name resolution.

```
    String host = System.getProperty("http.proxyHost");
    String port= System.getProperty("http.proxyPort");
    if (host != null && port != null) {
	    // Local proxy mode is used
	}
```
