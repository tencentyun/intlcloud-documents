DDoS 边界防护支持通过配置 IP 黑名单和白名单实现对访问 DDoS 边界的源 IP 封禁或者放行，从而限制访问您业务资源的用户。配置 IP 黑白名单后，当流量超过清洗阈值时，若是白名单中的 IP 进行访问，将被直接放行，不需要经过任何的防护策略；若是黑名单中的 IP 进行访问，将会被直接阻断。

## 前提条件
您需要成功[ 购买 DDoS 边界防护](https://intl.cloud.tencent.com/document/product/297/42172)，并设置防护对象。
>?
>- 当发生 DDoS 攻击时，IP 黑白名单的过滤才会生效。
>   - 白名单中的 IP，访问时将被直接放行，不经过任何防护策略过滤。
>   -	黑名单中的 IP，访问时将会被直接阻断。
>- 目前 DDoS 边界防护产品处于灰度优化中，如有需要，请 [联系我们](https://intl.cloud.tencent.com/contact-us) 申请。

## 操作步骤
1. 登录 [DDoS 边界防护管理控制台](https://console.cloud.tencent.com/ddos/antiddos-edge/policy/ddos) ，在左侧导航中，单击【防护策略】，并选择【DDoS防护】。
2. 在左边的列表选中实例的 ID，如“edge-xxxxxxx”。
![](https://main.qcloudimg.com/raw/dcb8de6c5b81f6f522b25962f4ad3c11.png)
3. 在右侧卡片中单击“IP 黑白名单”卡片中的【设置】，进入IP 黑白名单页面。
![](https://main.qcloudimg.com/raw/ef1dedadf78a150fea126532b79f7f68.png)
4. 在 IP 黑白名单页面中，单击【新建】。
5. 在新建 IP 黑白名单弹窗中，创建 IP 黑白名单规则，选择黑白名单类型，单击【确定】。
![](https://main.qcloudimg.com/raw/1c3a46e9eea39733555bec2741bedc10.png)
6. 新建完成后，IP 黑白名单列表将新增一条 IP 黑白名单规则，可以在右侧操作列，单击【删除】，删除 IP 黑白名单规则。
![](https://main.qcloudimg.com/raw/ffe79141e64da02c47ad887b3ca23ef2.png)
