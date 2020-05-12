## Business Flow Chart
The business flows of Layer-7 and Layer-4 CLB (formerly known as “application CLB”) are shown as below:
![](https://mc.qcloudimg.com/static/img/de6af7fca35640ed6d0937f05f5039d2/image.png)
Using Layer-7 CLB to forward a HTTP/HTTPS protocol, you can add a corresponding domain name when creating a forwarding rule in a CLB instance listener.
- If only one forwarding rule is created, you can access the corresponding forwarding rule and the service via VIP+URL.
- If multiple forwarding rules are created, the use of VIP+URL does not guarantee access to a specified domain name+URL. You should access a domain name+URL directly to make sure a forwarding rule has taken effect. In other words, when you configure multiple forwarding rules, a VIP may correspond to multiple domain names. In this case, we recommend you access the service via specified domain name+URL instead of VIP+URL.

## Layer-7 forwarding configuration
### Configuration rules for forwarding domain names
Layer-7 CLB can forward requests from different domain names and URLs to different servers for processing. A Layer-7 listener can be configured with multiple domain names, each of which can be configured with multiple forwarding paths.
- Length limit: 1-80 characters.
- It can not start with "/".
- It is supported to specify domain names, such as `www.example.com`.
- Wildcard domain names are supported, but currently only those in the form of `*.example.com` or `www.example.*`, that is, wildcard domain names start or end with `*` which appears only once.
- For the forwarded domain names of non-regular expressions, valid character sets include `a-z`, `0-9`, `.`, ` -` and `_`.
- Domain name forwarding supports regular expressions, the domain names of which:
  - Support character sets including `S`, `a-z`, `0-9`, `.`, `-`, `?`, `=`, `~`, `_`, `-`, `+`<code>\\</code>`^`, `*`, `!`, `$`, `&`, `|`, `(` `)` and `[` `]`.
  - Must start with `~` which can appear only once.
  - An example of regular domain name supported by CLB may be `~^www\d+\.example\.com$`.


### Matching forwarded domain names
1. If you enter an IP address instead of a domain name in the forwarding rule and configure multiple URLs in the forwarding group, VIP+URLs will be used to access the service.
2. If you configure a full domain name in the forwarding rule and multiple URLs in the forwarding group, domain name+URLs will be used to access the service.
3. If you configure a wildcard domain name in the forwarding rule and multiple URLs in the forwarding group, you will access the service through the matching of requested domain name and URLs. To have different domain names point to the same URL, you can use this method for configuration. Taking `example.qcould.com` as an example, the format is as follows:
 - `example.qcloud.com` exactly matches a domain name called  `example.qcloud.com`.
 - `\*.qcloud.com` matches all domain names ending with `qcloud.com`.
 - `example.qcloud.\*` matches all domain names starting with `example.qcloud`.
4. If you configure a domain name in the forwarding rule and a URL for fuzzy matching in the forwarding group, you can initiate full matching by using prefix matches and adding a postfixed wildcard `$`.
For example, if you configure `URL ~* \.(gif|jpg|bmp)$`. in the forwarding group, hopefully it will match any files that end with gif, jpg, or bmp.
5. It is recommended to configure the default access domain name. If no domain names in the listener are matched successfully, your request will be automatically redirected to this default domain name so that the default rules are under control. You can configure it using the following approaches:
>
> If no client request to match all forwarding rules succeeds, the  default_server will be matched. If your Layer-7 listener is not configured with a default server, your request will match up with the first domain name loaded by CLB (its loading order is different from the configuring order of the console, so the domain name matched may not be the one configured first in the console).
> To specify an access domain name for unmatched rules, make sure you have configured a default server for Layer-7 listener.
>
![](https://main.qcloudimg.com/raw/0bd726c5f0248a9033f02c851599bf2d.png)

### Configuration rules for URL-forwarding paths
Layer-7 CLB forwards requests from different URLs to different servers for processing, and can configure multiple URL-forwarding paths for a single domain name.
- Length limit: 1-200 characters.
- A forwarded URL of non-regular expression must start with `/`., with valid character sets including `a-z`, `A-Z`, `0-9`, `.`, `-`, `_`, `/`, `=` and `?`.
- URL forwarding supports regular expressions:
  - A URL of regular expression must start with `~` which can appear only once.
  - For a regular expression URL, the valid character sets include `a-z`, `A-Z`, `0-9`, `.`, `-`, `_`, `/`, `=`, `?`, `~`, `^`, `*` and `$`.
  - An example of regular expression URL may be `~* .png$`.
- The matching rules for a forwarded URL are as follows:
   - Starting with `=` indicates exact match.
   - Starting with `^~` indicates that the URL starts with a regular string and is not for RegExp match.
   - Starting with `~` indicates case-sensitive RegExp match.
   - Starting with `~*` indicates RegExp match that is not case-sensitive.
   - ` /` indicates generic match, where any requests will be matched if there are no other matches.

### Path matching for URL-forwarding
![](http://mc.qcloudimg.com/static/img/1c01dcd0959105dd7821f4e22f5cd796/image.png)
1. Matching rules: exact match takes priority over fuzzy match.
For example, after you configure the forwarding rules and forwarding groups as shown above, the following requests will be matched in sequence with different forwarding groups.
 1. Because `example.qloud.com/test1/image/index1.html` exactly matches the URL rule configured by forwarding group 1, the request will be forwarded to the real server associated with forwarding group 1, i.e., port 80 of RS1 and RS2 in the figure.
 2. Because `example.qloud.com/test1/image/hello.html` does not exactly match the first rule, it continues to match rules in forwarding group 2 and fuzzy match succeeds. The request will be forwarded to the real server associated with forwarding group 2, i.e., port 81 of RS2 and RS3 in the figure.
 3. Because `example.qloud.com/test2/video/mp4/` does not exactly match the first two rules, it continues to match until making a fuzzy match with rules in forwarding group 3. The request will be forwarded to the real server associated with forwarding group 3, i.e., port 90 of RS4 in the figure.
 4. Because `example.qloud.com/test3/hello/index.html` does not match rules in the first three forwarding groups, a match with the general rule `Default URL` will be applied. Nginx is the reverse proxy server that will forward the request to the real application server such as FastCGI (PHP) and Tomcat (JSP).
 5. Because `example.qloud.com/test2/` does not exactly match rules in the first three forwarding groups, a match with the general rule `Default URL` will be applied.
2. If the service does not run properly in configured URL rules, it will not be redirected to other pages after a successful match.
For example, the client requests `example.qloud.com/test1/image/index1.html` and matches it with URL rules of forwarding group 1. However, the real server of forwarding group 1 has an exception and a 404 error page appears. You will see the 404 error page, but not being redirected to other pages.
3. We recommend you configure and point the default URL to a stable page (such as a static page or homepage) as well as bind it to all real servers. If none of the rules match, the system will point the request to the default URL page. Otherwise, a 404 error may occur.
4. If no default URLs are configured and none of the forwarding rules are matched, a 404 error will be returned when you access the service.

## Health check configuration for Layer-7 forwarding
### Configuration rules for domain names of health check
A domain name of health check  is one that Layer-7 CLB uses to detect the health status of a real server.
- Length limit: 1-80 characters.
- Default: domain name to forward.
- Regular expressions are not supported. When you forward a wildcard domain name for health check, you need to specify a fixed one (non-regular).
- Valid character sets include `a-z`, `0-9`, `.` and ` -`.

### Configuration rules for paths of health check
A path of health check  is one that Layer-7 CLB uses to detect the health status of a real server.
- Length limit: 1-200 characters.
- Default: `/`, with which the path must start.
- Regular expressions are not supported. It is recommended to specify a fixed URL (static page) for health check.
- Valid character sets include `a-z`, `A-Z`, `0-9`, `.`, `-`, `_`, `/`, `=` and `?`.
