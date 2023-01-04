本文档为您介绍本地镜像功能，并指导您开启扫描数据和查看本地镜像列表。
![](https://qcloudimg.tencent-cloud.cn/raw/04040b472bd32cac3804987963f276fb.png)

## 开启扫描数据
扫描数据展示模块中提供最近扫描检测后的存在风险的镜像数量和镜像总数，镜像存在的安全漏洞、木马病毒和敏感信息数量。
### 开启一键扫描
1. 登录 [容器安全服务控制台](https://console.cloud.tencent.com/tcss)，在左侧导航中，单击**镜像风险管理** > **本地镜像**。
2. 在本地镜像页面，单击右侧**一键扫描**，可重新扫描获取最新镜像数据或镜像风险信息。
![](https://qcloudimg.tencent-cloud.cn/raw/6493d408dba3a3d417b161fd155eae5d.png)
3. 在扫描设置页面，可根据需求选择检测风险类别和镜像范围。
 - 检测风险类别：安全漏洞和敏感信息。
 - 镜像范围：全部镜像和自选镜像。其中单击所需的自选镜像![](https://main.qcloudimg.com/raw/37d813d17a69271ce31b3233ad0a949e.png)或![](https://main.qcloudimg.com/raw/be9e47bccb644d8a099149bac4aef1e0.png)图标，即可选中或删除自选镜像。
>? 支持按住 shift 键进行多选。

 ![](https://qcloudimg.tencent-cloud.cn/raw/8b1e0e71b1a89bb839dcea89d2de503f.png)
4.  选择所需内容后，单击**立即扫描**，即可开始扫描。
>! 开始扫描后，所选择的所有镜像的相同 ID 镜像将同时进行扫描。

 ### 开启定时扫描
 1. 在本地镜像页面，单击右侧**定时扫描设置**，可自定义设置是否开启定时扫描功能。
 ![](https://qcloudimg.tencent-cloud.cn/raw/a3e22341834abfc29f81901831d7ab55.png)
 2. 在定时扫描设置页面，单击开启**扫描开关**，并根据需求设置定时扫描时间、检测风险类别和镜像范围。
  - 定时扫描时间：可以选择固定周期：1天、7天、15天、30天；以及具体更新时间点。
  - 检测风险类别：单击![](https://main.qcloudimg.com/raw/86d08a45be3bc5b91de551b390ebe15d.png)图标、按需选择安全漏洞、敏感信息和木马病毒。
  - 镜像范围：全部镜像和自选镜像。其中单击所需的自选镜像![](https://main.qcloudimg.com/raw/37d813d17a69271ce31b3233ad0a949e.png)或![](https://main.qcloudimg.com/raw/be9e47bccb644d8a099149bac4aef1e0.png)图标，即可选中或删除自选镜像。
>? 支持按住 shift 键进行多选。

 ![](https://qcloudimg.tencent-cloud.cn/raw/2e64ea860827ca932d61f043467c328c.png)
 3. 选择所需内容后，单击**设置**或**取消**，即可完成或取消设置。

### 开启数据更新
在本地镜像页面，单击右侧**数据更新** > **确认**，可对所有镜像相关安全信息进行立即更新。
>? 最长时间需要1~3分钟。

![](https://qcloudimg.tencent-cloud.cn/raw/7218397cafe4e2ce2de5812c099482d6.png)

## 查看本地镜像列表
### 授权镜像事件
1. 在本地镜像页面，单击**授权**，将未授镜像被授权安全扫描，弹出“授权确认”窗口。
![](https://qcloudimg.tencent-cloud.cn/raw/56c392934a8a6aed42286865084d65b1.png)
2. 在“授权确认”窗口，单击**确认**，此镜像将被授权安全扫描。
>? 确认后，此镜像将被授权安全扫描，操作将消耗1个镜像授权。

### 筛选镜像资产
在本地镜像页面，可通过以下操作对镜像资产进行筛选：
 - 在本地镜像页面，单击扫描状态下拉框，按扫描状态对镜像资产进行筛选。
<img src="https://qcloudimg.tencent-cloud.cn/raw/9cf2975a897af7da245120bf98d59f57.png" style="zoom:67%;" />
 - 在本地镜像页面，单击安全状态下拉框，按安全状态对镜像资产进行筛选。
<img src="https://qcloudimg.tencent-cloud.cn/raw/d18a6990a7ffa21fc5c1d6aeae87a158.png" style="zoom:67%;" />
 - 在本地镜像页面，单击![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png)勾选仅展示重点关注镜像，可根据系统依据风险紧急程度等条件判断得出的重点关注镜像资产。
![](https://qcloudimg.tencent-cloud.cn/raw/b398ed69b86c9c2c337947da77ac3e4f.png)
 - 在本地镜像页面，单击搜索框通过“镜像名称、镜像 ID”等关键词对镜像资产进行查询。
![](https://qcloudimg.tencent-cloud.cn/raw/446265bb02db80b801696d810e3d2874.png)

### 导出镜像资产
在本地镜像页面，单击![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png)图标勾选所需的本地镜像后，单击![](https://main.qcloudimg.com/raw/24d375a75e4ee95c77910d101f7203dd.png)图标即可导出镜像资产。
![](https://qcloudimg.tencent-cloud.cn/raw/5cbf99421e5cd7910456416516d97b99.png)

### 查看列表详情
1. 在本地镜像页面，单击“镜像名称”，右侧弹出抽屉展示镜像详情。[](id:JXMC)
>?
>- 镜像风险：镜像扫描是否成功、安全漏洞数量、木马病毒数量和敏感信息数量。
>- 镜像详情：镜像名称、镜像 ID、镜像大小、操作系统类型。
>- 安全漏洞列表：可按漏洞威胁等级对镜像安全漏洞事件进行筛选，或按漏洞名称检索安全漏洞事件。单击**查看详情**可查看漏洞详情及其修复建议。
>- 木马病毒列表：可按木马病毒威胁等级对镜像安全事件进行筛选，或按文件名称检索安全事件。单击**查看详情**可查看木马病毒详情及其处置建议。
>- 敏感信息列表：可按敏感信息威胁等级、敏感信息名称和类型对安全事件进行筛选。
>- 镜像构建历史：镜像构建历史日志。

![](https://qcloudimg.tencent-cloud.cn/raw/a3cfc005c2e9c95b365fa8ea5fb13fc8.png)
2. 在本地镜像页面，单击“关联主机数”，弹出关联主机详情弹窗，展示了主机名称、主机 IP、Docker 版本等信息。
>? 若关联多个主机，还可以通过以下操作筛主机：
>- 单击主机状态下拉框，按主机状态对主机进行筛选。
>- 单击搜索框通过“主机名、业务组、Docker 版本”等关键词对主机进行查询。

![](https://qcloudimg.tencent-cloud.cn/raw/80294cdb1d33808c653ce78d6a3f2d29.png)
3. 在本地镜像页面，单击“关联容器数”，弹出关联的容器弹窗，展示了容器名称、容器 ID、容器运行状态、CMD、最近更新时间。
>?若关联多个容器，还可以通过以下操作筛容器：
>- 单击状态下拉框，按容器状态对容器进行筛选。
>- 输入主机名称单击![](https://main.qcloudimg.com/raw/b12f0b480adcd420cdd30445ba435c04.png)图标，对主机进行查询。

![](https://qcloudimg.tencent-cloud.cn/raw/7994ee84829353ad8968b22804267f4e.png)
4. 在本地镜像页面，单击**详情**，右侧抽屉展示镜像详情，展示内容可查看  [镜像名称](#JXMC)。
![](https://qcloudimg.tencent-cloud.cn/raw/f4b914eba2fdb66fab30d7d69fcb9a4a.png)

### 扫描镜像事件
1. 在本地镜像页面，对镜像扫描状态为“未扫描”时，单击**立即扫描** > **确定**，对镜像进行立即扫描。
![](https://qcloudimg.tencent-cloud.cn/raw/8298745c11b7dbb5f8fb018e56d5153b.png)
2. 在本地镜像页面，上一个扫描任务停止后，单击**重新扫描**，对镜像重新扫描。
>?可单击![](https://main.qcloudimg.com/raw/08dfa220659d6576a39a981e61ad02e2.png)勾选多个镜像后，单击②处**重新扫描**进行批量重新扫描。

![](https://qcloudimg.tencent-cloud.cn/raw/c561a56ecb6204e15f13639fcced60d4.png)
3. 在本地镜像页面，镜像扫描状态为“扫描中”时，单击**取消扫描**，取消扫描镜像。
>?可单击![](https://main.qcloudimg.com/raw/08dfa220659d6576a39a981e61ad02e2.png)勾选多个镜像后，单击②处**取消扫描**批量取消扫描任务。

![](https://qcloudimg.tencent-cloud.cn/raw/772b580a1ce1a82832196828239cedc5.png)

### 自定义列表管理
1. 在本地镜像页面，单击![](https://main.qcloudimg.com/raw/d42b27540eef9bf90a9e30f96b500bf3.png)图标，弹出自定义列表管理弹窗，在弹窗中可以自定义设定列表管理。
2. 在自定义列表管理弹窗，选择所需的类型后，单击**确定**，即可完成设置自定义列表管理。
<img src="https://qcloudimg.tencent-cloud.cn/raw/8c1342b4db00c09680d672890baf2954.png" style="zoom:67%;" />

#### 列表重点字段说明
1. 创建时间：镜像创建时间。
2. 最近扫描时间：显示最近一次扫描时间。
3. 安全风险：展示容器存在的安全风险类型。
4. 状态：展示容器扫描状态，包括已扫描、未扫描、扫描中、已取消和扫描异常。
>? 扫描异常时建议重新扫描。