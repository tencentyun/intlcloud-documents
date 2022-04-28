DDoS 高防支持针对 IP，TCP，UDP 报文头或载荷中的特征自定义拦截策略。开启特征过滤后，您可以将源端口、目的端口、报文长度、IP 报文头或荷载的匹配条件进行组合，并对命中条件的请求设置放行、拦截、丢弃、拦截并拉黑15分钟、丢弃并拉黑15分钟、继续防护等策略动作，特征过滤可以精准制定针对业务报文特征或攻击报文特征的防护策略。

## 前提条件

您需要成功 [购买 DDoS 高防包](https://intl.cloud.tencent.com/document/product/1029/36115) ，并设置防护对象。

## 操作步骤
1. 登录 [DDoS 高防包控制台](https://console.cloud.tencent.com/ddos/antiddos-native/package) ，在左侧导航中，单击**防护配置** > **DDoS 防护**。
2. 在 DDoS 防护页面的左侧列表中，选中高防包 ID，如"bgp-00xxxxxx"。
![](https://main.qcloudimg.com/raw/9cf812dc64f1dcd113fc2f35534544b5.png)
3. 在特征过滤卡片中，单击**设置**，进入特征过滤页面。
![](https://qcloudimg.tencent-cloud.cn/raw/8560684be1e643ce0eb00a3dad1e0f50.png)
4. 在特征过滤页面，单击**新建**，弹出新建特征过滤弹窗。
5. 在新建特征过滤弹窗中，创建特征过滤规则，根据需求，选择不同防护动作并填写相关字段，单击**保存**。
![](https://main.qcloudimg.com/raw/8cc71c584f2514fd432c9579a716c96b.png)
6. 新建完成后，特征过滤列表将新增一条特征过滤规则，可以在右侧操作列，单击**配置**，可以修改特征过滤规则。
![](https://main.qcloudimg.com/raw/dbf8f257ae3cdeb0d30a96a2e7ef4d1d.png)
