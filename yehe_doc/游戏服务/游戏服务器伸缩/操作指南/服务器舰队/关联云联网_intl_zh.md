
## 操作场景

本文档主要指导您如何关联云联网进行多点内网互联服务，实现各地域的云上、云下多点互联。

## 前提条件
已创建 [生成包](https://intl.cloud.tencent.com/document/product/1055/36674) 或 [镜像资源](https://intl.cloud.tencent.com/document/product/1055/39061)。

## 操作步骤

### 创建服务器舰队时

1. 登录 [游戏服务器伸缩控制台](https://console.cloud.tencent.com/gse/asset)，单机左侧菜单**服务器舰队**进入舰队列表页。
2. 单击**新建**创建服务器舰队。
<img src="https://camo.githubusercontent.com/02155cd8e3264bae81e2936d80c5a421bbde29c0340f690a24b1f859f8bedaf0/68747470733a2f2f6d61696e2e71636c6f7564696d672e636f6d2f7261772f35393464663837326437393431626663656462633237383939376139343866322e706e67" style="width: 95%;"/>
3. 在新建服务器舰队的“关联云联网”页面勾选**是**。
<dx-alert infotype="explain" title="">
 - 若您需要对同一账号下的 VPC 进行云联网自动审核，则在勾选后完成 [服务授权](#test51) 后再进行以下操作。
 - 若您无需自动授权则在“自动审核 VPC 授权”弹窗中单击**取消**或 “X” 关闭弹窗继续完成以下操作。
</dx-alert>


![](https://camo.githubusercontent.com/d01cc445038fa547acb626b29ca43a9766629b00e284397111976373e7ab4395/68747470733a2f2f6d61696e2e71636c6f7564696d672e636f6d2f7261772f36633937363661323636363332363932326438333238383966356361646431382e706e67)
4. 输入账号 ID 及云联网 ID 进行关联操作。
![](https://camo.githubusercontent.com/a30c3ed1cf7dda51ec46c1ee93a558a328e0773aa4d48e685964551063f52e53/68747470733a2f2f6d61696e2e71636c6f7564696d672e636f6d2f7261772f39313966636633626661313934643032616236663137376262343063373464302e706e67)
<dx-alert infotype="explain" title="">
- 在创建服务器舰队过程中关联云联网，需在20分钟内同意申请，否则创建失败。
- 实例加入云联网产生的网络互通费用，由云联网所在账号承担。  
- 请关注该云联网内实例所属地域，目前暂不支持跨境互联服务，如有需要请联系您的商务经理。 
</dx-alert>

 

### [完成服务器舰队创建后](id:test21)

1. 登录 [游戏服务器伸缩控制台](https://console.cloud.tencent.com/gse/asset)，单机左侧菜单**服务器舰队**进入舰队列表页。
2. 完成 [创建服务器舰队](https://intl.cloud.tencent.com/document/product/1055/36675)。
3. 单击**ID**进入需要关联云联网的舰队详情页面。
![](https://camo.githubusercontent.com/3bc6a3b373b8dab13e24bb09a8d80b5a0e7579a6dcd56e3c2d346364b17b1351/68747470733a2f2f6d61696e2e71636c6f7564696d672e636f6d2f7261772f36333433313438373761663863626633323162626231663762643635626437332e706e67)
4. 在服务器舰队详情页，单击右侧**立即关联**，即可进行关联操作。
<dx-alert infotype="explain" title="">
- 若您需要对同一账号下的 VPC 进行云联网自动审核，则在勾选后完成 [服务授权](#test51) 后再进行以下操作。
- 若您无需自动授权则在“自动审核 VPC 授权”弹窗中单击**取消**或 “X” 关闭弹窗继续完成以下操作。
</dx-alert>



![](https://camo.githubusercontent.com/cd203d79081eeb9400dfa0420edfafbe3850f776d8d3671e9f793d8a8bd67783/68747470733a2f2f6d61696e2e71636c6f7564696d672e636f6d2f7261772f36333634363064396435376536613034336131373531393763343632323662312e706e67)
5. 输入账号 ID 及云联网 ID 进行关联操作。
<img src="https://camo.githubusercontent.com/d71628bf784f991f4d683f53951fd34dd0eaf5aa31e886e0dab1971c4353121d/68747470733a2f2f6d61696e2e71636c6f7564696d672e636f6d2f7261772f61346137376234616666366234333366643733373564613463306536373639372e706e67" alt="" class="zoom-img-hover" style="
    width: 65%;
">
<dx-alert infotype="explain" title="">
- 在完成服务器舰队创建之后关联云联网，对方需在7天内同意申请，7天后申请将过期。  
- 实例加入云联网产生的网络互通费用，由云联网所在账号承担。  
- 请关注该云联网内实例所属地域，目前暂不支持跨境互联服务，如有需要请联系您的商务经理。  
</dx-alert>






### 复制舰队时

1. 登录 [游戏服务器伸缩控制台](https://console.cloud.tencent.com/gse/asset)，单机左侧菜单**服务器舰队**进入舰队列表页。
2. 完成 [创建服务器舰队](https://intl.cloud.tencent.com/document/product/1055/36675)。
3. 单击**复制**进入复制舰队页面。
![](https://qcloudimg.tencent-cloud.cn/raw/cb8288e39fc8067ba254712671042492.png)
4. 单击“基本信息”页面的**点击展开**，展开舰队详情页面。
5. 在舰队详情页面的“关联云联网”中勾选**是**。
<dx-alert infotype="explain" title="">
- 若您需要对同一账号下的 VPC 进行云联网自动审核，则在勾选后完成 [服务授权](#test51) 后再进行以下操作。
- 若您无需自动授权则在“自动审核 VPC 授权”弹窗中单击**取消**或 “X” 关闭弹窗继续完成以下操作。
</dx-alert>

![](https://qcloudimg.tencent-cloud.cn/raw/76a17da70c59d8bac78e668c3823445a.png)
6. 输入账号 ID 及云联网 ID 进行关联操作。
![](https://qcloudimg.tencent-cloud.cn/raw/9e763574c405f714e255020f5284398e.png)
7. 勾选关联时机。
 - 创建舰队过程中申请关联，对端账号需20分钟内审核，否则创建服务器舰队失败。
 - 创建舰队完成后申请关联，对端账号需在7天内同意申请。




## [服务授权](id:test51)

您可将服务授权给 GSE，对同一账号下的 VPC 进行云联网自动审核，具体操作步骤如下。
1. 在“自动审核 VPC 授权”弹窗中单击**前往访问管理**进入访问管理控制台。
<img src="https://qcloudimg.tencent-cloud.cn/raw/2a85c9164001aeb4b345b48c28331fd4.png" alt="" class="zoom-img-hover" style="
    width: 70%;
">
2. 在角色管理页面单击**同意授权**即可完成服务授权。
<img src="https://qcloudimg.tencent-cloud.cn/raw/f44c110c8866ddd2b14bbfd23730e422.png" alt="" class="zoom-img-hover" style="
    width: 70%;
">

另外，子账号若要实现“自动审核 VPC 授权”，则需主账号先完成服务授权，再将如下权限语法授权给子账号。
<dx-codeblock>
:::  Java
{
	"version": "2.0", 
	"statement": [
		{
				"effect": "allow",
				"action": [
						"cam:ListAttachedRolePolicies",
						"cam:GetRole"
				],
				"resource": "*"
		}
	]
}
:::
</dx-codeblock>



