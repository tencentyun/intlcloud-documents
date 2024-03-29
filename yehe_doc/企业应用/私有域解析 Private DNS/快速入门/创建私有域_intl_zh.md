## 概述
本文档将指导您如何通过 Private DNS 创建私有域。


## 操作步骤
1. 登录私有域解析 [Private DNS 控制台](https://console.cloud.tencent.com/privatedns/domains)，并单击左侧导航栏的【私有域列表】，即可进入私有域列表。
2. 在 “私有域列表” 中，单击【新建私有域】。如下图所示：
![](https://main.qcloudimg.com/raw/568e131b241a9e11182cf6a41cebeee5.png)
3. 在 “新建私有域” 页面中，填写私有域相关信息。如下图所示：
![](https://main.qcloudimg.com/raw/4172035b4d45210101666d9b7a0c5e3a.png)
 - **域名**：请自定义输入想要创建的私有域名，即您想要在 VPC 环境关联并使用的私有域名。
>?
>- 仅支持创建符合 IANA 规范的标准 TLD 域名。
>- 创建私有域名后需设置解析记录并关联 VPC 使用，且该域名解析仅在已关联的 VPC 环境生效。
>
 - **关联 VPC**：请选择当前 Private DNS 支持的地域且已创建的 VPC 进行关联，同一私有域名不支持关联同一 VPC。
>?
>- 为更好的体验，推荐您创建私有域名并设置解析记录后再关联 VPC。
>- 若当前可选地域中未显示 VPC，请您前往 [VPC 控制台](https://console.cloud.tencent.com/vpc/vpc?rid=1/) 进行添加。
>- 若现有的 VPC 不符合您的要求，请您前往 [VPC 控制台](https://console.cloud.tencent.com/vpc/vpc?rid=1/) 进行修改。
>- 当前支持关联的 VPC 区域有北京、上海、成都、重庆、广州、硅谷。
>
 - **标签**：请选择标签，您可以通过标签对云资源进行分类、搜索、和聚合。详情请查看：[标签](https://intl.cloud.tencent.com/document/product/651/13334)。
 - **备注**：请填写私有域备注信息。
 - **子域名递归解析**：请根据您的实际需求进行选择，默认状态为【关闭】。详情请查看：[子域名递归解析说明](https://intl.cloud.tencent.com/document/product/1097/40566)。
4. 单击【确定】，即可完成创建私有域。

## 下一步操作
对于已添加解析的私有域，私有域列表【记录】的数值代表该私有域的解析记录数量。
在 [Private DNS 控制台](https://console.cloud.tencent.com/privatedns/domains)，单击您需要进行解析的 “私有域” 名称，即可进入解析记录控制台，为该私有域添加解析记录。具体操作请参考 [解析记录设置](https://intl.cloud.tencent.com/zh/document/product/1097/40568)。


