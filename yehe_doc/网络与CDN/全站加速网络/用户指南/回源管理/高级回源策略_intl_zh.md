ECDN 全站加速支持的高级回源策略包括：  
- **[择优回源](#default)**
根据探测结果，回源时选择性能最佳的源站。
- **[分权重回源](#weight)**
根据探测结果和权重比例，回源时优先按照权重比例分摊请求。
- **[分主备回源](#master-backup)**
回源时总是优先选择主源，只有当主源异常时，才选择备源服务。

您可以根据您的业务需求，选择合适的回源策略。  
>!
>- ECDN 默认回源策略是择优回源。
>- 择优回源、主备回源、分权重回源三种回源方式均支持 IP 源站与域名源站。
>- 选择分权重回源时，平台调度时还会兼顾性能因素，因此实际的回源比例可能与设置值略有误差。
>- 选择主备回源时，当接收到源站返回400 - 599状态码（除416外）时，当次请求自动重试备源。
>- 若您的业务已迁移至 CDN 控制台，请参考 [CDN 产品文档](https://intl.cloud.tencent.com/document/product/228)，前往 CDN 控制台进行操作。


## 新增高级回源策略[](id:new)

### 1. 择优回源[](id:default)
择优回源是平台默认的回源策略。
![](https://main.qcloudimg.com/raw/cb4e342444e4bf4cd00cb27d940ec9fe.png)

>? 当源站类型为域名源站时，源站域名不可与加速域名相同。


### 2. 分权重回源[](id:weight)
您可以根据不同源站的负载能力定制回源的权重系数。
![](https://main.qcloudimg.com/raw/67d50247982e9eb4bcd5b244aa365f2f.png)   

>?
>- 权重支持配置0 - 100，但权重值不可全配置为0，系统根据权重值计算不同源站的回源比例。
>- 支持配置多个 IP 源站或域名源站，IP 源站与域名源站不可混填，最多支持配置32个 IP 地址或50个域名地址。
>- 若您需要 ECDN 回源节点 IP 列表做加白处理，可通过节点查询接口 获取节点信息，由于产品服务节点常有更新，对于源站开白的使用场景，请定期调用接口获取最新节点信息，若新增服务节点发布7日后您尚未更新加白导致回源失败等问题，ECDN 侧不对此承担责任。


### 3. 分主备回源[](id:master-backup)
当您有分主备回源的需求时可以使用该功能。
![](https://main.qcloudimg.com/raw/ec760ae6232996fe79090740a1f3812c.png)

## 修改高级回源策略
域名新增后，您还可以通过域名管理页面修改高级回源策略，修改步骤如下：
第一步：登录 [ECDN 控制台](https://console.cloud.tencent.com/dsa)，单击【域名管理】菜单，再单击**管理**操作。
![](https://main.qcloudimg.com/raw/2a6178c5f3c8fedb1b759c6adaaa0961.png)
第二步：在**基本信息**页面下，可以看到源站配置信息，单击【修改】进入修改页面。
![](https://main.qcloudimg.com/raw/f6c5c81c162d7da054da02ae47ce73b3.png)
第三步：在弹框处您可以根据需要调整源站配置，关于高级回源策略的配置，请参见 [新增高级回源策略](#new).
![](https://main.qcloudimg.com/raw/7787ebc04c0657f6edda95ef0f9545e3.png)

>!
>- 源站配置下发需要时间，生效时间约5 - 30分钟不等。
>- 新增源站地址时，请确保源站服务已正常启用，否则切换后可能导致部分请求失败。
>- 删除源站地址时，请先在 ECDN 平台删除源站配置后，再停用源站服务，可以降低源站切换的风险。
