## Features
The main purpose of HttpDNS is to effectively avoid the inability to access the optimal access point due to ISP's traditional LocalDNS resolution. The principle is to use the HTTP encryption protocol instead of the traditional DNS protocol, so that the domain name is not used during the entire process, greatly reducing the possibility of hijacking.

## Installation Package Structure
The compressed file contains a demo project, including:

| **Demo content** | **Description** | 
|---------|---------|
| MSDKDns.framework     | Applicable for projects where "Build Setting->C++ Language Dialect" is configured as "GNU++98" and "Build Setting->C++ Standard Library" as "libstdc++(GNU C++ standard library)" |
| MSDKDns_C11.framework | Applicable for projects where "Build Setting->C++ Language Dialect" and "Build Setting->C++ Standard Library" are configured as "GNU++11" and "libc++(LLVM C++ standard library with C++11 support)" respectively |

## Access Steps

### For Businesses with Access to Beacon
Simply introduce MSDKDns.framework or MSDKDns_C11.framework (select one based on the project configuration) in the HTTPDNSLibs directory.

### For Businesses Without Access to Beacon
1. Introduce the dependent libraries (located in the HTTPDNSLibs directory):
  - BeaconAPI_Base.framework
  - MSDKDns.framework or MSDKDns_C11.framework (select one based on the project configuration)
2. Introduce the following system libraries:
  - libz.tdb
  - libsqlite3.tdb
  - libstdc++.tdb
  - libstdc++.6.0.9.tdb
  - libc++.tdb
  - Foundation.framework
  - CoreTelephony.framework
  - SystemConfiguration.framework
  - CoreGraphics.framework
  - Security.framework
3. Add Beacon's registration code to application:didFinishLaunchingWithOptions:
```
// For businesses with access to Beacon, you can ignore the following code; for businesses without access to Beacon, call the following code to register Beacon
//******************************
NSString * appkey = @"Business' Beacon appkey obtained by registering at Tencent Cloud's official website";
[BeaconBaseInterface setAppKey:appkey];
[BeaconBaseInterface enableAnalytics:@"" gatewayIP:nil];
//******************************
```
> **Note:**
Please add the -ObjC flag in the Other linker flag.

## API and Usage Examples
To get the IP, two APIs are used: the sync API **WGGetHostByName** and the async API **WGGetHostByNameAsync**. Introduce the header file and call the corresponding API. The returned address format is NSArray with a fixed length of 2 values, where the first value is an IPv4 address and the second one is an IPv6 address. A detailed description of the return format is as follows:
- [IPv4, 0]: In general business scenarios, a result of this format will be returned in most cases, i.e. there is no IPv6 address and only the IPv4 address is returned to the business;
- [IPv4, IPv6]: In IPv6 environments, both IPv6 and IPv4 addresses are returned to the business;
- [0, 0]: In rare cases, this format will be returned to the business. At this time, both HttpDNS and LocalDNS requests time out, and the business can call the WGGetHostByName API again.

> **Note:**
When using an IPv6 address for URL request, you need to place it in brackets for processing, for example:
```
http://[64:ff9b::b6fe:7475]/*********
```
**Recommendations on usage:**
1. If IPv6 is 0, directly connect using the IPv4 address;
2. If IPv6 is not 0, use the IPv6 address for connection first, and if the IPv6 connection fails, the IPv4 address is used for connection.

