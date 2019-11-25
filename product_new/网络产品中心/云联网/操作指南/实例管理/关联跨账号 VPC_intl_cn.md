关联跨账号私有网络，需要由跨账号 VPC 侧发起申请，云联网所在账号同意 / 拒绝申请即可。 
操作流程如下图所示：
![0](https://main.qcloudimg.com/raw/c351b9e558517ee4d432f16ef4bd5448.png)
## 申请加入云联网（VPC 账号操作）
1. 登录 [腾讯云控制台](https://console.cloud.tencent.com/)，选择【云产品】>【网络】>【私有网络】，进入私有网络控制台。 
2. 单击左侧目录中的【私有网络】，在列表中找到需要加入云联网的私有网络 VPC，单击其 ID 进入详情页。 
3. 单击【立即关联】。
![](https://main.qcloudimg.com/raw/a17881a5c0441e3f1e834d8e7e0a0f98.png)
4. 在弹窗中，填写对端的账号 ID 和云联网 ID，单击【确定】，提交申请 。
 ![2](https://main.qcloudimg.com/raw/2a9c18546c2a1c0442564ff8445c438c.png)

## 同意申请（云联网账号操作）
1. 登录 [腾讯云控制台](https://console.cloud.tencent.com/)，选择【云产品】>【网络】>【私有网络】，进入私有网络控制台。 
2. 单击左侧目录中的【云联网】，在列表中找到有待同意申请的云联网实例，单击其 ID 进入详情页。 
3. 在“关联实例”页面，会显示待同意的 VPC 信息，单击【同意】并确认操作，即可将该 VPC 加入到云联网中。 
![](https://main.qcloudimg.com/raw/00e77fe68fb24e1de8f3ead93fcbea46.png)

## 检查路由表（可选）
同意申请并关联成功后，您还需检查路由表，避免该实例与云联网中已有实例因网段冲突而导致路由未生效的情况。 
相关操作请参见 [检查路由表](https://intl.cloud.tencent.com/document/product/1003/30066)。

## 设置跨域互通带宽（可选）
相关操作请参见 [设置跨域互通带宽](https://intl.cloud.tencent.com/document/product/1003/30073)。
