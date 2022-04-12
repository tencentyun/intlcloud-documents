## Overview
As a general solution to DNS optimization in the mobile internet era, HTTPDNS mainly addresses the following problems:
- Local DNS hijacking/failures
- Inaccurate local DNS scheduling

The HTTPDNS SDK for Android mainly provides DNS and cache management capabilities based on HTTPDNS:
- When the SDK resolves a domain, it first uses HTTPDNS to get the DNS query result. In extreme cases, when HTTPDNS is unavailable, the result provided by the local DNS will be used.
- The DNS query result returned by HTTPDNS will carry the TTL information, which the SDK will use to manage the cache storing the result provided by HTTPDNS.

For more information on HTTPDNS, see here.
You can get the HTTPDNS SDK for Android by [clicking here](https://github.com/tencentyun/httpdns-android-sdk).

## Preparations
1. First, you need to activate HTTPDNS in the [HTTPDNS console](https://console.cloud.tencent.com/httpdns) as instructed in [Activating HTTPDNS](https://intl.cloud.tencent.com/document/product/1130/44461).
2. After activating HTTPDNS, you need to add a domain to be resolved in the HTTPDNS console as instructed in [Adding a Domain](https://intl.cloud.tencent.com/document/product/1130/44465) before you can use it.
3. You need to [activate the SDK](https://intl.cloud.tencent.com/document/product/1130/44474) in the HTTPDNS console.
4. After activating the service, you will be assigned the configuration information such as authorization ID, AES and DES encryption keys, and HTTPS token. To use the SDK for Android, you need to get the following configuration:
![](https://main.qcloudimg.com/raw/9de378622bacb7ce9f67bcf77e4a602f.png)
 - **Authorization ID**: It is the unique ID of a development configuration used in HTTPDNS, i.e., the `dnsId` parameter in the SDK used for DNS authentication.
 - **DES encryption key**: The `dnsKey` parameter in the SDK, which you need to pass in when using the DES encryption method.
 - **AES encryption key**: The `dnsKey` parameter in the SDK, which you need to pass in when using the AES encryption method.
 - **HTTPS encryption token**: The `token` parameter in the SDK, which you need to pass in when using the HTTPS encryption method.
 -  **Android APPID**: The `appkey` of the [SDK for Android](https://intl.cloud.tencent.com/document/product/1130/44473) used for authentication.

## Connection
### Permission configuration

```xml
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.INTERNET" />

<!-- Optional and used to get the mobile phone's IMEI for data reporting -->
<uses-permission android:name="android.permission.READ_PHONE_STATE" />

<!-- Beacon -->
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```

### Compatibility with network security configuration

If targetSdkVersion of the application is 28 (Android 9.0) or later, HTTP network requests are not allowed by default. For more information, see [Opt out of cleartext traffic](https://developer.android.com/training/articles/security-config#Opt%20out%20of%20cleartext%20traffic).
In this case, you need to add the IP used by the HTTPDNS request to the domain allowlist:
- Configure in the `AndroidManifest` file.
```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest ... >
    <application android:networkSecurityConfig="@xml/network_security_config"
                    ... >
        ...
    </application>
</manifest>
```
- Add the `network_security_config.xml` configuration file in the XML directory.
```xml
<?xml version="1.0" encoding="utf-8"?>
<network-security-config>
    <domain-config cleartextTrafficPermitted="true">
        <domain includeSubdomains="false">119.29.29.99</domain>
        <domain includeSubdomains="false">119.29.29.98</domain>
    </domain-config>
</network-security-config>
```

### HTTPDNS connection
Copy `HttpDNSLibs\HTTPDNS_ANDROID_SDK_xxxx.aar` to the corresponding location in the application's `libs` folder.

### Beacon connection (optional)

Copy `HttpDNSLibs\beacon_android_xxxx.jar` to the corresponding location in the application's `libs` folder.
>! 
>- If you have already connected your application to Tencent Beacon, you can skip this step.
>- The Beacon SDK is developed by the Tencent Beacon team for statistical analysis of mobile applications. The HTTPDNS SDK uses the Beacon SDK to collect DNS quality data to assist with problem locating.

### API call
```Java

// Initialize Beacon: If you have already connected to MSDK or IMSDK or separately connected to Tencent Beacon, you don't need to initialize this API
try {
    // Note: You need to enter your own Beacon `appkey` here
    UserAction.setAppKey("0I000LT6GW1YGCP7");
    UserAction.initUserAction(MainActivity.this.getApplicationContext());
} catch (Exception e) {
    Log.e(TAG, "Init beacon failed", e);
}

/**
 * Set `OpenId`: Directly pass in the MSDK `OpenId` if you have already connected to MSDK, or pass "NULL" for other businesses
 *
 * @param String openId
 */
MSDKDnsResolver.getInstance().WGSetDnsOpenId("10000");
```

### SDK initialization

>?
- The service addresses for the HTTP and HTTPS protocols are `119.29.29.98` and `119.29.29.99` respectively (use the `99` IP only when you select an encryption method on your own and the `channel` is `Https`).
- The new version of the APIs now can be accessed at `119.29.29.99/98`, and the original HTTPDNS service address `119.29.29.29` is for development and debugging purposes only without an SLA guarantee, so it is not recommended for business purposes. Migrate your business to `119.29.29.99/98` as soon as possible.
- The IP is as provided in [API Description](https://intl.cloud.tencent.com/document/product/1130/44468).
- When you connect to HTTPDNS through the SDK, if HTTPDNS does not find a DNS query result, the domain will be resolved by the local DNS, and the result provided by the local DNS will be returned.

#### Encryption with DES by default
##### Not reporting abnormal DNS queries by default

```Java
// You can get the following authentication information after activating the service in the Tencent Cloud console (https://console.cloud.tencent.com/httpdns/configure)

/**
 * Initialize HTTPDNS (with DES encryption by default): If you have already connected to MSDK, we recommend you initialize it before initializing HTTPDNS
 *
 * @param context Application context. We recommend you pass in `ApplicationContext`
 * @param appkey Business `appkey`, i.e., SDK `AppID`, which can be applied for and obtained in the Tencent Cloud console (https://console.cloud.tencent.com/httpdns) for data reporting
 * @param dnsid DNS ID, i.e., authorization ID, which can be applied for and obtained in the Tencent Cloud console (https://console.cloud.tencent.com/httpdns) for DNS authentication
 * @param dnskey DNS key, i.e., the encryption key corresponding to the authorization ID, which can be applied for and obtained in the Tencent Cloud console (https://console.cloud.tencent.com/httpdns) for DNS authentication
 * @param dnsIp `dnsIp` passed in, which can be "119.29.29.98" and is as provided in the Tencent Cloud document (https://intl.cloud.tencent.com/document/product/1130/44468)
 * @param debug Specifies whether to enable debug logging. true: yes; false: no. We recommend you enable it during testing and disable it before launch
 * @param timeout DNS request timeout period in milliseconds. We recommend you set it to 1000
 */
MSDKDnsResolver.getInstance().init(MainActivity.this, appkey, dnsid, dnskey, dnsIp, debug, timeout);
```

##### Manually enabling reporting of abnormal DNS queries
```Java
// You can get the following authentication information after activating the service in the Tencent Cloud console (https://console.cloud.tencent.com/httpdns/configure)

/**
 * Initialize HTTPDNS (with DES encryption by default): If you have already connected to MSDK, we recommend you initialize it before initializing HTTPDNS
 *
 * @param context Application context. We recommend you pass in `ApplicationContext`
 * @param appkey Business `appkey`, i.e., SDK `AppID`, which can be applied for and obtained in the Tencent Cloud console (https://console.cloud.tencent.com/httpdns) for data reporting
 * @param dnsid DNS ID, i.e., authorization ID, which can be applied for and obtained in the Tencent Cloud console (https://console.cloud.tencent.com/httpdns) for DNS authentication
 * @param dnskey DNS key, i.e., the encryption key corresponding to the authorization ID, which can be applied for and obtained in the Tencent Cloud console (https://console.cloud.tencent.com/httpdns) for DNS authentication
 * @param dnsIp `dnsIp` passed in, which can be "119.29.29.98" (can be selected only for HTTP requests with the `DesHttp` or `AesHttp` channel) or "119.29.29.99" (can be selected only for HTTPS requests with the `Https` channel) and is as provided in the Tencent Cloud document (https://intl.cloud.tencent.com/document/product/1130/44468)
 * @param debug Specifies whether to enable debug logging. true: yes; false: no. We recommend you enable it during testing and disable it before launch
 * @param timeout DNS request timeout period in milliseconds. We recommend you set it to 1000
 * @param enableReport Specifies whether to enable reporting of abnormal DNS queries. Default value: false (no)
 */
MSDKDnsResolver.getInstance().init(MainActivity.this, appkey, dnsid, dnskey, dnsIp, debug, timeout, enableReport);
```


#### Selecting an encryption method (DesHttp, AesHttp, or Https)

```Java
/**
 * Initialize HTTPDNS (with a selected encryption method): If you have already connected to MSDK, we recommend you initialize it before initializing HTTPDNS
 *
 * @param context Application context. We recommend you pass in `ApplicationContext`
 * @param appkey Business `appkey`, i.e., SDK `AppID`, which can be applied for and obtained in the Tencent Cloud console (https://console.cloud.tencent.com/httpdns) for data reporting
 * @param dnsid DNS ID, i.e., authorization ID, which can be applied for and obtained in the Tencent Cloud console (https://console.cloud.tencent.com/httpdns) for DNS authentication
 * @param dnskey DNS key, i.e., the encryption key corresponding to the authorization ID, which can be applied for and obtained in the Tencent Cloud console (https://console.cloud.tencent.com/httpdns) for DNS authentication
 * @param dnsIp `dnsIp` passed in, which can be "119.29.29.98" (can be selected only for HTTP requests with the `DesHttp` or `AesHttp` channel) or "119.29.29.99" (can be selected only for HTTPS requests with the `Https` channel) and is as provided in the Tencent Cloud document (https://intl.cloud.tencent.com/document/product/1130/44468)
 * @param debug Specifies whether to enable debug logging. true: yes; false: no. We recommend you enable it during testing and disable it before launch
 * @param timeout DNS request timeout period in milliseconds. We recommend you set it to 1000
 * @param channel Channel. Valid values: DesHttp (default), AesHttp, Https
 * @param token Token, which can be applied for and obtained in the Tencent Cloud console (https://console.cloud.tencent.com/httpdns) for HTTPS verification
 * @param enableReport Specifies whether to enable reporting of abnormal DNS queries. Default value: false (no)
 */
MSDKDnsResolver.getInstance().init(MainActivity.this, appkey, dnsid, dnskey, dnsIp, debug, timeout, channel, token, true);
```

### API call
```Java

/**
 * HTTPDNS' sync DNS API
 * The cache is queried first. If the cache is hit, the result will be returned; otherwise, a sync DNS request will be sent
 * The latest DNS query result will be returned after the query is completed
 * The returned value string will be separated by semicolon, with the resolved IPv4 address ("0" if DNS query fails) before the semicolon and the resolved IPv6 address ("0" if DNS fails) after it
 * Sample response: 121.14.77.221;2402:4e00:1020:1404:0:9227:71a3:83d2
 * @param domain Domain (such as www.qq.com)
 * @return Set of resolved IP results that correspond to the domain
 */
String ips = MSDKDnsResolver.getInstance().getAddrByName(domain);

/**
 * HTTPDNS' batch sync DNS API
 * The cache is queried first. If the cache is hit, the result will be returned; otherwise, a sync DNS request will be sent
 * The latest DNS query result will be returned after the query is completed
 * The returned value `ipSet` is the set of resolved IP addresses
 * `ipSet.v4Ips` is the set of resolved IPv4 addresses, which may be `null`
 * `ipSet.v6Ips` is the set of resolved IPv6 addresses, which may be `null`
 * Sample response for a single domain: IpSet{v4Ips=[121.14.77.201, 121.14.77.221], v6Ips=[2402:4e00:1020:1404:0:9227:71ab:2b74, 2402:4e00:1020:1404:0:9227:71a3:83d2], ips=null}
 * Sample response for multiple domains: IpSet{v4Ips=[www.baidu.com:14.215.177.39, www.baidu.com:14.215.177.38, www.youtube.com:104.244.45.246], v6Ips=[www.youtube.com.:2001::1f0:5610], ips=null}
 * @param domain Multiple domains can be separated by comma, such as `qq.com,baidu.com`
 * @return Set of resolved IP results that correspond to the domain
 */
Ipset ips = MSDKDnsResolver.getInstance().getAddrsByName(domain);


// Async callback. Note that all async requests need to be used together with async callbacks
MSDKDnsResolver.getInstance().setHttpDnsResponseObserver(new HttpDnsResponseObserver() {
    @Override
    public void onHttpDnsResponse(String tag, String domain, Object ipResultSemicolonSep) {
        long elapse = (System.currentTimeMillis() - Long.parseLong(tag));
        String lookedUpResult = "[[getAddrByNameAsync]]:ASYNC:::" + ipResultSemicolonSep +
                ", domain:" + domain +  ", tag:" + tag +
                ", elapse:" + elapse;
    }
});

/**
 * HTTPDNS' async DNS API (to be used together with async callback)
 * The cache is queried first. If the cache is hit, the result will be returned; otherwise, an async DNS request will be sent
 * The latest DNS query result will be returned asynchronously after the query is completed
 * @param domain Domain (such as www.qq.com)
 */
MSDKDnsResolver.getInstance()
    .getAddrByNameAsync(hostname, String.valueOf(System.currentTimeMillis()))

/**
 * HTTPDNS' batch async DNS API (to be used together with async callbacks)
 * The cache is queried first. If the cache is hit, the result will be returned; otherwise, a sync DNS request will be sent
 * The latest DNS query result will be returned asynchronously after the query is completed
 * @param domain Multiple domains can be separated by comma, such as `qq.com,baidu.com`
 */
MSDKDnsResolver.getInstance()
    .getAddrsByNameAsync(hostname, String.valueOf(System.currentTimeMillis()))
```

### Connection verification

#### Log verification

When you pass in `true` for the `debug` parameter in the `init` API to filter logs with the `HTTPDNS` tag, if you see logs related to the local DNS (`ldns_ip`) and HTTPDNS (`hdns_ip`), the connection is correct.
- The `ldns_ip` key indicates the DNS query results provided by the local DNS.
- The `hdns_ip` key indicates the DNS query results of A records provided by HTTPDNS.
- The `hdns_4a_ips` key indicates the DNS query results of AAAA records provided by HTTPDNS.
- The `a_ips` key indicates the set of IPv4 addresses returned by the DNS API.
- The `4a_ips` key indicates the set of IPv6 addresses returned by the DNS API.

#### Simulating local DNS hijacking

When you simulate hijacking the local DNS, if the application works properly, HTTPDNS has been connected to successfully.
>!Due to the caching mechanism of the local DNS, when simulating the local DNS for connection verification, make sure that the cache of the local DNS has been cleared. You can clear the cache by restarting the server or switching the network. During verification, be sure to compare the effects of the local DNS and HTTPDNS.
>
- Modify the hosts file on your server.
  - The local DNS gets the DNS query result by reading the hosts file on your server first.
  - You can simulate hijacking the local DNS by modifying the hosts file to point the domain to an incorrect IP.
  - You can directly modify the hosts file on a root server.
- Modify the DNS server configuration.
  - You can simulate hijacking the local DNS by modifying the configuration of the DNS server to point it to an unavailable IP (such as another IP on the LAN).
  - When your server is connected to Wi-Fi, you can modify the DNS server settings by changing the IP settings to **Static** in the **Advanced Settings** option of the Wi-Fi (this operation may vary slightly by server).
  - Use a DNS modifier to modify the DNS server configuration (usually by tampering with the DNS packet through VPN).

#### Packet capture verification

The following takes accessing a network over HTTP as an example:
- Use **tcpdump** to capture packets.
>!Common mobile HTTP/HTTPS packet capture tools (such as Charles and Fiddler) capture packets through an HTTP proxy, so they are not suitable for verifying whether HTTPDNS works. For more information, see [Using HTTP proxy locally](#local).
>
  - You can use the `tcpdump` command to capture packets on a root server.
  - On a non-root server, the system may have a built-in debugging tool that can be used to get the packet capture result (the enabling method varies by server).
- Observe the packet capture result with **WireShark**.
  - For HTTP requests, you can observe plaintext information and confirm whether the IP used during request sending is the one returned by the SDK by comparing the log and the specific packet capture record, as shown below: 
![](https://main.qcloudimg.com/raw/63464903e3861007c1c9cb2130781701.png)
From the perspective of packet capture, the request for `xw.qq.com` is eventually sent to the server at the IP address `183.3.226.35`.
  - For HTTPS requests, a TLS handshake packet is actually a plaintext packet. After setting the SNI extension (see [HTTPS compatibility](#HTTPS)), you can verify whether the IP used during request sending is the one returned by the SDK by comparing the log and the specific packet capture record, as shown below:
![](https://main.qcloudimg.com/raw/544370c87fb2d09029699fb1f0db30d9.png)
    From the perspective of packet capture, the request for `xw.qq.com` is eventually sent to the server at the IP address `183.3.226.35`.


### Notes
- `getAddrByName` is a time-consuming sync API, so it should be called on a child thread.
- If the business on the client is bound to the host, such as the HTTP service of the host or the CDN service, you need to specify the host field of the HTTP header after replacing the domain in the URL with the IP returned by HTTPDNS.
 - Take `URLConnection` as an example:
```Java
URL oldUrl = new URL(url);
URLConnection connection = oldUrl.openConnection();
// Get the HTTPDNS query result 
String ips = MSDKDnsResolver.getInstance().getAddrByName(oldUrl.getHost());
String[] ipArr = ips.split(";");
if (2 == ipArr.length && !"0".equals(ipArr[0])) { // Get the IP successfully through HTTPDNS, replace the URL, and set the host header
    String ip = ipArr[0];
    String newUrl = url.replaceFirst(oldUrl.getHost(), ip);
    connection = (HttpURLConnection) new URL(newUrl).openConnection(); // Set the host field of the HTTP request header
    connection.setRequestProperty("Host", oldUrl.getHost());
}
```
 - Taking curl as an example, if you want to access `www.qq.com`, and the IP obtained by HTTPDNS is `192.168.0.111`, then you can access it as follows:
```shell
curl -H "Host:www.qq.com" http://192.168.0.111/aaa.txt
```
- Detect whether an HTTP proxy is used locally, and if so, we recommend you **not use HTTPDNS** to resolve domains. Below is a sample:
```Java
String host = System.getProperty("http.proxyHost");
String port= System.getProperty("http.proxyPort");
if (null != host && null != port) {
    // Local proxy mode is used
}
```

## Practice of Connecting HTTP Network Access to HTTPDNS SDK

In general, there are two ways to integrate the DNS capability of the HTTPDNS SDK into the HTTP (HTTPS) network access process:

- Replace the host part in the URL to get a new URL for accessing the network.
  In this implementation scheme, the URL discards the domain information; therefore, for network requests that require domain information, there is a lot of work to do to ensure compatibility.
- Inject the DNS capability of HTTPDNS into the network access process and replace the local DNS in the original process.
  - In this implementation scheme, you don't need to modify the URLs of the requests one by one, so there is no need to conduct extra work to ensure compatibility, but the network library used on the business side must support DNS replacement.
  - DNS replacement can be implemented by hooking the system's DNS function, but the function is already used in the HTTPDNS SDK, so hooking the function again may cause recursive calls or even stack overflow.

For more information on how to connect to different network libraries, see the corresponding connection documents (in the current directory) and the samples (in the `HttpDnsSample` directory).

### Compatibility for URL replacement
As described above, for network requests that require domain information (usually when multiple domains are mapped to the same IP), you need to conduct extra work to ensure compatibility. The following describes how to ensure compatibility from the perspective of protocols, and the specific implementation method is subject to the implementation of the network library.

#### HTTP compatibility
For HTTP requests, you need to notify the server of the domain information by specifying the host field in the header. For more information on the host field, see [Host](https://tools.ietf.org/html/rfc2616#page-128).

#### HTTPS compatibility [](id:HTTPS)
- HTTPS is a version of HTTP over TLS; therefore, for HTTPS requests, you also need to set the host field.
- In HTTPS requests, you should perform a TLS handshake first. During the TLS handshake, the server will send its own digital certificate to you for identity verification; therefore, you also need to notify the server of the domain information during the TLS handshake. In the TLS protocol, you can specify the domain information by using the SNI extension as detailed in [Server Name Indication](https://tools.ietf.org/html/rfc6066#page-6).

### Using HTTP proxy locally[](id:local)
If an HTTP proxy is used locally, we recommend you **not use HTTPDNS** to resolve domains.
The following makes a distinction between the two connection methods with a detailed analysis:

#### URL replacement
According to the HTTP/1.1 protocol, when an HTTP proxy is used, the request line will carry complete server address information on the client. For more information, see [origin-form](https://tools.ietf.org/html/rfc7230#page-42).
In this case (i.e., an HTTP proxy is used locally, the business has been connected to the HTTPDNS SDK by replacing the URL, and the host field has been set correctly), the HTTP request received by the HTTP proxy will contain the server IP information (in the request line) and domain information (in the host field). However, how the HTTP proxy will send the HTTP request to the real destination server depends on the proxy implementation, and the proxy may directly discard the set host field, causing the network request to fail.

#### DNS implementation replacement
Taking the OkHttp network library as an example, after the HTTP proxy is enabled locally, OkHttp will resolve only the host of the configured HTTP proxy but not the host field in the HTTP request. In this case, it is useless to enable HTTPDNS.

#### Determining whether an HTTP proxy is used locally
The code for determination is as follows:

```kotlin
val host = System.getProperty("http.proxyHost")
val port = System.getProperty("http.proxyPort")
if (null != host && null != port) {
    // An HTTP proxy is used locally
}
```

## Practice Scenario

### OkHttp

OkHttp provides a DNS API to inject a DNS implementation into OkHttp. Thanks to the excellent design of OkHttp, when OkHttp is used to access the network, you can connect to HTTPDNS to resolve domains by implementing the DNS API with no extra work required even in complex scenarios (HTTP/HTTPS + SNI), which causes little intrusion. Below is a sample:

```Java
mOkHttpClient =
    new OkHttpClient.Builder()
        .dns(new Dns() {
            @NonNull
            @Override
            public List<InetAddress> lookup(String hostname) {
                Utils.checkNotNull(hostname, "hostname can not be null");
                String ips = MSDKDnsResolver.getInstance().getAddrByName(hostname);
                String[] ipArr = ips.split(";");
                if (0 == ipArr.length) {
                    return Collections.emptyList();
                }
                List<InetAddress> inetAddressList = new ArrayList<>(ipArr.length);
                for (String ip : ipArr) {
                    if ("0".equals(ip)) {
                        continue;
                    }
                    try {
                        InetAddress inetAddress = InetAddress.getByName(ip);
                        inetAddressList.add(inetAddress);
                    } catch (UnknownHostException ignored) {
                    }
                }
                return inetAddressList;
            }
        })
        .build();
```

>! Implementing the DNS API means that all network requests processed by the current OkHttpClient instance will go through HTTPDNS. If you have only a small number of domains to be resolved by HTTPDNS, we recommend you filter them before calling the DNS API of HTTPDNS.

### Retrofit + OkHttp
Retrofit is actually a library that adds a layer of encapsulation bridging to the API based on OkHttp. Therefore, you can connect to HTTPDNS simply by customizing the OkHttpClient in Retrofit like in the OkHttp connection method as shown below:
```Java
mRetrofit =
    new Retrofit.Builder()
        .client(mOkHttpClient)
        .baseUrl(baseUrl)
        .build();
```

### WebView

The Android system provides APIs to intercept network requests and inject custom logic in WebView. You can get the host of a URL request by intercepting various types of network requests from WebView, call HTTPDNS to resolve the host, and then request the network address by using the new URL formed with the obtained IP.
```Java
mWebView.setWebViewClient(new WebViewClient() {
    // Use this method for API 21 or later
    @SuppressLint("NewApi")
    @Override
    public WebResourceResponse shouldInterceptRequest(WebView view, WebResourceRequest request) {
        if (request != null && request.getUrl() != null && request.getMethod().equalsIgnoreCase("get")) {
            String scheme = request.getUrl().getScheme().trim();
            String url = request.getUrl().toString();
            Log.d(TAG, "url:" + url);
            // HTTPDNS resolves the network and image requests of CSS files
            if ((scheme.equalsIgnoreCase("http") || scheme.equalsIgnoreCase("https"))
            && (url.contains(".css") || url.endsWith(".png") || url.endsWith(".jpg") || url .endsWith(".gif"))) {
                try {
                    URL oldUrl = new URL(url);
                    URLConnection connection = oldUrl.openConnection();
                    // Get the HTTPDNS query result
                    String ips = MSDKDnsResolver.getInstance().getAddrByName(oldUrl.getHost());
                    String[] ipArr = ips.split(";");
                    if (2 == ipArr.length && !"0".equals(ipArr[0])) { // Get the IP successfully through HTTPDNS, replace the URL, and set the host header
                        String ip = ipArr[0];
                        String newUrl = url.replaceFirst(oldUrl.getHost(), ip);
                        connection = (HttpURLConnection) new URL(newUrl).openConnection(); // Set the host field of the HTTP request header
                        connection.setRequestProperty("Host", oldUrl.getHost());
                    }
                    Log.d(TAG, "contentType:" + connection.getContentType());
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

    // Use this method for API 11–20
    public WebResourceResponse shouldInterceptRequest(WebView view, String url) {
        if (!TextUtils.isEmpty(url) && Uri.parse(url).getScheme() != null) {
            String scheme = Uri.parse(url).getScheme().trim();
            Log.d(TAG, "url:" + url);
            // HTTPDNS resolves the network and image requests of CSS files
            if ((scheme.equalsIgnoreCase("http") || scheme.equalsIgnoreCase("https"))
            && (url.contains(".css") || url.endsWith(".png") || url.endsWith(".jpg") || url.endsWith(".gif"))) {
                try {
                    URL oldUrl = new URL(url);
                    URLConnection connection = oldUrl.openConnection();
                    // Get the HTTPDNS query result
                    String ips = MSDKDnsResolver.getInstance().getAddrByName(oldUrl.getHost());
                    String[] ipArr = ips.split(";");
                    if (2 == ipArr.length && !"0".equals(ipArr[0])) { // Get the IP successfully through HTTPDNS, replace the URL, and set the host header
                        String ip = ipArr[0];
                        String newUrl = url.replaceFirst(oldUrl.getHost(), ip);
                        connection = (HttpURLConnection) new URL(newUrl).openConnection(); // Set the host field of the HTTP request header
                        connection.setRequestProperty("Host", oldUrl.getHost());
                    }
                    Log.d(TAG, "contentType:" + connection.getContentType());
                    return new WebResourceResponse("text/css", "UTF-8", connection.getInputStream());
                } catch (MalformedURLException e) {
                    e.printStackTrace();
                } catch (IOException e) {
                }
            }
        }
        return null;
    }});
// Load web resources
mWebView.loadUrl(targetUrl);
```

### HttpURLConnection

- The sample for HTTPS is as follows:
```Java
 // Take the domain `www.qq.com` and the IP `192.168.0.1` obtained by HTTPDNS as an example
String url = "https://192.168.0.1/"; // Your own request connection
 HttpsURLConnection connection = (HttpsURLConnection) new URL(url).openConnection();
 connection.setRequestProperty("Host", "www.qq.com");
 connection.setHostnameVerifier(new HostnameVerifier() {
 	@Override
 	public boolean verify(String hostname, SSLSession session) {
 		return HttpsURLConnection.getDefaultHostnameVerifier().verify("www.qq.com", session);
 	}
 });
 connection.setConnectTimeout(mTimeOut); // Set the connection timeout period
 connection.setReadTimeout(mTimeOut); // Set the stream read timeout period
 connection.connect();
```
- The sample for HTTPS + SNI is as follows:
```Java
 // Take the domain `www.qq.com` and the IP `192.168.0.1` obtained by HTTPDNS as an example
 String url = "https://192.168.0.1/"; // Encapsulate the business' request URL with the IP obtained by HTTPDNS
 HttpsURLConnection sniConn = null;
 try {
 	sniConn = (HttpsURLConnection) new URL(url).openConnection();
 	// Set the host field of the HTTP request header
 	sniConn.setRequestProperty("Host", "www.qq.com");
 	sniConn.setConnectTimeout(3000);
 	sniConn.setReadTimeout(3000);
 	sniConn.setInstanceFollowRedirects(false);
 	// Customize SSLSocketFactory to carry the requested domain ***(key step)
 	SniSSLSocketFactory sslSocketFactory = new SniSSLSocketFactory(sniConn);
 	sniConn.setSSLSocketFactory(sslSocketFactory);
 	// Verify whether the hostname and the server authentication scheme match
 	HostnameVerifier hostnameVerifier = new HostnameVerifier() {
 		@Override
 		public boolean verify(String hostname, SSLSession session) {
 			return HttpsURLConnection.getDefaultHostnameVerifier().verify("originally resolved domain", session);
 		}
 	};
 	sniConn.setHostnameVerifier(hostnameVerifier);
 	...
 } catch (Exception e) {
 	Log.w(TAG, "Request failed", e);
 } finally {
 	if (sniConn != null) {
 		sniConn.disconnect();
 	}
 }

 class SniSSLSocketFactory extends SSLSocketFactory {
 
 	private HttpsURLConnection mConn;

 	public SniSSLSocketFactory(HttpsURLConnection conn) {
 		mConn = conn;
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
 		String realHost = mConn.getRequestProperty("Host");
 		if (realHost == null) {
 			realHost = host;
 		}
 		Log.i(TAG, "customized createSocket host is: " + realHost);
 		InetAddress address = socket.getInetAddress();
 		if (autoClose) {
 			socket.close();
 		}
 		SSLCertificateSocketFactory sslSocketFactory = (SSLCertificateSocketFactory) SSLCertificateSocketFactory.getDefault(0);
 		SSLSocket ssl = (SSLSocket) sslSocketFactory.createSocket(address, port);
 		ssl.setEnabledProtocols(ssl.getSupportedProtocols());
 		if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.JELLY_BEAN_MR1) {
 			Log.i(TAG, "Setting SNI hostname");
 			sslSocketFactory.setHostname(ssl, realHost);
 		} else {
 			Log.d(TAG, "No documented SNI support on Android < 4.2, trying with reflection");
 			try {
 				Method setHostnameMethod = ssl.getClass().getMethod("setHostname", String.class);
 				setHostnameMethod.invoke(ssl, realHost);
 			} catch (Exception e) {
 				Log.w(TAG, "SNI not useable", e);
 			}
 		}
 		// verify hostname and certificate
 		SSLSession session = ssl.getSession();
 		HostnameVerifier hostnameVerifier = HttpsURLConnection.getDefaultHostnameVerifier();
 		if (!hostnameVerifier.verify(realHost, session)) {
 			throw new SSLPeerUnverifiedException("Cannot verify hostname: " + realHost);
 		}			
 		Log.i(TAG, "Established " + session.getProtocol() + " connection with " + session.getPeerHost() + " using " + session.getCipherSuite());
 		return ssl;
 	}
 }
```

### Unity

- Initialize the HTTPDNS and Beacon APIs
>! If you have connected to MSDK or separately connected to Tencent Beacon, you don't need to initialize Beacon.
>
	The example is as follows:
```C#
 private static AndroidJavaObject sHttpDnsObj;
 public static void Init() {
 	AndroidJavaClass unityPlayerClass = new AndroidJavaClass("com.unity3d.player.UnityPlayer");
 	if (unityPlayerClass == null) {
 		return;
 	}	
 	AndroidJavaObject activityObj = unityPlayerClass.GetStatic<AndroidJavaObject>("currentActivity");
 	if (activityObj == null) {
 		return;
 	}
 	AndroidJavaObject contextObj = activityObj.Call<AndroidJavaObject>("getApplicationContext");
 	// Initialize HTTPDNS
 	AndroidJavaObject httpDnsClass = new AndroidJavaObject("com.tencent.msdk.dns.MSDKDnsResolver");
 	if (httpDnsClass == null) {
 		return;
 	}
 	sHttpDnsObj = httpDnsClass.CallStatic<AndroidJavaObject>("getInstance");
 	if (sHttpDnsObj == null) {
 		return;
 	}
 	sHttpDnsObj.Call("init", contextObj, appkey, dnsid, dnskey, debug, timeout);
 }
```
- Call the `getAddrByName` API to resolve a domain as shown below:
```C#
// We recommend you perform this operation on a child thread or with Coroutine
// Note that you need to call the `AttachCurrentThread` and `DetachCurrentThread` functions before calling the `getAddrByName` API on the child thread 
public static string GetHttpDnsIP(string url) {
	string ip = string.Empty;
	AndroidJNI.AttachCurrentThread(); // You need to add this when calling the `getAddrByName` API on the child thread
	// Get the IP configuration set
	string ips = sHttpDnsObj.Call<string>("getAddrByName", url);
	AndroidJNI.DetachCurrentThread(); // You need to add this when calling the `getAddrByName` API on the child thread
	if (null != ips) {
		string[] ipArr = ips.Split(';');
        if (2 == ipArr.Length && !"0".Equals(ipArr[0]))
		ip = ipArr[0];
	}
	return ip;
}
```

​	
