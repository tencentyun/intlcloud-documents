## Feature Overview
- Based on the referer mechanism supported by the HTTP protocol, the source of a request can be identified through the referer field in the HTTP header. You can configure a referer blacklist or whitelist to identify and authenticate the sources of video requests.
- Blacklist and whitelist modes are supported. When a video playback request reaches a CDN node, the node will authenticate the request source according to the configured referrer blacklist or whitelist. If a request meets the rule, CDN will return video data; otherwise, it will return a 403 response code and reject the playback request.

> For more information on enabling referer hotlink protection, please see [Setting Hotlink Protection](https://cloud.tencent.com/document/product/266/33469#referer-.E9.98.B2.E7.9B.97.E9.93.BE).

## Precautions
* This feature is optional and not enabled by default.
* After enabling this feature, select and configure the blacklist or whitelist. The two modes are mutually exclusive, and only one is supported at the same time.
* 1–10 domain names can be entered in the blacklist or whitelist (one entry per line).
* Do not put a protocol name (`http://` or `https://`) before a domain name. Domain name matching is based on the prefix (for example, if you enter `abc.com`, then both `abc.com/123` and `abc.com.cn` will be matched), and wildcard (e.g., `*.abc.com)` is supported.
