## Business Flow Chart
The business flows of Layer-7 and Layer-4 CLB (formerly “application CLB”) are as shown below:
![](https://mc.qcloudimg.com/static/img/de6af7fca35640ed6d0937f05f5039d2/image.png)
If Layer-7 CLB is used to forward HTTP/HTTPS protocol, you can add a corresponding domain name when creating the forwarding rule in a CLB listener.
- If only one forwarding rule is created, you can access VIP+URL for the corresponding forwarding rule and normal service.
- If multiple forwarding rules are created, accessing VIP+URL does not guarantee access to a specified domain name+URL. You should access domain name+URL directly to make sure the specified forwarding rule has taken effect. In other words, when users configure multiple forwarding rules, a VIP may correspond to multiple domain names. We recommend you access the service via specified domain name+URL, instead of VIP+URL.

## Forwarding rule configuration description
### Domain name configuration rules
When you configure domain name for a forwarding rule of a Layer-7 CLB listener, a regular expression containing 1–120 characters can be used.
- A non-regular domain name can contain the following characters:
`a–z` `0–9` `.` `-`
- A wildcard domain name is supported only in the following formats:  
`*.example.com` or `www.example.*`. Only one `*` can be presented in a single domain name. 		
- A regular expression in domain name cannot contain the following characters:
`"` `{` `}` `;` `~` `'` ``` `blank space`
- Below is an example of regular domain name supported by CLB:
`~^www\d+\.example\.com$`

### Health check configuration rules
- If a wildcard domain name is entered, a fixed domain name (non-regular) must be specified as the health check domain name, which can contain the following characters:
`a–z` `0–9` `.` `-`
- The health check path for Layer-7 CLB listener must be configured to begin with `/` and can contain 1–120 characters. Regular expression is not supported. We recommend you specify a fixed URL path (static page) for health check, which can contain the following character set:
`a–z` `A–Z` `0–9` `.` `-` `/` `=` `?`

### Domain name matching rules
1. If you enter an IP address instead of a domain name in the forwarding rule and configure multiple URLs in the forwarding group, VIP+URL will be used for access.
2. If you configure a full domain name in the forwarding rule and multiple URLs in the forwarding group, domain name+URL will be used for access.
3. If you configure a wildcard domain name in the forwarding rule and multiple URLs in the forwarding group, matching request domain name+URL will be used for access. To have different domain names point to the same URL, you can use this method for configuration. Taking `example.qcould.com` as an example, the format is as follows:
  - `example.qcloud.com` exactly matches the `example.qcloud.com` domain name.
  - `\*.qcloud.com` matches all domain names ending with `qcloud.com`.
  - `example.qcloud.\*` matches all domain names beginning with `example.qcloud`.
4. If you configure a domain name in the forwarding rule and a fuzzy matching URL in the forwarding group, you should use prefix match and add the wildcard `$` at the end for full matching.
For example, if you want to match any files that end with gif, jpg, or bmp, you can configure the forwarding group `URL ~* \.(gif|jpg|bmp)$`.
5. We recommend you configure the default access domain name. If all domain names in the listener fail to be matched, the system will point the request to the default access domain name. You can configure the default access domain name.
 >
 > If the client request fails to match all forwarding rules, the default access rule (default_server) will be matched. If you have not configured default access for Layer-7 listener, the request will match the first domain name loaded by CLB (its loading order is different from that configured in the console. The domain name may not be the first one configured in the console).
 > To specify the access domain name for unmatched rules, make sure you have configured default access for Layer-7 listener.

## Forwarding group URL matching rules
### URL configuration rules
A forwarding path URL of a Layer-7 CLB listener is in the format of `/` by default, which must begin with `/` and contain 1–120 characters.
- Regular expression is supported for URLs and identified as follows:
 - Beginning with `=` indicates exact match.
 - Beginning with `^~` indicates that the URL begins with a general string and is not regex match.
 - Beginning with `~ ` indicates case-sensitive regex match.
 - Beginning with `~*` indicates regex match that is not case-sensitive.
 - `/ ` indicates general match, where any requests will be matched if there are no other matches.
- A non-regular URL path must begin with ` /` and can contain the following characters:
`a–z` `A–Z` `0–9` `.` `-` `/` `=` `?`
- A regular URL cannot contain the following character sets:
`"` `{` `}` `;` `\` ``` `~` `'` `blank space`  

### URL matching rules
![](http://mc.qcloudimg.com/static/img/1c01dcd0959105dd7821f4e22f5cd796/image.png)
1. Matching rules: exact match takes priority over fuzzy match.
For example, after you configure the forwarding rules and forwarding groups as shown above, the following requests will be matched into different forwarding groups in sequence.
 1. Because `example.qloud.com/test1/image/index1.html` exactly matches the URL rule configured by forwarding group 1, the request will be forwarded to the real server associated with forwarding group 1, i.e., port 80 of RS1 and RS2 in the figure.
 2. Because `example.qloud.com/test1/image/hello.html` does not exactly match the first rule, it continues to match rules in forwarding group 2 and fuzzy match succeeds. The request will be forwarded to the real server associated with forwarding group 2, i.e., port 81 of RS2 and RS3 in the figure.
 3. Because `example.qloud.com/test2/video/mp4/` does not exactly match the first two rules, it continues to match until making a fuzzy match with rules in forwarding group 3. The request will be forwarded to the real server associated with forwarding group 3, i.e., port 90 of RS4 in the figure.
 4. Because `example.qloud.com/test3/hello/index.html` does not match rules in the first three forwarding groups, a match with the general rule `Default URL` will be applied. Nginx is the reverse proxy server that will forward the request to the backend application server such as FastCGI (PHP) and Tomcat (JSP).
 5. Because `example.qloud.com/test2/` does not exactly match rules in the first three forwarding groups, a match with the general rule `Default URL` will be applied.
2. If the service does not run properly in configured URL rules, it will not be redirected to other pages after a successful match.
For example, the client requests `example.qloud.com/test1/image/index1.html` and matches it with URL rules of forwarding group 1. However, the real server of forwarding group 1 has an exception and a 404 error page appears. You will see the 404 error page, but not being redirected to other pages.
3. We recommend you configure and point the default URL to a stable page (such as a static page or homepage) as well as bind it to all real servers. If none of the rules match, the system will point the request to the default URL page. Otherwise, a 404 error may occur.
4. If default URL is not configured and none of the forwarding rules match, a 404 error will be returned when you access the service.
