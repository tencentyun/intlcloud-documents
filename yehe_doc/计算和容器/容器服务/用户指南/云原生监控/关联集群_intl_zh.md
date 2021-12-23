

## 操作场景

本文档介绍如何在云原生监控服务中关联集群与监控实例，关联成功后即可编辑数据采集规则等配置。当前服务仅支持与实例所属同一 VPC 下的容器服务 TKE 独立集群、托管集群和弹性集群与监控实例进行关联。

## 前提条件
- 已登录 [容器服务控制台](https://console.cloud.tencent.com/tke2)，并创建独立集群。
- 已在集群所在 VPC 中 [创建监控实例](https://intl.cloud.tencent.com/document/product/457/38824)。

## 操作步骤

### 关联集群
>! 关联集群成功后将在集群中安装监控数据采集插件，该插件在解除关联的同时会被删除。
>
1. 登录 [容器服务控制台](https://console.cloud.tencent.com/tke2)，选择左侧导航栏中的**云原生监控**。
2. 在监控实例列表页，选择需要关联集群操作的实例名称，进入该实例详情页。
3. 在“关联集群”页面，单击**关联集群**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/81e9d2c0fc87d301871b1a9065fb9cb6.png)
4. 在弹出的“关联集群”窗口，勾选当前 VPC 下需要关联的集群。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/26fafe0e7e21e259614036623ee2338a.png)
5. 单击**确定**即可将所选集群和当前监控实例关联。





### 解除关联

1. 登录 [容器服务控制台](https://console.cloud.tencent.com/tke2)，选择左侧导航栏中的**云原生监控**。
2. 在监控实例列表页，选择解除关联的实例名称，进入该实例详情页。
3. 在“关联集群”页面，单击实例右侧的**解除关联**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/4b53316a8d1c885f7a21e1afeb40dc7d.png)
4. 在弹出的“解除关联集群”窗口，单击**确定**即可解除关联。



