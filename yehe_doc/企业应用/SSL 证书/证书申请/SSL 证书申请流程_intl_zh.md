本文档通过介绍证书申请流程，让您可以充分了解如何申请证书以及填写资料验证的过程。

## 证书申请流程

购买证书完整流程如下图所示：
![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100023397743/b67b3c0b398e11ed8088525400463ef7.png?q-sign-algorithm=sha1&q-ak=AKIDd2WHer59yXTd_a_JJDkcyZ1SHi9Wf9PX43L_4V5Lj9VowvyHxxy5ko8yzSM6Vuhq&q-sign-time=1677228325;1677231925&q-key-time=1677228325;1677231925&q-header-list=&q-url-param-list=&q-signature=bd2a87217d1e6b62fb3f5cf64fd36be3b3978aff&x-cos-security-token=6hMEYRM6EVK7wQVx1850tcGp3oXIcQLa7d0f59e280aa92cc99fda2265cc99ddclq4GrbYk_Xrb8oMoMGYe5GnqBBwAmi6wx9HfvSJ82dm5blzxcEXv2P9BMB95ym8UW3BkD9HKIk5Zft9m_q99iyS6o6SaWLPHEA17EMLN9CyfBospWfLdAj-f9dr1aT8HEXpIxxkdSODRCEmH8tlR_JF8RE2x_Wunz1PzpvyKAz3z1R71omtu0pBE5p-FFJcwURRkyx7bxnazbQJviqblccStlqlWRKo1raKXz8EwPyk6l2GhRoDwV2MIc_nZTawwp_bCZd-g8OWjOvkSg2kg0j8ANnbEsAZmFs3QJOstZ9oH-QizOZCBgnDZeBseGlr-gOiG8P0M_ZYaAC82EavJTr7XyM40jABG92fEZBs4yVMqUjJr71P5Xy5EELZ6LeCD)

### 步骤1：购买证书
1. 登录腾讯云  [SSL 证书控制台](https://console.cloud.tencent.com/ssl) ，进入 “证书列表” 管理页面，单击**购买证书**。如下图所示：
   

> **说明**
>   - 您也可以在腾讯云 [SSL 证书购买页](https://intl.cloud.tencent.com/pricing/ssl) 进行购买。
>   - 如您对证书种类以及品牌不熟悉，可单击**快速配置**，选择系统为您推荐的证书，更快速购买证书。
>   - 支付订单后，会生成一张证书ID，证书签发过程中绑定域名，域名一经绑定，无法再次修改或新增。


2. 选择您需要的证书种类、证书品牌、域名类型以及证书年限等。具体操作请参考 [购买流程](https://intl.cloud.tencent.com/document/product/1007/30159)。


### 步骤2：提交资料验证

#### 方式1

**域名型（DV）免费 SSL 证书：**
证书申请完成后，需进行域名所有权验证，验证成功后 CA 机构将签发证书。

#### 方式2

**其他品牌 OV 与 EV 型 SSL 证书：**
购买证书完成后，请登录 [证书管理控制台](https://console.cloud.tencent.com/certoverview)  ，选择并进入**待提交**管理页面，提交资料并上传确认函进行证书申请，提交申请后，需人工审核，人工审核通过后 CA 机构将签发证书。详情请查看 [其他品牌 OV 与 EV 型证书材料提交流程](https://intl.cloud.tencent.com/document/product/1007/30160)。

> **说明**
> 
> - 您在提交资料过程中，如勾选使用 [我的资料](https://console.cloud.tencent.com/ssl/info) 中已通过审核的公司信息以及管理人信息，则无需上传确认函。
> - GlobalSign 证书在提交资料过程中仍需上传确认函。


#### 方式3
- **域名型（DV）SSL 证书：**
购买证书完成后，请登录 [证书管理控制台](https://console.cloud.tencent.com/certoverview)  ，选择并进入**待提交**管理页面，提交资料并完成域名身份验证后，CA 机构将签发证书。

- **Wotrus 品牌 OV 与 EV 型 SSL 证书：**
购买证书完成后，请登录 [证书管理控制台](https://console.cloud.tencent.com/certoverview)  ，选择并进入**待提交**管理页面，提交资料进行证书预申请，预申请审核通过后需进行域名身份验证，域名验证通过后还需进行人工审核，人工审核通过后 CA 机构将签发证书。详情请查看 [Wotrus 品牌证书 OV 与 EV 型 SSL 证书提交流程](https://intl.cloud.tencent.com/document/product/1007/40206)。

- **DNSPod 品牌国密标准（SM2）OV 与 EV 型 SSL 证书：**
购买证书完成后，请登录 [证书管理控制台](https://console.cloud.tencent.com/certoverview)  ，选择并进入**待提交**管理页面，提交资料并上传确认函以及完成域名身份验证，提交申请后，需人工审核，人工审核通过后 CA 机构将签发证书。


### 步骤3：颁发证书

证书申请通过审核后，CA 机构会为您颁发证书。

### 步骤4：安装证书
1. 重新登录 [SSL 证书控制台](https://console.cloud.tencent.com/ssl)，进入 “我的证书” 管理页面。

2. 选择您需要安装的证书，单击操作栏的**下载**。

3. 下载证书后，将证书解压后安装至您的云服务资源中。具体操作请参考 [证书安装至云服务器](https://intl.cloud.tencent.com/document/product/1007/30173)。
