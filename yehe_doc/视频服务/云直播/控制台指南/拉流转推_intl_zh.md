腾讯云直播控制台提供拉流转推工具，若您直播源无推流能力或点播视频内容需通过直播形式分发，拉流转推服务提供内容拉取并推送的功能，无需进行直播推流，即可快速拉取已有的视频/直播，推送到目标地址上。
![](https://main.qcloudimg.com/raw/8f0b044ce2104efdc1ed835287b9b683.png)

## 前提条件
- 已开通 [腾讯云直播服务](https://intl.cloud.tencent.com/product/css)，并登录云直播控制台。
- 已添加 [推拉流域名](https://intl.cloud.tencent.com/document/product/267/35970)。

## 注意事项
- 最多支持创建**20个**拉流转推任务。
- 使用拉流转推服务会产生**拉流转推任务时长账单**，详细费用请参见 [拉流转推计费说明](https://intl.cloud.tencent.com/document/product/267/41059)。
- 拉流转推功能仅提供内容拉取与推送服务，**请确保内容已获得授权并符合内容传播相关的法律法规。若因版权问题或内容违规，云直播会停止相关的功能服务并保留追究法律责任的权利**。

[](id:create)
## 创建任务
1. 选择 **直播工具箱** > **[拉流转推](https://console.cloud.tencent.com/live/tools/relay)**。单击 **创建任务**，进入拉流转推任务创建页面。
![](https://qcloudimg.tencent-cloud.cn/raw/4328e092758efd15d6436837dc618f50.png)
2. 填写配置任务基本信息，进行如下配置：
![](https://qcloudimg.tencent-cloud.cn/raw/018e81846aa6bad9686fdb7884889b5c.png)
<table>
<tr><th width="15%">配置项</th><th>配置说明</th></tr>
<tr>
<td>任务备注</td>
<td>自定义任务备注信息。</td>
</tr><tr>
<td>任务时间</td>
<td>默认为 <code>当前时刻</code> 至 <code>当前时刻 + 24小时</code>，可选任务时间为当前时间一年内任意时间至时间跨度不超过7天。<br>假设当前时间2021年03月24日11:50:01，则：<ul style="margin:0"><li/>可选择时间为2022年03月24日11:50:01至2022年03月30日11:50:01。<li/>结束时间不可超过2022年03月30日11:50:01。</ul></td>
</tr><tr>
<td>地域</td>
<td><ul style="margin:0"><li/>任务执行地域可选择：华北地区（北京）、华东地区（上海）、华南地区（广州）、亚太东南（新加坡）、亚太东南（泰国）、亚太东北（韩国）、亚太南部（印度）。<li/><b>若选择境内随机地域，系统会自动分配就近地域。</b></ul></td>
</tr><tr>
<td>事件回调通知</td>
<td>填写用于接收拉流转推任务事件的回调地址。</td>
</tr></table>

3. 选择内容来源类型，可选择**直播**或**点播视频**类型，具体配置如下：
   - 内容类型为**直播**，需填写直播来源地址（限填**1个**内容来源地址）。
   ![](https://qcloudimg.tencent-cloud.cn/raw/319311810174f09ac2286f7ff5350250.png)
   - 内容类型为**点播视频**：
      - **可输入多条**内容来源地址，上限30个。
      - 可设置播放循环次数，可选**无限循环**或**指定循环次数**。选择指定次数最少为1次，最高100次。
      ![](https://qcloudimg.tencent-cloud.cn/raw/8a94ddbcc7dc2c612ce39e35e0e0b379.png)
>? 
>- 当任务达到所设循环次数或者任务结束时间任一条件后，系统会停止拉流转推任务。
>- 若您需修改任务信息：
    - 变更循环次数，更新后按新的循环次数播放，当前有播放任务的记为1次。
    - 变更点播来源地址和循环次数，不论选择立即更新还是播完更新，当前播放任务不计为循环次数，按照新的循环次数播放。
    - 变更目标地址，循环次数重置。
4. 填写接收内容的目标地址。
   1. 单击目标地址输入栏下方的 **地址生成器**，进入生成器配置页。
   ![](https://qcloudimg.tencent-cloud.cn/raw/59b8cf4d58770d201190db7404f6b5ad.png)
   2. 选择已有的推流域名，填写 Appname、StreamName 和过期时间。单击 **确定** 生成推流地址，该地址自动填写到目标地址栏中。
   ![](https://qcloudimg.tencent-cloud.cn/raw/b01df24dffa14c35350048ae7fd3cfef.png)
    >! 地址过期时间应大于任务结束时间，若任务已开始后更新目标推流地址，会导致任务中断重推。
5. 填写完成后，单击 **保存** 完成创建。

## 管理任务
[](id:view)
### 查看任务详情
在 [任务列表](https://console.cloud.tencent.com/live/tools/relay) 中，选择您需查看的拉流转推任务，单击对应的 `任务备注/ID`，右侧弹窗将展示该任务详情信息。
![](https://qcloudimg.tencent-cloud.cn/raw/8fa3d70b6fe0d961048cc508ea72ca4b.png)

>? 您可在任务详情信息下方单击 **编辑** 或 **禁用**，对该任务进行 [修改](#change) 和 [禁用](#disable) 操作。

[](id:change)
### 修改任务
1. 在 [任务列表](https://console.cloud.tencent.com/live/tools/relay) 中，选择您已创建成功的拉流转推任务，并单击右侧操作栏的 **编辑**，进入修改拉流转推任务。
![](https://qcloudimg.tencent-cloud.cn/raw/97b07fc0d224a06fe268cdc1177102e3.png)
2. 根据您的实际需求修改任务信息，单击 **保存**。
>!
>- 地域及内容类型不支持修改。
>- 修改任务结束时间，需确保目标地址有效期在任务结束前有效。修改目标地址会导致任务中断重新发起。

![](https://qcloudimg.tencent-cloud.cn/raw/d950a8029e1944e9029445dd8e428933.png)
3.  在弹出的修改任务确认页中，查看修改前后的对比信息：
  - 当变更内容包括**任务备注、任务时间、事件回调通知**或**播放次数**时，对比信息显示如下示例：
![](https://qcloudimg.tencent-cloud.cn/raw/4cadcabeef99828ab4be144040cbfd19.png)
  - 当变更内容包括**点播内容**时，将提示您变更前的来源为点播内容，可选择此次修改的更新方式为 **当前播放视频结束后更新**/**立即更新**；若不选择，默认为 **当前播放视频结束后更新**。更新后会按照新的顺序重头开始进行拉流转推。
![](https://qcloudimg.tencent-cloud.cn/raw/9591b91b7e5e307860c9ea2244b4e14e.png)
   - 当变更内容包括**目标地址**时，将提示您变更修改目标地址，确认修改后当前拉流转推任务会被**中断后重新启动**。
![](https://qcloudimg.tencent-cloud.cn/raw/0a7e04f65ae8bbdd9cb7ef3bc0ece656.png)
4. 核实信息无误后，单击 **确定** 即可成功修改任务内容。

[](id:copy)
### 复制任务
1. 在 [任务列表](https://console.cloud.tencent.com/live/tools/relay) 中，选择您想复制的拉流转推任务，单击右侧操作栏的 **复制**，进入创建拉流转推任务界面。
![](https://qcloudimg.tencent-cloud.cn/raw/28a0a3542ab9ab838d26dfc565f321d1.png)
2. 当前选中的任务信息填充至新增创建任务页面中，您可在复制的原任务信息上进行 [修改](#create)。
3. 单击 **保存** 即可创建新的拉流转推任务。



[](id:reboot)
### 重启任务
重启任务后，任务**状态不会改变**，执行中的任务将会**重头开始执行**。若您需重启任务，具体操作如下：

1. 在 [任务列表](https://console.cloud.tencent.com/live/tools/relay) 中，选择您想重启的拉流转推任务，单击右侧操作栏的 **重启**。
2. 确认是否要重启当前拉流转推任务，单击 **重启** 即可。
![](https://qcloudimg.tencent-cloud.cn/raw/d1b03e226297e44cbb7504d57c54af4f.png)

[](id:disable)
### 禁用任务
禁用任务后，**任务会直接停止**，需要 [启用](#enable) 才能重新开始执行任务。若您需禁用任务，具体操作如下：

1. 在 [任务列表](https://console.cloud.tencent.com/live/tools/relay) 中，选择您想禁用的拉流转推任务，单击右侧操作栏的 **禁用**。
2. 确认是否要禁用当前拉流转推任务，单击 **禁用** 即可。
![](https://qcloudimg.tencent-cloud.cn/raw/c3acfb89f425b50ba53a8d63075091d8.png)


[](id:enable)
### 启用任务
启用任务后，**任务将会重新重头开始执行**。若您需启用任务，具体操作如下：

1. 在 [任务列表](https://console.cloud.tencent.com/live/tools/relay) 中，选择您想启用的已被禁用拉流转推任务，单击右侧操作栏的 **启用**。
2. 确认是否要启用当前拉流转推任务，单击 **确定** 即可。
![](https://qcloudimg.tencent-cloud.cn/raw/77417a9c8406fe9d763c4d3960d98b21.png)

[](id:delete)
### 删除任务
删除任务**不支持找回**，若您需删除任务，具体操作如下：

1. 在 [任务列表](https://console.cloud.tencent.com/live/tools/relay) 中，选择您想删除的拉流转推任务，单击右侧操作栏的 **删除**。
2. 确认是否要删除当前拉流转推任务，单击 **删除** 即可。
![](https://qcloudimg.tencent-cloud.cn/raw/44a15ad52bfc81f62c0aa907cdc7eb5c.png)

[](id:batch)
### 批量操作
拉流转推支持批量删除、禁用、启用任务，批量处理支持**最多10个任务**。
1. 在 [任务列表](https://console.cloud.tencent.com/live/tools/relay) 中，勾选您想批量处理的拉流转推任务。
2. 选择您想批量处理的操作，可单击选择 **批量删除**、**批量禁用** 或 **批量启用**。
![](https://qcloudimg.tencent-cloud.cn/raw/6b93d5c3af7ec83d9a56840a40a2073a.png)
3. 确认是否要删除/禁用/启用当前拉流转推任务，在弹框中单击 **删除** / **禁用** / **启用** 即可完成批量处理。
![](https://qcloudimg.tencent-cloud.cn/raw/5874636c548a4733281cd33eaca35abe.png)

   
