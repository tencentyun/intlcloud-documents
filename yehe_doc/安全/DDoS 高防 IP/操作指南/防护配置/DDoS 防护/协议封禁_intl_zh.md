DDoS 高防支持对访问 DDoS 高防的源流量按照协议类型一键封禁。您可配置 ICMP 协议封禁、TCP 协议封禁、UDP 协议封禁和其他协议封禁，配置后相关访问请求会被直接截断。由于 UDP 协议的无连接性（不像 TCP 具有三次握手过程）具有天然的不安全性缺陷，若您没有 UDP 业务，建议封禁 UDP 协议。

## 前提条件
您需要已成功 [购买 DDoS 高防 IP](https://intl.cloud.tencent.com/document/product/297/37241)，并设置防护对象。

## 操作步骤
1. 登录 [DDoS 高防 IP 控制台](https://console.cloud.tencent.com/ddos/antiddos-advanced/config/port)，在左侧导航中，单击**防护配置** > **DDoS 防护**。
2. 在 DDoS 防护页面的左侧，选中高防 IP 的 ID，如“bgpip-xxxxxx”。
![](https://main.qcloudimg.com/raw/9c8bb19be4726a46a2261b35e048c8cb.png)
3. 在协议封禁卡片中，单击**设置**，进入协议封禁页面。
![](https://qcloudimg.tencent-cloud.cn/raw/265fb9c70725dff7d10744603f876972.png)
4. 在协议封禁页面，单击**新建**。
>?仅首次使用协议封禁时，会出现新建按钮。

5. 在新建协议封禁弹窗中，单击开启所需协议后，单击**确定**，创建协议封禁规则。
![](https://main.qcloudimg.com/raw/2b862288e7aa29b0470e4be5b2e94be4.png)
6. 新建完成后，协议封禁列表将新增一条协议封禁规则，单击![](https://qcloudimg.tencent-cloud.cn/raw/a37db6bf4c68ee412857e5260cb6724a.png)，修改协议封禁规则开关。
![](https://main.qcloudimg.com/raw/6eb66d6d739b3ea4eea0e23e0588c3a1.png)

