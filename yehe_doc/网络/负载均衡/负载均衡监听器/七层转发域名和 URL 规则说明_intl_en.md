## Business Flow Chart
The business flows of layer-7 and layer-4 CLB (formerly application CLB) are as shown below:
![](https://main.qcloudimg.com/raw/9c30c679e6a5fd70f9dd9273f8784d6d.jpg)
If layer-7 CLB is used to forward HTTP/HTTPS protocols, you can add a corresponding domain name when creating the forwarding rule in a CLB listener.
- If only one forwarding rule is created, you can access the corresponding forwarding rule and the service through VIP+URL.
- If multiple forwarding rules are created, the use of VIP+URL does not guarantee access to a specified domain name+URL. You should access a domain name+URL directly to make sure a forwarding rule has taken effect. In other words, when you configure multiple forwarding rules, a VIP may correspond to multiple domain names. In this case, we recommend you access the service via specified domain name+URL instead of VIP+URL.

## Layer-7 Forwarding Configuration Description
### Forwarded domain name configuration rules
Layer-7 CLB can forward requests from different domain names and URLs to different servers for processing. A layer-7 listener can be configured with multiple domain names, each of which can be configured with multiple forwarding paths.
- Length limit for forwarded domain name: 1–80 characters.
- It cannot begin with `_`.
- It is supported to specify domain names, such as `www.example.com`.
- Wildcard domain names are supported, but currently only those in the format of `*.example.com` or `www.example.*`, that is, wildcard domain names begin or end with `*` which appears only once.
- For non-regex forwarded domain names, valid character sets include `a–z`, `0–9`, `.`, ` -` and `_`.
- Forwarded domain name supports regex. Regex domain names:
  - Support character sets including `S`, `a–z`, `0–9`, `.`, `-`, `?`, `=`, `~`, `_`, `-`, `+`, <code>\\</code>, `^`, `*`, `!`, `$`, `&`, `|`, `(`, `)`, `[`, and `]`.
  - Must begin with `~` which can appear only once.
  - An example of regex domain name supported by CLB may be `~^www\d+\.example\.com$`.

### Forwarded domain name matching description
#### General matching policy for forwarded domain name
1. If you enter an IP address instead of a domain name in the forwarding rule and configure multiple URLs in the forwarding group, VIP+URLs will be used to access the service.
2. If you configure a full domain name in the forwarding rule and multiple URLs in the forwarding group, domain name+URLs will be used to access the service.
3. If you configure a wildcard domain name in the forwarding rule and multiple URLs in the forwarding group, you will access the service through the matching of requested domain name and URLs. To have different domain names point to the same URL, you can use this method for configuration. Taking `example.qcould.com` as an example, the format is as follows:
 - `example.qcloud.com` exactly matches the `example.qcloud.com` domain name.
 - `*.qcloud.com` matches all domain names ending with `qcloud.com`.
 - `example.qcloud.*` matches all domain names beginning with `example.qcloud`.
4. If you configure a domain name in the forwarding rule and a URL for fuzzy matching in the forwarding group, you can initiate full matching by using prefix matches and adding a suffixed wildcard `$`.
For example, if you configure `URL ~*.(gif|jpg|bmp)$`. in the forwarding group, hopefully it will match any files that end with gif, jpg, or bmp.

#### <span id="default" />Default domain name policy for forwarded domain name
If a client request cannot be matched with any domain name of this listener, CLB will forward the request to the default domain name (`Default Server`) to make the default rule controllable. Only one default domain name can be configured under one listener.
For example, the `HTTP:80` listener of CLB instance 1 is configured with two domain names: `www.test1.com` and `www.test2.com`, where `www.test1.com` is the default domain name. When a user visits `www.example.com`, since no domain name is matched, CLB will forward the request to the default domain name `www.test1.com`.

>?
>- Before May 18, 2020, the default domain name is optional for layer-7 listeners.
>  - If your layer-7 listener has a default domain name configured, client requests that do not match other rules will be forwarded to it.
>  - If your layer-7 listener has no default domain name configured, client requests that do not match other rules will be forwarded to the first domain name loaded by CLB (its loading order may be different from that configured in the console; therefore, it may not be the first one configured in the console). 
>- Starting from May 18, 2020:
>  - All new layer-7 listeners must have a default domain name configured: the first rule of a layer-7 listener must enable the default domain name. When an API is called to create a layer-7 rule, CLB will automatically set the `DefaultServer` field to `true`.
>  - For all listeners that have a default domain name configured, you need to specify a new default domain name when modifying or deleting the existing default domain name: when you perform the operation in the console, you need to specify a new default domain name; when you perform the operation by calling an API, if you do not set a new default domain name, CLB will set the earliest-created one among the remaining domain names as the new default domain name.
>  - For existing rules without a default domain name, you can directly configure a default domain name based on your business needs as instructed in [operation 4](#step4) below. If you don't do so, Tencent Cloud will set the first domain name loaded by CLB as the default domain name. This operation has no impact on the business. Existing listeners will be all processed before June 19, 2020.
>
>The above policy will be implemented gradually starting from May 18, 2020, and the effective date for each instance may vary slightly. As of June 20, 2020, all layer-7 listeners that have a forwarded domain name will have a default domain name.

The following four operations can be performed on the default domain name:
- **Operation 1**: when configuring the first forwarding rule for the layer-7 listener, the default domain name must be in "enabled" status.
- **Operation 2**: disable the current default domain name.
 - If there are multiple domain names under a listener, when disabling the current default domain name, you need to specify a new default domain name.
 - If a listener has only one domain name and the domain name is the default domain name, it cannot be disabled.
- **Operation 3**: delete the default domain name.
 - If there are multiple domain names under a listener, when you delete a rule under the default domain name:
   - If the rule is not the last rule of the default domain name, you can delete it directly.
   - If the rule is the last rule of the default domain name, you need to set a new default domain name.
 - If there is only one domain name under a listener, you can directly delete all rules without setting a new default domain name.
- <span id = "step4"></span>**Operation 4**: you can quickly modify the default domain name in the listener list.

### Forwarded URL path configuration rules
Layer-7 CLB can forward requests from different URLs to different servers for processing, and multiple forwarded URL paths can be configured for a single domain name.
- Length limit of forwarded URL: 1–200 characters.
- A non-regex forwarded URL must start with `/`., with valid character sets including `a-z`, `A-Z`, `0-9`, `.`, `-`, `_`, `/`, `=` and `?`.
- Forwarded URL supports regex:
  - A regex URL must begin with `~` which can appear only once.
  - For a regex URL, the valid character sets include `a–z`, `A–Z`, `0–9`, `.`, `-`, `_`, `/`, `=`, `?`, `~`, `^`, `*`, `$`, and `:`.
  - An example of regex URL may be `~* .png$`.
- The matching rules for a forwarded URL are as follows:
   - Beginning with `=` indicates exact match.
   - Beginning with `^~` indicates that the URL starts with a regular string and is not for regex match.
   - Beginning with `~` indicates case-sensitive regex match.
   - Beginning with `~*` indicates case-insensitive regex match.
   - `/` indicates generic match, where any requests will be matched if there are no other matches.

### Forwarded URL path matching description
![](https://main.qcloudimg.com/raw/6399b39845c9f23adccb90089e10bade.jpg)
1. Matching rules: based on longest prefix match, exact match is performed first followed by fuzzy match.
For example, after you configure the forwarding rules and forwarding groups as shown above, the following requests will be matched into different forwarding rules in sequence.
 1. Because `example.qloud.com/test1/image/index1.html` exactly matches the URL rule configured by forwarding rule 1, the request will be forwarded to the real servers associated with forwarding rule 1, i.e., port 80 of CVM1 and CVM2 in the figure.
 2. Because `example.qloud.com/test1/image/hello.html` has no exact match, it will match forwarding rule 2 based on longest prefix match; therefore, the request will be forwarded to the real servers associated with forwarding rule 2, i.e., port 81 of CVM2 and CVM3 in the figure.
 3. Because `example.qloud.com/test2/video/mp4/` has no exact match, it will match forwarding rule 3 based on longest prefix match; therefore, the request will be forwarded to the real server associated with forwarding rule 3, i.e., port 90 of CVM4 in the figure. 
 4. Because `example.qloud.com/test3/hello/index.html` has no exact match, it will match the root directory's default URL `example.qloud.com/` by longest prefix match. In this case, Nginx will forward the request to the real server such as FastCGI (php) or Tomcat (jsp), while Nginx will exist as a reverse proxy server.
 5. Because `example.qloud.com/test2/` has no exact match, it will match the root directory's default URL `example.qloud.com/` by longest prefix match.
2. If the service does not work properly in the set URL rules, it will not be redirected to other pages after successful match.
For example, the client requests `example.qloud.com/test1/image/index1.html` and matches it with forwarding rule 1. However, the real server of forwarding rule 1 has an exception and a 404 error page appears. You will see the 404 error page, but not being redirected to other pages.
3. You are recommended to point the default URL to a stable page (such as a static page or homepage) and bind it to all real servers. If none of the rules match, the system will point the request to the default URL page; otherwise, a 404 error may occur.
4. If you do not set the default URL, and none of the forwarding rules match, a 404 error will be returned when you access the service.
5. Note on the slash at the end of the layer-7 URL path: if the URL you set ends with `/`, but the access request from the client does not contain `/`, then the request will be redirected to a rule ending with `/` (301 redirect).
For example, under the `HTTP:80` listener, the configured domain name is `www.test.com`:
 1. If the URL set under this domain name is `/abc/`:
     - When the client accesses `www.test.com/abc`, it will be redirected to `www.test.com/abc/`.
     - When the client accesses `www.test.com/abc/`, it will match `www.test.com/abc/`.
 2. If the URL set under this domain name is `/abc`:
     - When the client accesses `www.test.com/abc`, it will match `www.test.com/abc`.
     - When the client accesses `www.test.com/abc/`, it will also match `www.test.com/abc`.

## Layer-7 Health Check Configuration Description
### Health check domain name configuration rules
A health check domain name is the domain name used by layer-7 CLB to detect the health status of a real server.
- Length limit: 1–80 characters.
- Default: forwarded domain name.
- Regex is not supported. If your forwarded domain name is a wildcard domain name, you should specify a fixed one (non-regex).
- Valid character sets include `a–z`, `0–9`, `.`, `-`, and `_`. For example, `www.example.qcloud.com`.

### Health check path configuration rules
A health check path is the URL path used by layer-7 CLB to detect the health status of a real server.
- Length limit: 1–200 characters.
- Default: `/`, with which the path must begin.
- Regex is not supported. You are recommended to specify a fixed URL (static page) for health check.
- Valid character sets include `a–z`, `A–Z`, `0–9`, `.`, `-`, `_`, `/`, `=`, `?`, and `:`. For example,  `/index`.
