This document explains the HTTPS scenario of HttpDNS.

### Code for iOS

#### How It Works
During the process of certificate verification, the IP is replaced with the original domain name for verification.

#### Demo Example
Take the NSURLConnection API as an example.

```
#pragma mark - NSURLConnectionDelegate

- (BOOL)evaluateServerTrust:(SecTrustRef)serverTrust
                  forDomain:(NSString *)domain
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
     * It is officially recommended that if result = kSecTrustResultUnspecified or kSecTrustResultProceed,
     * serverTrust can pass the verification; https://developer.apple.com/library/ios/technotes/tn2232/_index.html
     * For details on SecTrustResultType, see SecTrust.h
     */
    SecTrustResultType result;
    SecTrustEvaluate(serverTrust, &result);

    return (result == kSecTrustResultUnspecified || result == kSecTrustResultProceed);
}

- (void)connection:(NSURLConnection *)connection willSendRequestForAuthenticationChallenge:(NSURLAuthenticationChallenge *)challenge
{
    if (!challenge) {
        return;
    }

    /*
     * The host in the URL is set to IP when HttpDNS is used. Here, the real domain name is obtained from the HTTP header.
     */
    NSString* host = [[self.request allHTTPHeaderFields] objectForKey:@"Host"];
    if (!host) {
        host = self.request.URL.host;
    }

    /*
     * Determine whether the authentication method of challenge is NSURLAuthenticationMethodServerTrust (this authentication process will be performed in HTTPS mode).
     * Perform the default network request process if no authentication method is configured.
     */
    if ([challenge.protectionSpace.authenticationMethod isEqualToString:NSURLAuthenticationMethodServerTrust])
    {
        if ([self evaluateServerTrust:challenge.protectionSpace.serverTrust forDomain:host]) {
            /*
             * After authentication, you need to construct an NSURLCredential and send it to the initiator.
             */
            NSURLCredential *credential = [NSURLCredential credentialForTrust:challenge.protectionSpace.serverTrust];
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
