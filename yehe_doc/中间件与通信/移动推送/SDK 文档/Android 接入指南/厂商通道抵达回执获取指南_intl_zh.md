为了帮助客户全链路分析推送效果，移动推送 TPNS 提供厂商通道抵达数据展示。国内不同厂商通道对抵达数据回执的支持程度不同，部分通道抵达数据不能直接获取，需要开发者进行相应配置。

配置成功后，开发者可在移动推送 TPNS 控制台推送详情中查看推送转化数据，也可通过移动推送 TPNS  Rest API 获取推送转化数据。

## 概览

| 厂商通道  | 是否支持抵达回执 | 是否需要配置 |
| --------- | ------------ | ------------ |
| 华为通道  | 是           | **是**       |
| 魅族通道  | 是           | **是**          |
| 小米通道  | 是           | 否           |
| OPPO 通道 | 是           | 否           |
| vivo 通道 | 是           | 否           |
| FCM 通道  | 是           | 否           |

>? 厂商通道抵达回执数据仅供参考。
>

## 华为厂商通道回执配置指引

完成华为厂商通道 SDK 集成后，需要开发者在华为开放平台开通并配置消息回执，才能获取到华为通道抵达数据。具体配置方法可参考华为开放平台 [消息回执](https://developer.huawei.com/consumer/cn/doc/development/HMS-Guides/push-receipt#h1-1575515478691)，配置流程如下：

### 开通回执权益

1. 登录 [AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html) 网站 ，选择【我的应用】。
![](https://main.qcloudimg.com/raw/59521f7425a5d6e1bccae726635096dc.png)
2. 选择需要开通服务的应用所属产品的名称，进入应用信息页面。
3. 在“应用信息”页面，选择【全部服务】>【推送服务】。
4. 在“推送服务”页面，找到【应用回执状态】，单击【开通】。
![](https://main.qcloudimg.com/raw/32556c2eb1d74756583cc8c27d436883.png)

### 回执参数配置

1. 配置消息回执地址。请在 [TPNS 控制台](https://console.cloud.tencent.com/tpns) 查看您的应用的服务接入点，并复制该应用的 AccessID，选择对应服务接入点的回执地址进行配置：

<table>
 <tbody><tr>
 <th>服务接入点 </th>
 <th>回执地址 </th> 
 </tr>
 <tr>
 <td >广州服务接入点 </td>
 <td>https://stat.tpns.tencent.com/log/statistics/hw/AccessID  </td>
 </tr>
 <tr>
 <td>中国香港服务接入点 </td>
 <td>https://stat.tpns.hk.tencent.com/log/statistics/hw/AccessID </td>
 </tr>
 <tr>
 <td>新加坡服务接入点 </td>
 <td>https://stat.tpns.sgp.tencent.com/log/statistics/hw/AccessID </td>
 </tr>
 <tr>
 <td>上海服务接入点 </td>
 <td>https://stat.tpns.sh.tencent.com/log/statistics/hw/AccessID </td>
 </tr>
 </tbody></table>

> ?AccessID 替换为您应用的 AccessID。例如应用为广州服务接入点，则回执地址配置为`https://stat.tpns.tencent.com/log/statistics/hw/1500016691` 

2. 根据您的应用服务接入点，下载对应的 HTTPS 证书，下载完成后，用文本打开该证书，将内容复制到文本框中。
<table>
 <tbody><tr>
 <th>服务接入点 </th>
 <th>下载地址 </th> 
 </tr>
 <tr>
 <td >广州服务接入点 </td>
 <td><a href="https://tpns-1259470370.cos.ap-guangzhou.myqcloud.com/tpnshttpscert/tpns-https-cert/tpns-gz1.crt">点击下载</a></td>
 </tr>
 <tr>
 <td>中国香港服务接入点 </td>
 <td><a href=" https://tpns-1259470370.cos.ap-guangzhou.myqcloud.com/tpnshttpscert/tpns-https-cert/tpns-hk.crt">点击下载</a> </td>
 </tr>
 <tr>
 <td>新加坡服务接入点 </td>
 <td><a href="https://tpns-1259470370.cos.ap-guangzhou.myqcloud.com/tpnshttpscert/tpns-https-cert/tpns-sgp.crt">点击下载</a> </td>
 </tr>
 <tr>
 <td>上海服务接入点 </td>
 <td><a href=" https://tpns-1259470370.cos.ap-guangzhou.myqcloud.com/tpnshttpscert/tpns-https-cert/tpns-sh.crt">点击下载</a> </td>
 </tr>
 </tbody></table>
3. 配置用户名和密钥（非必填）进行身份验证。
4. 单击【测试回执】，可以对回执地址进行功能测试。
> !目前单击【测试回执】，会提示“测试回调地址失败”，请忽略并直接单击【提交】。
5. 单击【提交】，即可完成服务的开通。
![](https://main.qcloudimg.com/raw/98a53519ef466977928ebfc1eac879fa.png)

## 魅族厂商通道回执配置指引

完成魅族厂商通道 SDK 集成后，需要开发者在 Flyme 推送平台中新建回执，并在 TPNS 控制台完成激活后，才能获取到魅族通道抵达数据，配置方法如下：

> !以下两步缺一不可，否则可能导致魅族通道下发失败。

### 配置回执

1. 登录 [Flyme 推送平台](https://open.flyme.cn/open-web/views/push.html)  ，选择需要配置回执的应用，单击【打开应用】。
2. 在推送通知页面，点击【配置管理】>【回执管理】。
3. 在【新建回执】中填写回执地址。请在 [TPNS 控制台](https://console.cloud.tencent.com/tpns) 查看您的应用的服务接入点，并选择对应服务接入点的回执地址进行配置：
   ![](https://main.qcloudimg.com/raw/a7940ac0e3a6d8c68523cce9d8483d22.png)
	
	<table>
	 <tbody><tr>
	 <th>服务接入点 </th>
	 <th>回执地址 </th> 
	 </tr>
	 <tr>
	 <td rowspan="2">广州服务接入点 </td>
	 <td>https://api.tpns.tencent.com/log/statistics/mz  </td>
	 </tr>
	 <tr>
	 <td>https://stat.tpns.tencent.com/log/statistics/mz </td> 
	 </tr>
	 <tr>
	 <td>中国香港服务接入点 </td>
	 <td>https://stat.tpns.hk.tencent.com/log/statistics/mz </td>
	 </tr>
	 <tr>
	 <td>新加坡服务接入点 </td>
	 <td>https://stat.tpns.sgp.tencent.com/log/statistics/mz </td>
	 </tr>
		<tr>
	 <td>上海服务接入点 </td>
	 <td>https://stat.tpns.sh.tencent.com/log/statistics/mz </td>
	 </tr>
 </tbody></table>

> ?广州服务接入点的两个回执地址都需要填写。

4. 填写回执地址后，单击右侧【新增】，【回执列表】中正确显示新建的回执即完成配置。



### 激活回执

1. 进入 [产品管理](https://console.cloud.tencent.com/tpns) 页面，选择需要激活的应用，单击【配置管理】。
   ![](https://main.qcloudimg.com/raw/7ac8c31f122ae267796672f50a10b55f.png)
2. 在配置管理页面，【厂商通道】>【魅族官方推送通道】> 单击编辑图标。
   ![](https://main.qcloudimg.com/raw/f12fc508aca29874b4d70afdc365b6c8.png)
3. 在编辑魅族官方推送通道页面，按照提示单击【点击激活】。
   ![](https://main.qcloudimg.com/raw/6c6c40c0f4867e118b54ebdb7083a7f9.png)