### Get the IP
#### Sync API WGGetHostByName
```
/**
* Sync API
*  @param domain   Domain name
* @return IP array queried, timeout (1s) or [0,0] array if no results is queried
*/
- (NSArray*) WGGetHostByName:(NSString*) domain;
```
Code example for API call:
```
NSArray* ipsArray = [[MSDKDns sharedInstance] WGGetHostByName: @"www.qq.com"];
if (ipsArray && ipsArray.count > 1){
NSString* ipv4 = ipsArray[0];
NSString* ipv6 = ipsArray[1];
if (![ipv6 isEqualToString:@"0"]) {
// Advice for usage: If the IPv6 address exists, it is used preferentially
// When using the IPv6 address for URL connection, pay attention to the format: IPv6 needs to be placed in brackets for processing, for example: http://[64:ff9b::b6fe:7475]/
} else if (![ipv4 isEqualToString:@"0"]) {
// Use the IPv4 address to connect
} else {
// 0,0 is returned in exceptional cases; it is recommended to retry
} 
}
```
#### Async API: WGGetHostByNameAsync
```
/**
* Async API
*  @param domain   Domain name
* @return IP array queried, timeout (1s) or [0,0] array if no results is queried
*/
- (void) WGGetHostByNameAsync:(NSString*) domain returnIps:(void (^)(NSArray* ipsArray))handler;
```
Code example:
- API call example 1: Wait for the completion of the resolution process, get the result and connect.
```
[[MSDKDns sharedInstance] WGGetHostByNameAsync:domain returnIps:^(NSArray *ipsArray) {
if (ipsArray && ipsArray.count > 1) {
NSString* ipv4 = ipsArray[0];
NSString* ipv6 = ipsArray[1];
if (![ipv6 isEqualToString:@"0"]) {
// Advice for usage: If the IPv6 address exists, it is used preferentially
// When using the IPv6 address for URL connection, pay attention to the format: IPv6 needs to be placed in brackets for processing, for example: http://[64:ff9b::b6fe:7475]/
} else if (![ipv4 isEqualToString:@"0"]){
// Use the IPv4 address to connect
} else {
// 0,0 is returned in exceptional cases; it is recommended to retry
}
	}
}];
```
- API call example 2: No need to wait, you can get the cached result directly; if there is no cache, the result is nil.
```
__block NSArray* result;
[[MSDKDns sharedInstance] WGGetHostByNameAsync:domain returnIps:^(NSArray *ipsArray) {
result = ipsArray;
}];
// No need to wait, you can get the cached result directly; if there is no cache, the result is nil
if (result) {
// Get the cached result for connection
} else {
// This request has no cache; the business can use the original logic
}
```
You can choose either one of the calling methods based on your needs:
- Example 1:
 - Advantages: It guarantees that each request can get the return result for subsequent connection operations;
 - Disadvantages: The processing of the async API is slightly more complicated than the sync API.
- Example 2:
 - Advantages: For businesses with strict resolution time requirements, you can use this example to eliminate the waiting time and get the result from the cache for subsequent connection operations, completely avoiding the situation where the resolution time in the sync API may exceed 100 ms.
 - Disadvantages: When the first request is made, the result must be nil, and the business needs to add processing logic.

### Setting Basic Business Information
```
/**
	 Set basic business information (for Tencent Cloud businesses)
 
	 @param appkey   The business' appKey, obtained by applying for at Tencent Cloud's official website (https://console.cloud.tencent.com/httpdns) and used for reporting
	 @param dnsid   DNS resolution ID, i.e. the authorization ID, obtained by applying for at Tencent Cloud's official website (https://console.cloud.tencent.com/httpdns) and used for domain name resolution authentication
	 @param dnsKey   DNS resolution key, i.e. the key corresponding to the authorization ID; obtained by applying for at Tencent Cloud's official website (https://console.cloud.tencent.com/httpdns) and used for domain name resolution authentication
	 @param debug   Whether to enable the Debug log; YES: on; NO: off. It is recommended to turn it on during joint testing and turn it off before the official launch.
	 @param timeout   Timeout in ms; if set to 0, the default value of 2000 ms is used
 
	 @return   YES: successfully set; NO: failed to set
	 */
	- (BOOL) WGSetDnsAppKey:(NSString *) appkey DnsID:(int)dnsid DnsKey:(NSString *)dnsKey Debug:(BOOL)debug TimeOut:(int)timeout;
```

