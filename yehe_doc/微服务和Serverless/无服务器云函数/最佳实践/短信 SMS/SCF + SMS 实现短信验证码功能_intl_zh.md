通过手机短信发送验证码，是最普遍、最安全验证用户真实身份的方式。目前，短信验证码广泛应用于用户注册、密码找回、登录保护、身份认证、随机密码、交易确认等应用场景。
本文以使用 [云函数](https://intl.cloud.tencent.com/zh/document/product/583) 开发一个短信验证码登录注册服务为例，帮助您了解如何实现短信验证码功能。

除云函数之外，还可通过使用 [发送短信接口](https://intl.cloud.tencent.com/document/product/382/34859) 实现。

## 准备工作
- 已 [注册腾讯云](https://intl.cloud.tencent.com/document/product/378/17985) 账号，并完成 [企业实名认证](https://intl.cloud.tencent.com/zh/document/product/378/10496)。
- 已购买短信套餐包。
- 准备短信签名归属方资质证明文件，详细的文件清单以及规范请参见 [签名审核标准](https://intl.cloud.tencent.com/document/product/382/40658)。
 本文以使用企业营业执照作为资质证明文件为例。
- 了解短信正文内容审核规范，详情请参见 [正文模板审核标准](https://intl.cloud.tencent.com/document/product/382/40659)。
- 已获取短信应用的 SDKAppID。

## 相关资料
- [Demo 源码](https://github.com/tencentyun/scf-demo-repo/tree/master/Nodejs8.9-SmsVerificationCode)
- 其他产品文档
 - [私有网络产品文档](https://intl.cloud.tencent.com/zh/document/product/215)
 - [云数据库 Redis 产品文档](https://intl.cloud.tencent.com/document/product/239/3205)
 - [云函数产品文档](https://intl.cloud.tencent.com/zh/document/product/583)

## 步骤1：配置短信内容[](id:Step1)
短信签名、短信正文模板提交后，我们会在2个小时左右完成审核，您可以 [配置告警联系人](https://intl.cloud.tencent.com/document/product/382/35470) 并设置接收模板和签名审核通知，便于及时接收审核通知。

### 步骤1.1：创建签名[](id:Step1_1)

1. 登录 [短信控制台](https://console.cloud.tencent.com/smsv2)。
2. 在左侧导航栏选择**国内短信**>**签名管理**，单击**创建签名**。
3. 结合实际情况和 [短信签名审核标准](https://intl.cloud.tencent.com/document/product/382/40658) 设置以下参数：
 <table>
     <tr>
         <th width="20%">参数</th>  
         <th>取值样例</th>  
     </tr>
	 <tr>      
       <td>签名用途</td>   
	     <td>自用（签名为本账号实名认证的公司、网站、产品名等）</td>   
     </tr> 
	 <tr>      
       <td>签名类型</td>   
	     <td>App</td>   
     </tr> 
	 <tr>      
       <td>签名内容</td>   
	     <td>测试 Demo</td>   
     </tr> 
	 <tr>      
       <td>证明类型</td>   
	     <td>小程序设置页面截图</td>   
     </tr> 
	 <tr>      
       <td>证明上传</td>   
	<td><img src="https://main.qcloudimg.com/raw/48ad431a784461465054160737b9b166.png" width=400/></td>    
     </tr> 
</table>
3. 单击**确定**。
等待签名审核，当状态变为**已通过**时，短信签名才可用。


### 步骤1.2：创建正文模板[](id:Step1_2)
1. 登录 [短信控制台](https://console.cloud.tencent.com/smsv2)。
2. 在左侧导航栏选择**国内短信**>**正文模板管理**，单击**创建正文模板**。
3. 结合实际情况和 [短信正文模板审核标准](https://intl.cloud.tencent.com/document/product/382/40659) 设置以下参数：
 <table>
     <tr>
         <th width="20%">参数</th>  
         <th>取值样例</th>  
     </tr>
	 <tr>      
        <td>模板名称</td>   
	     <td>验证码短信</td>   
     </tr> 
	 <tr>      
        <td>短信类型</td>   
	     <td>普通短信</td>   
     </tr> 
	 <tr>      
        <td>短信内容</td>   
	     <td>您的注册验证码：{1}，请于{2}分钟内填写，如非本人操作，请忽略本短信。</td>   
     </tr> 
</table>
4. 单击**确定**。
等待正文模板审核，当状态变为**已通过**时，正文模板才可用，请记录模板 ID。

## 步骤2：设置短信发送频率限制（可选）[](id:Step2)
>!个人认证用户不支持修改频率限制，如需使用该功能，请将 “个人认证” 变更为 “企业认证”，具体操作请参见 [实名认证变更指引](https://intl.cloud.tencent.com/document/product/378/37276)。

为了保障业务和通道安全，减少业务被刷后的经济损失，建议 [设置发送频率限制](https://intl.cloud.tencent.com/document/product/382/35469)。
本文以短信的默认频率限制策略为例。
- 同一号码同一内容30秒内最多发送1条。
- 同一手机号一个自然日最多发送10条。

## 步骤3：配置私有网络和子网[](id:Step3)
默认情况下，云函数部署在公共网络中，只可以访问公网。如果开发者需要访问腾讯云的 TencentDB 等资源，需要建立私有网络来确保数据安全及连接安全。

1. 按需 [规划网络](https://intl.cloud.tencent.com/document/product/215/31795)。
2. 创建私有网络，具体操作请参见 [创建 VPC](https://intl.cloud.tencent.com/document/product/215/31805)。
 >!私有网络和子网的 CIDR 创建后不可修改。
 >
 <table>
     <tr>
         <th width="20%">参数</th>  
         <th>取值样例</th>  
     </tr>
	 <tr>      
        <td>所属地域</td>   
	     <td>	华南地区(广州)</td>   
     </tr> 
	 <tr>      
        <td>名称</td>   
	     <td>Demo VPC</td>   
     </tr> 
	 <tr>      
        <td>IPv4 CIDR</td>   
	     <td>10.0.0.0/16</td>   
     </tr> 
	 <tr>      
        <td>子网名称</td>   
	     <td>Demo 子网</td>   
     </tr> 
	 <tr>      
        <td>IPv4 CIDR</td>   
	     <td>10.0.0.0/16</td>   
     </tr> 
	 <tr>      
        <td>可用区</td>   
	     <td>广州三区</td>   
     </tr> 
</table>

## 步骤4：配置 Redis 数据库[](id:Step4)
云数据库 Redis 实例需与 [步骤3](#Step3) 配置私有网络的地域和子网的可用区保持一致。

1. 购买云数据库  Redis 实例，具体操作请参见 [购买方式](https://intl.cloud.tencent.com/document/product/239/37712)。
 <table>
     <tr>
         <th width="20%">参数</th>  
         <th>取值样例</th>  
     </tr>
	 <tr>      
        <td>计费模式</td>   
	     <td>	按量计费</td>   
     </tr> 
	 <tr>      
        <td>地域</td>   
	     <td>广州</td>   
     </tr> 
	 <tr>      
        <td>数据库版本</td>   
	     <td>Redis 4.0	</td>   
     </tr> 
	 <tr>      
        <td>架构</td>   
	     <td>标准架构</td>   
     </tr> 
	 <tr>      
        <td>网络</td>   
	     <td>Demo VPC，Demo 子网</td>   
     </tr> 
	 <tr>      
        <td>实例名</td>   
	     <td>立即命名：Demo 数据库</td>   
     </tr> 
	 <tr>      
        <td>购买数量</td>   
	     <td>1</td>   
     </tr> 
</table>

## 步骤5：新建云函数[](id:Step5)
云函数目前支持 Python、Node.js、PHP、Java 以及 Golang 语言开发，本文以 Node.js 为例。

1. 在 [步骤3](#Step3) 创建的 VPC 所属地域中新建函数，具体操作请参见 [编写函数](https://intl.cloud.tencent.com/document/product/583/32742)。
  <table>
     <tr>
         <th width="20%">参数</th>  
         <th>取值样例</th>  
     </tr>
	 <tr>      
        <td>函数名称</td>   
	     <td>Demo</td>   
     </tr> 
	 <tr>      
        <td>运行环境</td>   
	     <td>Nodejs 8.9</td>   
     </tr> 
	 <tr>      
        <td>创建方式</td>   
	     <td>模板函数：helloworld</td>   
     </tr> 
</table>
2. 部署函数并配置触发方式为**API网关触发器**，具体操作请参见 [部署函数](https://intl.cloud.tencent.com/document/product/583/32742)。

## 步骤6：启用公网访问配置（可选）[](id:Step6)
- 2020年4月29日前，部署在 VPC 中的云函数默认隔离外网。若需使云函数同时具备内网访问和外网访问能力，可通过启用公网配置方式实现。
 登录 [云函数控制台](https://console.cloud.tencent.com/scf/index?rid=1)，选择**函数服务**，在云函数列表中单击目标函数名进入函数配置页。单击**编辑**，勾选**公网访问**并单击**保存**保存配置。
- 2020年4月29日及以后，新部署的云函数默认已启用公网访问，无需额外操作。

## 步骤7：部署短信 Demo[](id:Step7)
1. 前往 [云函数控制台](https://console.cloud.tencent.com/scf/) 并选择 SMS Demo 进行部署。
![](https://qcloudimg.tencent-cloud.cn/raw/be4eb37abbf2467adcb49fc58bae867a.png)

2. 在**高级配置**中设置 Demo 的环境变量。
![](https://qcloudimg.tencent-cloud.cn/raw/7047cab8759d3f506445fb1b8c5c988d.png)


| 字段 |说明|
| ----- | ----- |
| REDIS_HOST|Redis 数据库地址|
|REDIS_PASSWORD|Redis 数据库密码|
| SMS_TEMPLATE_ID|模板 ID，必须填写已审核通过的模板 ID。模板 ID 可登录  [短信控制台](https://console.cloud.tencent.com/smsv2) 查看。|
| SMS_SIGN|短信签名内容，使用 UTF-8 编码，必须填写已审核通过的签名，签名信息可登录 [短信控制台](https://console.cloud.tencent.com/smsv2)  查看。注：国内短信为必填参数。|
| SMS_SDKAPPID|短信 SdkAppid 在 [短信控制台](https://console.cloud.tencent.com/smsv2) 添加应用后生成的实际 SdkAppid，示例如1400006666。|


3. 在**高级配置**中设置与 Redis 数据库相同的 VPC 环境。
![](https://qcloudimg.tencent-cloud.cn/raw/b8d7e97e7d4a61c2b81ce772d5b183c4.png)


4. 在**高级配置**中设置 SCF **运行角色**权限。
![](https://qcloudimg.tencent-cloud.cn/raw/f15d9c23d81b1537722aece6f88d7252.png)
需要在 [访问管理](https://console.cloud.tencent.com/cam/role) 控制台给 SCF_QcsRole 角色添加短信 QcloudSMSFullAccess 权限
![](https://qcloudimg.tencent-cloud.cn/raw/a62783752425bb5a82743e1d2dcc98d2.png)
这样代码里就能获取到`TENCENTCLOUD_SECRETID、TENCENTCLOUD_SECRETKEY、TENCENTCLOUD_SESSIONTOKEN`环境变量了，发送短信的 sdk 会用到这些环境变量。

5. 点击**完成**，即可完成函数部署。

6. 创建函数 **API网关触发器**，请求该触发器地址，即可使用短信相关能力。
![](https://qcloudimg.tencent-cloud.cn/raw/5f6c8e7e13063767ac992d9974463215.png)

## 步骤8：功能使用及说明
验证码的时效性要求较高，您可以把验证码存在内存中或存在云数据库 Redis 中。以手机号作为 key，存储发送时间、验证码、验证次数、是否已验证过等信息。

### 功能
#### 发送短信验证码
请求参数：

| 字段 | 类型 | 说明 |
| ----- | ----- | ----- |
| method|string|请求方法，值为 getSms|
|phone|string|手机号，值为区号+手机号，例如86185662466**|

#### 校验验证码（登录）
请求参数：

| 字段 |类型|说明|
| ----- | ----- | ----- |
| method|string|请求方法，值为 login|
|phone|string|手机号，值为区号+手机号，例如86185662466**|
| code|string|值为6位数字验证码|

### 错误码
| 字段 |说明|
| ----- | ----- |
| InValidParam|缺少参数|
| MissingCode|缺少验证码参数|
| CodeHasExpired|验证码已过期|
| CodeHasValid|验证码已失效|
| CodeIsError|请检查手机号和验证码是否正确|

如有任何疑问，请联系 [腾讯云短信小助手](https://tccc.qcloud.com/web/im/index.html#/chat?webAppId=8fa15978f85cb41f7e2ea36920cb3ae1&title=Sms)，将有专人为您解答。
