DDoS 高防支持对已接入防护的网站业务，设置基于地理区域的访问请求封禁策略。开启针对域名的区域封禁功能后，您可以一键阻断指定地区来源 IP 对网站业务的所有访问请求。支持多地区、国家进行流量封禁。
## 前提条件
您需要成功 [购买 DDoS 高防包](https://intl.cloud.tencent.com/document/product/1029/36115)  ，并设置防护对象。

## 操作步骤
1. 登录 [DDoS 高防包（新版）管理控制台](https://console.cloud.tencent.com/ddos/antiddos-native/config/port)，在左侧导航中，单击 **DDoS 高防包** > **防护配置**。
2. 在左边的列表选中高防包的 ID，如“bgp-00xxxxxx”，单击**域名防护**。
![](https://qcloudimg.tencent-cloud.cn/raw/fd23f28fb0ec73efac2dd85ff52b3022.png)
3. 在右侧卡片中单击**区域封禁**卡片中的**设置**，进入区域封禁页面。
![](https://qcloudimg.tencent-cloud.cn/raw/db8937ee4a40c01cf9a0b289c2900890.png)
4. 在区域封禁页面中，单击**新建**，弹出新建区域封禁弹窗。
5. 在新建区域封禁弹窗中，选择 IP、域名、所封禁的区域，单击**确定**，创建区域封禁规则。
![](https://qcloudimg.tencent-cloud.cn/raw/acb49706477347c879d611c70506852c.png)
6. 新建完成后，在区域封禁列表，将新增一条区域封禁规则，可以在右侧操作列，单击**配置**，修改区域封禁规则。
![](https://qcloudimg.tencent-cloud.cn/raw/ba58c26434079c973e3df69e61fe773b.png)
