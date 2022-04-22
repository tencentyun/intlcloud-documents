
您可以通过 DDoS 防护管理控制台查看所购买的 DDoS 高防包的基础信息（如实例保底防护峰值、运行状态）及实例的弹性防护配置。

## 操作步骤

示例：查看广州地区独享包实例“bgp-0000008o”的实例信息。
1. 登录 [DDoS 高防包（新版）管理控制台](https://console.cloud.tencent.com/ddos/antiddos-native/package)，在左侧导航栏中，单击【高防包】，找到实例 ID 为“bgp-0000008o”的高防包，单击 ID“bgp-0000008o”查看实例详细信息。如果实例数量较多可以使用右上角的搜索框过滤。
![](https://qcloudimg.tencent-cloud.cn/raw/7aa188a4c52299aa7b4344d494206414.png)
2. 在弹出的页面中查看如下信息：
![](https://main.qcloudimg.com/raw/2d7fc182f997e1ec26459b59e93a6546.png)

**参数说明：**
- **高防包名称**
该 DDoS 高防包实例的名称，用于辨识与管理 DDoS 高防包实例。长度为1 - 20个字符，不限制字符类型。资源名称由用户根据实际业务需求自定义设置。
- **所在地区**
[购买 DDoS 高防包](https://intl.cloud.tencent.com/document/product/1029/36115) 时选择的【地域】。
- **绑定 IP**
该 DDoS 高防包实例所防护业务的实际 IP。
- **保底防护峰值**
该 DDoS 高防包实例的保底防护带宽能力，即 [购买](https://intl.cloud.tencent.com/document/product/1029/36115) 时选择的【保底防护峰值】。若未开启弹性防护，则保底防护峰值为高防服务实例的最高防护峰值。
- **当前状态**
DDoS 高防包实例当前的使用状态。状态包括运行中，清洗中以及封堵中等。
- **标签**
表示该 DDoS 高防包实例所属的标签名称，可以编辑、删除。


