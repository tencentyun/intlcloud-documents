 云联网可以实现 VPC 之间、VPC 和 IDC 间的通信。本文将介绍如何使用云联网实例，以实现同账号下的广州和上海地域的 VPC 互通。

## 背景信息

创建云联网实例时，您可以根据实际选择月95后付费模式，具体如下图所示：
![](https://main.qcloudimg.com/raw/23e11b65f008292a6803ffe53fc786d1.png)
本文以同账号下的广州和上海地域的 VPC 互通为例，为您介绍相关操作。

## 前提条件

在上海和广州地域下已创建 VPC 和子网，且二者网段不重叠，并已在子网内分别创建云服务器，详情请参见[ 快速搭建 IPv4 私有网络](https://intl.cloud.tencent.com/document/product/215/31891)。


## 步骤一：创建云联网实例[](id:1)

1. 登录 [私有网络控制台](https://console.cloud.tencent.com/vpc/vpc?rid=1) 。
2. 在左侧导航栏中单击【云联网】，在云联网管理页面上方单击【+新建】。
3. 在“新建云联网实例”对话框中配置以下信息，然后单击【确定】。
![](https://main.qcloudimg.com/raw/67e42dd8cb0f3c2d509e59bcfc24df0a.png)

 <table>
 <thead>
 <tr>
  <th >字段</th>
  <th >子字段</th>
  <th >说明</th>
 </tr>
  </thead>
 <tr>
  <td align="center">名称</td>
   <td align="center">-</td>
  <td >云联网实例的名称。</td>
 </tr>
 <tr >
  <td align="center" >计费模式</td>
  <td align="center" style='white-space:nowrap'>月95后付费</td>
  <td>按当月实际使用带宽 95 削峰计费，适合带宽波动较大业务。</td>
 </tr>
 <tr>
  <td rowspan=3 align="center">服务质量</td>
  <td align="center">白金</td>
  <td>适用于通信质量最敏感的关键业务，金牌次之，主要包括支付，游戏加速等。</td>
 </tr>
 <tr>
  <td align="center" white-space="nowrap">金</td>
  <td >适用于重要数据业务数据传输业务，如企业商务数据传递、ERP 等。</td>
 </tr>
 <tr >
  <td align="center">银</td>
  <td >银牌适用成本敏感，抖动不敏感，安全性高的业务。</td>
 </tr>
 <tr>
  <td rowspan=2>限速方式</td>
  <td align="center" style='white-space:nowrap'>地域出口限速</td>
  <td >某地域去往其它地域的总体出带宽限速。</td>
 </tr>
 <tr>
   <td align="center" style='white-space:nowrap'>地域间限速</td>
  <td >两地域之间的出入带宽限速。</td>
 </tr>
 <tr>
  <td   align="center">关联实例</td>
  <td   align="center">-</td>
  <td >可关联私有网络、专线网关、黑石私有网络、VPN
  网关等实例，本示例中选择关联上海地域的 VPC。</td>
 </tr>
</table>


## 步骤二：关联网络实例[](id:2)

将广州地域的 VPC 关联至云联网，具体步骤如下：

1. 在云联网列表页面，单击目标云联网实例 ID，进入详情页。
2. 在“关联实例”页面单击【新增实例】。 
3. 在“关联实例”对话框中，选择广州地域的 VPC 实例进行关联。

>?如还需关联其他网络实例，可单击【添加】继续关联。
>
![](https://main.qcloudimg.com/raw/02cb17c3741827d4f01cecda590dd381.png)

4. 单击【确定】，将所选网络实例加入云联网。


## 步骤三：检查路由表[](id:3)

查看云联网关联的 VPC 下各子网的路由策略是否生效。若所关联的网络实例网段有冲突，则会产生失效路由。

1. 在云联网列表页面，单击目标云联网实例 ID。
2. 在云联网实例详情页单击【路由表】标签页，查看该云联网路由表。
3. 检查是否存在状态为**失效**的路由策略。若存在，则根据 [路由冲突原则 ](https://intl.cloud.tencent.com/document/product/1003/30052)修改路由表并启用路由，详情请参见 [启用路由](https://intl.cloud.tencent.com/document/product/1003/30069)。
  ![](https://main.qcloudimg.com/raw/30e2fa3a3d0948d3dad64045040fff9f.png)

## 步骤四：配置带宽

**设置跨地域带宽限制（仅月95后付费云联网实例适用）**
  若您创建的月95后付费云联网实例，可以按需配置跨地域带宽上限，有设置地域间带宽限速和设置地域出口带宽限速两种方式。

>?默认带宽上限为 1Gbps，如需更大默认带宽，请提 [工单申请](https://console.cloud.tencent.com/workorder/category)。
>
  1. 在云联网列表页面，单击目标云联网实例 ID。
  2. 在云联网实例详情页，单击【带宽管理】标签页。
  3. (可选) 单击【变更】，在“变更限速方式”页签，按需选择配置跨地域带宽上限的方式。![](https://main.qcloudimg.com/raw/b721393fb8cb95e9ebb14ee8c3db1536.png) ![](	https://main.qcloudimg.com/raw/e267c561ea9be180cd3dcdab451b1233.png)
 
 > !限速方式变更后，原有限速配置将删除，带宽将设置为1Gbps（默认），如需更大默认带宽，请提[ 工单申请](https://console.cloud.tencent.com/workorder/category)。
 >     

4. 根据您创建的云联网限速方式，按需配置限速：	 
 -  设置地域间带宽限速
   单击【调整带宽】，在弹框中选择需要限速的两个地域，填写地域间的带宽上限，如需添加多条请单击【添加】继续，完成添加后单击【确定】。
    ![](https://main.qcloudimg.com/raw/8985f4739ef6e55716e4d56370745365.png)
  -  设置地域出口带宽限速
   单击【调整带宽限速】，在弹框中勾选需要限速的地域，填写地域出口的带宽上限，单击【确定】即可。
    ![](https://main.qcloudimg.com/raw/a204cb4fadc323ea81af2aa5daa00aa6.png)

>?云联网实例间通信可能会产生费用，详情请参见 [计费总览](https://intl.cloud.tencent.com/document/product/1003/30053)。

## 结果验证

登录上海地域的云服务器，向广州地域的云服务器执行 `ping <IP 地址>` 命令，若出现以下结果说明网络连接成功。
![](https://main.qcloudimg.com/raw/85cf83efdb100080db078e4f497baf7e.png)
