
本文档介绍云服务器因安全组设置问题导致无法远程连接的排查方法和解决方案。

## 检查工具

您可以通过腾讯云提供的 [安全组（端口）验通工具](https://console.cloud.tencent.com/vpc/helper) 判断无法远程连接是否与安全组设置相关。
1. 登录 [安全组（端口）验通工具](https://console.cloud.tencent.com/vpc/helper)。
2. 在**实例端口验通**页面，选择您需要检测的实例，单击【一键检测】。如下图所示：
![](https://main.qcloudimg.com/raw/a792a1692e0a21b3f9dfe111d4b86789.png)
如果该实例检测出有未放通的端口，可以通过【一键放通】功能放通服务器常用端口，并再次尝试远程登录。
<img src="https://main.qcloudimg.com/raw/a743739b5885874c15a6b5c7869f5acd.png" height="400" width="420">


## 修改安全组设置

如果通过工具检查，确认为安全组端口设置问题，但您不想通过【一键放通】功能放通所有云服务器的常用端口，或者您需要自定义远程登录端口，您还可以通过自定义配置安全组的入站和出站规则，解决无法远程连接的问题。具体操作请参考 [修改安全组规则](https://intl.cloud.tencent.com/document/product/213/34825)。