```
[[MSDKDns sharedInstance] WGSetDnsAppKey: @"Business' appkey, obtained by applying for at Tencent Cloud's official website" DnsID: DNS resolution ID DnsKey:@"DNS resolution key" Debug:YES TimeOut:2000];
```

## Precautions
1. If the client's business is already bound with the Host (such as its HTTP service or CDN service), then, after replacing the domain name in the URL with the IP returned by HttpDNS, you also need to specify the Host field in the HTTP header.
 - Take NSURLConnection as an example:
     ```
     NSURL* httpDnsURL = [NSURL URLWithString:@"URL spliced using the resolved IP"];
     float timeOut = the timeout set;
     NSMutableURLRequest* mutableReq = [NSMutableURLRequest requestWithURL:httpDnsURL cachePolicy:NSURLRequestUseProtocolCachePolicy timeoutInterval: timeOut];
     [mutableReq setValue:@"Original domain name" forHTTPHeaderField:@"host"];
     NSURLConnection* connection = [[NSURLConnection alloc] initWithRequest:mutableReq delegate:self];
     [connection start];
     ```
 - Take curl as an example:
     If you want to access www.qq.com and the IP address resolved by HttpDNS is 192.168.0.111, then you can call it by this method:
     ```
     curl -H "host:www.qq.com" http://192.168.0.111/aaa.txt.
     ```
  - Take Unity's WWW API as an example:
     ```
     string httpDnsURL = "URL spliced using the resolved IP";
     Dictionary<string, string> headers = new Dictionary<string, string> ();
     headers["host"] = "Original domain name";
     WWW conn = new WWW (url, null, headers);
     yield return conn;
     if (conn.error != null)  
     {  
     	print("error is happened:"+ conn.error);      
     } else  
     {  
     	print("request ok" + conn.text); 
     }  
     ```
2. Check whether an HTTP proxy is used locally. If yes, it is recommended not using HttpDNS for domain name resolution.
   - Check whether an HTTP proxy is used:
     ```
     - (BOOL)isUseHTTPProxy {
     	CFDictionaryRef dicRef = CFNetworkCopySystemProxySettings();
     	const CFStringRef proxyCFstr = (const CFStringRef)CFDictionaryGetValue(dicRef, (const void*)kCFNetworkProxiesHTTPProxy);
     	NSString* proxy = (__bridge NSString *)proxyCFstr;
     	if (proxy) {
     		return YES;
     	} else {
     		return NO;
     	}
     }
     ```
   - Check whether an HTTPS proxy is used:
     ```
     - (BOOL)isUseHTTPSProxy {
     CFDictionaryRef dicRef = CFNetworkCopySystemProxySettings();
     const CFStringRef proxyCFstr = (const CFStringRef)CFDictionaryGetValue(dicRef, (const void*)kCFNetworkProxiesHTTPSProxy);
     NSString* proxy = (__bridge NSString *)proxyCFstr;
     if (proxy) {
     	return YES;
     } else {
     	return NO;
     }
     }
     ```

