## 操作场景

云原生网关是腾讯云孵化的一款100%兼容开源 Kong 网关的 API 网关托管产品，目前正在免费公测中。

该任务指导您通过云原生网关控制台创建一个云原生网关实例。


## 操作步骤

1. 登录 [API 网关控制台](https://console.cloud.tencent.com/apigateway/index?rid=1) ，在左侧导航栏单击**云原生网关**。
2. 单击**新建**，进入云原生网关创建页。

| 参数         | 是否必填 | 说明                                                         |
| ------------ | -------- | ------------------------------------------------------------ |
| 地域         | 是       | 选择当前云原生网关所在地域。                                 |
| 可用区       | 是       | 选择当前云原生网关所在可用区。可用区属于地域，不可选择的可用区代表该可用区资源不足。 |
| 网关名称     | 是       | 输入当前云原生网关的名称。                                   |
| 网关类型     | 是       | 目前仅支持 Kong 网关。                                       |
| 网关版本     | 是       | 所选择的网关类型的开源版本号。                               |
| 集群节点规格 | 是       | 云原生网关集群由多个节点组成，此处选择每个节点的规格。       |
| 集群节点数量 | 是       | 云原生网关集群由多个节点组成，此处选择节点的数量。           |
| 所属网络     | 是       | 选择当前云原生网关所部署在的腾讯云 VPC 网络。                |
| 所属子网     | 是       | 选择当前云原生网关所部署在的腾讯云子网，子网属于 VPC 网络。  |
| 描述         | 否       | 输入当前云原生网关的描述信息。                               |

3. 单击**保存**，耐心等待实例创建完成。

## 注意事项

- 创建云原生网关要求账号必须拥有 ApiGateWay_QCSRole 角色，并且角色下必须有 QcloudAccessForApiGateWayRoleInCloudNativeAPIGateway 策略。如无相关角色和策略，请在创建过程中弹出的授权弹窗中完成授权。
- 云原生网关日志功能依赖于 [腾讯云日志服务](https://intl.cloud.tencent.com/document/product/614)（简称 CLS），请您确保已经开通 CLS 服务，否则在创建云原生网关前请前往 [CLS 控制台](https://console.cloud.tencent.com/cls/overview) 开通服务。
- 目前云原生网关正处于免费公测期间，完全免费。
