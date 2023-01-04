异常进程是基于自适应学习技术，通过系统规则和用户自定义检测规则，实时监控进程异常启动行为，并实时告警通知或拦截。异常进程包含事件列表和规则配置两大模块。本文档介绍高级防御的规则配置功能。

## 筛选刷新规则
1. 登录 [容器安全服务控制台](https://console.cloud.tencent.com/tcss)，在左侧导航中，单击**高级防御** > **异常进程** > **规则配置**，进入规则配置页面。
2. 在规则配置页面，单击搜索框，可通过“规则名称”关键词对配置规则进行查询。
![](https://qcloudimg.tencent-cloud.cn/raw/c29e8d57105c9b08960a9a4d14b0efa7.png)
3. 在规则配置页面，单击操作栏右侧![](https://main.qcloudimg.com/raw/84b6cc4d2eabf9ed7fc0bea43503bb1d.png)图标，即可刷新规则列表。

## 新增规则
1. 登录 [容器安全服务控制台](https://console.cloud.tencent.com/tcss)，在左侧导航中，单击**高级防御** > **异常进程** > **规则配置**，进入规则配置页面。
2. 在规则配置页面，单击**创建规则**，右侧抽屉弹出新增规则页面。
<img src="https://qcloudimg.tencent-cloud.cn/raw/7953fc514320e3c19c865744b0f0ffd0.png" style="zoom:67%;" />
3. 在新增规则页面，需配置基本信息、配置规则和镜像生效范围。
 - 基本信息：输入事件的规则名称，单击![](https://main.qcloudimg.com/raw/9053f4e9bc709aa720fccd5045eb8cd0.png)图标开启或关闭规则检查。
>? 关闭后，将不再进行该规则检测！

![](https://qcloudimg.tencent-cloud.cn/raw/27cf3c930bf2a7dd28e8e46213c81304.png)
 - 配置规则：需输入进程路径和执行动作。单击**添加**或**删除**，可进行添加或删除规则。
>?
>- 配置规则最多可添加30条。
>- 执行动作有：
>  - 拦截：命中规则条件时，将自动拦截进程运行，记录事件详情。
>  - 告警：命中规则条件时，仅自动告警事件，不拦截进程运行，记录事件详情。
>  - 放行：命中规则条件时，将自动放行进程运行，不产生事件记录。	

 - 镜像范围：全部镜像和自选镜像。其中单击所需的自选镜像![](https://main.qcloudimg.com/raw/37d813d17a69271ce31b3233ad0a949e.png)或![](https://main.qcloudimg.com/raw/be9e47bccb644d8a099149bac4aef1e0.png)图标，即可选中或删除自选镜像。
>? 支持按住 shift 键进行多选。

 ![](https://qcloudimg.tencent-cloud.cn/raw/0abb56b89008e45c97729b71b39d6add.png)
4. 选择所需内容后，单击**设置**或**取消**，即可完成或取消设置。

## 复制规则
1. 登录 [容器安全服务控制台](https://console.cloud.tencent.com/tcss)，在左侧导航中，单击**高级防御** > **异常进程** > **规则配置**，进入规则配置页面。
2. 在规则配置页面，单击右侧**复制**，右侧弹出复制规则页面。
![](https://qcloudimg.tencent-cloud.cn/raw/3bfb95e0f3efb76350b09f554396507c.png)
3. 在复制规则页面，需输入规则名称，可修改启用状态、配置规则和镜像生效范围。
![](https://qcloudimg.tencent-cloud.cn/raw/974d0beb1971db02649617d450084f59.png)
4. 选择所需内容后，单击**确定**或**取消**，即可完成或取消复制规则。


## 编辑规则
1. 登录 [容器安全服务控制台](https://console.cloud.tencent.com/tcss)，在左侧导航中，单击**高级防御** > **异常进程** > **规则配置**，进入规则配置页面。
2. 在规则配置页面，单击右侧**编辑**，右侧弹出编辑规则设置页面。
![](https://qcloudimg.tencent-cloud.cn/raw/1b6ebaf254df4508307b4c5f985df5cc.png)
3. 在编辑规则设置页面，可修改规则的基本信息、配置规则和镜像生效范围。
![](https://qcloudimg.tencent-cloud.cn/raw/948140a88f137e45044f96ac70bff31b.png)
4. 选择所需内容后，单击**确定**或**取消**，即可完成或取消修改规则。


## 删除规则
1. 登录 [容器安全服务控制台](https://console.cloud.tencent.com/tcss)，在左侧导航中，单击**高级防御** > **异常进程** > **规则配置**，进入规则配置页面。
2. 在规则配置页面，可选择如下两种方式删除规则：
 - 选择所需的规则单击![](https://main.qcloudimg.com/raw/37d813d17a69271ce31b3233ad0a949e.png)图标，后单击操作栏左侧**删除**，弹出“确认删除”弹窗。
![](https://qcloudimg.tencent-cloud.cn/raw/51136a3342f796aa5f8ed58657184124.png)
 - 选择所需规则的所作行，单击右侧**删除**，弹出“确认删除”弹窗。
![](https://qcloudimg.tencent-cloud.cn/raw/de865ee03cdbe5234ff24e74ea54cbd7.png)
2. 在“确认删除”弹窗中，单击**删除**或**取消**，即可删除或取消删除规则。
>? 删除后，规则将无法恢复，该规则的关联镜像将自动关联系统默认规则。

## 导出规则
1. 登录 [容器安全服务控制台](https://console.cloud.tencent.com/tcss)，在左侧导航中，单击**高级防御** > **异常进程** > **规则配置**，进入规则配置页面。
2. 在规则配置页面，单击![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png)图标勾选所需的异常进程规则后，单击![](https://main.qcloudimg.com/raw/24d375a75e4ee95c77910d101f7203dd.png)图标即可导出异常进程规则。
>? 单击操作栏处![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png)图标，可进行批量勾选。

![](https://qcloudimg.tencent-cloud.cn/raw/bda1849aff54d9a116a5f15eb1d74ac0.png)


## 自定义列表管理
1. 登录 [容器安全服务控制台](https://console.cloud.tencent.com/tcss)，在左侧导航中，单击**高级防御** > **异常进程** > **规则配置**，进入规则配置页面。
2. 在规则配置页面，单击![](https://main.qcloudimg.com/raw/d42b27540eef9bf90a9e30f96b500bf3.png)图标，弹出自定义列表管理弹窗，在弹窗中可以自定义设定列表管理。
3. 在自定义列表管理弹窗，选择所需的类型后，单击**确定**，即可完成设置自定义列表管理。
<img src="https://qcloudimg.tencent-cloud.cn/raw/07cf68282b79f005d5f2b74c42985edc.png" style="zoom:67%;" />

### 列表重点字段说明
1. 规则类别：系统规则或自定义规则。
2. 生效镜像：规则生效的镜像数量。单击生效镜像“数字”，右侧抽屉展示规则详情。
![](https://qcloudimg.tencent-cloud.cn/raw/a2aa5b3d703709882bbffd76270b37d7.png)
3. 状态：启用/禁用。
4. 操作：系统策略操作栏仅复制规则，用户自定义规则支持复制、编辑和删除。
