## Overview
HTTPDNS helps avoid the failure to access the optimal access point caused by the traditional local DNS of ISPs. It works by replacing the traditional DNS protocol with the HTTP encryption protocol, and domains are not used throughout the process, which greatly reduces the possibility of being hijacked.

## Preparations
1. First, you need to activate HTTPDNS in the [HTTPDNS console](https://console.cloud.tencent.com/httpdns) as instructed in [Activating HTTPDNS](https://intl.cloud.tencent.com/document/product/1130/44461).
2. After activating HTTPDNS, you need to add a domain to be resolved in the HTTPDNS console as instructed in [Adding a Domain](https://intl.cloud.tencent.com/document/product/1130/44465) before you can use it.
4. You need to [activate the SDK](https://intl.cloud.tencent.com/document/product/1130/44474) in the HTTPDNS console.
5. After activating the service, you will be assigned the configuration information such as authorization ID, AES and DES encryption keys, and HTTPS token. To use the SDK for iOS, you need to get the following configuration:
![](https://main.qcloudimg.com/raw/0a4481963d31b07e20a3136021fb4743.png)
 - **Authorization ID**: It is the unique ID of a development configuration used in HTTPDNS, i.e., the `dnsId` parameter in the SDK used for DNS authentication.
 - **DES encryption key**: The `dnsKey` parameter in the SDK, which you need to pass in when using the DES encryption method.
 - **AES encryption key**: The `dnsKey` parameter in the SDK, which you need to pass in when using the AES encryption method.
 - **HTTPS encryption token**: The `token` parameter in the SDK, which you need to pass in when using the HTTPS encryption method.
 -  **iOS APPID**: the `appId (application ID)` authentication information of the [SDK for iOS](https://intl.cloud.tencent.com/document/product/1130/44472).


## Installation Package Structure
- The latest version of the SDK package can be downloaded [here](https://github.com/tencentyun/httpdns-ios-sdk/tree/master/HTTPDNSLibs).
- The open-source repository of the SDK is [here](https://github.com/DNSPod/httpdns-sdk-ios).

| Name       | Applicable Scope           |
| ------------- |-------------|
| MSDKDns.xcframework | Applicable to projects with "Build Setting->C++ Language Dialect" configured as **"GNU++98"** and "Build Setting->C++ Standard Library" configured as **"libstdc++(GNU C++ standard library)"**. |
| MSDKDns_C11.xcframework | Applicable to projects with the two items configured as **"GNU++11"** and **"libc++(LLVM C++ standard library with C++11 support)"** respectively. |


## SDK Integration
HTTPDNS provides two integration methods for iOS:
- Integration through CocoaPods.
- Manual integration.

For the directions of manual integration, see the following demos:
- The Objective-C demo can be downloaded [here](https://github.com/tencentyun/httpdns-ios-sdk/tree/master/HTTPDNSDemo).
- The Swift demo can be downloaded [here](https://github.com/tencentyun/httpdns-ios-sdk/tree/master/HTTPDNSSwiftDemo).


### Integration through CocoaPods
Add the following code in the `Podfile` of the project:
```
# Applicable to projects with "Build Setting->C++ Language Dialect" configured as **"GNU++98"** and "Build Setting->C++ Standard Library" configured as **"libstdc++(GNU C++ standard library)"**.
  pod 'MSDKDns'
# Applicable to projects with the two items configured as **"GNU++11"** and **"libc++(LLVM C++ standard library with C++11 support)"** respectively.
# pod 'MSDKDns_C11'
```
Save, run `pod install`, and open the project with a file with the `.xcworkspace` extension.

>?For more information on `CocoaPods`, visit the [CocoaPods website](https://cocoapods.org/).

### Manual integration

#### For business connected to Beacon (optional)
>?The Beacon SDK is developed by the Tencent Beacon team for statistical analysis of mobile applications. The HTTPDNS SDK uses the Beacon SDK to collect DNS quality data to assist with problem locating.
>
Import `MSDKDns.framework` (or `MSDKDns_C11.framework`, depending on the project configuration) in the `HTTPDNSLibs` directory.

#### For business not connected to Beacon (optional)
- Import dependent libraries (in the `HTTPDNSLibs` directory):
	- BeaconAPI_Base.framework
	- `MSDKDns.framework` (or `MSDKDns_C11.framework`, depending on the project configuration)
- Import system libraries:
	- libz.tbd
	- libsqlite3.tbd
	- libc++.tbd
	- Foundation.framework
	- CoreTelephony.framework
	- SystemConfiguration.framework
	- CoreGraphics.framework
	- Security.framework
- Add the code for registering Beacon in `application:didFinishLaunchingWithOptions:`:
```
// Ignore the following code if your business is already connected to Beacon; otherwise, call the following code to register Beacon
//******************************
[BeaconBaseInterface setAppKey:@"0000066HQK3XNL5U"];
[BeaconBaseInterface enableAnalytics:@"" gatewayIP:nil];
//******************************
```
>!Add the `-ObjC` flag in `Other Linker Flags`.

## API and Use Case

### Setting basic business information

#### Type definition

```c++

/**
	Encryption method
**/
typedef enum {
    HttpDnsEncryptTypeDES = 0, // DES encryption
    HttpDnsEncryptTypeAES = 1, // AES encryption
    HttpDnsEncryptTypeHTTPS = 2 // HTTPS encryption
} HttpDnsEncryptType;

/**
	Configuration structure
	You can get the following authentication information after activating the service in the Tencent Cloud console (https://console.cloud.tencent.com/httpdns/configure).
**/
typedef struct DnsConfigStruct {
    NSString* appId; // Application ID, which is optional and can be applied for and obtained in the Tencent Cloud console. It is used for Beacon data reporting (and will not take effect if Beacon is not integrated)
    int dnsId; // Authorization ID, which you can directly view in the Tencent Cloud console after applying
    NSString* dnsKey; // Encryption key, which you must pass in for the AES or DES encryption method and can view in the Tencent Cloud console after applying. It is used for DNS authentication
    NSString* token; // Encryption token, which you must pass in for the HTTPS encryption method
    NSString* dnsIp; // HTTPDNS server IP. The service addresses for the HTTP and HTTPS protocols are `119.29.29.98` and `119.29.29.99` respectively
    BOOL debug; // Specify whether to enable debug logging. YES: enable; NO: disable. We recommend you enable it during joint testing and disable it before launch
    int timeout; // Timeout period in milliseconds, which is optional. If you set it to `0`, the default value `2000ms` will be used
    HttpDnsEncryptType encryptType; // Control the encryption method
    NSString* routeIp; // The ECS (EDNS-Client-Subnet) value of the DNS request. By default, the HTTPDNS server will query the client's egress IP in order to query the IP for the DNS split zone. You can specify the split zone's IP address by passing in an IPv4/IPv6 address
    BOOL httpOnly;// This parameter is optional. It specifies whether to return only the DNS query result provided by HTTPDNS. false (default): when HTTPDNS query fails, the DNS query result provided by the local DNS will be returned; true: only the DNS query result provided by HTTPDNS will be returned
    NSUInteger retryTimesBeforeSwitchServer; // Number of retries before the IP switch, which is optional and 3 by default
    NSUInteger minutesBeforeSwitchToMain; // Interval for switching back to the main IP, which is optional and 10 minutes by default
    BOOL enableReport; // Specify whether to enable reporting of abnormal DNS queries. Default value: NO
} DnsConfig;
```

#### API declaration

```objc
/**
 Set the basic business information (for Tencent Cloud services)

 @param config Business configuration structure
 @return YES: set successfully; NO: failed to set
 */
- (BOOL) initConfig:(DnsConfig *)config;

/**
 * It is configured through `Dictionary` as for the `DnsConfig` structure. It is used for compatibility with Swift projects to address the inability to recognize the `DnsConfig` type in Swift projects
 *
 * @param config Configuration
 * @return YES: set successfully; NO: failed to set
 */
- (BOOL) initConfigWithDictionary:(NSDictionary *)config;
```
#### Sample code

Sample API call:
- In an Objective-C project:
```objc
	DnsConfig *config = new DnsConfig();
	config->dnsIp = @"HTTPDNS server IP";
	config->dnsId = @"DNS authorization ID";
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

### DNS API

**There are the following four APIs to get IPs**, and you only need to import the header file to call the corresponding API.
- Sync API 
	-	Single query API **WGGetHostByName:**;
	- Batch query API **WGGetHostsByNames:**;
- Async API 
	- Single query API **WGGetHostByNameAsync:returnIps:**;
	- Batch query API **WGGetHostsByNamesAsync:returnIps:**;

**The returned address is in the following format:**
- **Single query**: The single query API will return `NSArray` with a fixed length of 2, where the first value is the IPv4 address, and the second value is the IPv6 address. The response format is as described below:
 - Under IPv4, only the IPv4 address will be returned; that is, the response format will be `[ipv4, 0]`.
 - Under IPv6, only the IPv6 address will be returned; that is, the response format will be `[0, ipv6]`.
 - Under a dual stack network, the resolved IPv4 and IPv6 addresses (if they exist) will be returned; that is, the response format will be `[ipv4, ipv6]`.
 - If DNS query fails, `[0, 0]` will be returned; in this case, you only need to call the `WGGetHostByName` API again.
- **Batch query**: The batch query API will return a `NSDictionary`, where `key` is the queried domain, `value` is `NSArray` with a fixed length of 2. The first value is the IPv4 address, and the second value is the IPv6 address. The response format is as described below:
 - Under IPv4, only the IPv4 address will be returned; that is, the response format will be `{"queryDomain" : [ipv4, 0]}`.
 - Under IPv6, only the IPv6 address will be returned; that is, the response format will be `{"queryDomain" : [0, ipv6]}`.
 - Under a dual stack network, the resolved IPv4 and IPv6 addresses (if they exist) will be returned; that is, the response format will be `{"queryDomain" : [ipv4, ipv6]}`.
 - If DNS query fails, `{"queryDomain" : [0, 0]}` will be returned; in this case, you only need to call the `WGGetHostByNames` API again.

>!
>- When you make a URL request by using an IPv6 address, you need to enclose the IPv6 address in square brackets, such as `http://[64:ff9b::b6fe:7475]/`.
>- If the IPv6 address is 0, you can directly use the IPv4 address for connection.
>- If the IPv4 address is 0, you can directly use the IPv6 address for connection.
>- If neither the IPv4 address nor the IPv6 address is 0, the client can determine which address to use first for connection; if the client fails to connect to the preferred address, it should switch to the other one. 
>- When you connect to HTTPDNS through the SDK, if HTTPDNS does not find a DNS query result, the domain will be resolved by the local DNS, and the result provided by the local DNS will be returned.

#### Sync DNS APIs: WGGetHostByName and WGGetHostByNames

##### API declaration

```objc
/**
 Sync DNS API (general)
 @param domain Domain 
 @return Array of found IPs. The `[0,0]` array will be returned if timeout (1s) occurs or no IPs are found
*/
- (NSArray *) WGGetHostByName:(NSString *) domain;

/**
 Batch sync DNS API (general)
 @param domains Domain array
 @return Dictionary of found IPs
 */
- (NSDictionary *) WGGetHostsByNames:(NSArray *) domains;
```
##### Sample code

Sample API call:

```objc
// Query a single domain
NSArray *ipsArray = [[MSDKDns sharedInstance] WGGetHostByName: @"qq.com"];
if (ipsArray && ipsArray.count > 1) {
	NSString *ipv4 = ipsArray[0];
	NSString *ipv6 = ipsArray[1];
	if (![ipv6 isEqualToString:@"0"]) {
		// TODO: When making a URL connection by using an IPv6 address, be sure to enclose the IPv6 address in square brackets, such as `http://[64:ff9b::b6fe:7475]/`
	} else if (![ipv4 isEqualToString:@"0"]){
		// Connect by using the IPv4 address
	} else {
		// `0,0` will be returned if an exception occurs. In this case, we recommend you retry once
	}
}

// Batch query domains
NSDictionary *ipsDict = [[MSDKDns sharedInstance] WGGetHostByNames: @[@"qq.com", @"dnspod.cn"]];
NSArray *ips = [ipsDict objectForKey: @"qq.com"];
if (ips && ips.count > 1) {
	NSString *ipv4 = ips[0];
	NSString *ipv6 = ips[1];
	if (![ipv6 isEqualToString:@"0"]) {
		// TODO: When making a URL connection by using an IPv6 address, be sure to enclose the IPv6 address in square brackets, such as `http://[64:ff9b::b6fe:7475]/`
	} else if (![ipv4 isEqualToString:@"0"]){
		// Connect by using the IPv4 address
	} else {
		// `0,0` will be returned if an exception occurs. In this case, we recommend you retry once
	}
}
```
#### Async DNS APIs: `WGGetHostByNameAsync` and `WGGetHostByNamesAsync`

##### API declaration

```objc
/**
 Async DNS API (general)
 @param domain Domain
 @param handler Array of returned IPs. The `[0,0]` array will be returned if timeout (1s) occurs or no IPs are found
 */
 - (void) WGGetHostByNameAsync:(NSString *) domain returnIps:(void (^)(NSArray *ipsArray))handler;

 /**
 Batch async DNS API (general)

 @param domains Domain array
 @param handler Dictionary of returned IPs. {"queryDomain" : [0, 0] ...} will be returned if timeout (1s) occurs or no IPs are found
 */
- (void) WGGetHostsByNamesAsync:(NSArray *) domains returnIps:(void (^)(NSDictionary * ipsDictionary))handler;
```
##### Sample code
>!You can select any call method based on your business needs.
 - Example 1:
     - Strengths: It is guaranteed that each request can get the returned result for subsequent connection operations.
     - Shortcomings: Processing through the async API is slightly more complex than that through the sync API.
 - Example 2:
     - Strengths: Businesses that have demanding requirements for the DNS time don't need to wait and can directly get the cached result to perform subsequent connection operations, unlike the sync API where the DNS query may take more than 100 milliseconds.
     - Shortcomings: The result of the first request will definitely be `nil`, and you need to add the processing logic.

- Sample API call 1: Wait for the end of the complete DNS query process, get the result, and make a connection.
```objc
// Query a single domain
[[MSDKDns sharedInstance] WGGetHostByNameAsync:@"qq.com" returnIps:^(NSArray *ipsArray) {
	// Wait for the end of the complete DNS query process, get the result, and make a connection
	if (ipsArray && ipsArray.count > 1) {
		NSString *ipv4 = ipsArray[0];
		NSString *ipv6 = ipsArray[1];
		if (![ipv6 isEqualToString:@"0"]) {
			// Suggestion: Use an IPv6 address first if it exists
			// TODO: When making a URL connection by using an IPv6 address, be sure to enclose the IPv6 address in square brackets, such as `http://[64:ff9b::b6fe:7475]/`
		} else if (![ipv4 isEqualToString:@"0"]){
			// Connect by using the IPv4 address
		} else {
			// `0,0` will be returned if an exception occurs. In this case, we recommend you retry once
		}
	}
}];
// Batch query domains
[[MSDKDns sharedInstance] WGGetHostByNamesAsync:@[@"qq.com", @"dnspod.cn"] returnIps:^(NSDictionary *ipsDict) {
	// Wait for the end of the complete DNS query process, get the result, and make a connection
	NSArray *ips = [ipsDict objectForKey: @"qq.com"];
	if (ips && ips.count > 1) {
		NSString *ipv4 = ips[0];
		NSString *ipv6 = ips[1];
		if (![ipv6 isEqualToString:@"0"]) {
			// Suggestion: Use an IPv6 address first if it exists
			// TODO: When making a URL connection by using an IPv6 address, be sure to enclose the IPv6 address in square brackets, such as `http://[64:ff9b::b6fe:7475]/`
		} else if (![ipv4 isEqualToString:@"0"]){
			// Connect by using the IPv4 address
		} else {
			// `0,0` will be returned if an exception occurs. In this case, we recommend you retry once
		}
	}
}];
```

- Sample API call 2: Directly get the cached result with no need to wait. If there is no cache, `result` will be `nil`.
```
__block NSArray* result;
[[MSDKDns sharedInstance] WGGetHostByNameAsync:domain returnIps:^(NSArray *ipsArray) {
	result = ipsArray;
}];
// You can directly get the cached result with no need to wait. If there is no cache, `result` will be `nil`
if (result) {
	// Get the cached result and make a connection
} else {
	// There is no cache for this request, and you can follow the original logic
}
```




## Notes
1. If the business on the client is bound to the host, such as the HTTP service of the host or the CDN service, you need to specify the host field of the HTTP header after replacing the domain in the URL with the IP returned by HTTPDNS.
 - Take `NSURLConnection` as an example:
```
NSURL *httpDnsURL = [NSURL URLWithString:@"URL obtained by concatenating the resolved IP"];
float timeOut = Set timeout period;
NSMutableURLRequest *mutableReq = [NSMutableURLRequest requestWithURL:httpDnsURL cachePolicy:NSURLRequestUseProtocolCachePolicy timeoutInterval: timeOut];
[mutableReq setValue:@"original domain" forHTTPHeaderField:@"host"];
NSURLConnection *connection = [[NSURLConnection alloc] initWithRequest:mutableReq delegate:self];
[connection start];
```
 - Take `NSURLSession` as an example:  
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
 - Take curl as an example:  
If you want to access `www.qq.com`, and the IP obtained by HTTPDNS is `192.168.0.111`, then you can perform a call as follows:
```
curl -H "host:www.qq.com" http://192.168.0.111/aaa.txt.
```
 - Take the `WWW` API of Unity as an example:  
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
2. Detect whether an HTTP proxy is used locally, and if so, we recommend you not use HTTPDNS to resolve domains.
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

## Practice Scenario 
### Unity project connection

1. Copy the **HttpDns.cs** file in `HTTPDNSUnityDemo/Assets/Plugins/Scripts` to the corresponding `Assets/Plugins/Scripts` path of Unity.
2. For the part that requires DNS query, call the `HttpDns.GetAddrByName(string domain)` or `HttpDns.GetAddrByNameAsync(string domain)` method.
	- If you use the sync API **HttpDns.GetAddrByName**, directly call it.
	- If you use the async API **HttpDns.GetAddrByNameAsync**, you need to set the callback function **onDnsNotify(string ipString)**, which you can rename.
	 We also recommend you add the following processing code:
``` 
string[] sArray=ipString.Split(new char[] {';'}); 
if (sArray != null && sArray.Length > 1) {
	if (!sArray[1].Equals("0")) {
		// Suggestion: Use an IPv6 address first if it exists
		// TODO: When making a URL connection by using an IPv6 address, be sure to enclose the IPv6 address in square brackets, such as `http://[64:ff9b::b6fe:7475]/`
	} else if(!sArray [0].Equals ("0")) {
		// Connect by using the IPv4 address
	} else {
		// `0,0` will be returned if an exception occurs. In this case, we recommend you retry once
		HttpDns.GetAddrByName(domainStr);
	}
}
```
3. After packaging the Unity project into an Xcode project, import the required dependent libraries.
4. Import the `MSDKDnsUnityManager.h` and `MSDKDnsUnityManager.mm` files in `HTTPDNSUnityDemo` into the project. Note that the following parts need to be the same as the corresponding `GameObject` name and callback function name in Unity as shown below:
![](https://main.qcloudimg.com/raw/f9a10fb9306f73cfd99c6dde705fc956.jpg)
![](https://main.qcloudimg.com/raw/5e34886a01bb50d17df72be53db03984.jpg)

### Using HTTPDNS query result in HTTPS scenario (non-SNI)

#### How it works

Replace the IP with the original domain before verifying a certificate.

#### Demo

 - **Take the `NSURLConnection` API as an example:**
```
#pragma mark - NSURLConnectionDelegate
- (BOOL)evaluateServerTrust:(SecTrustRef)serverTrust forDomain:(NSString *)domain {

	// Create a certificate verification policy
	NSMutableArray *policies = [NSMutableArray array];
	if (domain) {
		[policies addObject:(__bridge_transfer id)SecPolicyCreateSSL(true, (__bridge CFStringRef)domain)];
	} else {
		[policies addObject:(__bridge_transfer id)SecPolicyCreateBasicX509()];
	}

	// Bind the verification policy to the certificate on the server
	SecTrustSetPolicies(serverTrust, (__bridge CFArrayRef)policies);

	// Evaluate whether the current `serverTrust` is trustworthy
	// We recommend that only when `result` is `kSecTrustResultUnspecified` or `kSecTrustResultProceed` can `serverTrust` pass the verification
	//https://developer.apple.com/library/ios/technotes/tn2232/_index.html
	// For more information on `SecTrustResultType`, see `SecTrust.h`    
	SecTrustResultType result;
	SecTrustEvaluate(serverTrust, &result);
	return (result == kSecTrustResultUnspecified || result == kSecTrustResultProceed);
}

- (void)connection:(NSURLConnection *)connection willSendRequestForAuthenticationChallenge:(NSURLAuthenticationChallenge *)challenge {
	if (!challenge) {
		return;
	}

	// When HTTPDNS is used, the host in the URL is set to the IP, and you can get the actual domain from the HTTP header
	NSString *host = [[self.request allHTTPHeaderFields] objectForKey:@"host"];
	if (!host) {
		host = self.request.URL.host;
	}

	// Determine whether the challenge authentication method is `NSURLAuthenticationMethodServerTrust` (this authentication process will be performed for HTTPS mode)
	// The default network request process will be performed if no authentication method is configured.
	if ([challenge.protectionSpace.authenticationMethod isEqualToString:NSURLAuthenticationMethodServerTrust]) {
		if ([self evaluateServerTrust:challenge.protectionSpace.serverTrust forDomain:host]) {        

			// After authentication, you need to construct a `NSURLCredential` and send it to the initiator    
			NSURLCredential *credential = [NSURLCredential credentialForTrust:challenge.protectionSpace.serverTrust];
			[[challenge sender] useCredential:credential forAuthenticationChallenge:challenge];
		} else {
			// If authentication fails, the authentication process will be canceled
			[[challenge sender] cancelAuthenticationChallenge:challenge];
		}
	} else {

		// For other authentication methods, directly proceed with the process
		[[challenge sender] continueWithoutCredentialForAuthenticationChallenge:challenge];
	}
}
```
 - **Take the `NSURLSession` API as an example:**
```
 #pragma mark - NSURLSessionDelegate
- (BOOL)evaluateServerTrust:(SecTrustRef)serverTrust forDomain:(NSString *)domain {

	// Create a certificate verification policy
	NSMutableArray *policies = [NSMutableArray array];
	if (domain) {
		[policies addObject:(__bridge_transfer id)SecPolicyCreateSSL(true, (__bridge CFStringRef)domain)];
	} else {
		[policies addObject:(__bridge_transfer id)SecPolicyCreateBasicX509()];
	}

	// Bind the verification policy to the certificate on the server
	SecTrustSetPolicies(serverTrust, (__bridge CFArrayRef)policies);

	// Evaluate whether the current `serverTrust` is trustworthy
	// We recommend that only when `result` is `kSecTrustResultUnspecified` or `kSecTrustResultProceed` can `serverTrust` pass the verification
	//https://developer.apple.com/library/ios/technotes/tn2232/_index.html
	// For more information on `SecTrustResultType`, see `SecTrust.h`    
	SecTrustResultType result;
	SecTrustEvaluate(serverTrust, &result);

	return (result == kSecTrustResultUnspecified || result == kSecTrustResultProceed);
}

- (void)URLSession:(NSURLSession *)session task:(NSURLSessionTask *)task didReceiveChallenge:(NSURLAuthenticationChallenge *)challenge completionHandler:(void (^)(NSURLSessionAuthChallengeDisposition disposition, NSURLCredential * __nullable credential))completionHandler {
	if (!challenge) {
		return;
	}

	NSURLSessionAuthChallengeDisposition disposition = NSURLSessionAuthChallengePerformDefaultHandling;
	NSURLCredential *credential = nil;

	// Get the original domain information
	NSString *host = [[self.request allHTTPHeaderFields] objectForKey:@"host"];
	if (!host) {
		host = self.request.URL.host;
	}
	if ([challenge.protectionSpace.authenticationMethod  isEqualToString:NSURLAuthenticationMethodServerTrust]) {
		if ([self evaluateServerTrust:challenge.protectionSpace.serverTrust forDomain:host]) {
			disposition = NSURLSessionAuthChallengeUseCredential;
			credential = [NSURLCredential credentialForTrust:challenge.protectionSpace.serverTrust];
		} else {
			disposition = NSURLSessionAuthChallengePerformDefaultHandling;
		}
	} else {
		disposition = NSURLSessionAuthChallengePerformDefaultHandling;
	}

	// For other challenges, directly use the default authentication scheme
	completionHandler(disposition,credential);
}
```
 - **Take the `WWW` API of Unity as an example:**
After importing the Unity project as an Xcode project, open the `Classes/Unity/**WWWConnection.mm**` file and modify the following code:
 ```
//const char* WWWDelegateClassName = "UnityWWWConnectionSelfSignedCertDelegate";
const char* WWWDelegateClassName = "UnityWWWConnectionDelegate";
 ```
To:
```
const char* WWWDelegateClassName = "UnityWWWConnectionSelfSignedCertDelegate";
//const char* WWWDelegateClassName = "UnityWWWConnectionDelegate";
```

### Using HTTPDNS query result in SNI (single-IP, multi-HTTPS-certificate) scenario

Server Name Indication (SNI) is an extension to SSL/TLS that allows a server to use multiple domains and certificates. It works as follows:
- Send the domain (hostname) of the site to be accessed before connecting to the server to establish an SSL connection.
- The server returns an appropriate certificate according to the domain.

In the above process, when the client uses HTTPDNS to resolve a domain, the host in the request URL will be replaced with the IP resolved by HTTPDNS, so that the domain obtained by the server will be the resolved IP, and the client cannot find a matching certificate and can return only the default certificate or no certificate. As a result, an SSL/TLS handshake failure will occur.

As iOS' upper level network libraries of NSURLConnection and NSURLSession don't provide an API to configure the SNI field, you can consider using `NSURLProtocol` to intercept network requests, using `CFHTTPMessageRef` to create an `NSInputStream` instance for socket communication, and setting the value of its `kCFStreamSSLPeerName`.

Note that when you use `NSURLProtocol` to intercept a POST request made by `NSURLSession`, `HTTPBody` will be empty. There are two solutions to this:
- Send a POST request by using `NSURLConnection`.
- Place `HTTPBody` in the HTTP header field first and then get it from `NSURLProtocol`.

For specific examples, see the demo. Below is the sample code:
Register the `NSURLProtocol` subclass in `SNIViewController.m` of the demo before sending network requests.
```
// Register `NSURLProtocol` to intercept requests
[NSURLProtocol registerClass:[MSDKDnsHttpMessageTools class]];

// Set the SNI URL
NSString *originalUrl = @"your url";
NSURL *url = [NSURL URLWithString:originalUrl];
NSMutableURLRequest *request = [[NSMutableURLRequest alloc] initWithURL:url];
NSArray *result = [[MSDKDns sharedInstance] WGGetHostByName:url.host];
NSString *ip = nil;
if (result && result.count > 1) {
	if (![result[1] isEqualToString:@"0"]) {
		ip = result[1];
	} else {
		ip = result[0];
	}
}
// Get the IP successfully through HTTPDNS, replace the URL, and set the host header
if (ip) {
	NSRange hostFirstRange = [originalUrl rangeOfString:url.host];
	if (NSNotFound != hostFirstRange.location) {
		NSString *newUrl = [originalUrl stringByReplacingCharactersInRange:hostFirstRange withString:ip];
		request.URL = [NSURL URLWithString:newUrl];
		[request setValue:url.host forHTTPHeaderField:@"host"];
	}
}

// Sample `NSURLConnection`
self.connection = [[NSURLConnection alloc] initWithRequest:request delegate:self];
[self.connection start];

// Sample `NSURLSession`
NSURLSessionConfiguration *configuration = [NSURLSessionConfiguration defaultSessionConfiguration];
NSArray *protocolArray = @[ [MSDKDnsHttpMessageTools class] ];
configuration.protocolClasses = protocolArray;
NSURLSession *session = [NSURLSession sessionWithConfiguration:configuration delegate:self delegateQueue:[NSOperationQueue mainQueue]];
self.task = [session dataTaskWithRequest:request];
[self.task resume];

// Note: When you use `NSURLProtocol` to intercept a POST request made by `NSURLSession`, `HTTPBody` will be empty.
// There are two solutions:
// 1. Use `NSURLConnection` to send POST requests.
// 2. Place `HTTPBody` in the HTTP header field first and then get it from `NSURLProtocol`.
// The following mainly demonstrates the second solution
// NSString *postStr = [NSString stringWithFormat:@"param1=%@&param2=%@", @"val1", @"val2"];
// [_request addValue:postStr forHTTPHeaderField:@"originalBody"];
// _request.HTTPMethod = @"POST";
// NSURLSessionConfiguration *configuration = [NSURLSessionConfiguration defaultSessionConfiguration];
// NSArray *protocolArray = @[ [CFHttpMessageURLProtocol class] ];
// configuration.protocolClasses = protocolArray;
// NSURLSession *session = [NSURLSession sessionWithConfiguration:configuration delegate:self delegateQueue:[NSOperationQueue mainQueue]];
// NSURLSessionTask *task = [session dataTaskWithRequest:_request];
// [task resume];
```
#### Notes
You need to call the following API to set the domains to be or not to be intercepted:
```
#pragma mark - In SNI scenarios, call it only once
/**
 Set the list of domains to be intercepted in SNI scenarios
 We recommend you call the API to intercept domains only in SNI scenarios but not other scenarios

 @param hijackDomainArray List of domains to be intercepted
 */
- (void) WGSetHijackDomainArray:(NSArray *)hijackDomainArray;

/**
 Set the list of domains not to be intercepted in SNI scenarios

 @param noHijackDomainArray List of domains not to be intercepted
 */
 - (void) WGSetNoHijackDomainArray:(NSArray *)noHijackDomainArray;
```
- If you set the list of domains to be intercepted, only HTTPS requests in the list will be intercepted and processed, while other domains will not.
- If you set the list of domains not to be intercepted, HTTPS requests in the list will not be intercepted and processed.

>!We recommend you use `WGSetHijackDomainArray` to intercept domains only in SNI scenarios but not other scenarios.

