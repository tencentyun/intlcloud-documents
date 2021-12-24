应用创建成功后，您可通过【应用信息】进入查看应用的详细信息，其中展示信息包含应用基本信息、旁路直播信息、实时音视频服务状态及应用标签等内容。

## 应用信息
### 应用信息说明
1. 进入实时音视频控制台，选择【[应用管理](https://console.cloud.tencent.com/trtc/app)】，查看应用列表。
2. 选择需要修改应用信息的应用，单击其右侧操作栏的【应用信息】。
![](https://main.qcloudimg.com/raw/495a71aedd1f8ab6296be0d9e3c31406.png)
3. 进入应用详情页，通过【应用信息】页签的“应用信息”模块即可查看当前应用的基本信息。
![](https://main.qcloudimg.com/raw/0fc9aeb7b75617c9b702a8f2c5e4a8ba.png)
<table>
<tr><th width="18%">信息项</th><th>说明</th></tr><tr>
<td>应用名称</td>
<td>应用创建时用户定义的名称，可自定义修改。</td>
</tr><tr>
<td>SDKAppID</td>
<td>应用创建成功后自动生成的 SDKAppID，是应用的唯一标识，调用语音 API 接口时，需要提供该参数。</td>
</tr><tr>
<td>创建时间</td>
<td>应用成功创建的时间。</td>
</tr><tr>
<td>应用介绍</td>
<td>应用介绍描述，可自定义修改。</td>
</tr><tr>
<td>应用来源</td>
<td>应用创建来源情况：<ul style="margin:0"><li/>从 <a href="https://intl.cloud.tencent.com/document/product/1047/34540">IM 控制台中开通腾讯实时音视频服务</a> 后，会显示“应用来源”字段。<li/>在 TRTC 控制台主动创建的不会显示“应用来源”字段。</ul></td>
</tr></table>



### 修改应用信息
1. 在【[应用管理](https://console.cloud.tencent.com/trtc/app)】中选择需要修改应用信息的应用，单击其右侧操作栏的【应用信息】进入应用详情页。
2. 在【应用信息】页签中，查看“应用信息”模块，单击右侧的【编辑】。
![](https://main.qcloudimg.com/raw/818c5c71aa54d05b6bed152121d43e6e.png)
3. 进入应用信息修改弹框，可修改**应用名称**及**应用介绍**信息，单击【修改】即可保存成功。
![](https://main.qcloudimg.com/raw/019312c2244ee5e311619dc64436b960.png)
> ? 
> - **应用名称**输入框仅支持填写数字、中英文和下划线，不能超过15个字符。
> - **应用介绍**输入框仅支持填写数字、中英文和下划线，不能超过300个字符。



## 旁路直播信息
旁路直播指的是TRTC 在云端使用旁路转码集群，将 TRTC 所使用的 UDP 协议转换为标准的直播 RTMP 协议，把 TRTC 的音视频数据推送到标准的云直播系统中，再经由 CDN 进行分发。当您需要 [实现 CDN 直播观看](https://intl.cloud.tencent.com/document/product/647/35242) 功能时将会用到此处的信息。
![](https://main.qcloudimg.com/raw/d16f88ce8704ee236866bc9947df2f17.png)

## 实时音视频服务状态
主要展示当前应用的实时音视频基础服务和增值服务状态情况，包括“正常”、“已停用”两种状态。
- **正常：**
状态为正常时，实时音视频基础服务和增值服务皆可正常使用。为了保证服务持续正常可用，请及时 [续购套餐包](https://buy.cloud.tencent.com/trtc) ，或 [开启后付费](https://intl.cloud.tencent.com/document/product/647/41979) 并保持 [腾讯云账户](https://console.cloud.tencent.com/expense) 余额充足。
![](https://main.qcloudimg.com/raw/0e2b88e7a8fc1ac1186bcbcd703a9fe4.png)
- **已停用：**
状态为已停用时，实时音视频基础服务和增值服务皆不可用，请检查是否存在下方描述情况：
	1. 未开启后付费，免费试用套餐包用完或过期自动停服：您可以 [购买套餐包](https://buy.cloud.tencent.com/trtc) 重新激活服务或直接 [开启后付费](https://intl.cloud.tencent.com/document/product/647/41979)。
	2. 已开启后付费，腾讯云账户欠费后导致停服：[欠费冲正](https://console.cloud.tencent.com/expense/overview) 后将自动恢复服务。
	3. 您手动操作将应用停用使其处于停服状态：单击【启用应用】即可重新恢复服务。
![](https://main.qcloudimg.com/raw/faa1e34ad79109a665af1393b0cfeb5f.png)

[](id:deactivate)
### 自助停用应用
1. 选择【更多操作】下拉菜单，单击【停用应用】。
2. 阅读《停用声明》并点击确认【停用】。
3. 确认停用应用后，您需要进行二次身份验证，以防操作失误带来不必要的损失。
4. 停用操作发起成功后，全量生效需要3-5分钟，请耐心等待。

[](id:enable)
### 自助启用应用
1. 单击【启用应用】。
2. 阅读《启用声明》并单击确认【启用】。
3. 确认启用应用后，您需要进行二次身份验证，以防操作失误带来不必要的损失。
4. 启用操作发起成功后，全量生效需要3分钟 - 5分钟，请稍后再刷新页面查看。

[](id:delete)
### 自助删除应用
1. 选择【更多操作】单击【删除应用】。

2. 阅读《删除声明》并点击确认【删除】。

3. 确认删除应用后，您需要进行二次身份验证，以防操作失误带来不必要的损失。
4. 删除操作发起成功后，全量生效需要3分钟 - 5分钟，请耐心等待。

>?
>- 控制台二次身份验证成功后，30分钟内无需重新验证，请谨慎操作。
>- 停用/删除生效后，只会阻止新的用户进入 [房间](https://intl.cloud.tencent.com/document/product/647/37714) ，生效之前已经进房的用户仍然会正常计费。您可以通过 [解散房间](https://intl.cloud.tencent.com/document/product/647/34269) 接口，强行关闭使用中的房间。
>- 停用/删除生效后，该应用的基础服务（音视频通话、互动直播）和增值服务（混流转码、云端录制等）都将无法使用。
>- 自助 停用/启用/删除 应用 发起后，全量生效需要3分钟-5分钟，请耐心等待。
>- 正常状态下，无法删除应用；请先自助停用后再删除。


## 标签
[标签](https://intl.cloud.tencent.com/document/product/651/13334) 用于标识和组织您在腾讯云的各种资源。例如：企业可能有多个业务部门，每个部门有1个或多个 TRTC 应用，这时，企业可以通过给 TRTC 应用添加标签来标记部门信息。

### 添加应用标签
1. 在【[应用管理](https://console.cloud.tencent.com/trtc/app)】中选择需要修改标签信息的应用，单击其右侧操作栏的【应用信息】进入应用详情页。
2. 在【应用信息】页签中，查看“标签”模块，单击右侧的【编辑】。
![](https://main.qcloudimg.com/raw/faa1e34ad79109a665af1393b0cfeb5f.png)
3. 进入标签编辑弹框，选择已在 [标签管理](https://console.cloud.tencent.com/tag/taglist) 中创建的**标签键**和**标签值**。
![](https://main.qcloudimg.com/raw/7189bab1421cb112881d20dfce1d31a8.png)
>? 
>- 若现有的标签不符合您的要求，请前往 [标签管理](https://console.cloud.tencent.com/tag/taglist) 进行创建操作。
>- 支持为应用添加多个标签，单击【+添加】即可创建新的标签配置框。
4. 单击【确定】保存，控制台会刷新弹框显示是否修改成功。

### 删除应用标签
1. 在【[应用管理](https://console.cloud.tencent.com/trtc/app)】中选择需要修改标签信息的应用，单击其右侧操作栏的【应用信息】进入应用详情页。
3. 在【应用信息】页签中，查看“标签”模块，单击右侧的【编辑】。
	![](https://main.qcloudimg.com/raw/faa1e34ad79109a665af1393b0cfeb5f.png)
4. 进入标签编辑弹框，选择需要删除的标签，单击右侧的删除按钮。
![](https://main.qcloudimg.com/raw/7189bab1421cb112881d20dfce1d31a8.png)
5. 单击【确定】保存，控制台会刷新弹框显示是否修改成功。



## 相关文档
- 若需创建新的应用，具体操作请参见 [创建应用](https://intl.cloud.tencent.com/document/product/647/39077)。
- 若需在应用列表中搜索相关应用，具体操作请参见 [搜索应用](https://intl.cloud.tencent.com/document/product/647/39078)。
- 若需配置或查看应用的功能配置信息，具体操作请参见 [功能配置](https://intl.cloud.tencent.com/document/product/647/39080)。
- 若需在云端混流转码时设置自定义背景图片，可在素材管理中添加对应的图片素材，具体操作请参见 [素材管理](https://intl.cloud.tencent.com/document/product/647/39081)。
- 若需快速跑应用通配套的 Demo 源码，具体操作请参见 [快速上手](https://intl.cloud.tencent.com/document/product/647/39082)。







