DDoS 高防 IP（境外企业版）是针对业务部署在腾讯云内境外地区的用户，以提升 DDoS 境外防护能力的付费产品。
- DDoS 高防 IP（境外企业版）可以独立购买和持有的公网 IP 地址资源。
- DDoS 高防 IP（境外企业版）绑定云资源后，云资源可以通过 DDoS 高防 IP（境外企业版）与公网通信。

本文以 DDoS 高防 IP（境外企业版）关联云资源为例介绍 DDoS 高防 IP（境外企业版）的使用生命周期。

## 背景信息
DDoS 高防 IP（境外企业版）的使用生命周期包括购买 DDoS 高防 IP（境外企业版）、DDoS 高防 IP（境外企业版）实例配置防护规则、DDoS 高防 IP（境外企业版）配置业务规则 ，DDoS 高防 IP（境外企业版）销毁。
![](https://main.qcloudimg.com/raw/389a53aa7c9d5fd4b2931415ce3e44c3.png)

1. [购买 DDoS 高防 IP（境外企业版）](https://buy.cloud.tencent.com/antiddos#/advanced-intl)：根据实际使用需求，购买 DDoS 高防 IP（境外企业版）资源。
2. DDoS 高防 IP（境外企业版）实例 [配置防护规则](https://intl.cloud.tencent.com/document/product/297/34092)：配置贴合业务的防护策略。
3. DDoS 高防 IP（境外企业版）配置业务规则：将 DDoS 高防 IP（境外企业版） 的实例关联到需防护的云上资源。
4. DDoS 高防 IP（境外企业版）销毁：将 DDoS 高防 IP（境外企业版）与云资源取消关联后，您可以将该 DDoS 高防 IP（境外企业版）与其他云资源关联。取消关联操作可能会导致对应云资源的网络不通，且未绑定云资源的 DDoS 高防 IP（境外企业版）会产生 IP 资源费。

## 操作步骤
### 购买 DDoS高防IP（境外企业版）
1. 登录 [DDoS 高防 IP（境外企业版）](https://console.cloud.tencent.com/ddos/ddos-basic) 控制台。
2. 参考上文 [购买指引](https://intl.cloud.tencent.com/zh/document/product/297/37241) 进行套餐购买。
3. 单击控制台【DDoS 高防 IP】>【实例列表】，即可查看已购买的 DDoS 高防 IP（境外企业版），此时处于未绑定状态。
>?建议您及时为处于未绑定状态的 DDoS 高防 IP（境外企业版）绑定云资源，节省 IP 资源费。IP 资源费按小时计费，精确到秒级，不足一小时，按闲置时间占比收取费用，因此请及时绑定云资源。详细标准可参考 [计费概述](https://intl.cloud.tencent.com/zh/document/product/297/37240)。

 ![](https://main.qcloudimg.com/raw/d774d3d95a58cbd4504cf1bf470df356.png) 

### 配置防护规则
登录[ DDoS 高防 IP（境外企业版）](https://console.cloud.tencent.com/ddos/ddos-basic)控制台，单击【DDoS 高防 IP】>【实例列表】中，选择对应 DDoS 高防 IP（境外企业版）实例，单击【防护配置】，配置方式可参考 [配置防护规则](https://intl.cloud.tencent.com/document/product/297/34092)。
![](https://main.qcloudimg.com/raw/75512d5a31b23fff0a5250d319aec8f8.png) 
### 关联云资源
1. 登录 [DDoS 高防 IP（境外企业版）](https://console.cloud.tencent.com/ddos/ddos-basic) 控制台，单击【DDoS 高防 IP】>【业务接入】进入业务接入页面。
2. 在业务界面中选择【IP 接入】，单击【添加规则】，弹出绑定资源页面。
3. 在绑定资源页面，“关联 Anycast 高防 IP”处选择 DDoS 高防 IP（境外企业版）实例，单击【确定】，即可完成与云资源的绑定。
![](https://main.qcloudimg.com/raw/0df0b4c8f905ccde1d1a6e6488766473.png)

### 解除云资源绑定
1. 登录 [DDoS 高防 IP（境外企业版）](https://console.cloud.tencent.com/ddos/ddos-basic) 控制台，单击【DDoS 高防 IP】>【业务接入】进入业务接入页面。
2. 在业务界面中选择【IP 接入】，单击右上角处【删除】，即可取消关联。
![](https://main.qcloudimg.com/raw/2bb05580869f9f70b6f6454e2e530bab.png)
