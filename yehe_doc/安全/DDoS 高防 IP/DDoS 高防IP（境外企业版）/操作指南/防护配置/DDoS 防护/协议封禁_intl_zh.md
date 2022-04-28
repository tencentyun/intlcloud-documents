

DDoS 高防 IP （境外企业版）支持对访问 DDoS 高防 IP 的源流量按照协议类型一键封禁。您可配置 ICMP 协议封禁、TCP 协议封禁、UDP 协议封禁和其他协议封禁，配置后相关访问请求会被直接截断。由于 UDP 协议的无连接性（不像 TCP 具有三次握手过程）具有天然的不安全性缺陷，若您没有 UDP 业务，建议封禁 UDP 协议。

## 前提条件
您需要成功 [购买 DDoS 高防 IP （境外企业版）](https://intl.cloud.tencent.com/document/product/297/41154) ，并设置防护对象。

## 操作步骤
1.	登录 [DDoS 高防 IP（境外企业版）](https://console.cloud.tencent.com/ddos/ddos-basic) 控制台 ，在左侧导航中，单击 **DDOS 高防 IP**>**防护配置** > **DDoS 防护**。
2.	在左边的列表选中高防 IP 的 ID，如“xxx.xx.xx.xx bgpip-000003n2”。
![](https://main.qcloudimg.com/raw/9c8bb19be4726a46a2261b35e048c8cb.png)
3. 在协议封禁卡片中，单击**设置**。
4. 在协议封禁页面，单击**新建**，设置相关条件，单击**确定**，创建协议封禁规则。
![](https://main.qcloudimg.com/raw/2b862288e7aa29b0470e4be5b2e94be4.png)
6. 新建完成后，协议封禁列表将新增一条协议封禁规则，单击“开关”，可修改协议封禁规则。
![](https://main.qcloudimg.com/raw/6eb66d6d739b3ea4eea0e23e0588c3a1.png)
