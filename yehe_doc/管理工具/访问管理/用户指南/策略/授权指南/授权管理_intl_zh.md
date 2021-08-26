## 操作场景
创建用户/用户组时，默认没有任何权限，您可以通过为其关联策略，使用户/用户组获得对应的操作权限。


## 前提条件
- 已 [创建子用户](https://intl.cloud.tencent.com/document/product/598/13674) / [用户组](https://intl.cloud.tencent.com/document/product/598/33380)。
- 如果需要关联自定义策略，请先 [创建自定义策略](https://intl.cloud.tencent.com/document/product/598/35596)。

## 操作步骤
您可以通过策略关联用户/用户组，或者通过用户/用户组关联策略，两种方式操作入口有区别，实现的功能无区别。

### 通过策略关联用户/用户组
<dx-tabs>
::: 通过策略关联用户
1. 在访问管理控制台的【[策略](https://console.cloud.tencent.com/cam/policy)】页面，选择策略类型。
>?本示例以【预设策略】为例，您也可以选择【自定义策略】。
2. 通过搜索筛选需要授权的预设策略，单击操作列的【关联用户/组】。
![](https://main.qcloudimg.com/raw/c3c39a4e97345a3b31728f0e1b0ed379.png)
3. 在弹出的关联用户/用户组窗口，勾选要关联的用户，单击【确定】，完成通过策略关联用户操作。
![](https://main.qcloudimg.com/raw/59476a8d463f448046cca3362deaae7c.png)
:::
::: 通过策略关联用户组
1. 在访问管理控制台的【[策略](https://console.cloud.tencent.com/cam/policy)】页面，选择策略类型。
>?本示例以【预设策略】为例，您也可以选择【自定义策略】。
2. 通过搜索筛选需要授权的预设策略，单击操作列的【关联用户/组】。
![](https://main.qcloudimg.com/raw/c3c39a4e97345a3b31728f0e1b0ed379.png)
3. 在弹出的关联用户/用户组窗口，单击【切换用户组】。
4. 勾选要关联的用户组，单击【确定】，完成通过策略关联用户组操作。
![](https://main.qcloudimg.com/raw/65c0a435424d34db5e6b529e07ca1e99.png)
:::
</dx-tabs>


### 通过用户/用户组关联策略

<dx-tabs>
::: 通过用户关联策略
1. 在访问管理控制台的【用户】>【[用户列表](https://console.cloud.tencent.com/cam)】页面，找到需要授权的用户，单击操作列的【授权】，进入关联策略页面。
![](https://main.qcloudimg.com/raw/a29dc8dd4c1a7e587140b9dfeb101b58.png)
2. 在关联策略页面，选择策略类型。
>?默认展示全部策略，您可以筛选自定义策略或预设策略，方便查找具体的策略信息。
3. 勾选需要授权的策略，单击【确定】，完成通过用户关联预设策略操作。
![](https://main.qcloudimg.com/raw/a743ce549be775bd50b42296c03af43b.png)
:::
::: 通过用户组关联策略
1. 在访问管理控制台的【[用户组](https://console.cloud.tencent.com/cam/groups)】页面，单击目标用户组名称，进入用户组详情页。
2. 在用户组详情页，单击【关联策略】，进入关联策略页面。
![](https://main.qcloudimg.com/raw/78e647a8af6f34e96c384e5f02fd15d0.png)
3. 在关联策略页面，选择策略类型。
>?默认展示全部策略，您可以筛选自定义策略或预设策略，方便查找具体的策略信息。
4. 勾选需要授权的策略，单击【确定】，完成通过用户关联预设策略操作。
![](https://main.qcloudimg.com/raw/a743ce549be775bd50b42296c03af43b.png)
:::
</dx-tabs>

## 关联文档

 如果您想了解策略概念，请参阅 [策略相关定义](https://intl.cloud.tencent.com/document/product/598/10601)。 

