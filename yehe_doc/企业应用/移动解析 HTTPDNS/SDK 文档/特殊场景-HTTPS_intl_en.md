This document describes how to verify a certificate over HTTPS in HTTPDNS.

### Sample Code for iOS

#### How it works
Replace the IP with the original domain before verifying a certificate.

#### Demo
Take the `NSURLConnection` API as an example:

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
     * Evaluate whether the current `serverTrust` is trustworthy
     * We recommend that only when `result` is `kSecTrustResultUnspecified` or `kSecTrustResultProceed`
     * can `serverTrust` pass the verification. For more information, visit https://developer.apple.com/library/ios/technotes/tn2232/_index.html
     * For more information on `SecTrustResultType`, see `SecTrust.h`
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
     * When HTTPDNS is used, the host in the URL is set to the IP, and you can get the actual domain from the HTTP header
     */
    NSString* host = [[self.request allHTTPHeaderFields] objectForKey:@"Host"];
    if (!host) {
        host = self.request.URL.host;
    }

    /*
     * Determine whether the challenge authentication method is `NSURLAuthenticationMethodServerTrust` (this authentication process will be performed for HTTPS mode)
     * The default network request process will be performed if no authentication method is configured
     */
    if ([challenge.protectionSpace.authenticationMethod isEqualToString:NSURLAuthenticationMethodServerTrust])
    {
        if ([self evaluateServerTrust:challenge.protectionSpace.serverTrust forDomain:host]) {
            /*
             * After authentication, you need to construct a `NSURLCredential` and send it to the initiator
             */
            NSURLCredential *credential = [NSURLCredential credentialForTrust:challenge.protectionSpace.serverTrust];
            [[challenge sender] useCredential:credential forAuthenticationChallenge:challenge];
        } else {
            /*
             * If authentication fails, the authentication process will be canceled
             */
            [[challenge sender] cancelAuthenticationChallenge:challenge];
        }
    } else {
        /*
         * For other authentication methods, directly proceed with the process
         */
        [[challenge sender] continueWithoutCredentialForAuthenticationChallenge:challenge];
    }
}
```




