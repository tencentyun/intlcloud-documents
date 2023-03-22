本文帮助您通过全量录制的方式快速接入**GME服务端录制**功能。



## 使用场景

GME对实时语音流提供**服务端录制**能力，帮助开发者实现内容留存、内容管理、内容再生产等场景。全量录制：支持录制应用内全量语音房间按房间维度混流、按用户维度单流；自定义录制：支持录制用户指定房间按房间维度混流、按用户维度单流。录制后的音频文件将存储在您账号下的**对象存储(COS)**服务中。


本文仅针对**全量录制**的开发接入方法进行说明。若您需要对应用开启自定义录制，请参考[开发指南-自定义录制](https://www.tencentcloud.com/document/product/607/53748)

>! 
>- 使用GME服务端录制功能，录制过程将在GME产生录制服务费用。GME国际站录制服务将从2023年4月1日起正式计费，详细计费信息将提前公示在[GME购买指南](https://www.tencentcloud.com/zh/document/product/607/50009)；
>- 录制后的文件将存储在您的腾讯云账号下的**对象存储(COS)**服务中，将会根据您的存储量、存储时长、访问频次等具体使用方式产生**对象存储(COS)**账单。详细计费信息请参考[COS计费说明](https://www.tencentcloud.com/zh/document/product/436/16871)。

## 前提条件

- **已开通实时语音服务**：可参见 [服务开通指引](https://www.tencentcloud.com/document/product/607/10782)。
- **已开通服务端录制服务**：目前服务端录制功能针对白名单用户提供，请联系我们开通白名单。
- **已接入GME SDK**：包括核心接口和实时语音接口的接入，详情可参见 [Native SDK 快速接入](https://www.tencentcloud.com/document/product/607/40858)、[Unity SDK 快速接入](https://www.tencentcloud.com/document/product/607/44544)、[Unreal SDK 快速接入](https://www.tencentcloud.com/document/product/607/44545)。


## 服务架构
![](https://staticintl.cloudcachetci.com/yehe/backend-news/j2pg571_PRELIM__%E6%B8%B8%E6%88%8F%E5%A4%9A%E5%AA%92%E4%BD%93%E5%BC%95%E6%93%8E_%E4%BA%A7%E5%93%81%E7%9B%AE%E5%BD%95_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US-1.png)

## 功能说明
### 1、录制范围

开启全量录制，将对所有实时语音房间进行录制。您可以配置仅录制房间混流，或仅录制用户单流，或同时录制单流和混流。

### 2、录制机制


#### 录制任务启动机制

- 第一个用户进房后触发录制任务启动

#### 录制任务终止机制

- 最后一个用户退房后触发录制任务终止

#### 录制任务分片机制

- 当单个音频文件时长达到两个小时，将自动进行音频文件分片
- 当用户关麦，用户单流录制音频将自动分片，用户开麦后启动新的分片
- 若录制中的任务异常中断，任务自动重连后将启动新的分片


#### 录制任务事件通知机制

- 录制任务事件通过回调机制通知到您配置的回调地址。当发生这些事件时，您会收到回调通知：**录制开始**、**录制停止**、**录制文件上传完成**
- 关于回调信息的详情，请参考 [录制回调说明]()



### 3、存储位置

GME服务端录制，录制完成后的音频文件将存储在您账号下的**对象存储COS**服务中的指定存储桶。存储桶地域由您指定，可选的地域列表请参考[对象存储地域说明](https://www.tencentcloud.com/document/product/436/6224)。


### 4、录制文件格式

- .mp3


### 5、录制文件命名规则

- 用户单流录制文件：bizid_roomid_userid/${任务开始时间}_${id}_audio.mp3
- 房间混流录制文件：bizid_roomid/${taskid}_${任务开始时间}_${id}_audio.mp3

 ***bizid:*** GME应用ID。可在[GME控制台](https://console.tencentcloud.com/gamegme)获取
 ***roomid:*** 语音房间ID。是您在使用实时语音服务时定义并传入至GME SDK
 ***userid:*** 玩家ID。是您在使用实时语音服务时定义并传入至GME SDK
 ***taskid:*** 录制任务ID，由GME录制服务生成。每一个录制任务都具有一个独特的任务ID
 ***id:*** 针对一个录制任务的分片的序列号。序列号初始序号为0



## 接入步骤

<dx-steps>
-<dx-tag-link link="#StartRealTimeASR" tag="业务侧">在控制台完成录制服务配置</dx-tag-link>
-<dx-tag-link link="#callback" tag="业务侧">接收录制任务回调（可选）</dx-tag-link> 
-<dx-tag-link link="#result" tag="业务侧"> 查看/管理录制文件</dx-tag-link>
</dx-steps>


### 步骤一：在控制台完成录制服务配置

- #### 开通/关闭录制服务

登录[GME控制台](https://console.tencentcloud.com/gamegme)，进入【服务管理】菜单，对希望启用录制服务的应用点击【设置】，进入应用详情页。在页面中对【语音录制服务】点击 **修改** 。

![](https://qcloudimg.tencent-cloud.cn/raw/9e2c89f462a81ba228c978cd725abf5a.png)

将录制开关置为 **开启** 。

首次开启录制服务时，GME将会向您申请服务授权，以便于访问您的**对象存储COS服务**，您需要在弹窗页面需要同意授权后，才能正常开启服务端录制服务。


![](https://qcloudimg.tencent-cloud.cn/raw/33407cf16b4ad310b65c4897ea766340.png)

- #### 录音文件存储配置

进入应用详情页面，在页面中对【语音录制服务】点击 **修改** ，在 **录制文件存储桶** 点击 **绑定** 。
在 **绑定存储桶**弹窗中，您可以绑定一个已有的COS存储桶（已有的存储桶需要您在[COS控制台](https://console.tencentcloud.com/cos/bucket)先行创建），或新建一个存储桶。

![](https://qcloudimg.tencent-cloud.cn/raw/c63e0fd24da877f5f79f49360f4ff9e1.png)

- #### 录制事件回调配置（可选）
如果您希望接收录制服务的事件回调，可以配置回调地址。操作路径：进入应用详情页面，在页面中对【语音录制服务】点击 **修改** ，在 **回调地址** 点击 **修改** ，在弹窗中输入接收回调的url地址。目前仅针对录制任务完成状态推送事件回调消息。

![](https://qcloudimg.tencent-cloud.cn/raw/92314d86dbf00e8cdafe6ac24d1c17b8.png)

- #### 录制范围配置
录制范围可选自定义录制或全量录制。您此时应选中全量，并在复选框中指定是否录制单流、是否录制混流。

完成上述配置后，点击 **保存**，录制服务即可开启。若您不再需要使用录制服务，请及时在控制台将录制服务开关置为 **关闭**， 避免产生预期之外的费用。




### 步骤二：接收录制任务回调（可选）

如果您在**步骤一**中配置了回调地址，则需要接收录制任务事件回调。



### 步骤三：查看/管理录制文件

一个录制任务结束后的数分钟内即可生成完成的音频文件。您需要登录您的[对象存储COS控制台](https://console.tencentcloud.com/cos/bucket)对录制文件进行查看和管理。







