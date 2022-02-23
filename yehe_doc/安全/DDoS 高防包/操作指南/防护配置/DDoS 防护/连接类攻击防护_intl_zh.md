
当连接类发起异常， DDoS 高防支持自动发起封禁惩罚策略。在源 IP 最大异常连接数开启防护后，如果 DDoS 高防检测到同一个源 IP，在短时间内频繁发起大量异常连接状态的报文时，会将该源 IP 纳入黑名单中进行封禁惩罚。其中封禁时间为15分钟，等封禁时间过后可恢复访问。
>? 链接类攻击防护支持以下字段：
>- 源新建连接限速：基于源地址端口新建连接频率限制。
>- 源并发连接限制：访问源某一刻 TCP 的活跃连接数达到限制。
>- 目的新建连接限速：目的 IP 地址端口新建连接频率限制。
>- 目的并发连接限制：目的 IP 地址某一刻 TCP 的活跃连接数达到限制。
>- 源 IP 最大异常连接数：访问源 IP 支持最大的异常连接数。

## 前提条件
您需要成功 [购买 DDoS 高防包](https://intl.cloud.tencent.com/document/product/1029/36115)  ，并设置防护对象。

## 操作步骤
1. 登录 [DDoS 高防包控制台](https://console.cloud.tencent.com/ddos/antiddos-native/package) ，在左侧导航中，单击**防护配置** > **DDoS 防护**。
2. 在 DDoS 防护页面的左侧列表中，选中高防包 ID，如"bgp-00xxxxxx"。
![](https://main.qcloudimg.com/raw/f3910ce6e7bd09a90bd2526c137a7e62.png)
3. 在连接类攻击防护卡片中，单击**设置**，进入连接类攻击防护页面。
![](https://qcloudimg.tencent-cloud.cn/raw/6d304ffdc2bf4457f7b53ab72584d44c.png)
4.	在连接类攻击防护页面中，单击**新建**，弹出配置连接类攻击防护弹窗。
5.	在配置连接类攻击防护弹窗中，开启连接耗尽防护和异常连接防护后，单击**确定**。
![](https://main.qcloudimg.com/raw/1cd6b0ba5863c2b90b458a5410a68ea2.png)
6.	新建完成后，连接类攻击防护列表将增加一条连接类攻击防护规则，可以在右侧操作列，单击**配置**，修改异常连接规则。
![](https://main.qcloudimg.com/raw/9dfcd1c64ffd984f65dfac5572077d7e.png)
