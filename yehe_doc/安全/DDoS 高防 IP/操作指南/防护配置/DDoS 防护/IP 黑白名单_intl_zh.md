
DDoS 高防支持通过配置 IP 黑名单和白名单实现对访问 DDoS 高防的源 IP 封禁或者放行，从而限制访问您业务资源的用户。配置 IP 黑白名单后，当流量超过清洗阈值时，若白名单中的 IP 进行访问，将被直接放行，不经过任何防护策略过滤。若黑名单中的 IP 进行访问，将会被直接阻断。

## 前提条件
您需要成功 [购买 DDoS 高防 IP](https://intl.cloud.tencent.com/document/product/297/37241)，并设置防护对象。
>? 创建 IP 黑白名单后常态化生效。
>- 白名单中的 IP，访问时将被直接放行，不经过任何防护策略过滤。
>- 黑名单中的 IP，访问时将会被直接阻断。

## 操作步骤
1. 登录 [DDoS 高防 IP 控制台](https://console.cloud.tencent.com/ddos/antiddos-advanced/config/port)，在左侧导航中，单击**防护配置** > **DDoS 防护**。
2. 在 DDoS 防护页面的左侧，选中高防 IP 的 ID，如“bgpip-xxxxxx”。
![](https://main.qcloudimg.com/raw/9926499f6012c6a88194642aae7474e0.png)
3. 在 IP 黑白名单卡片中，单击**设置**，进入 IP 黑白名单页面。
![](https://qcloudimg.tencent-cloud.cn/raw/6865bd3d710068fc607fbe4799aef9ad.png)
4. 在 IP 黑白名单页面中，单击**新建**，创建 IP 黑白名单规则，选择黑白名单类型，单击**保存**。
![](https://main.qcloudimg.com/raw/1c3a46e9eea39733555bec2741bedc10.png)
5. （可选）新建完成后，IP 黑白名单列表将新增一条 IP 黑白名单规则，可以在右侧操作列，单击**删除**，删除 IP 黑白名单规则。
![](https://main.qcloudimg.com/raw/ffe79141e64da02c47ad887b3ca23ef2.png)