
DDoS 高防支持通过配置 IP 黑名单和白名单实现对访问 DDoS 高防的源 IP 封禁或者放行，从而限制访问您业务资源的用户。配置 IP 黑白名单后，当流量超过清洗阈值时，若白名单中的 IP 进行访问，将被直接放行，不经过任何防护策略过滤。若黑名单中的 IP 进行访问，将会被直接阻断。

## 前提条件
您需要成功 [购买 DDoS 高防 IP](https://intl.cloud.tencent.com/document/product/297/37241) ，并设置防护对象。
>?当发生DDoS攻击时，IP 黑白名单的过滤才会生效。
>- 白名单中的 IP，访问时将被直接放行，不经过任何防护策略过滤。
>- 黑名单中的 IP，访问时将会被直接阻断。
## 操作步骤
1. 登录 [DDoS 高防 IP（新版）管理控制台](https://console.cloud.tencent.com/ddos/antiddos-advanced/package) ，在左侧导航中，单击【防护配置】。
2. 在左边的列表选中高防 IP 的 ID 或端口，如"212.64.xx.xx bgpip-000002jt”或 “119.28.xx.xx bgpip-000002ju"> "tcp:8000"，并在右侧卡片中单击“IP 黑白名单”卡片中的【设置】，进入 IP 黑白名单列表。
![](https://main.qcloudimg.com/raw/188d333af2cbd161c06c096c7d767531.png)
4. 在 IP 黑白名单列表中，单击【新建】。
5. 在“新建 IP 黑白名单”弹窗中，创建 IP 黑白名单规则，选择黑白名单类型，单击【确定】。
![](https://main.qcloudimg.com/raw/1c3a46e9eea39733555bec2741bedc10.png)
6. 新建完成后，IP 黑白名单列表将新增一条 IP 黑白名单规则，可以在右侧操作列，单击【删除】，删除 IP 黑白名单规则。
![](https://main.qcloudimg.com/raw/3453f2025be0bccc6429a8358986a8ed.png)
