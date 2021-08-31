
DDoS 高防支持针对 IP、TCP 及 UDP 报文头或载荷中的特征自定义拦截策略。开启特征过滤后，您可以将源端口、目的端口、报文长度、IP 报文头或荷载的匹配条件进行组合，并对命中条件的请求设置放行、拦截、丢弃、拦截并拉黑15分钟、丢弃并拉黑15分钟、继续防护等策略动作，特征过滤可以精准制定针对业务报文特征或攻击报文特征的防护策略。

## 前提条件
您需要成功 [购买 DDoS 高防 IP](https://intl.cloud.tencent.com/document/product/297/37241) ，并设置防护对象。

## 操作步骤
1. 登录 [DDoS 高防 IP（新版）管理控制台](https://console.cloud.tencent.com/ddos/antiddos-advanced/package) ，在左侧导航中，单击【防护配置】。
2. 在左边的列表选中高防 IP 的 ID 或端口，如"212.64.xx.xx bgpip-000002jt”或 “119.28.xx.xx bgpip-000002ju"> "tcp:8000"，并在右侧卡片中单击“特征过滤”卡片中的【设置】，进入特征过滤列表。。
![](https://main.qcloudimg.com/raw/56516d0de6b77e5df9aa5592465f5c4d.png)
4. 单击【新建】按钮，创建特征过滤规则，填写相关字段，单击【确定】。
![](https://main.qcloudimg.com/raw/775ad163e64f17450dae4ae697011e54.png)
5. 新建完成后特征过滤列表，将新增一条特征过滤规则，可以在右侧操作列，单击【配置】，可以修改特征过滤规则。
![](https://main.qcloudimg.com/raw/11435bbcd6ea6c2b6a762d2a0bd863f3.png)

