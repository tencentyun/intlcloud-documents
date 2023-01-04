白名单管理展示模块中提供配置白名单接口和白名单展示列表。

## 筛选刷新白名单
1. 登录 [容器安全服务控制台](https://console.cloud.tencent.com/tcss)，在左侧导航中，单击**高级防御** > **高危系统调用** > **白名单管理**，进入白名单管理页面。
2. 在白名单管理页面，单击搜索框，可通过“进程路径、系统调用名称”关键词对配置的白名单进行查询。
![](https://qcloudimg.tencent-cloud.cn/raw/3af7f9a072e7259e4d5ffffc1aa4deb2.png)
3. 在白名单管理页面，单击操作栏右侧![](https://main.qcloudimg.com/raw/84b6cc4d2eabf9ed7fc0bea43503bb1d.png)图标，即可刷新白名单管理列表。

## 新增白名单
1. 登录 [容器安全服务控制台](https://console.cloud.tencent.com/tcss)，在左侧导航中，单击**高级防御** > **高危系统调用** > **白名单管理**，进入白名单管理页面。
2. 在白名单管理页面，单击**新增白名单**，右侧弹出新增白名单设置页面。
![](https://qcloudimg.tencent-cloud.cn/raw/bf7552706d1f26034c719fe625826e81.png)
3. 在新增白名单设置页面，需配置白名单生效的进程路径、系统调用名称和生效范围。
   - 单击进程路径和系统调用名称左侧![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png)图标，输入进程路径，并选择系统调用名称。
>? 进程路径不能为空。

  ![](https://qcloudimg.tencent-cloud.cn/raw/060e1bf87ac7a95c29f9d3907fb26dd0.png)
   - 白名单生效范围为全部镜像或自选镜像。其中单击所需的自选镜像![](https://main.qcloudimg.com/raw/37d813d17a69271ce31b3233ad0a949e.png)或![](https://main.qcloudimg.com/raw/be9e47bccb644d8a099149bac4aef1e0.png)图标，即可选中或删除自选镜像。
>? 支持按住 shift 键进行多选。

   ![](https://qcloudimg.tencent-cloud.cn/raw/af04a100e2244f44bd54c622c4417f71.png)
4. 选择所需内容后，单击**确定**或**取消**，即可完成或取消新增白名单。

## 编辑白名单
1. 登录 [容器安全服务控制台](https://console.cloud.tencent.com/tcss)，在左侧导航中，单击**高级防御** > **高危系统调用** > **白名单管理**，进入白名单管理页面。
2. 在白名单管理页面，单击右侧**编辑**，右侧弹出编辑白名单设置页面。
![](https://qcloudimg.tencent-cloud.cn/raw/265a29fb233439ffd391ea8a5fbad3b3.png)
3. 在编辑白名单设置页面，可修改白名单生效的进程路径、系统调用名称和生效范围。  
![](https://qcloudimg.tencent-cloud.cn/raw/549e549ae6b9e422fe63af687d99fd84.png)
4. 选择所需内容后，单击**确定**或**取消**，即可完成或取消修改白名单。

## 删除白名单
1. 登录 [容器安全服务控制台](https://console.cloud.tencent.com/tcss)，在左侧导航中，单击**高级防御** > **高危系统调用** > **白名单管理**，进入白名单管理页面。
2. 在白名单管理页面，单击右侧**删除**，弹出“确认删除”弹窗。
![](https://qcloudimg.tencent-cloud.cn/raw/a0b4718e31b3a45c87ff72050d3115c1.png)
3. 在“确认删除”弹窗中，单击**删除**或**取消**，即可删除或取消删除白名单。
>? 删除后，白名单将无法恢复，该白名单的关联镜像触发系统策略时将再次产生告警。

## 自定义列表管理
1. 登录 [容器安全服务控制台](https://console.cloud.tencent.com/tcss)，在左侧导航中，单击**高级防御** > **高危系统调用** > **白名单管理**，进入白名单管理页面。
2. 在白名单管理页面，单击![](https://main.qcloudimg.com/raw/d42b27540eef9bf90a9e30f96b500bf3.png)图标，弹出自定义列表管理弹窗，在弹窗中可以自定义设定列表管理。
3. 在自定义列表管理弹窗，选择所需的类型后，单击**确定**，即可完成设置自定义列表管理。
<img src="https://qcloudimg.tencent-cloud.cn/raw/78d398e43f2ba372a820c01d2b92360b.png" style="zoom:67%;" />

### 列表重点字段说明
1. 镜像数：白名单生效的镜像。
2. 进程路径：白名单生效的进程路径。
3. 系统调用名称：白名单生效的系统调用名称。
4. 操作：用户可编辑、删除白名单。
