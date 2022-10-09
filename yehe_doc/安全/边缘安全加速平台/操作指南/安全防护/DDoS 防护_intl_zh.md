本文将介绍 DDoS 防护功能的 DDoS 防护等级、IP 黑白名单、区域封禁、协议封禁等功能以及相关配置操作。
>?DDoS 防护功能和相关配置可能根据您选购的 EdgeOne 产品套餐有所不同。

## 前提条件
您需要成功 [购买](https://intl.cloud.tencent.com/document/product/1145/48705) 边缘安全加速平台（EdgeOne）产品（企业版），并完成 [接入站点](https://intl.cloud.tencent.com/document/product/1145/45966) 或 [接入四层代理](https://intl.cloud.tencent.com/document/product/1145/46194)。

## DDoS防护等级
针对 DDoS 攻击，EdgeOne 提供不同防护等级的相关操作及应用场景，并为您介绍如何在控制台中设置 DDoS 防护等级。


### 应用场景
EdgeOne 提供防护策略调整功能，针对 DDoS 攻击提供三种防护等级供您选择，各个防护等级的具体防护操作如下：

| 防护等级 | 防护操作                                                     | 描述                                                         |
| :------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| 宽松     | <li>过滤明确攻击特征的 SYN、ACK 数据包。</li><li>过滤不符合协议规范的 TCP、UDP、ICMP 数据包。</li><li>过滤具有明确攻击特征的 UDP 数据包。</li> | <li>清洗策略相对宽松，仅对具有明确攻击特征的攻击包进行防护。</li><li>建议在怀疑有误拦截时启用，遇到复杂攻击时可能会有攻击透传。</li> |
| 适中     | <li>过滤明确攻击特征的 SYN、ACK 数据包。</li><li>过滤不符合协议规范的 TCP、UDP、ICMP 数据包。</li><li>过滤具有明确攻击特征的 UDP 数据包。</li><li>过滤常见基于 UDP 的攻击数据包。</li><li>对部分访问源 IP 进行主动验证。</li> | <li>清洗策略适配绝大多数业务，可有效防护常见攻击。</li><li>默认为适中模式。</li> |
| 严格     | <li>过滤明确攻击特征的 SYN、ACK 数据包。</li><li>过滤不符合协议规范的 TCP、UDP、ICMP 数据包。</li><li>严格检查过滤具有明确攻击特征的 UDP 数据包和基于 UDP 的攻击数据包。</li><li>对部分访问源 IP 进行主动验证。</li><li>过滤 ICMP 攻击包。</li> | 清洗策略相对严格，建议在适中模式出现攻击透传时使用。         |

>?
>- 如果您的业务有遭受大规模攻击的历史，或者需要使用 UDP，建议您[联系我们](https://intl.cloud.tencent.com/contact-us) 进行策略定制，以免严格模式影响业务流程。
>- 默认情况下，您所购买的 EdgeOne（企业版） 采用适中防护等级，您可以根据实际业务情况自由调整 DDoS 防护等级。
>- 默认情况下，您所购买的EdgeOne（标准版）采用适中防护等级。


### 操作步骤
1. 登录 [边缘安全加速平台控制台](https://console.cloud.tencent.com/edgeone)，在左侧导航中，单击**安全防护** > **DDoS 防护**。
2. 在 DDoS 防护页面的左侧，选中防护业务对象，如“企业版 DDoS 防护”或“企业版 DDoS 防护 - 四层代理”实例。
![](https://qcloudimg.tencent-cloud.cn/raw/c0a6eed4c3425ea285b3d296e5ee6a05.png)
3. 在 DDoS 防护等级卡片中，默认在开启“防护状态”的情况下，业务刚接入的 EdgeOne 站点采用适中防护等级，您可以根据实际业务防护需求自由调整 DDoS 防护等级。
![](https://qcloudimg.tencent-cloud.cn/raw/fbe8f793333d8bd6264d1cfe9f382275.png)


## IP 黑白名单
EdgeOne 支持通过配置 IP 黑名单和白名单的方式，控制对 EdgeOne 站点的访问，基于客户端源 IP 封禁或者放行访问请求。
>? IP 黑白名单规则保存后，将在5-10秒内生效。
>- 白名单中的 IP，访问时请求将被直接放行，不再经过其他 DDoS 防护策略过滤。
>- 黑名单中的 IP，访问时请求将被直接丢弃。

1. 登录 [边缘安全加速平台控制台](https://console.cloud.tencent.com/edgeone)，在左侧导航中，单击**安全防护** > **DDoS 防护**。
2. 在 DDoS 防护页面的左侧，选中防护业务对象，如“企业版 DDoS 防护”或“企业版 DDoS 防护 - 四层代理”实例。
![](https://qcloudimg.tencent-cloud.cn/raw/cb03113aaf23a11c95d58abd73fbb79f.png)
3. 在 IP 黑白名单卡片中，单击**设置**，进入 IP 黑白名单页面。
![](https://qcloudimg.tencent-cloud.cn/raw/e7529d2fea115fc61402a2e7a21e9c46.png)
4. 在 IP 黑白名单页面中，单击**新建**，创建 IP 黑白名单规则，输入需要匹配规则的 IP，并选择黑白名单类型，单击**保存**。
![](https://qcloudimg.tencent-cloud.cn/raw/b2aeaffa7a3ba49d3c7e5cf9a564665c.png)
6. （可选）新建完成后，IP 黑白名单列表将新增一条 IP 黑白名单规则，可以在右侧操作列，单击**删除**，删除 IP 黑白名单规则。
![](https://qcloudimg.tencent-cloud.cn/raw/2fd20196deb21eb3b44de05c48d885db.png)


## 区域封禁
EdgeOne 支持通过指定区域列表的方式，禁止源 IP 归属指定区域的客户端访问 EdgeOne 站点。支持多地区、国家进行流量封禁。
>?在配置了区域封禁后，该区域的攻击流量依然会被平台统计和记录，但不会流入业务源站。

1. 登录 [边缘安全加速平台控制台](https://console.cloud.tencent.com/edgeone)，在左侧导航中，单击**安全防护** > **DDoS 防护**。
2. 在 DDoS 防护页面的左侧，选中防护业务对象，如“企业版 DDoS 防护”或“企业版 DDoS 防护 - 四层代理”实例。
![](https://qcloudimg.tencent-cloud.cn/raw/4c1a18fce71a8c0e476a5f7a215603fb.png)
3. 在区域封禁卡片中，单击**设置**，进入区域封禁页面。
![](https://qcloudimg.tencent-cloud.cn/raw/8cbec0bbc75da0a5917d75ded9257eca.png)
4. 在区域封禁页面，单击**新建**。
5. 在新建区域封禁对话框中，选择封禁区域，单击**确定**，创建区域封禁规则。
![](https://qcloudimg.tencent-cloud.cn/raw/e92efeddba9852eddb4fabf4a5b70097.png)
6. （可选）新建完成后，在区域封禁列表，将新增一条区域封禁规则，可以在右侧操作列，单击**配置**，修改区域封禁规则。
![](https://qcloudimg.tencent-cloud.cn/raw/05a61a7dc3d0fe2225f5315e658fd3e9.png)

## 端口过滤

EdgeOne 支持通过指定端口和协议的方式，管控客户端访问 EdgeOne 站点。开启端口过滤后，可以根据需求自定义协议类型、源端口范围、目的端口范围的组合，并对匹配中的规则进行设置丢弃、、继续防护的策略动作。端口过滤可以针对源端口的访问流量，进行精准制定防护策略。

1. 登录 [边缘安全加速平台控制台](https://console.cloud.tencent.com/edgeone)，在左侧导航中，单击**安全防护** > **DDoS 防护**。
2. 在 DDoS 防护页面的左侧，选中防护业务对象，如“企业版 DDoS 防护”或“企业版 DDoS 防护 - 四层代理”实例。
![](https://qcloudimg.tencent-cloud.cn/raw/075f32b046ef6b723e879176eedc40b9.png)
3. 在端口过滤卡片中，单击**设置**，进入端口过滤页面。
![](https://qcloudimg.tencent-cloud.cn/raw/60963e3373ddec51e672044b61b6bf1d.png)
4. 在端口过滤页面中，单击**新建**，创建端口过滤规则，根据需求，选择不同防护动作并填写相关字段，单击**保存**。
>?
>- 支持选择多个实例资源批量创建，未绑定防护资源的实例，不允许创建规则。
>- 优先级：请填写一个介于1-1000的数字，数字越小优先级越高，该条规则排列位置越靠前，默认优先级为10。

![](https://qcloudimg.tencent-cloud.cn/raw/6d3e7f363891dca41da7ff2a89e86ae2.png)
6. （可选）新建完成后，在端口过滤列表将新增一条端口过滤规则，可以在右侧操作列，单击**配置**，可以修改特征端口规则。
![](https://qcloudimg.tencent-cloud.cn/raw/e0021e07c52c56f45d2f1e2d35b1ced7.png)

## 特征过滤
EdgeOne 支持针对 IP、TCP 及 UDP 报文头或载荷中的特征自定义拦截策略。开启特征过滤后，您可以将源端口、目的端口、报文长度、IP 报文头或荷载的匹配条件进行组合，并对命中条件的请求设置丢弃、放行、丢弃并拉黑、继续防护等策略动作，特征过滤可以精准制定针对业务报文特征或攻击报文特征的防护策略。

1. 登录 [边缘安全加速平台控制台](https://console.cloud.tencent.com/edgeone)，在左侧导航中，单击**安全防护** > **DDoS 防护**。
2. 在 DDoS 防护页面的左侧，选中防护业务对象，如“企业版 DDoS 防护”或“企业版 DDoS 防护 - 四层代理”实例。
![](https://qcloudimg.tencent-cloud.cn/raw/a53ab5c87e42aeb8f4c84d119f7c4a30.png)
3. 在特征过滤卡片中，单击**设置**，进入特征过滤页面。
![](https://qcloudimg.tencent-cloud.cn/raw/71417e41054e15dc88ed797bd6ace249.png)
4. 在特征过滤页面中，单击**新建**。
5. 在新建特征过滤对话框中，创建特征过滤规则，根据需求，选择不同防护动作并填写相关字段，单击**确定**。
![](https://qcloudimg.tencent-cloud.cn/raw/d6d1c0ebe6732904651b6ec615d4808e.png)
6. （可选）新建完成后，特征过滤列表将新增一条特征过滤规则，可以在右侧操作列，单击**配置**，可以修改特征过滤规则。
![](https://qcloudimg.tencent-cloud.cn/raw/68fd8c9f7e28a575f0ddf897280fd131.png)

## 协议封禁
EdgeOne 支持对访问站点的源流量按照协议类型一键封禁。您可配置 ICMP 协议封禁、TCP 协议封禁、UDP 协议封禁和其他协议封禁，配置后相关访问请求会被直接截断。由于 UDP 协议无连接的特点（不像 TCP 具有三次握手过程）具有天然的安全性缺陷。若您没有 UDP 业务，建议封禁 UDP 协议。

1. 登录 [边缘安全加速平台控制台](https://console.cloud.tencent.com/edgeone)，在左侧导航中，单击**安全防护** > **DDoS 防护**。
2. 在 DDoS 防护页面的左侧，选中防护业务对象，如“企业版 DDoS 防护”或“企业版 DDoS 防护 - 四层代理”实例。
![](https://qcloudimg.tencent-cloud.cn/raw/66e66d073a66a9332a03977a62e90694.png)
3. 在协议封禁卡片中，单击**设置**，进入协议封禁页面。
![](https://qcloudimg.tencent-cloud.cn/raw/edadfe2d6d2662e78e845d456e48b45d.png)
4. 在协议封禁页面，单击封禁所需协议开关![](https://qcloudimg.tencent-cloud.cn/raw/0e86da85c0afc62ad707cf59f1442d6b.png)。
![](https://qcloudimg.tencent-cloud.cn/raw/1d8457083b163985f50e8e8929ec7cef.png)

## 连接类攻击
EdgeOne 支持对连接型攻击进行防护，对连接行为异常的客户端自动封禁。在源 IP 最大异常连接数开启防护后，当边缘安全加速平台检测到同一个源 IP 短时间内频繁发起大量异常连接状态的报文时，会将该源 IP 纳入黑名单中进行封禁惩罚，封禁时间为15分钟，等封禁解除后可恢复访问。

1. 登录 [边缘安全加速平台控制台](https://console.cloud.tencent.com/edgeone)，在左侧导航中，单击**安全防护** > **DDoS 防护**。
2. 在 DDoS 防护页面的左侧，选中防护业务对象，如“企业版 DDoS 防护”或“企业版 DDoS 防护 - 四层代理”实例。
![](https://qcloudimg.tencent-cloud.cn/raw/4396712ec21168045dbeda6bdcc0448c.png)
3. 在连接类攻击防护卡片中，单击**设置**，进入连接类攻击防护页面。
![](https://qcloudimg.tencent-cloud.cn/raw/bbdd0e66bfd561d3614c35f4a7b56cd3.png)
4. 在连接类攻击防护页面中，单击**配置**，配置连接类攻击防护。
5. 在配置连接类攻击防护对话框中，开启异常连接防护，单击**确定**。
![](https://qcloudimg.tencent-cloud.cn/raw/74112df3401d38a43ea5943d27a206c5.png)
6. （可选）新建完成后，连接类攻击防护列表将增加一条连接类攻击防护规则，可以在右侧操作列，单击**配置**，修改异常连接规则。
![](https://qcloudimg.tencent-cloud.cn/raw/291584edc4d33b3ef7a9dbb4a0b4bf6d.png)
