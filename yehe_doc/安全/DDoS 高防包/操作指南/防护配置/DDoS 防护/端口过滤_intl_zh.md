DDoS 高防支持针对访问 DDoS 高防的源流量，基于端口进行一键封禁或者放行。开启端口过滤后，可以根据需求自定义协议类型、源端口范围、目的端口范围的组合，并对匹配中的规则进行设置丢弃、放行、继续的防护策略动作。端口过滤可以精准制定针对访问的源流量，进行端口设置的防护策略。


## 前提条件
您需要成功 [购买 DDoS 高防包](https://intl.cloud.tencent.com/document/product/1029/36115)  ，并设置防护对象。

## 操作步骤
1. 登录  [DDoS 高防包控制台](https://console.cloud.tencent.com/ddos/antiddos-native/package) ，在左侧导航中，单击**防护配置** > **DDoS 防护**。
2. 在 DDoS 防护页面的左侧列表中，选中高防包 ID，如"bgp-00xxxxxx"。
![](https://main.qcloudimg.com/raw/dcb8de6c5b81f6f522b25962f4ad3c11.png)
3. 在端口过滤卡片中，单击**设置**，进入端口过滤页面。
![](https://qcloudimg.tencent-cloud.cn/raw/f49c805c5fbf89de4e5cd8ab8bf941ab.png)
4. 在端口过滤页面中，单击**新建**，创建端口过滤规则，根据需求，选择不同防护动作并填写相关字段，单击**保存**。
>?支持选择多个实例资源批量创建，未绑定防护资源的实例，不允许创建规则。

![](https://main.qcloudimg.com/raw/b05f2100f14ecd0269673d26bfc84ce9.png)
6. 新建完成后，在端口过滤列表，将新增一条端口过滤规则，可以在右侧操作列，单击**配置**，可以修改端口过滤规则。
![](https://main.qcloudimg.com/raw/90e5bfe35208179bd42ba04313960eb4.png)
