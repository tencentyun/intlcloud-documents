本文将引导您通过云联网，实现云联网跨账号关联 VPC 的功能。

## 前提条件
- 需要互联的私有网络 VPC 已创建。
- 需要互联的各 VPC 子网网段、IDC 网段没有冲突。

## 步骤一：账号 A 创建云联网实例
1. 使用账号 A  登录 [云联网控制台](https://console.cloud.tencent.com/vpc/ccn) ，在云联网管理页面，单击**+新建**。 
2. 在弹出框中填写云联网实例名称、描述，选择计费模式、服务质量、限速方式和关联实例的 VPC ID。
>?关联实例，可在新建云联网时关联，也可创建好云联网后再关联。
>
![](https://main.qcloudimg.com/raw/b72cc7c286f94d8b958def554dfc0150.png)
3. 单击**确定**即可。

## 步骤二：VPC 所属账号 B 申请关联云联网
1. 使用账号 B 登录 [私有网络控制台](https://console.cloud.tencent.com/vpc/vpc?rid=1) ，在私有网络列表中，单击需要关联至云联网的 VPC 的 ID，进入详情页。
2. 单击**立即关联**。
![](https://main.qcloudimg.com/raw/3d034f69e2bb198c0604f698a8c5e614.png)
3. 在弹出框中，选择**其他账号**，并输入账号 A 的账号 ID、云联网实例 ID。
![](https://main.qcloudimg.com/raw/461d6ca46bb20c141dc538348b542f1a.png)
4. 单击**确定**，即可向云联网所属账号发送关联申请。

## 步骤三：云联网账号 A 同意账号 B 的关联申请
1. 使用账号 A 登录 [云联网控制台](https://console.cloud.tencent.com/vpc/ccn) 。
2. 在列表中找到有待同意申请的云联网实例，单击其 ID 进入详情页。 
3. 在“关联实例”页面，会显示待同意的 VPC 信息，单击**同意**并确认操作，即可将该 VPC 加入到云联网中。 
![](https://main.qcloudimg.com/raw/a6371867413e26ec0274c12386b4c6ff.png)

## 步骤四：检查路由表
若所关联的网络实例网段有冲突，则会产生失效路由，查看操作如下：
1. 在云联网列表中，单击要查看路由的云联网 ID，进入详情页。
2. 单击**路由表**，查看该云联网路由表。
3. 检查是否存在状态为失效的路由策略。
![](https://main.qcloudimg.com/raw/6e8f71bbd8addfa7df60ed6061df9b38.png)
4. 路由冲突原则，请参见 [路由限制](https://intl.cloud.tencent.com/document/product/1003/30052)，如需启用冲突路由，请参见 [启用路由](https://intl.cloud.tencent.com/document/product/1003/30069)。

## 步骤五：设置跨地域带宽限制（可选）
1. 在云联网列表中，单击需要设置带宽的云联网 ID，进入详情页。
2. 在云联网实例详情页，单击**带宽管理**标签页。
3. （可选）单击**变更**，在“变更限速方式”页签，按需选择配置跨地域带宽上限的方式。
![](https://main.qcloudimg.com/raw/bc93b28f5c0fb5fee6ce51e1b73dab1c.png)
![](https://main.qcloudimg.com/raw/f7d06cf1f591f25950d0b8a745fafa71.png)
4. 根据您创建的云联网限速方式，按需配置限速：
>?默认带宽上限为 1Gbps，如需更大默认带宽，请提 [工单申请](https://console.cloud.tencent.com/workorder/category)。
>
 - 地域间带宽限速
单击**调整带宽**，在弹框中选择需要限速的两个地域，填写地域间的带宽上限，如需添加多条请单击【添加】继续，完成添加后单击**确定**即可。
![](https://main.qcloudimg.com/raw/5424741fb17864f3f98da59ba047d9f5.png)
 - 地域出口带宽限速
单击**调整带宽限速**，在弹框中勾选需要限速的地域，填写地域出口的带宽上限，单击**确定**即可。
![](https://main.qcloudimg.com/raw/aef1779f4c11d8f0fe716c287cb60b90.png)
>?云联网实例间通信可能会产生费用，详情请参见 [计费总览](https://intl.cloud.tencent.com/document/product/1003/30053)。



