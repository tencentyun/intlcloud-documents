本文档为您介绍仓库镜像功能，并指导您开启扫描数据和查看仓库镜像列表。
>? 支持的镜像仓类型：
>- 腾讯云容器镜像服务 TCR/CCR。
>- 第三方镜像仓 Harbor。

## 前提条件
已购买容器安全服务镜像安全 [增值功能](https://www.tencentcloud.com/document/product/1163/50875)。

## 接入腾讯云容器镜像服务
容器安全服务与腾讯云容器镜像服务已默认集成，支持对 TCR 和 CCR 仓库进行镜像扫描。
>?
>- 容器安全服务默认通过公网请求 TCR 仓库资产，若您的仓库实例启用了访问控制，使用前请先添加服务 IP 地址段白名单，或切换网络类型。在 [仓库镜像页面](https://console.cloud.tencent.com/tcss/security/imageStore)，单击页面上方的**操作指南**展开弹窗，按照配置方法添加 IP 地址白名单或切换网络类型使用 VPC 网络。
>- 首次使用时需手动进行仓库镜像资产数据更新，单击 [仓库镜像页面](https://console.cloud.tencent.com/tcss/security/imageStore) 右上方的**数据更新**，更新仓库镜像资产，首次同步时间可能较长。
>- 后台每天凌晨0点至3点间会自动同步仓库镜像资产数据。

## 接入第三方镜像仓 Harbor
1. 登录 [容器安全服务控制台](https://console.cloud.tencent.com/tcss)，在左侧导航中，单击**镜像风险管理** > **仓库镜像**。
2. 在仓库镜像页面，单击右上角的**镜像仓管理**。
![](https://qcloudimg.tencent-cloud.cn/raw/ff436b4e47732b3484916a7ed990ed83.png)
3. 在镜像仓库列表中，单击**新增镜像仓**。
4. 在添加镜像仓弹窗中，配置相关参数，单击**确定**。
<img src="https://qcloudimg.tencent-cloud.cn/raw/5970b9994b88a371f7192b13ebb7be72.png" style="zoom:67%;" />
参数说明：
<table>
<thead>
<tr>
<th>参数名称</th>
<th>说明</th>
</tr>
</thead>
<tbody><tr>
<td>实例名称</td>
<td>填写镜像仓实例名称，实例名称唯一，不可为空</td>
</tr>
<tr>
<td>仓库类型</td>
<td>选择第三方镜像仓库类型。目前支持选择<strong>harbor</strong>仓。</td>
</tr>
<tr>
<td>版本</td>
<td>选择第三方镜像仓库的版本。支持选择以下版本： <ul><li>  V1：镜像仓库版本为1.X.X。</li>  <li>  V2：镜像仓库版本为2.X.X及以上。  </li></td>
</tr>
<tr>
<td>网络类型</td>
<td>选择第三方镜像仓库的网络访问类型。目前支持<strong>公网</strong>。</td>
</tr>
<tr>
<td>地域</td>
<td>选择第三方镜像仓库所在区域，Harbor 类型为默认值“默认地域”。</td>
</tr>
<tr>
<td>地址</td>
<td>输入第三方镜像仓库访问地址。</td>
</tr>
<tr>
<td>用户名</td>
<td>输入访问第三方镜像仓库的用户名。</td>
</tr>
<tr>
<td>密码</td>
<td>输入访问第三方镜像仓库的密码。</td>
</tr>
<tr>
<td>限速</td>
<td>选择每小时可同步拉取的镜像个数。默认为不限制。可选值：5、10、20、50、100、500、1000、无限制</td>
</tr>
<tr>
<td>验证远程证书</td>
<td>确定镜像同步是否要验证远程镜像仓库实例的证书，如果远程实例使用的是自签或者非信任证书，不要勾选此项。默认为勾选。</td>
</tr>
</tbody></table>

## 开启扫描数据
在 [仓库镜像页面](https://console.cloud.tencent.com/tcss/security/imageStore) 扫描数据展示模块中提供最近扫描检测后的存在风险的镜像数量和镜像总数，镜像存在的安全漏洞、木马病毒和敏感信息数量。

### 开启一键扫描
1. 在仓库镜像页面，单击右侧**一键扫描**，可获取最新镜像数据或镜像风险信息。
![](https://qcloudimg.tencent-cloud.cn/raw/21848447eea15d8153c125325ef0a416.png)
2. 在扫描设置页面，可根据需求选择检测风险类别和镜像范围。
 - 检测风险类别：包含安全漏洞和敏感信息。
 - 镜像范围：全部镜像和自选镜像。其中单击所需的自选镜像![](https://main.qcloudimg.com/raw/37d813d17a69271ce31b3233ad0a949e.png)或![](https://main.qcloudimg.com/raw/be9e47bccb644d8a099149bac4aef1e0.png)图标，即可选中或删除自选镜像。
>? 支持按住 shift 键进行多选。

![](https://qcloudimg.tencent-cloud.cn/raw/193fec47268152f6f22c00917f18f0c3.png)
4.  选择所需内容后，单击**立即扫描**，即可开始扫描。
>! 开始扫描后，所选择的所有镜像的相同 ID 镜像将同时进行扫描。

### 开启定时扫描
1. 在仓库镜像页面，单击右侧**定时扫描设置**，可自定义设置是否开启定时扫描功能。
![](https://qcloudimg.tencent-cloud.cn/raw/2490eb906ee424df4da3668467a6da67.png)
2. 在定时扫描设置页面，单击开启**扫描开关**，并根据需求设置定时扫描时间、检测风险类别和镜像范围。
  - 定时扫描时间：可以选择固定周期：1天、7天、15天、30天；以及具体更新时间点。
  - 检测风险类别：单击![](https://main.qcloudimg.com/raw/86d08a45be3bc5b91de551b390ebe15d.png)图标、按需选择安全漏洞、敏感信息和木马病毒。
  - 镜像范围：全部镜像和自选镜像。其中单击所需的自选镜像![](https://main.qcloudimg.com/raw/37d813d17a69271ce31b3233ad0a949e.png)或![](https://main.qcloudimg.com/raw/be9e47bccb644d8a099149bac4aef1e0.png)图标，即可选中或删除自选镜像。
>? 支持按住 shift 键进行多选。

![](https://qcloudimg.tencent-cloud.cn/raw/c0214f06f98410aeba6119c4da6bf618.png) 
4. 选择所需内容后，单击**设置**或**取消**，即可完成或取消设置。

##  查看仓库镜像列表
登录 [容器安全服务控制台](https://console.cloud.tencent.com/tcss)，在左侧导航中，单击**镜像风险管理** > **仓库镜像**，进入仓库镜像页面。
### 授权镜像事件
1. 在仓库镜像页面，单击**授权**，将未授镜像被授权安全扫描，弹出“授权确认”窗口。
![](https://qcloudimg.tencent-cloud.cn/raw/5d9c5a577d4d05e063ecc06024012f95.png)
2. 在“授权确认”窗口，单击**确认**，此镜像将被授权安全扫描。
>? 确认后，此镜像将被授权安全扫描，操作将消耗1个镜像授权。

### 筛选镜像资产
在仓库镜像页面，可通过以下操作对镜像资产进行筛选：
 -  在仓库镜像页面，单击扫描状态下拉框，按扫描状态对镜像资产进行筛选。
<img src="https://qcloudimg.tencent-cloud.cn/raw/81ad2f85e431a81f0e3d298663d13393.png" style="zoom:67%;" />
 -  在仓库镜像页面，单击安全状态下拉框，按安全状态对镜像资产进行筛选。
<img src="https://qcloudimg.tencent-cloud.cn/raw/088d6ed03dec1a3ff217e2599b64e00a.png" style="zoom:67%;" />
 -  在仓库镜像页面，单击仓库类型下拉框，按仓库类型对镜像资产进行筛选。
<img src="https://qcloudimg.tencent-cloud.cn/raw/47758deacb9b105b460dfde4b021f609.png" style="zoom:80%;" />
 -  在仓库镜像页面，单击授权状态下拉框，按授权状态对镜像资产进行筛选。
![](https://qcloudimg.tencent-cloud.cn/raw/5fd65ec7c30fe0f69ed981ef5ad1bba7.png)
 - 在仓库镜像页面，单击搜索框，可通过“镜像名称、镜像 Digest”等关键词对镜像资产进行查询。
![](https://qcloudimg.tencent-cloud.cn/raw/bd9fd719cc1c29ecaf86a11fbd760f16.png)

### 导出镜像资产
在仓库镜像页面，单击![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png)图标勾选所需的镜像仓库后，单击![](https://main.qcloudimg.com/raw/24d375a75e4ee95c77910d101f7203dd.png)图标即可导出镜像资产。
![](https://qcloudimg.tencent-cloud.cn/raw/58af135a04cad401d294c8c6f5a4bde4.png)

### 查看列表详情
在仓库镜像页面，单击**详情**，右侧抽屉展示镜像详情，可查看镜像风险、镜像详情和安全漏洞列表等信息。
>?
>- 镜像风险：镜像扫描是否成功、安全漏洞数量、木马病毒数量和敏感信息数量。
>- 镜像详情：镜像名称、镜像Digest、镜像大小。
>- 安全漏洞列表：可按漏洞威胁等级对镜像安全漏洞事件进行筛选，或按漏洞名称检索安全漏洞事件。单击**查看详情**查看漏洞详情及其修复建议。
>- 木马病毒列表：可按木马病毒威胁等级对镜像安全事件进行筛选，或按文件名称检索安全事件。单击**查看详情**查看木马病毒详情及其处置建议。
>- 敏感信息列表：可按敏感信息威胁等级、敏感信息名称和类型对安全事件进行筛选。
>- 镜像构建历史：镜像构建历史日志。

![](https://qcloudimg.tencent-cloud.cn/raw/d14610d7260e0121408f96497929c561.png)

### 扫描镜像事件
1. 在仓库镜像页面，对镜像扫描状态为“未扫描”时，单击**立即扫描** > **确定**，对镜像进行立即扫描。
![](https://qcloudimg.tencent-cloud.cn/raw/f823637c5aa5feb425a8028d2e63e555.png)
2. 在仓库镜像页面，镜像扫描状态为“扫描中”时，单击**取消扫描**，取消扫描镜像。
>? 可单击![](https://main.qcloudimg.com/raw/08dfa220659d6576a39a981e61ad02e2.png)勾选多个镜像后，单击②处**取消扫描**批量取消扫描任务。

![](https://qcloudimg.tencent-cloud.cn/raw/8ebb8afb81335b5b4e48bb948e82b29a.png)
3. 在仓库镜像页面，上一个扫描任务停止后，单击**重新扫描**，对镜像重新扫描。
>? 可单击![](https://main.qcloudimg.com/raw/08dfa220659d6576a39a981e61ad02e2.png)勾选多个镜像后，单击②处**重新扫描**进行批量重新扫描。

![](https://qcloudimg.tencent-cloud.cn/raw/38ecf1dc48567fdf322953b2d3b1f602.png)

### 自定义列表管理
1. 在仓库镜像页面，单击![](https://main.qcloudimg.com/raw/d42b27540eef9bf90a9e30f96b500bf3.png)图标，弹出自定义列表管理弹窗，在弹窗中可以自定义设定列表管理。
2. 在自定义列表管理弹窗，选择所需的类型后，单击**确定**，即可完成设置自定义列表管理。
<img src="https://qcloudimg.tencent-cloud.cn/raw/152b44b9e08a9897baf033472fdffacf.png" style="zoom:67%;" />

#### 列表字段说明
1. 镜像仓库地址：仓库镜像来源地址。
2. 仓库类型：镜像仓库的类型，目前包括 tcr、ccr 等。
4. 镜像版本：仓库镜像的版本号。
6. 最近扫描时间：显示最近一次扫描时间。
7. 安全风险：展示容器存在的安全风险类型。
8. 状态：展示容器扫描状态，包括已扫描、未扫描、扫描中、已取消和扫描异常。
>! 扫描异常时建议重新扫描。