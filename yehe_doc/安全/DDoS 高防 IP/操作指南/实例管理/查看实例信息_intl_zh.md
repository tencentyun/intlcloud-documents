
您可以通过 DDoS 防护管理控制台，查看所购买的 DDoS 高防 IP 的基础信息（如实例保底防护峰值及运行状态）及实例的弹性防护配置。

## 操作步骤

示例：查看高防 IP 实例“bgpip-000002jf”的实例信息。
1. 登录 [DDoS 高防 IP（新版）管理控制台](https://console.cloud.tencent.com/ddos/antiddos-advanced/package)，在左侧导航栏中，单击**实例列表**，选择所需实例 ，单击 “ID”查看实例详细信息。如果实例数量较多可以使用右上角的搜索框过滤。
![](https://qcloudimg.tencent-cloud.cn/raw/c174ccf351d369aaa1e0470c97278bfa.png)
3. 在弹出的页面中查看如下信息：
![](https://main.qcloudimg.com/raw/77f50dfce86cccc4dc24dd4d3b5cd331.png)
  - **高防 IP 名称**：该 DDoS 高防 IP 实例的名称，用于辨识与管理 DDoS 高防 IP 实例。长度为1 - 20个字符，不限制字符类型。资源名称由用户根据实际业务需求自定义设置。
  - **解析目标 IP**：该 DDoS 高防 IP 实例具有高防属性的 IP。此 IP 地址将不定期更换。
>!建议将您的 DNS 解析地址修改至 CNAME，避免 DNS 解析失败。

  - **所在地区**：[购买 DDoS 高防 IP ](https://intl.cloud.tencent.com/document/product/297/15483) 时选择的**地域**。
  - **CNAME**：该 DDoS 高防 IP 实例的 CNAME。由该 CNAME 解析至拥有高防属性的 IP 上，通过清洗中心后并转发回源站，实现防护。
>! 建议将您的 DNS 解析地址修改至 CNAME，避免 DNS 解析失败。

  - **保底防护峰值**：该 DDoS 高防 IP 实例的保底防护带宽能力，即 [购买](https://intl.cloud.tencent.com/document/product/297/15483) 时选择的**保底防护峰值**。若未开启弹性防护，则保底防护峰值为高防服务实例的最高防护峰值。
  - **当前状态**：DDoS 高防 IP 实例当前的使用状态。状态包括运行中，清洗中以及封堵中等。
  - **到期时间**：根据 [购买](https://intl.cloud.tencent.com/document/product/297/37241) 时选择的**购买时长**以及支付购买订单的具体时间计算所得，精确到秒级。腾讯云会在此时间前的前7天内，通过站内信、短信及邮件的方式向腾讯云账号的创建者以及所有协作者推送服务即将到期并提醒及时续费的信息。
	 - **标签**：表示该 DDoS 高防 IP 实例所属的标签名称，可以编辑、删除。
	 - **回源 IP 段**：清洗集群转发至源站所用 IP。


