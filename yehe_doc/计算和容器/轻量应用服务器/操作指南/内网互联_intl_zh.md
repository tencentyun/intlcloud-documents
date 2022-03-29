## 操作场景
轻量应用服务器使用腾讯云自动分配的私有网络 VPC 进行网络隔离，默认情况下内网不与云服务器 CVM、云数据库等其他处于私有网络 VPC 中的腾讯云资源内网互通，需通过关联云联网实现。该功能主要适用于以下业务场景：
 - 轻量应用服务器访问云服务器 CVM
 - 轻量应用服务器访问云数据库

<dx-alert infotype="explain" title="">
- 同账号下同一地域内的不同轻量应用服务器默认内网互通。更多轻量应用服务器内网连通能力介绍，请参见 [内网连通性说明](https://intl.cloud.tencent.com/document/product/1103/41266)。
- 同地域下轻量应用服务器与对象存储 COS 默认内网互通，无需通过关联云联网实现。
</dx-alert>

本文介绍如何通过轻量应用服务器控制台进行实例关联、解关联云联网。如需了解云联网的更多信息，请查阅 [云联网产品文档](https://intl.cloud.tencent.com/document/product/1003/30049)。

## 注意事项
- 轻量应用服务器内网互联功能本身免费，您仅需关注云联网产品计费信息，详情请参见 [云联网计费总览](https://intl.cloud.tencent.com/document/product/1003/30053)。其中同地域5Gbps及以下带宽免费，如需实现跨地域内网互联，需在云联网中购买 [非跨境带宽](https://intl.cloud.tencent.com/document/product/1003/38894)。
- 轻量应用服务器不支持通过关联云联网实现跨境内网互联，即使该云联网已购买跨境带宽。
- 同一账号下：
  - 同地域内的所有轻量应用服务器处于同一个 VPC 中，一个 VPC 只能同时关联一个云联网。
  - 不同地域内的轻量应用服务器处于不同的 VPC 中，不同 VPC 需要分别执行关联云联网操作。
- 如果某地域中不存在轻量应用服务器实例，则用户无法在该地域执行关联云联网操作。

## 操作步骤

### 申请云联网关联[](id:association)
1. 登录轻量应用服务器控制台，选择左侧导航栏中的 <b>[内网互联](https://console.cloud.tencent.com/lighthouse/ccn/index)</b>。
2. 选择需关联云联网地域中的**关联云联网**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/fdf2d7e60a095e95303e226c693cbfa2.png)
3. 在弹出的“关联云联网”窗口中，选择云联网并单击**确定**即已提交关联申请。
<dx-alert infotype="notice" title="">
- 仅支持关联同账号下的云联网。
- 提交关联申请后，请您在7天内登录 [云联网控制台](https://console.cloud.tencent.com/vpc/ccn) 同意申请。否则7天后申请过期，需进行重新关联申请。
</dx-alert>
4. 登录 [云联网控制台](https://console.cloud.tencent.com/vpc/ccn)，选择云联网 ID 进入云联网详情页。
5. 在云联网详情页中，选择关联申请所在行右侧的**同意**。
轻量应用服务器的 VPC 实例默认会添加备注为 “Lighthouse VPC”，请注意选择。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/363bd10b3f88e60e86da7e3e58c2e6f8.png)
6. 在弹出窗口中单击**确定**即可完成关联操作，内网互联页面显示该地域状态为“已连接”。
您可按需将云服务器 CVM、云数据库等云资源关联至云联网，实现内网互联。详情请参见 [关联网络实例](https://intl.cloud.tencent.com/document/product/1003/30064)。
<dx-alert infotype="notice" title="">
完成关联后，需前往 [云联网控制台](https://console.cloud.tencent.com/vpc/ccn) 查看路由信息，确认新增的路由条目是否有效。若存在 CIDR 冲突的情况，则该路由条目可能无效。详情请参见 [查看路由信息](https://intl.cloud.tencent.com/document/product/1003/30066)。
</dx-alert>



### 云联网解关联[](id:disassociate)
您可根据实际需求，在云联网关联申请状态为申请中、已过期及已连接时进行解关联。当状态为“已连接”时，解关联将中断当前地域下所有实例与云联网中其他 VPC 的连接，请确认对您的业务无影响后，再执行本操作。步骤如下：
1. 登录轻量应用服务器控制台，选择左侧导航栏中的 <b>[内网互联](https://console.cloud.tencent.com/lighthouse/ccn/index)</b>。 
2. 选择需解关联云联网地域中的**解关联**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/565a447f7c1b5b9a147cb7706c1c634e.png)
3. 在弹出的“解关联云联网”窗口中，单击**确定**即可。

## 操作示例
<dx-accordion>
::: 示例1：轻量应用服务器与云服务器内网互通
#### 示例场景
广州地域下的轻量应用服务器及云服务器，默认内网不互通。需关联云联网，实现内网互通。

#### 示例步骤
 1. 登录轻量应用服务器，执行以下命令：
```
ping 云服务器内网 IP
```
返回如下图所示信息，说明无法 ping 通。
![](https://main.qcloudimg.com/raw/49e76f62b5f7ae7e6fb504bf92b842a7.png)
 2. 参考 [申请云联网关联](#association) 步骤，关联云联网。
 同时，也需将云服务器的 VPC 关联云联网，详情请参见 [关联网络实例](https://intl.cloud.tencent.com/document/product/1003/30064)。 
 3. 登录轻量应用服务器，执行以下命令：
```
ping 云服务器内网 IP
```
返回如下图所示信息，说明已 ping 通，内网已互通。
![](https://main.qcloudimg.com/raw/b487ec4b7ae4be87059bd13db2f5f9b4.png)
:::
::: 示例2：轻量应用服务器与云数据库 MySQL 内网互通
#### 示例场景
广州地域下的轻量应用服务器及云数据库 MySQL，默认内网不互通。需关联云联网，实现内网互通。

#### 示例步骤
1. 登录轻量应用服务器，执行以下命令安装 `telnet`。
```shell
sudo yum install telnet -y
```
2. 执行以下命令，测试是否内网连通。
```
telnet 云数据库MySQL内网 IP 3306
``` 返回如下图所示信息，说明无法连通。
![](https://main.qcloudimg.com/raw/e4faffa0bf9bb3448296d3bcae1c6dec.png)
3. 参考 [申请云联网关联](#association) 步骤，关联云联网。
 同时，也需将云数据库 MySQL 的 VPC 关联云联网，详情请参见 [关联网络实例](https://intl.cloud.tencent.com/document/product/1003/30064)。 
4. 登录轻量应用服务器，执行以下命令。
```
telnet 云数据库MySQL内网 IP 3306
``` 返回如下图所示信息，说明内网已互通。
![](https://main.qcloudimg.com/raw/98f0b235240869f954b7dcfa23df202c.png)
:::
</dx-accordion>
