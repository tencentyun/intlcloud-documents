## 操作场景

当您创建投递到 COS/Ckafka 的任务时，因为涉及云产品之间的访问，需要您授权日志服务（Cloud Log Service，CLS）服务角色访问 COS/CKafka 的权限。大部分用户通过控制台操作，系统会引导用户完成授权，小部分用户会直接使用 API，这时候需要手动去授权。手动授权之前，可以先通过以下步骤检查是否已经完成了对 CLS 服务角色的授权。

## 检查是否已经授权 CLS

1. 登录访问管理控制台，选择左侧导航栏中的 **[角色](https://console.cloud.tencent.com/cam/role)**。
2. 在“角色”页面中，查看是否存在 `CLS_QcsRole` 角色。可通过列表右上角的搜索框进行搜索。
3. 单击角色名称，进入角色详情页。
 - 选择**权限**，查看是否已具备 `QcloudCOSAccessForCLSRole` 及 `QcloudCKAFKAAccessForCLSRole` 权限。
 - 选择**角色载体**，查看角色载体是否为 `cls.cloud.tencent.com`。
若不具备角色及相关权限，则请参考下文进行创建。

## 操作步骤

### 授权 CLS 访问权限

您可通过以下方式授权CLS投递 COS/Ckafka 权限：

<dx-tabs>
::: 通过控制台自动创建
您在首次通过控制台创建投递到 COS/Ckafka 的任务时，请根据页面指引创建角色和策略：
1. 在弹出的“该功能需创建服务角色”窗口中，单击**前往访问管理**。
2. 在“角色管理”页面中，单击**同意授权**。
:::
::: 使用访问管理手动创建
1. 登录访问管理控制台，选择左侧导航栏中的 **[角色](https://console.cloud.tencent.com/cam/role)**。
2. 在“角色”页面中，单击**新建角色**。
3. 在弹出的“选择角色载体”窗口中，选择**腾讯云产品服务**。
4. 在“新建自定义角色”中，进行如下配置：
 1. 在“输入角色载体信息”中，勾选“日志服务 (cls)”，并单击**下一步**。
 2. 在“配置角色策略”中，使用 `clsrole` 进行搜索，并在结果中勾选 `QcloudCKAFKAAccessForCLSRole` 及 `QcloudCOSAccessForCLSRole` 策略后，单击**下一步**。
 3. 在“审阅”中，输入角色名 `CLS_QcsRole`，并单击**完成**。

:::
</dx-tabs>

至此您已完成 CLS 服务角色访问 COS/Ckafka 的授权。若您是主账号，则可直接进行投递操作；若您是子账号或协作者账号，需要主账号授予您投递 COS/Ckafka 的权限，授权步骤参考[基于 CAM 管理权限](https://intl.cloud.tencent.com/document/product/614/32854)， 复制授权策略参考 [自定义权限策略示例](https://intl.cloud.tencent.com/document/product/614/45004)。




