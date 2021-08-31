 私有网络（VPC） 是使用云服务的基础，例如购买 CVM 等实例时，需选择对应实例的所属 VPC。本文将介绍 VPC 的使用生命周期。

## 背景信息


1. [创建 VPC](#1)：创建 VPC 前，您需要提前做好 [网络规划](https://intl.cloud.tencent.com/document/product/215/31795)。VPC 和子网的 CIDR 创建后不可更改。
2. [查看 VPC](#2)：可查看 VPC 的基本信息、云联网的关联情况以及包含资源。
3. （可选）根据实际使用场景选择不同操作：
 - 主 CIDR 不够分配时：
    - [创建辅助 CIDR](#21)：主 CIDR 不够分配时，可以创建辅助 CIDR 以满足实际网络需求。
    - [删除辅助 CIDR](#32)：若不需要辅助 CIDR，可将其删除。
4. [删除 VPC](#3)：删除 VPC 后，该 VPC 下的子网和路由表将一并被删除。

<span id ="1"></span>
## 创建 VPC

VPC 中至少包含一个子网，只有在子网中才可以添加云服务资源。
1. 登录 [私有网络控制台](https://console.cloud.tencent.com/vpc)。
2. 在“私有网络”页面顶部，选择 VPC 所属地域，单击【+新建】。
3. 在“新建 VPC” 对话框中填写 VPC 信息和初始子网信息，然后单击【确定】。
>?VPC 和子网的 CIDR 创建后不可修改。
>
 - VPC  CIDR 支持使用如下网段中的任意一个，如果您有不同  VPC 间内网通信的需要，两端 CIDR 的配置请不要重叠：
 - `10.0.0.0` - `10.255.255.255`（掩码范围需在16 - 28之间）
 - `172.16.0.0` - `172.31.255.255`（掩码范围需在16 - 28之间）
 - `192.168.0.0` - `192.168.255.255` （掩码范围需在16 - 28之间）
 - 子网的 CIDR 必须在 VPC 的 CIDR 内或相同。
   例如，VPC 的网段是`192.168.0.0/16`，那么该 VPC 内的子网的网段可以是`192.168.0.0/16`、`192.168.0.0/17`等。 
   ![](https://main.qcloudimg.com/raw/ed9901dce2ec94302ae14a1fca7d06b8.png)

<span id ="2"></span>
## 查看 VPC
1. 登录 [私有网络控制台](https://console.cloud.tencent.com/vpc)。
2. 在“私有网络”页面顶部，选择 VPC 所属地域。
3. 在 VPC 列表中，单击需要查看的 VPC ID。
 详情页中展示了 VPC 的基本信息、云联网的关联情况以及包含资源。
![](https://main.qcloudimg.com/raw/779074772193dfa8394256a674f4c36f.png)

<span id ="21"></span>
## 创建辅助 CIDR
>?
>- 目前辅助 CIDR 处于内测中，如有需要，请提交 [工单申请](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=168&source=0&data_title=%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9CVPC&step=1)。
>- 辅助 CIDR 可以和自定义路由的目的网段重叠；但需要谨慎操作，因为辅助 CIDR 的路由属于 Local 路由，Local 路由比自定义子网路由优先级更高。
>- 基础网络云服务器不支持和辅助 CIDR 内的云资源互通。
>- 目前仅云联网支持传递辅助 CIDR，即：辅助 CIDR 内的云服务器无法通过对等连接、专线接入和其他 VPC、IDC 通信。

1. 登录 [私有网络控制台](https://console.cloud.tencent.com/vpc)。
2. 在“私有网络”页面顶部，选择 VPC 所属地域。
3. 在 VPC 列表中目标 VPC 右侧**操作**列选择【更多】>【编辑IPv4 CIDR】。
	![](https://main.qcloudimg.com/raw/2f70c86d42da11ba7fa502b3b58e9b74.png)
4. 在弹出编辑对话框中单击【添加】，并编辑辅助 CIDR。
<img src="https://main.qcloudimg.com/raw/2dce76adc2f3b4428d68a9727f55966b.png" width="50%" />
5. 单击【确定】完成辅助 CIDR 的创建。

<span id ="32"></span>
## 删除辅助 CIDR
>?目前辅助 CIDR 处于内测中，如有需要，请提交 [工单申请](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=168&source=0&data_title=%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9CVPC&step=1)。
>
1. 登录 [私有网络控制台](https://console.cloud.tencent.com/vpc)。
2. 在“私有网络”页面顶部，选择 VPC 所属地域。
3. 在 VPC 列表中，待删除辅助 CIDR 的 VPC 右侧**操作**列选择【更多】>【编辑 IPv4 CIDR】。
4. 在弹出的编辑对话框中，单击辅助 CIDR 后的【删除】。
<img src="https://main.qcloudimg.com/raw/07867a0b1fbca9ad4350ca82d2c54200.png" width="50%" />
5. 单击【确定】完成删除操作。

<span id ="3"></span>
## 删除 VPC
>?删除 VPC 的前提条件：待删除 VPC 的 IP 没有被占用，且 VPC 内没有云资源（如云服务器、云数据库、网关等）。
>
1. 登录 [私有网络控制台](https://console.cloud.tencent.com/vpc)。
2. 在“私有网络”页面顶部，选择 VPC 所属地域。
3. 在 VPC 列表中待删除的 VPC 右侧**操作**列单击【删除】，并确认操作。
![](https://main.qcloudimg.com/raw/5aaffa07e85e3119c358ff7bc9af9eeb.png)
