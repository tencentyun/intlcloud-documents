容器页面展示容器资产的基线合规情况，包括基线概览、检测信息、容器检测项结果列表。

## 查看容器概览
1. 登录 [容器安全服务控制台](https://console.cloud.tencent.com/tcss)，在左侧导航中，单击**基线管理** > **容器**。
2. 在容器页面，基线概览窗口展示合规容器占比百分比和严重、高危、中危、低危四个威胁等级的检测项数量。
>? 合规容器占比百分比计算逻辑为：合规容器资产数量/容器总数（含检查失败数量）。

![](https://qcloudimg.tencent-cloud.cn/raw/3a2434deb613e9bf5c29f4ab81b3438c.png)
3. 在容器页面，单击百分比中的**查看**，可在弹出的容器抽屉中查看容器资产的检测结果列表。
![](https://qcloudimg.tencent-cloud.cn/raw/f49a2fa88fb61cefaa49880dd0ca4945.png)
4. 在容器抽屉中，单击搜索框，可通过“基线检测项和 ID”关键词对容器资产的检测结果进行查询。
![](https://qcloudimg.tencent-cloud.cn/raw/054fdebd6e44a854f63615034b3402a0.png)
5. 在容器抽屉中，单击![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png)图标勾选所需的容器基线检测项后，单击**重新检查** > **确定**，对选中的容器基线检测项进行重新检测。
![](https://qcloudimg.tencent-cloud.cn/raw/7581a3db59fa5ca44f6d3487a17a744b.png)
6. 在容器抽屉中，单击**基线检测项**，可查看指定容器的基线检测情况。
![](https://qcloudimg.tencent-cloud.cn/raw/77df6c07922a2da0bd8bbfe89cd1d892.png)

## 查看检测信息
1. 登录 [容器安全服务控制台](https://console.cloud.tencent.com/tcss)，在左侧导航中，单击**基线管理** > **容器**。
2. 在容器页面，检测信息窗口展示容器资产最近一次的基线检测时间、检测耗时和自动检测周期配置。
![](https://qcloudimg.tencent-cloud.cn/raw/8c92ffe8e087c229d0f68ab022c4f550.png)
3. 在容器页面，单击**重新检测**，可立即对容器资产进行一次基线检测。
![](https://qcloudimg.tencent-cloud.cn/raw/7b82a3a6979d23c615156d6bb7102186.png)
4. 在容器页面，单击**基线设置**，可设置基线策略和基线忽略列表。
![](https://qcloudimg.tencent-cloud.cn/raw/d929438f40c2b787fb14e649860d47dd.png)

### 设置基线策略
基线策略设置展示当前资产检测的基线标准，基线检查项数量。
1. 在基线策略设置页面，可通过单击![](https://main.qcloudimg.com/raw/9053f4e9bc709aa720fccd5045eb8cd0.png)图标开关开启或关闭当前基线标准的周期性检测。
![](https://qcloudimg.tencent-cloud.cn/raw/50f39ad938444c89f3ff54a7d70fdf04.png)
2. 在基线策略设置页面，单击**检测周期设置**，弹出检测周期设置弹窗，可在检测周期设置弹窗中设定检测周期。
![](https://qcloudimg.tencent-cloud.cn/raw/1e0edd49fe6d07246b0faa760a8c0ccb.png)
3. 在检测周期设置弹窗，可设置检测周期为：1天、3天、7天，以及设定具体时间点。
<img src="https://qcloudimg.tencent-cloud.cn/raw/dc5e798e4d088b594f5ec20752431e82.png" style="zoom:67%;" />
4. 单击**确定**，即可完成检测周期设置。

### 基线忽略列表
基线忽略列表展示了忽略的容器基线检测项。
1. 在基线忽略列表页面，单击搜索框，可通过“基线检测项”关键词对容器基线检测项进行查询。
<img src="https://qcloudimg.tencent-cloud.cn/raw/a57c2df4ec45ad236b8f3603a2cdd911.png" style="zoom:67%;" />
2. 在基线忽略列表页面，单击![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png)图标勾选所需的容器基线检测项后，单击**取消忽略**，将会对选中的容器基线检测项取消忽略。
>? 检测项取消忽略后，检测内容将恢复正常检测。

## 查看检测结果列表
### 筛选刷新基线检测项
1. 登录 [容器安全服务控制台](https://console.cloud.tencent.com/tcss)，在左侧导航中，单击**基线管理** > **容器**。
2. 在容器页面，单击搜索框，可通过“ID 和基线检测项”关键词对容器基线检测项进行查询。
<img src="https://qcloudimg.tencent-cloud.cn/raw/9b176d794d544082cf5b3946c484e1ef.png" style="zoom:67%;" />
3. 在容器页面，单击左上角的类型下拉框，按类型对容器基线检测项进行筛选。
<img src="https://qcloudimg.tencent-cloud.cn/raw/377965051b57173419d9d49d13f0efaf.png" style="zoom:67%;" />
4. 在容器页面，单击左上角的威胁等级下拉框，按威胁等级对容器基线检测项进行筛选。
<img src="https://qcloudimg.tencent-cloud.cn/raw/9e1faad620683c83078bf40c5f1df7c6.png" style="zoom:67%;" />
3.在容器页面，单击操作栏右侧![](https://main.qcloudimg.com/raw/84b6cc4d2eabf9ed7fc0bea43503bb1d.png)图标，即可刷新容器基线检测项。

### 重新检测基线检测项
1. 登录 [容器安全服务控制台](https://console.cloud.tencent.com/tcss)，在左侧导航中，单击**基线管理** > **容器**。
2. 在容器页面，单击![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png)图标勾选所需容器基线检测项后，单击**重新检测** > **确认**，可对容器基线检测项产进行重新检测。
>? 选定多个容器基线检测项，单击②处的**重新检测**，可进行批量检测。

![](https://qcloudimg.tencent-cloud.cn/raw/97bbdf4d8983d16faa5f33df94880be9.png)

### 忽略基线检测项
1. 登录 [容器安全服务控制台](https://console.cloud.tencent.com/tcss)，在左侧导航中，单击**基线管理** > **容器**。
2. 在容器页面，单击![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png)图标勾选所需基线检测项后，单击**忽略** > **确定**，可对基线检测项进行忽略。
>? 选定多个基线检测项，单击②处的**忽略**，可进行批量忽略。

![](https://qcloudimg.tencent-cloud.cn/raw/19eaa1b115dcc167415fec3220224e2d.png)

### 自定义列表管理
1. 登录 [容器安全服务控制台](https://console.cloud.tencent.com/tcss)，在左侧导航中，单击**基线管理** > **容器**。
2. 在容器页面，单击![](https://main.qcloudimg.com/raw/d42b27540eef9bf90a9e30f96b500bf3.png)图标，弹出自定义列表管理弹窗，在弹窗中可以自定义设定列表管理。
3. 在自定义列表管理弹窗，选择所需的类型后，单击**确定**，即可完成设置自定义列表管理。
<img src="https://qcloudimg.tencent-cloud.cn/raw/1654a9c6e0e0e43a6f11b1e95d12c97c.png" style="zoom:67%;" />

#### 列表重点字段说明
1. 基线检测项：单击“基线检测项	”，可查看检测项详情。
1. 未通过检测项：未通过的检测项数量。
2. 检测结果：存在未通过的检测项检测结果为未通过，所有检测项通过则检测结果为已通过。
3. 最近检测时间：最近一次的检测时间。
