## 概述

腾讯云 SSL 证书提供 API 接口申请 SSL 付费证书，本文档将指导您如何使用 SSL 证书 API 接口申请付费证书的具体流程。

## 前提条件

已注册腾讯云账号。 

## 证书 API 接口申请流程

由于证书品牌及类型原因，证书 API 接口申请流程具有一定差异，请根据您的实际需求申请证书的品牌和类型。


### 付费 DV 型证书 API 接口申请流程

请您按照流程图调用相关 SSL 证书接口，CA 机构会审核相关材料并联系您完成人工审核。
证书签发后可通过下载证书（DownloadCertificate）接口进行证书下载操作。如下图所示：
![](https://main.qcloudimg.com/raw/3e66184ff219d6c9031a0ab468f5707a.png)

### GeoTrust、SecureSite、TrustAsia、GlobalSign 品牌 OV/EV 型证书 API 接口申请流程

请您按照流程图调用相关 SSL 证书接口，CA 机构会审核相关确认函材料并联系您完成域名验证操作。具体验证操作请参考 [DNS 验证](https://intl.cloud.tencent.com/document/product/1007/45895) 或 [文件验证](https://intl.cloud.tencent.com/document/product/1007/43542)。
证书签发后可通过下载证书（DownloadCertificate）接口进行证书下载操作。如下图所示：
![](https://main.qcloudimg.com/raw/61d621dcdc7f5430a6809f29c6383aec.png)

### WoTrus 品牌付费 OV/EV 型证书 API 接口申请流程

请您按照流程图调用相关 SSL 证书接口，CA 机构会审核相关材料并联系您完成人工审核。
证书签发后可通过下载证书（DownloadCertificate）接口进行证书下载操作。如下图所示：
![](https://main.qcloudimg.com/raw/c484b304196d476495c3c62856011bcf.png)
