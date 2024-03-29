## 操作场景
服务发布之后，您还需要创建密钥对和使用计划，并与服务环境进行绑定，才能调用成功。
本文以特定用户的使用计划为例，提供从配置使用计划到提供给用户使用的完整示例。

## 前提条件
1. 已完成 [服务创建](https://intl.cloud.tencent.com/document/product/628/11787)、[API 创建和调试](https://intl.cloud.tencent.com/document/product/628/11795)，确保 API 有效可响应。
2. 已 [发布服务](https://intl.cloud.tencent.com/document/product/628/11809) 到某一环境中，例如发布环境 release。

## 操作步骤
### 创建密钥对
1. 登录 [API 网关控制台](https://console.cloud.tencent.com/apigateway/index)，在左侧菜单栏单击**应用**，进入应用管理页面。
2. 在应用管理页面，单击页面上方的**密钥**，切换到密钥管理标签页。
3. 在密钥管理标签页，单击**新建**，在弹出的对话框中选择密钥类型并填写以下信息。
<dx-tabs>
::: 自动生成密钥
填写密钥名即可。
密钥名：最长50个字符，支持字母、数字、下划线
:::
::: 自定义密钥
填写密钥名、SecretId 和 SecretKey。
- 密钥名：最长50个字符，支持字母、数字、下划线、中横线
- SecretId：5-50个字符，支持字母、数字、下划线、中划线
- SecretKey：10-50个字符，支持字母、数字、下划线、中划线
:::
</dx-tabs>
4. 单击**提交**，系统会自动生成或保存您自定义的密钥对（SecretId 和 SecretKey）。
![](https://main.qcloudimg.com/raw/774299c4fa7afdc0db1247a7d26f02f4.png)

### 创建使用计划
1. 在左侧菜单栏单击 **[使用计划](https://console.cloud.tencent.com/apigateway/plan)**，进入使用计划的列表页。
2. 在页面左上角，单击**新建**，根据提示填写配置信息。
3. 单击**提交**，完成创建。

### 绑定使用计划和密钥对
1. 在 **[使用计划](https://console.cloud.tencent.com/apigateway/plan)** 页面，单击目标使用计划的 ID，进入详情页的使用计划信息。
2. 在使用计划信息页，单击**绑定密钥**。
3. 勾选需要绑定的 SecretId，单击**提交**，完成使用计划和密钥对的绑定。
![](https://main.qcloudimg.com/raw/774299c4fa7afdc0db1247a7d26f02f4.png)

### 绑定使用计划和服务环境
1. 在 **[服务](https://console.cloud.tencent.com/apigateway/service)** 列表页面，选择已创建的服务，切换到使用计划标签页，单击**绑定**。
![](https://main.qcloudimg.com/raw/a2c9314e9fb5fa9d72d8a5a7a8f2bebe.png)
2. 在绑定使用计划的窗口中，选择要绑定的生效环境和使用计划。
生效环境：发布、预发布、测试
3. 单击**提交**，完成使用计划和服务环境的绑定。
![](https://main.qcloudimg.com/raw/b831f08fab2563c4d07d175ffcb093c5.png)
>!如果两个使用计划需要绑定到同一个环境，则这两个使用计划不能绑定相同的密钥对。

完成上述步骤后，就可以将创建好的 SecretId 和 SecretKey 提供给最终用户。最终用户可以通过服务的二级域名（或增加绑定的私有域名），使用提供的 SecretId 和 SecretKey 认证，访问服务内发布的 API。
