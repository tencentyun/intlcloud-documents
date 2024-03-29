## 操作场景
本文档指导您如何创建腾讯云边缘计算机器（Edge Computing Machine，ECM）实例。

## 前提条件
在创建边缘计算机器实例前，您需要完成以下工作：
- [注册腾讯云账号](https://intl.cloud.tencent.com/document/product/378/17985)，并完成 [实名认证](https://intl.cloud.tencent.com/document/product/378/3629)。
- 已 [创建边缘模块](https://intl.cloud.tencent.com/document/product/1119/43421)。
- 如需使用 Windows 镜像，则请通过 [提交工单](https://console.intl.cloud.tencent.com/workorder) 申请或联系您的专属商务经理。

## 操作步骤

1. 登录 [边缘计算机器控制台](https://console.cloud.tencent.com/ecm/overview)，在左侧导航栏中选择**实例列表**。
2. 在实例列表页面，单击**新增实例**，进入创建实例进行部署页面。
3. 根据页面提示，配置以下信息：
![](https://qcloudimg.tencent-cloud.cn/raw/46a23b1b3ca42a49e4a0415bb46d410e.png)
 - **选择所属模块**：请根据实际需求进行选择。
 - **默认镜像**：腾讯云提供公共镜像和自定义镜像。默认为与所属模块相同的镜像，请根据实际需求进行选择。
 - **默认网络带宽上限**：对带宽上限进行限制，若超出此上限，则默认丢包。默认为25Mbps，上限为1024Mbps。
 - **安全组**：安全组是一种虚拟防火墙，用于实例的网络访问控制。默认已选安全组为所属模块的安全组，用户可自行更改安全组设置。
 - **高级设置**：可修改默认 IP 直通和默认标签的设置，请根据实际需求进行选择：
    - **IP直通**：IP 直通功能适用于边缘云服务器内需要查看公网 IP 的场景。例如，将内网流量和外网流量分别转发到不同的 IP 地址。
    <dx-alert infotype="notice" title="">
    创建 Linux 操作系统的边缘实例时，系统默认按 IP 直通方式创建（您也可以在高级设置中，修改为非直通方式创建），创建后不支持修改 IP 直通方式。若创建 Windows 操作系统的边缘实例，系统会按非直通方式创建（Windows 操作系统暂时不支持 IP 直通方式）。
    </dx-alert>
    - **标签**：通过设置默认标签，您可以对边缘模块进行分类管理。边缘模块已设置的默认标签会在创建新实例时作为新实例的标签建议键值，您也可以在创建实例时修改为您需要的标签键值。
    <dx-alert infotype="notice" title="">
    该设置项仅修改边缘模块的标签键值，不会自动同步修改已创建成功的实例标签键值。
    </dx-alert>
 - **实例名称**：表示需要创建的实例名称，用户自定义。
 - **设置密码和确认密码**：自定义设置登录实例的密码。
7. 单击**下一步**。
8. 在创建实例进行部署的“区域部署”页面，根据提示，配置以下信息：
![](https://qcloudimg.tencent-cloud.cn/raw/3c834b87a5994c90107ff15aaa02c95a.png)
 - **节点省份**：建议选择与您的客户最近的省份，可降低访问时延、提高访问速度。
 - **节点地区**：请根据实际需求进行选择。
 - **网络类型**：请根据实际需求选择公网运营商。
 - **实例数量**：表示需购买云服务器的数量。
 - **免费开通主机安全加固**：默认勾选，帮助用户构建服务器安全防护体系，防止数据泄露。
 - **免费开通云监控**：默认勾选，免费开通云产品监控，安装组件获取主机监控指标并以监控图标形式展示，且支持设置自定义告警阈值等。
9. 单击**确定购买**。
实例创建成功后，相关信息将通过您订阅的通知消息通道发送给您。您也可以在 [实例列表](https://console.cloud.tencent.com/ecm/instance) 中查看新创建的资源。

