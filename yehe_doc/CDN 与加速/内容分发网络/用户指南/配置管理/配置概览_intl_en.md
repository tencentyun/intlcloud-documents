## Configuration Overview

CDN supports various custom configurations and you can adjust them based on your business needs.

### Basic configurations

Basic configurations are the contents required for CDN acceleration, including origin server configurations and the basic acceleration service information such as acceleration region and service type, etc.

| Configuration                                                     | Description                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Basic Information](https://intl.cloud.tencent.com/document/product/228/7864) | Modifies basic information such as the project, acceleration region, and service type, etc.         |
| [Origin Server Configuration](https://intl.cloud.tencent.com/document/product/228/6289) | Configures multi-IP round-robin origin-pull, domain name-based origin-pull, weighted round-robin origin-pull, origin domains, and origin-pull protocols.<br/>Supports configuring hot backup origin servers.<br/>**For global acceleration domain names, the acceleration in and outside the Chinese mainland can be configured separately.** |

### Access control

You can configure various rules based on user requests to allow or block access requests.

| Configuration                                                     | Description                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Hotlink Protection](https://intl.cloud.tencent.com/document/product/228/6292) | Supports setting referer allowlists and blocklists to determine whether to allow or deny HTTP access requests based on the request referer headers.<br/>**For global acceleration domain names, the acceleration in and outside the Chinese mainland can be configured separately.** |
| [IP Blocklist/Allowlist](https://intl.cloud.tencent.com/document/product/228/6298) | Supports setting IP allowlists and blocklists to determine whether to allow or deny HTTP access requests based on the request client IPs.<br/>**For global acceleration domain names, the acceleration in and outside the Chinese mainland can be configured separately.** |
| [IP Access Limit](https://intl.cloud.tencent.com/document/product/228/6420) | Limits the frequency that an IP can access a single node to deny the access requests from client IPs exceeding the limit.  |
| [Authentication](https://intl.cloud.tencent.com/document/product/228/35237) | Supports various timestamp signature algorithms and rules for anti-hotlinking configuration.<br/>**For global acceleration domain names, the acceleration in and outside the Chinese mainland can be configured separately.** |
| [Video Dragging](https://intl.cloud.tencent.com/document/product/228/8111) | It is designed for streaming VOD acceleration.<br/>With the video dragging feature enabled, you can specify the start point of a video through the parameter `start`.|
| [UA Blocklist/Allowlist](https://intl.cloud.tencent.com/document/product/228/37256)  | Determines whether to deny or allow requests according to HTTP request header `User-Agent`.  |
| [Downstream Speed Limit](https://intl.cloud.tencent.com/document/product/228/37257) | Controls the CDN access bandwidth by setting the downstream speed limit on a URL.   |

### Cache configuration

Cache configuration controls cache on CDN nodes.

| Configuration                                                     | Description                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Ignore Query String](https://intl.cloud.tencent.com/document/product/228/35316) | For resource cache, it supports configuring whether to ignore parameters after "?" in an access URL.<br/>**We recommend disabling this feature if the parameters after "?" indicate differen contents of your business.** |
| [Node Cache Validity](https://intl.cloud.tencent.com/document/product/228/35317) | Supports configuring the cache validity of files on nodes based on file path and type.    |
| [Status Code Cache](https://intl.cloud.tencent.com/document/product/228/35318) | Supports configuring status code cache validity for CDN nodes to respond to 2XX status codes directly, thus reducing pressure on the origin server. |
| [HTTP Header Cache](https://intl.cloud.tencent.com/document/product/228/35319) | It can be disabled as needed. CDN nodes cache all origin server response headers by default.        |
| [Cache Ignore URL Case](https://intl.cloud.tencent.com/document/product/228/35316) | CDN node cache does not ignore letter case by default. Letter case can be ignored as needed. |
| [Access URL Rewrite](https://intl.cloud.tencent.com/document/product/228/38074)| Supports customizing URL rewrite configuration to redirect requests from URLs with 302 status code to target URLs.|


### Origin-pull configuration

Origin-pull configuration controls the process of forwarding requests from CDN nodes to origin servers.

| Configuration                                                     | Description                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Range GETs](https://intl.cloud.tencent.com/document/product/228/7184) | Range GETs is used for origin-pull by default. If it is not supported by your origin server, you can disable it. |
| [Request Header](https://intl.cloud.tencent.com/document/product/228/37037) | Adds specified headers during origin-pull such as the real client IP.      |
| [Follow 301/302](https://intl.cloud.tencent.com/document/product/228/7183) | It can be enabled for origin-pull as needed.                                  |
| [Origin-pull Timeout](https://intl.cloud.tencent.com/document/product/228/35227) | Configures the TCP connection timeout period (which defaults to 5 seconds) and loading period (which defaults to 10 seconds) of origin-pull. |

### HTTPS acceleration configuration

HTTPS acceleration supports various HTTPS-related configurations.

| Configuration                                                     | Description                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [HTTPS Configuration](https://intl.cloud.tencent.com/document/product/228/35213) | Supports uploading a self-owned certificate or a hosted certificate to enable HTTPS acceleration.  |
| [HTTP2.0 Configuration](https://intl.cloud.tencent.com/document/product/228/35215) | With it is enabled, CDN edge servers can support HTTP2.0.<br/>**Please first configure a certificate to enable HTTP2.0.** |
| [Forced Redirection Configuration](https://intl.cloud.tencent.com/document/product/228/35214) | Forced redirection from HTTPS to HTTP access can be achieved with or without a certificate.<br/>Forced redirection from HTTP to HTTPS access requires a certificate. |
| [OCSP Stapling](https://intl.cloud.tencent.com/document/product/228/35216) | With it is enabled, OCSP stapling is support.<br/>**Please first configure a certificate to enable OCSP stapling.** |
| [HSTS Configuration](https://intl.cloud.tencent.com/document/product/228/37036) | If it is enabled, the header `strict-transport-security` will be added.<br/>**Please first configure a certificate to enable HSTS configuration.** |

### Advanced configuration

| Configuration                                                     | Description                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Bandwidth Cap Configuration](https://intl.cloud.tencent.com/document/product/228/7541) | Supports configuring bandwidth cap for the acceleration in and outside the Chinese mainland. Acceleration service can be stopped as needed if the cap is exceeded. <br/>**For global acceleration domain names, the acceleration in and outside the Chinese mainland can be configured separately.** |
| [SEO Configuration](https://intl.cloud.tencent.com/document/product/228/35219) | Supports automatically recognizing that whether an access IP belongs to a search engine.<br/>If yes, requests from the IP will be forwarded to the origin server to guarantee the stability of the search engine's weight. |
| [Response Header Configuration](https://intl.cloud.tencent.com/document/product/228/35320) | Sets HTTP response headers as needed and adds them to the response requests to clients.  |
| [Smart Compression Configuration](https://intl.cloud.tencent.com/document/product/228/35220) | Performs Gzip or Brotli compression on specified files based on the file type and range.                           |


