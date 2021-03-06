## 配置概览

腾讯云 CDN 在请求的各阶段支持多项自定义配置，您可以根据自身业务需要进行调整。

### 基本配置

基本配置包括域名的加速服务基本信息，如加速区域、业务类型等，及源站相关配置，为 CDN 加速必须配置的内容。

| 配置名称                                                     | 功能说明                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [基本信息](https://intl.cloud.tencent.com/document/product/228/7864) | 修改域名所属项目、加速区域、业务类型等基础信息。               |
| [源站配置](https://intl.cloud.tencent.com/document/product/228/6289) | 支持多 IP 轮询回源配置、域名回源、权重回源、回源 Host 设置、回源协议设置。<br/>支持热备源站配置。<br/>**全球加速域名支持境内境外分开配置。** |

### 访问控制

访问控制配置根据用户实际请求内容，配置各类规则进行访问拦截或放行。

| 配置名称                                                     | 功能说明                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [防盗链配置](https://intl.cloud.tencent.com/document/product/228/6292) | referer 黑白名单配置，根据访问 HTTP 请求中的 referer 头部，判定是否拒绝/放行请求。<br/>**全球加速域名支持境内境外分开配置。** |
| [IP 黑白名单配置](https://intl.cloud.tencent.com/document/product/228/6298) | IP 黑白名单配置，根据访问 HTTP 请求的 client ip，判定是否拒绝/放行请求。<br/>**全球加速域名支持境内境外分开配置。** |
| [IP 访问限频配置](https://intl.cloud.tencent.com/document/product/228/6420) | 设置单 IP 单节点访问限频，超出访问频次的 client ip 发起的请求将直接被拒绝。 |
| [鉴权配置](https://intl.cloud.tencent.com/document/product/228/35237) | 时间戳防盗链配置，支持多种时间戳签名算法及规则。<br/>**全球加速域名支持境内境外分开配置。** |
| [视频拖拽](https://intl.cloud.tencent.com/document/product/228/8111) | 用于流媒体点播加速场景。<br/>开启视频拖拽功能后，支持通过 start 参数指定视频开始播放位置。 |
| [UA 黑白名单配置](https://intl.cloud.tencent.com/document/product/228/37256) | UA 黑白名单配置，根据访问 HTTP 请求的 User-Agent 头部，判定是否拒绝/放行请求。 |
| [下行限速配置](https://intl.cloud.tencent.com/document/product/228/37257) | 设置单链接下行限速配置，一定程度上可控制 CDN 访问带宽 。       |

### 缓存配置

缓存配置控制了 CDN 节点的缓存行为。

| 配置名称                                                     | 功能说明                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [过滤参数配置](https://intl.cloud.tencent.com/document/product/228/35316) | 设置节点缓存资源时，是否忽略访问 URL ? 之后的参数。<br/>**若您的业务通过 URL 后参数代表不同内容，建议不要开启过滤参数配置。** |
| [缓存过期配置](https://intl.cloud.tencent.com/document/product/228/35317) | 支持根据路径、文件类型配置文件在 CDN 节点上的缓存过期时间。    |
| [状态码缓存配置](https://intl.cloud.tencent.com/document/product/228/35318) | 当源站响应异常状态码(如404 405)时，CDN 节点上对响应内容的缓存过期时间配置。 |
| [HTTP 头部缓存配置](https://intl.cloud.tencent.com/document/product/228/35319) | 默认情况下 CDN 节点将缓存所有源站响应头部，可按需关闭。        |
| [忽略大小写缓存配置](https://intl.cloud.tencent.com/document/product/228/35316) | 默认情况下 CDN 节点区分大小写缓存，可按需忽略大小写。         |
| [URL 重写配置](https://intl.cloud.tencent.com/document/product/228/38074)|支持自定义 URL 重写配置，将 URL 302 重定向到目标 URL。|


### 回源配置

回源配置控制了 CDN 节点将请求发送至源站的行为。

| 配置名称                                                     | 功能说明                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Range 回源配置](https://intl.cloud.tencent.com/document/product/228/7184) | 默认情况下 CDN 节点回源均为分片回源，若源站不支持，可关闭此项配置。 |
| [回源 Request Header 配置](https://intl.cloud.tencent.com/document/product/228/37037) | 请求回源时按需添加指定头部信息，如携带真实 client ip 等。      |
| [回源跟随301/302配置](https://intl.cloud.tencent.com/document/product/228/7183) | 支持开启回源跟随301/302配置。                                  |
| [回源超时时间配置](https://intl.cloud.tencent.com/document/product/228/35227) | 配置回源 TCP 连接超时时间(默认 5秒)及回源加载时间(默认 10秒)。 |

### HTTPS 加速配置

HTTPS 加速配置模块支持各项 HTTPS 相关配置。

| 配置名称                                                     | 功能说明                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [HTTPS 配置](https://intl.cloud.tencent.com/document/product/228/35213) | 上传自有证书或使用已托管的证书，启动 HTTPS 加速。              |
| [HTTP2.0 配置](https://intl.cloud.tencent.com/document/product/228/35215) | 开启后 CDN 边缘节点支持 HTTP2.0 协议。<br/>**开启 HTTP2.0 协议前需要先进行证书配置。** |
| [强制跳转配置](https://intl.cloud.tencent.com/document/product/228/35214) | 未配置/已配置证书情况下，均可设置 HTTPS 强制跳转为 HTTP 请求。<br/>已配置证书情况下，可配置 HTTP 强制跳转为 HTTPS 请求。 |
| [OCSP 装订配置](https://intl.cloud.tencent.com/document/product/228/35216) | 开启后支持 OCSP 装订。<br/>**开启 OCSP 装订前需要先进行证书配置。** |
| [HSTS 配置](https://intl.cloud.tencent.com/document/product/228/37036) | 开启后添加 strict-transport-security 头部。<br/>**开启 HSTS 配置前需要先进行证书配置。** |

### 高级配置

| 配置名称                                                     | 功能说明                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [带宽封顶配置](https://intl.cloud.tencent.com/document/product/228/7541) | 支持设置境内、境外加速封顶带宽，超出后可按需停止加速服务。<br/>**全球域名支持境内境外分开配置。** |
| [SEO 优化配置](https://intl.cloud.tencent.com/document/product/228/35219) | 开启后可自动识别访问 IP 是否为搜索引擎。<br/>确认后自动回源，尽量保证搜索引擎权重的稳定性。 |
| [Response Header 配置](https://intl.cloud.tencent.com/document/product/228/35320) | 按需进行 HTTP Response Header 设置，在响应请求中返回给客户端。 |
| [智能压缩配置](https://intl.cloud.tencent.com/document/product/228/35220) | 指定文件类型和文件范围进行 Gzip 或 Brotli 压缩。                             |


