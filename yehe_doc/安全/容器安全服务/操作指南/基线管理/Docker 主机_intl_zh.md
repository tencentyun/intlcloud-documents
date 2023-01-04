Docker 主机页面展示主机资产的基线合规情况，包括基线概览、检测信息、主机检测项结果列表。

## 查看 Docker 主机概览
1. 登录 [容器安全服务控制台](https://console.cloud.tencent.com/tcss)，在左侧导航中，单击**基线管理** > **Docker 主机**。
2. 在 Docker 主机页面，基线概览窗口展示合规主机占比百分比中严重、高危、中危、低危四个威胁等级的检测项数量。
>? 合规 Docker 主机占比百分比计算逻辑为：合规 Docker 主机资产数量/Docker 主机总数（含检查失败数量）。

![](https://qcloudimg.tencent-cloud.cn/raw/20f6a4f66da98b0c446ecd839addf232.png)
3. 在 Docker 主机页面，单击百分比中的**查看**，可在弹出的主机抽屉中查看主机资产的检测结果列表。
4. 在 Docker 主机抽屉中，单击搜索框，可通过“基线检测项和 ID”关键词对主机资产的检测结果进行查询。
![](https://qcloudimg.tencent-cloud.cn/raw/f42b3c4a6ccfd620cd738091c512c8b7.png)
5. 在 Docker 主机抽屉中，单击![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png)图标勾选所需的 Docker 主机基线检测项后，单击**重新检测** > **确定**，将会对选中的基线检测项进行重新检测。
>? 选定多个主机基线检测项，单击②处的**重新检测**，可进行批量重新检测。

![](https://qcloudimg.tencent-cloud.cn/raw/a3360909cb6076aaa584a883c2c220c8.png)
6. 在 Docker 主机抽屉中，单击**基线检测项**，可查看指定 Docker 主机的基线检测情况。
![](https://qcloudimg.tencent-cloud.cn/raw/702b7e8c1070f5c0350e2e0d8067dddd.png)

## 查看检测信息
1. 在 Docker 主机页面，检测信息窗口展示主机资产最近一次的基线检测时间、检测耗时和自动检测周期配置。
![](https://qcloudimg.tencent-cloud.cn/raw/28b81698276618f55f4d6f9287874deb.png)
2. 在 Docker 主机页面，单击**重新检测**，可立即对主机资产进行一次基线检测。
![](https://qcloudimg.tencent-cloud.cn/raw/2b963706ac58cea9050402553d84e3ec.png)
3. 在 Docker 主机页面，单击**基线设置**，可设置基线策略和基线忽略列表。
![](https://qcloudimg.tencent-cloud.cn/raw/fdd13194c19a1bd0b2e21e03a539741d.png)

### 设置基线策略
基线策略设置展示当前资产检测的基线标准，基线检查项数量。
1. 在基线策略设置页面，可通过单击![](https://qcloudimg.tencent-cloud.cn/raw/5e6cbf6d522b288cdd3c901e63ffc416.png)图标开关开启或关闭当前基线标准的周期性检测。
2. 在基线策略设置页面，单击检测周期的**编辑**，弹出检测周期设置弹窗，可在检测周期设置弹窗中设定检测周期。
![](https://qcloudimg.tencent-cloud.cn/raw/695a6f1da2751aad52d65e8ff53d1c38.png)
3. 在检测周期设置弹窗，可设置检测周期为：1天、3天、7天，以及设定具体时间点。
<img src="https://qcloudimg.tencent-cloud.cn/raw/8e422b986b9e40605e3a29a9bedf6997.png" style="zoom:67%;" />
4. 单击**确定**，即可完成检测周期设置。

### 基线忽略列表
基线忽略列表展示了忽略的主机基线检测项。
1. 在基线忽略列表页面，单击搜索框，可通过“基线检测项、主机名称、主机 IP”关键词对主机基线检测项进行查询。
![](https://qcloudimg.tencent-cloud.cn/raw/2c370630a0f1489a9259a73d57ff884d.png)
2. 在基线忽略列表页面，单击![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png)图标勾选所需的主机基线检测项后，单击**取消忽略**，将会对选中的主机基线检测项取消忽略。
>? 检测项取消忽略后，检测内容将恢复正常检测。

## 查看检测结果列表
### 筛选刷新基线检测项
1. 在 Docker 主机页面，单击搜索框，可通过“ID 和基线检测项”关键词对 Docker 主机基线检测项进行查询。
![](https://qcloudimg.tencent-cloud.cn/raw/cc235c93d7649fd18a2125504d9097cf.png)
2. 在 Docker 主机页面，单击左上角的类型下拉框，按类型对 Docker 主机基线检测项进行筛选。
<img src="https://qcloudimg.tencent-cloud.cn/raw/4091bfe54b69562d999899439d7d12ed.png" style="zoom:67%;" />
3. 在 Docker 主机页面，单击左上角的威胁等级下拉框，按威胁等级对 Docker 主机基线检测项进行筛选。
<img src="https://qcloudimg.tencent-cloud.cn/raw/11430b1a4d9a33c8cc344c7525f473f7.png" style="zoom:67%;" />
4. 在 Docker 主机页面，单击操作栏右侧![](https://main.qcloudimg.com/raw/84b6cc4d2eabf9ed7fc0bea43503bb1d.png)图标，即可刷新事件列表。

### 重新检测基线检测项
在 Docker 主机页面，单击![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png)图标勾选所需 Docker 主机基线检测项后，单击**重新检测** > **确认**，可对主机基线检测项进行重新检测。
>? 选定多个主机基线检测项，单击②处的**重新检测**，可进行批量检测。

![](https://qcloudimg.tencent-cloud.cn/raw/e829e61548f0058173bb5324eb1e65ad.png)

### 忽略基线检测项
在 Docker 主机页面，单击![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png)图标勾选所需基线检测项后，单击**忽略** > **确定**，可对基线检测项进行忽略。
>? 选定多个基线检测项，单击②处的**忽略**，可进行批量忽略。

![](https://qcloudimg.tencent-cloud.cn/raw/598413d2e82af3dc0f0ff97ee7917981.png)

### 自定义列表管理
1. 在 Docker 主机页面，单击![](https://main.qcloudimg.com/raw/d42b27540eef9bf90a9e30f96b500bf3.png)图标，弹出自定义列表管理弹窗，在弹窗中可以自定义设定列表管理。
3. 在自定义列表管理弹窗，选择所需的类型后，单击**确定**，即可完成设置自定义列表管理。
<img src="https://qcloudimg.tencent-cloud.cn/raw/33d2472985cb38fe32c8a5ed8e88b048.png" style="zoom:67%;" />

#### 列表重点字段说明
1. ID：检测项ID，该ID全局唯一。
2. 基线检测项：检测内容，单击“ 基线检测项”，可查看检测项详情。
3. 类型：检测项的类型。
4. 基线标准：检测项所属基线标准。
5. 威胁等级：检测项的威胁等级定义，含严重、高危、中危、底危、提示。
6. 检测结果：展示当前检测项下通过的资产数量和未通过的资产数量。
7. 操作：重新检测和忽略。