DDoS 边界防护支持针对访问 DDoS 高防的源流量，基于端口进行一键封禁或者放行。开启端口过滤后，可以根据需求自定义协议类型、源端口范围、目的端口范围的组合，并对匹配中的规则进行设置丢弃、放行、继续的防护策略动作。端口过滤可以精准制定针对访问的源流量进行端口设置的防护策略。

## 前提条件
您需要成功[ 购买 DDoS 边界防护](https://intl.cloud.tencent.com/document/product/297/42172)，并设置防护对象。


## 操作步骤
1. 登录 [DDoS 边界防护管理控制台](https://console.cloud.tencent.com/ddos/antiddos-edge/policy/ddos) ，在左侧导航中，单击【防护策略】，并选择【DDoS防护】。
2. 在左边的列表选中高防实例的 ID，如“edge-xxxxxxx”。
![](https://main.qcloudimg.com/raw/dcb8de6c5b81f6f522b25962f4ad3c11.png)
3. 在右侧卡片中单击“端口过滤”卡片中的【设置】，进入端口过滤页面。
![](https://main.qcloudimg.com/raw/e7aea83ac323c878cc2376af7fe4d218.png)
4. 在端口过滤页面中，单击【新建】。
5. 在新建端口过滤弹窗中，创建端口过滤规则，根据需求，选择不同防护动作并填写相关字段，单击【确定】。
![](https://main.qcloudimg.com/raw/b05f2100f14ecd0269673d26bfc84ce9.png)
6. 新建完成后端口过滤列表，将新增一条端口过滤规则，可以在右侧操作列，单击配置，可以修改端口过滤规则。
![](https://main.qcloudimg.com/raw/90e5bfe35208179bd42ba04313960eb4.png)