## Practice Scenario
### Unity Project Access
1. Copy the **HttpDns.cs** file in HTTPDNSUnityDemo/Assets/Plugins/Scripts to the corresponding Assets/Plugins/Scripts path in Unity.
2. In the part where domain name resolution is required, call the **HttpDns.GetAddrByName(string domain)** or **HttpDns.GetAddrByNameAsync(string domain)** method.
 - If the sync API **HttpDns.GetAddrByName** is used, call the API directly;
 - If the async API **HttpDns.GetAddrByNameAsync** is used, you need to set the callback function **onDnsNotify(string ipString)**, and the function name can be customized. And it is recommended to add the following [code](#code).
3. After packaging the Unity project as an Xcode project, introduce the required dependent libraries;
4. Import the MSDKDnsUnityManager.h and MSDKDnsUnityManager.mm files in HTTPDNSUnityDemo into the project. Note that the following parts need to be the same as the corresponding GameObject name and callback function name in Unity:
   ![](https://main.qcloudimg.com/raw/4f24e4c6cca796fd93751ca30255fa51.png)
![](https://main.qcloudimg.com/raw/91050cb9cbfb7199fae6a4b27e04fa09.png)
5. Call as per the required API.
<a id="code"></a>
**Code recommended for adding:**   
```
string[] sArray=ipString.Split(new char[] {';'}); 
if (sArray != null && sArray.Length > 1) {
	if (!sArray[1].Equals("0")) {
		// Advice for usage: If the IPv6 address exists, it is used preferentially
		// When using the IPv6 address for URL connection, pay attention to the format: the address needs to be placed in brackets for processing, for example: http://[64:ff9b::b6fe:7475]/
					
	} else if(!sArray [0].Equals ("0")) {
		// Use the IPv4 address to connect
			
	} else {
		// 0,0 is returned in exceptional cases; retry is recommended
		HttpDns. GetAddrByName (domainStr);
	}
}
```

### Ordinary HTTPS Scenario (Non-SNI)
How it works: When verifying the certificate, replace the IP with the original domain name for verification.
Demo example:
1. Take the NSURLConnection API as an example to implement the following two methods:
   ```
   - (BOOL)evaluateServerTrust:(SecTrustRef)serverTrust forDomain:(NSString *)domain        
   {
   /*
   * Create a certificate verification policy
   */
   NSMutableArray *policies = [NSMutableArray array];
   if (domain) {
   [policies addObject:(__bridge_transfer id)SecPolicyCreateSSL(true, (__bridge CFStringRef)domain)];
   } else {
   [policies addObject:(__bridge_transfer id)SecPolicyCreateBasicX509()];
   }
   /*
   * Bind the verification policy to the certificate on the server
   */
   SecTrustSetPolicies(serverTrust, (__bridge CFArrayRef)policies);
   /*
   * Assess whether the current serverTrust is trustworthy,
   * It is officially recommended that serverTrust can pass the verification in case the result = kSecTrustResultUnspecified or kSecTrustResultProceed
   *  https://developer.apple.com/library/ios/technotes/tn2232/_index.html
   * For details on SecTrustResultType, see SecTrust.h
   */
   SecTrustResultType result;
   SecTrustEvaluate(serverTrust, &result);
   return (result == kSecTrustResultUnspecified || result == kSecTrustResultProceed);        
   }
   -(void)connection:(NSURLConnection*)connection willSendRequestForAuthenticationChallenge:(NSURLAuthenticationChallenge *)challenge        
   {
   if (!challenge) {
   return;
   }   
   /*
   * The host in the URL is set to IP when HttpDNS is used. Here, the real domain name is obtained from the HTTP header.
   */
   NSString* host = [[self.request allHTTPHeaderFields] objectForKey:@"host"];
   if (!host) {
   host = self.request.URL.host;
   }        
   
   /*
   * Determine whether the authentication method of challenge is NSURLAuthenticationMethodServerTrust (this authentication process will be performed in HTTPS mode).
   * Perform the default network request process if no authentication method is configured.
   */
   if([challenge.protectionSpace.authenticationMethod isEqualToString:NSURLAuthenticationMethodServerTrust])
   {
   if([self evaluateServerTrust:challenge.protectionSpace.serverTrust 
   forDomain:host]) {
   /*
   * After authentication, you need to construct an NSURLCredential and send it to the initiator.
   */
   NSURLCredential *credential = [NSURLCredential 
   credentialForTrust:challenge.protectionSpace.serverTrust];
   [[challenge sender] useCredential:credential forAuthenticationChallenge:challenge];
   } else {
   /*
   * Authentication failed; cancel the authentication process
   */
   [[challenge sender] cancelAuthenticationChallenge:challenge];
   }
   } else {
   /*
   * For other authentication methods, follow the processing flow directly
   */
   [[challenge sender] continueWithoutCredentialForAuthenticationChallenge:challenge];
   }
   }
   ```

2. Take the NSURLSession API as an example to implement the following two methods:
   ```
   - (BOOL)evaluateServerTrust:(SecTrustRef)serverTrust forDomain:(NSString *)domain        
   {
   /*
   * Create a certificate verification policy
   */
   NSMutableArray *policies = [NSMutableArray array];
   if (domain) {
   [policies addObject:(__bridge_transfer id)SecPolicyCreateSSL(true, (__bridge CFStringRef)domain)];
   } else {
   [policies addObject:(__bridge_transfer id)SecPolicyCreateBasicX509()];
   }
   /*
   * Bind the verification policy to the certificate on the server
   */
   SecTrustSetPolicies(serverTrust, (__bridge CFArrayRef)policies);
   /*
   * Assess whether the current serverTrust is trustworthy,
   * It is officially recommended that serverTrust can pass the verification in case the result = kSecTrustResultUnspecified or kSecTrustResultProceed
   *  https://developer.apple.com/library/ios/technotes/tn2232/_index.html
   * For details on SecTrustResultType, see SecTrust.h
   */
   SecTrustResultType result;
   SecTrustEvaluate(serverTrust, &result);
   return (result == kSecTrustResultUnspecified || result == kSecTrustResultProceed);        
   }
   - (void)URLSession:(NSURLSession *)session task:(NSURLSessionTask *)task
   didReceiveChallenge:(NSURLAuthenticationChallenge *)challenge completionHandler:(void (^)(NSURLSessionAuthChallengeDisposition disposition, NSURLCredential * __nullable credential))completionHandler
   {
   if (!challenge) {
   return;
   }
   NSURLSessionAuthChallengeDisposition disposition = NSURLSessionAuthChallengePerformDefaultHandling;
   NSURLCredential *credential = nil;
   /*
   * Get the original domain name information.
   */
   NSString* host = [[self.request allHTTPHeaderFields] objectForKey:@"host"];
   if (!host) {
   host = self.request.URL.host;
   }
   if ([challenge.protectionSpace.authenticationMethod
   isEqualToString:NSURLAuthenticationMethodServerTrust]) {
   if ([self evaluateServerTrust:challenge.protectionSpace.serverTrust 
   forDomain:host]) {
   disposition = NSURLSessionAuthChallengeUseCredential;
   		credential = [NSURLCredential 
   credentialForTrust:challenge.protectionSpace.serverTrust];
   } else {
   disposition = NSURLSessionAuthChallengePerformDefaultHandling;
   }
   } else {
   disposition = NSURLSessionAuthChallengePerformDefaultHandling;
   }
   // Use the default authentication scheme directly for other challenges
   completionHandler(disposition,credential);
   }
   ```

3. Take Unity's WWW API as an example:
After importing the Unity project as an Xcode project, open the Classes/Unity/WWWConnection.mm file and change the following code:
   ```
   //const char* WWWDelegateClassName = "UnityWWWConnectionSelfSignedCertDelegate";
   const char* WWWDelegateClassName = "UnityWWWConnectionDelegate";
   ```
to:
   ```
   const char* WWWDelegateClassName = "UnityWWWConnectionSelfSignedCertDelegate";
   //const char* WWWDelegateClassName = "UnityWWWConnectionDelegate";
   ```

### HTTPS SNI (Single-IP Multi-HTTPS Certificate) Scenario
Server Name Indication (SNI) is an SSL/TLS extension to enable one server to use multiple domain names and certificates. It works as follows:
- It sends the domain name (Hostname) of the website to be accessed before connecting to the server to establish an SSL link.
- The server returns a suitable certificate based on this domain name.

In the process above, if the client uses HttpDNS to resolve the domain name, the host in the request URL will be replaced with the IP resolved by HttpDNS, so that the domain name obtained by the server is the resolved IP, and the matching certificate cannot be found. As a result, only the default certificate can be returned, or no certificate is returned at all, leading to SSL/TLS handshake failure.
Since the iOS upper-layer network library NSURLConnection/NSURLSession does not provide an API for SNI field configuration, we can consider using NSURLProtocol to intercept the network request and then use CFHTTPMessageRef to create an NSInputStream instance for Socket communication and set its kCFStreamSSLPeerName value.
Please note that HTTPBody is empty when using NSURLProtocol to intercept a POST request initiated by NSURLSession. There are two solutions:
1. Send a POST request using NSURLConnection.
2. Put the HTTPBody into the HTTP Header field and extract it from NSURLProtocol.

See the demo for specific examples. Some of the code is as follows:
Register the NSURLProtocol subclass in SNIViewController.m in the example before initiating the network request,
   ```
   // Register NSURLProtocol for request interception
   [NSURLProtocol registerClass:[MSDKDnsHttpMessageTools class]];
   
   // The URL for which to set the SNI
   NSString *originalUrl = @"your url";
   NSURL* url = [NSURL URLWithString:originalUrl];
   NSMutableURLRequest* request = [[NSMutableURLRequest alloc] initWithURL:url];
   NSArray* result = [[MSDKDns sharedInstance] WGGetHostByName:url.host];
   NSString* ip = nil;
   if (result && result.count > 1) {
       if (![result[1] isEqualToString:@"0"]) {
           ip = result[1];
       } else {
           ip = result[0];
       }
   }
   // Get IP successfully through HTTPDNS, perform URL replacement and HOST header settings
   if (ip) {
       NSRange hostFirstRange = [originalUrl rangeOfString:url.host];
       if (NSNotFound != hostFirstRange.location) {
           NSString *newUrl = [originalUrl stringByReplacingCharactersInRange:hostFirstRange withString:ip];
           request.URL = [NSURL URLWithString:newUrl];
           [request setValue:url.host forHTTPHeaderField:@"host"];
       }
   }
   
   // NSURLConnection example
   self.connection = [[NSURLConnection alloc] initWithRequest:request delegate:self];
   [self.connection start];
   
   // NSURLSession example
   NSURLSessionConfiguration *configuration = [NSURLSessionConfiguration defaultSessionConfiguration];
   NSArray *protocolArray = @[ [MSDKDnsHttpMessageTools class] ];
   configuration.protocolClasses = protocolArray;
   NSURLSession *session = [NSURLSession sessionWithConfiguration:configuration delegate:self delegateQueue:[NSOperationQueue mainQueue]];
   self.task = [session dataTaskWithRequest:request];
   [self.task resume];
   
   // Note: *HTTPBody is empty when using NSURLProtocol to intercept a POST request initiated by NSURLSession.
   // There are two solutions: 1. Send a POST request using NSURLConnection.
   // 2. Put the HTTPBody into the HTTP Header field and extract it from NSURLProtocol.
   // The following mainly demonstrates the second solution.
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

#### Use Instructions
The following API needs to be called to set the domain names to be intercepted or allowed:
```
#pragma mark - SNI scenario; call only once; do not call repeatedly
/**
 Set the list of domain names to be intercepted in the SNI scenario
 It is recommended that you set this API to intercept only the domain names in the SNI scenario and avoid intercepting domain names in other scenarios

 @param hijackDomainArray   The list of domain names to be intercepted
 */
- (void) WGSetHijackDomainArray:(NSArray *)hijackDomainArray;

/**
 Set the list of domain names not to be intercepted in the SNI scenario

 @param noHijackDomainArray   The list of domain names not to be intercepted
 */
- (void) WGSetNoHijackDomainArray:(NSArray *)noHijackDomainArray;
```

- If the list of domain names to be intercepted is set, only HTTPS requests in the list will be intercepted, and other domain names will not be processed;
- If a list of domain names not to be intercepted is set, the HTTPS request in the list will not be intercepted;

It is recommended that you use WGSetHijackDomainArray to intercept only the domain names in the SNI scenario and avoid intercepting domain names in other scenarios.
