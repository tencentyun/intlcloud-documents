## 操作场景
本文介绍如何创建、编辑和删除边缘函数，以及如何配置函数的触发规则。

## 创建并部署函数
1. 登录 [边缘安全加速平台](https://console.cloud.tencent.com/edgeone) 控制台，在左侧导航栏中，单击**边缘函数** > **函数管理**。
2. 在边缘函数页面，单击**新建函数**。
3. 在新建边缘函数页面，配置相关参数，单击**创建并部署**。
![](https://qcloudimg.tencent-cloud.cn/raw/3589c7b8d57c4d5228426fb42f52dd2a.png)
参数说明：
 - 函数名称：必填项，只能包含字母、数字、连字符，以字母开头，以数字或字母结尾，2~30个字符。
 - 描述：非必填项，最多支持60个字符。
4. 当弹窗如下对话框，即表示部署成功。
![](https://qcloudimg.tencent-cloud.cn/raw/169e3c72c79b921acfd6b13719e9268d.png)

## 配置触发规则
1. 创建并部署函数成功后，按照提示单击**新增触发规则**。
2. 在新增触发规则页面，按需选择匹配类型、运算符和值。  
![](https://qcloudimg.tencent-cloud.cn/raw/42b6752efec560c43f8b220a43670eed.png)
3. 单击**确定**，即可创建触发规则。
![](https://qcloudimg.tencent-cloud.cn/raw/47572b634cbb916520705d7e98c5d46f.png)

## 编辑边缘函数
1. 如已部署的函数通过验证不符合您的预期，您可在 [边缘函数页面](https://console.cloud.tencent.com/edgeone/edgefunctions)，选择需要修改的函数，单击**详情**，进入函数信息页面，单击**编辑**。
![](https://qcloudimg.tencent-cloud.cn/raw/01e3f361566ba12d3d498f86dae1a800.png)
2. 修改代码后单击**保存并部署**，如此函数已存在触发规则则会提示如下： 
<img src="https://qcloudimg.tencent-cloud.cn/raw/3b6087cf41036e1e0908299ce3930531.png" style="zoom:70%;" />

## 删除边缘函数
1. 如需要删除已新建的函数，您可在 [边缘函数页面](https://console.cloud.tencent.com/edgeone/edgefunctions)，选择需要删除的函数，单击操作列的**删除**。  
![](https://qcloudimg.tencent-cloud.cn/raw/8df886ed3f6ad0032976a2a77439aaf3.png)
2. 在确认删除对话框中，单击**确定**，即可完成删除操作。  
>! 此函数一旦删除不可恢复，已添加的触发规则会一并删除。