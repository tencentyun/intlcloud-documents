
### 如何对项目内资源进行精细化权限管理？
您可以参考 [按标签授权](https://intl.cloud.tencent.com/document/product/598/47827) 对项目内资源进行精细化的权限管理。


### 能否查看项目下所使用的资源？
访问管理 CAM 当前无法直接查看到项目下所使用的资源，您可在 [项目管理](https://console.cloud.tencent.com/project) 中查看消费信息。
![](https://qcloudimg.tencent-cloud.cn/raw/a76b6760667723c351fbeddc31ddbb99.png)
您可在 [控制台总览](https://console.cloud.tencent.com/) 中查看到当前账号下所使用的资源：
![](https://qcloudimg.tencent-cloud.cn/raw/7399078b020486dfa9c3891cd2292383.png)


### 子用户登录腾讯云账号提示“使用证书校验saml失败”如何处理？
子用户登录腾讯云账号时出现证书校验错误请按照如下方法排查：
1. 请先使用 [工具](https://www.samltool.com/validate_response.php) 校验 saml response 格式是否正确。
2. 请检查 saml response 中是否按照文档中的格式提供了必须参数（尤其注意 Role 相关的参数）。
3. 请检查第2步提供的参数是否按照 [使用 SAML 2.0 联合身份用户访问腾讯云管理控制台](https://intl.cloud.tencent.com/document/product/598/32672) 创建了对应的身份提供商和角色。

如仍然无法解决您的问题，请 [提交工单](https://console.intl.cloud.tencent.com/workorder/category) 联系我们。
