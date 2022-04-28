
DDoS 高防支持通过配置 IP 黑名单和白名单实现对访问 DDoS 高防的源IP封禁或者放行，从而限制访问您业务资源的用户。配置 IP 黑白名单后，当白名单中的 IP 访问时，将被直接放行，不经过任何防护策略过滤。当黑名单中的 IP 访问时，将会被直接阻断。

## 前提条件
您需要成功 [购买 DDoS 高防包](https://intl.cloud.tencent.com/document/product/1029/36115) ，并设置防护对象。
>?
>- 当发生 DDoS 攻击时，IP 黑白名单的过滤才会生效。
>  - 白名单中的 IP，访问时将被直接放行，不经过任何防护策略过滤。
>  - 黑名单中的 IP，访问时将会被直接阻断。


## 操作步骤
1. 登录 [DDoS 高防包控制台](https://console.cloud.tencent.com/ddos/antiddos-native/package) ，在左侧导航中，单击**防护配置** > **DDoS 防护**。
2. 在 DDoS 防护页面的左侧列表中，选中高防包 ID，如"bgp-00xxxxxx"。
![](https://main.qcloudimg.com/raw/ceb4f1ebedc2efb78e428f5ffe071473.png)
3. 在 IP 黑白名单卡片中，单击**设置**，进入 IP 黑白名单页面。
![](https://qcloudimg.tencent-cloud.cn/raw/9ba58f2a728b955813ecd9b27b675ec6.png)
4. 在 IP 黑白名单页面，单击**新建**，选择黑白名单类型，填写相关字段，单击**保存**。
![](https://main.qcloudimg.com/raw/e16a265499ee7762b497d1aac0370ab4.png)
6. 新建完成后 ，IP 黑白名单列表将新增一条IP黑白名单规则，可以在右侧操作栏中，单击**删除**，删除 IP 黑白名单规则。
![](https://main.qcloudimg.com/raw/a7f5b24ff9d6ebcdac1282297e85c432.png)
