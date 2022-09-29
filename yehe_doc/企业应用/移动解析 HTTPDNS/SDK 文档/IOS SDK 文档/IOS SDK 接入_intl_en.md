## Overview
HTTPDNS helps avoid the failure to access the optimal access point during the traditional local DNS of ISPs. It works by replacing the traditional DNS protocol with the HTTP encryption protocol, with domains not used throughout the process, which greatly reduces the possibility of DNS hijacking.


## Preparations
1. Activate HTTPDNS as instructed in [Activating HTTPDNS](https://intl.cloud.tencent.com/document/product/1130/44461).
2. Add domains to be resolved in the HTTPDNS console as instructed in [Adding a Domain](https://intl.cloud.tencent.com/document/product/1130/44465).
3. In the HTTPDNS console, apply for integrating the SDK as instructed in [SDK Activation Process](https://intl.cloud.tencent.com/document/product/1130/44474).
4. After the SDK is integrated, an authorization ID, AES and DES encryption keys, HTTPS token and other configuration information will be available on the [Development Configuration](https://console.cloud.tencent.com/httpdns/configure) page in the HTTPDNS console.
![](https://qcloudimg.tencent-cloud.cn/raw/5ee8acd231036cf1b74d8fc818fae974.png)
Configuration items required for using the SDK for iOS:
 - **Authorization ID**: The unique ID of a development configuration used in HTTPDNS, namely the `dnsId` parameter in the SDK used for DNS authentication.
 - **DES encryption key**: The `dnsKey` parameter in the SDK, which you need to pass in when using the DES encryption method.
 - **AES encryption key**: The `dnsKey` parameter in the SDK, which you need to pass in when using the AES encryption method.
 - **HTTPS encryption token**: The `token` parameter in the SDK, which you need to pass in when using the HTTPS encryption method.
 -  **IOS APPID**： The `appId` authentication info of the SDK for iOS.


## Installation Package Structure
- Download the latest version of the SDK package [here](https://github.com/tencentyun/httpdns-ios-sdk/tree/master/HTTPDNSLibs).
- Get the open-source repository of the SDK [here](https://github.com/DNSPod/httpdns-sdk-ios).

| Name       | Scope of Application          |
| ------------- |-------------|
| MSDKDns.xcframework | Projects with "Build Setting->C++ Language Dialect" configured as **"GNU++98"** and "Build Setting->C++ Standard Library" configured as **"libstdc++(GNU C++ standard library)"**. |
| MSDKDns_C11.xcframework | Projects with the above-mentioned two items configured as **"GNU++11"** and **"libc++(LLVM C++ standard library with C++11 support)"**, respectively. |

<dx-alert infotype="notice" title="">
For MSDKDns_C11 v1.6.0 or later, the local data storage is added, but you need to add the WCDB package as instructed in [How to integrate WCDB](https://github.com/Tencent/wcdb/wiki#%E5%AE%89%E8%A3%85).
MSDKDns does not support permanently local storage of data. You can choose MSDKDns_C11 as needed.
</dx-alert>



## SDK Integration
HTTPDNS provides two integration methods for iOS:
- Integration through CocoaPods.
- Manual integration.


### Integration through CocoaPods
1. Add the following code in `Podfile` of the project:
```shellsession
# Applicable to projects with "Build Setting->C++ Language Dialect" configured as **"GNU++98"** and "Build Setting->C++ Standard Library" as **"libstdc++(GNU C++ standard library)"**.
  pod 'MSDKDns'
# Applicable to projects with the above-mentioned two items configured as **"GNU++11"** and **"libc++(LLVM C++ standard library with C++11 support)"**, respectively.
# pod 'MSDKDns_C11'
```
2. Save, run `pod install`, and open the project with the `.xcworkspace` file.


<dx-alert infotype="explain" title="">
For more information on `CocoaPods`, see [CocoaPods](https://cocoapods.org/).
</dx-alert>



### Manual integration
For the directions of manual integration, see the following demos:
 - Download the Objective-C demo [here](https://github.com/tencentyun/httpdns-ios-sdk/tree/master/HTTPDNSDemo).
 - Download the Swift demo [here](https://github.com/tencentyun/httpdns-ios-sdk/tree/master/HTTPDNSSwiftDemo).

** (Optional) ** Perform following steps if Tencent Beacon is to be integrated:
<dx-alert infotype="explain" title="">
Developed by the Tencent Beacon team for statistics of mobile applications, the Beacon SDK helps HTTPDNS SDK collect DNS quality data for problem finding.
</dx-alert>
<dx-tabs>
::: For services connected to Beacon

Import `MSDKDns.framework` (or `MSDKDns_C11.framework`, depending on the project configuration) in the `HTTPDNSLibs` directory.
:::
::: For services not connected to Beacon

1. Import dependency libraries (in the `HTTPDNSLibs` directory):
	 - BeaconAPI_Base.framework
	 - `MSDKDns.framework` (or `MSDKDns_C11.framework`, depending on the project configuration)
2. Import system libraries:
	 - libz.tbd
	 - libsqlite3.tbd
	 - libc++.tbd
	 - Foundation.framework
	 - CoreTelephony.framework
	 - SystemConfiguration.framework
	 - CoreGraphics.framework
	 - Security.framework
3. Add the code for registering Beacon in `application:didFinishLaunchingWithOptions:`:
```
// Omit the following code if your service is already connected to Beacon, and call the following code to register Beacon if not.
//******************************
[BeaconBaseInterface setAppKey:@"0000066HQK3XNL5U"];
[BeaconBaseInterface enableAnalytics:@"" gatewayIP:nil];
//******************************
```
<dx-alert infotype="notice" title="">
Add the `-ObjC` flag in `Other Linker Flags`.
</dx-alert>



:::
</dx-tabs>


### SDK initialization

Sample API call:
- In an Objective-C project:
```objc
	DnsConfig *config = new DnsConfig();
	config->dnsIp = @"HTTPDNS server IP";
	config->dnsId = DNS authorization ID;
	config->dnsKey = @"Encryption key";
	config->encryptType = HttpDnsEncryptTypeDES;
	config->debug = YES;
	config->timeout = 2000;
	config->routeIp = @"Split zone IP";
	[[MSDKDns sharedInstance] initConfig: config];
```

- In a Swift project:
```swift
let msdkDns = MSDKDns.sharedInstance() as? MSDKDns;
msdkDns?.initConfig(with: [
		"dnsIp": "HTTPDNS server IP",
		"dnsId": "DNS authorization ID",
		"dnsKey": "Encryption key",
		"encryptType": 0, // 0: DES; 1: AES; 2: HTTPS
]);
```


## Integration Verification

### Log verification
Enable the SDK DEBUG logging (set `debug` in `DnsConfig` to `YES`), find the printed `ReportingEvent, name:HDNSGetHostByName, events: { ... }` log, and check the log info of the local DNS (`ldns_ip` in the log) and HTTPDNS (`hdns_ip` in the log) to see whether the connection is successful.
- The `ldns_ip` key indicates the DNS query results provided by the local DNS.
- The `hdns_ip` key indicates the DNS query results of A records provided by HTTPDNS.
- The `hdns_4a_ips` key indicates the DNS query results of AAAA records provided by HTTPDNS.
- If `hdns_ip` or `hdns_4a_ips` is not empty, the connection is successful.


## Notes
- If the service on the client is bound to the host, such as the HTTP service or the CDN service of the host, you need to specify the host field of the HTTP header after replacing the domain in the URL with the IP returned by HTTPDNS.
<dx-tabs>
::: NSURLConnection
```
NSURL *httpDnsURL = [NSURL URLWithString:@"URL obtained by concatenating the resolved IP"];
float timeOut = The set timeout period;
NSMutableURLRequest *mutableReq = [NSMutableURLRequest requestWithURL:httpDnsURL cachePolicy:NSURLRequestUseProtocolCachePolicy timeoutInterval: timeOut];
[mutableReq setValue:@"original domain" forHTTPHeaderField:@"host"];
NSURLConnection *connection = [[NSURLConnection alloc] initWithRequest:mutableReq delegate:self];
[connection start];
```

:::
::: NSURLSession
 ```
NSURL *httpDnsURL = [NSURL URLWithString:@"URL obtained by concatenating the resolved IP"];
float timeOut = Set timeout period;
NSMutableURLRequest *mutableReq = [NSMutableURLRequest requestWithURL:httpDnsURL cachePolicy:NSURLRequestUseProtocolCachePolicy timeoutInterval: timeOut];
[mutableReq setValue:@"original domain" forHTTPHeaderField:@"host"];
NSURLSessionConfiguration *configuration = [NSURLSessionConfiguration defaultSessionConfiguration];
NSURLSession *session = [NSURLSession sessionWithConfiguration:configuration delegate:self delegateQueue:[NSOperationQueue currentQueue]];
NSURLSessionTask *task = [session dataTaskWithRequest:mutableReq];
[task resume];
 ```

:::
::: curl
If you want to access `www.qq.com` and the IP obtained by HTTPDNS is `192.168.0.111`, you can perform a call as follows:
```
curl -H "host:www.qq.com" http://192.168.0.111/aaa.txt.
```
:::
::: The `WWW` API of Unity
```    
string httpDnsURL = "URL obtained by concatenating the resolved IP";
Dictionary<string, string> headers = new Dictionary<string, string> ();
headers["host"] = "Original domain";
WWW conn = new WWW (url, null, headers);
yield return conn;
if (conn.error != null) {
	print("error is happened:"+ conn.error);
} else {
	print("request ok" + conn.text);
}
```

:::
</dx-tabs>
- Detect whether an HTTP proxy is used locally, and if yes, we recommend you not resolve domains with HTTPDNS.
  - Detect whether an HTTP proxy is used:
```
	- (BOOL)isUseHTTPProxy {
		CFDictionaryRef dicRef = CFNetworkCopySystemProxySettings();
		const CFStringRef proxyCFstr = (const CFStringRef)CFDictionaryGetValue(dicRef, (const void*)kCFNetworkProxiesHTTPProxy);
		NSString *proxy = (__bridge NSString *)proxyCFstr;
		if (proxy) {
			return YES;
		} else {
			return NO;
		}
	}
```
 - Detect whether an HTTPS proxy is used:
```
	- (BOOL)isUseHTTPSProxy {
		CFDictionaryRef dicRef = CFNetworkCopySystemProxySettings();
		const CFStringRef proxyCFstr = (const CFStringRef)CFDictionaryGetValue(dicRef, (const void*)kCFNetworkProxiesHTTPSProxy);
		NSString *proxy = (__bridge NSString *)proxyCFstr;
		if (proxy) {
			return YES;
		} else {
			return NO;
		}
	}
```

