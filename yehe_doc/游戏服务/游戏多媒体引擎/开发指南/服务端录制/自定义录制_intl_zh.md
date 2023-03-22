本文帮助您通过自定义录制的方式接入**GME服务端录制**功能。



## 使用场景

GME对实时语音流提供**服务端录制**能力，帮助开发者实现内容留存、内容管理、内容再生产等场景。全量录制：支持录制应用内全量语音房间按房间维度混流、按用户维度单流。自定义录制：支持录制用户指定房间按房间维度混流、按用户维度单流。录制后的音频文件将存储在您账号下的**对象存储(COS)**服务中。

本文仅针对**自定义录制**的开发接入方法进行说明。若您需要对应用开启全量录制，请参考[开发指南-全量录制]()

>! 
>- 使用GME服务端录制功能，录制过程将在GME产生录制服务费用。GME国际站录制服务将从2023年4月1日起正式计费，计费详情请参考[GME购买指南](https://www.tencentcloud.com/document/product/607/50009)；
>- 录制后的文件将存储在您的腾讯云账号下的**对象存储(COS)**服务中，将会根据您的存储量、存储时长、访问频次等具体使用方式产生**对象存储(COS)**账单。详细计费信息请参考[COS计费说明](https://www.tencentcloud.com/document/product/436/16871)。

## 前提条件

- **已开通实时语音服务**：可参见 [服务开通指引](https://www.tencentcloud.com/document/product/607/10782)。
- **已开通服务端录制服务**：目前服务端录制功能针对白名单用户提供，请联系我们开通白名单。
- **已接入GME SDK**：包括核心接口和实时语音接口的接入，详情可参见 [Native SDK 快速接入](https://www.tencentcloud.com/zh/document/product/607/40858)、[Unity SDK 快速接入](https://www.tencentcloud.com/zh/document/product/607/44544)、[Unreal SDK 快速接入](https://www.tencentcloud.com/zh/document/product/607/44545)。


## 服务架构

![](https://qcloudimg.tencent-cloud.cn/raw/115956742ac610dfb784d68a909dd032.jpg)

## 功能说明

### 1、录制范围
您可通过服务端接口指定需要录制的房间ID混流或房间内用户单流。
针对指定录制的房间ID，您可以通过服务端接口参数指定需要录制的玩家白名单，或无需录制的玩家黑名单。

### 2、相关接口

- [ ***StartRecord()*** ](https://www.tencentcloud.com/document/product/607/53736)   **开始录制**
您可在这个接口参数中定义录制单流或混流、指定需要录制的RoomID、指定订阅的白名单用户ID或黑名单用户ID。

- [ ***StopRecord()***](https://www.tencentcloud.com/document/product/607/53735)  **结束录制**
您可以通过这个接口，对某个taskid停止录制。若您没有记录taskid，则需要先通过DescribeTaskInfo()获取指定房间正在进行的录制任务taskid。

- [***ModifyRecordInfo()***](https://www.tencentcloud.com/document/product/607/53737)  **更新录制信息**
您可以通过这个接口，对某个taskid更新录制信息。包括更新录制类型、更新订阅的白名单用户ID或黑名单用户ID。若您没有记录taskid，则需要先通过DescribeTaskInfo()获取指定房间正在进行的录制任务taskid。

- [***DescribeTaskInfo()***](https://www.tencentcloud.com/document/product/607/53738) **查询房间录制信息**
您可以通过这个接口，查询指定房间的录制信息。包括进行中的录制任务taskid、订阅的白名单/黑名单用户ID。

- [***DescribeRecordInfo()***](https://www.tencentcloud.com/document/product/607/53739) **查询录制任务信息**
您可以通过这个接口，查询某个taskid的任务信息。包括录制类型、录制的房间ID、录制的用户ID、录制文件信息


### 3、录制机制

#### 录制任务启动机制
- 您调用 ***StartRecord()*** 接口后，指定的房间录制任务将会启动

#### 录制任务终止机制
- 您调用 ***StopRecord()*** 接口后，指定的房间录制任务将会结束


#### 录音文件生成时机
- 房间混流录音文件：房间录制任务启动后，若房间已有用户，则混流音频文件立刻开始生成；若房间内无用户，则第一个用户进房后，混流音频文件立刻开始生成
- 用户单流录音文件：房间录制任务启动后，在录制范围内的用户进房，则该用户的单流音频文件立刻开始生成。


#### 录制任务分片机制

- 当单个音频文件时长达到两个小时，将自动进行音频文件分片
- 当用户关麦，用户单流录制音频将自动分片，用户开麦后启动新的分片
- 若录制中的任务异常中断，任务自动重连后将启动新的分片


#### 录制任务事件通知机制

- 录制任务事件通过回调机制通知到您配置的回调地址。当发生这些事件时，您会收到回调通知：**录制开始**、**录制停止**、**录制文件上传完成**
- 关于回调信息的详情，请参考 [录制回调说明](https://www.tencentcloud.com/document/product/607/53749)


### 4、存储位置

GME服务端录制，录制完成后的音频文件将存储在您账号下的**对象存储COS**服务中的指定存储桶。存储桶地域由您指定，可选的地域列表请参考[对象存储地域说明](https://www.tencentcloud.com/document/product/436/6224)。


### 5、录制文件格式

- .mp3


### 6、录制文件命名规则

- 用户单流录制文件：bizid_roomid_userid/${任务开始时间}_${id}_audio.mp3
- 房间混流录制文件：bizid_roomid/${taskid}_${任务开始时间}_${id}_audio.mp3

 ***bizid:*** GME应用ID。可在[GME控制台](https://console.tencentcloud.com/gamegme)获取
 ***roomid:*** 语音房间ID。是您在使用实时语音服务时定义并传入至GME SDK
 ***userid:*** 玩家ID。是您在使用实时语音服务时定义并传入至GME SDK
 ***taskid:*** 录制任务ID，由GME录制服务生成。每一次成功调用 录制任务都具有一个独特的任务ID
 ***id:*** 针对一个录制任务的分片的序列号。序列号初始序号为0



## 接入步骤

<dx-steps>
-<dx-tag-link link="#StartRealTimeASR" tag="业务侧">在控制台完成录制服务配置</dx-tag-link>
-<dx-tag-link link="#StartRealTimeASR" tag="业务侧">调用服务端接口，定义录制范围</dx-tag-link>
-<dx-tag-link link="#callback" tag="业务侧">接收录制任务回调（可选）</dx-tag-link> 
-<dx-tag-link link="#result" tag="业务侧"> 查看/管理录制文件</dx-tag-link>
</dx-steps>


### 步骤一：在控制台完成录制服务配置

登录[GME控制台](https://console.tencentcloud.com/gamegme)，进入【服务管理】菜单，对希望启用录制服务的应用点击【设置】，进入应用详情页。
- #### 开通/关闭录制服务

![](https://qcloudimg.tencent-cloud.cn/raw/4d72f57ae8f4463bc009d8ef8048232e.png)


在页面中对【语音录制服务】点击 **修改** ，将录制开关置为 **开启** 。

首次开启录制服务时，GME将会向您申请服务授权，以便于访问您的**对象存储COS服务**，您需要在弹窗页面需要同意授权后，才能正常开启服务端录制服务。


![](https://qcloudimg.tencent-cloud.cn/raw/5e38302c5e3b0013ba53bd29af14fab2.png)

- #### 录音文件存储配置

在 **录制文件存储桶** 点击 **绑定** 。
在 **绑定存储桶**弹窗中，您可以绑定一个已有的COS存储桶（已有的存储桶需要您在[COS控制台](https://console.tencentcloud.com/cos/bucket)先行创建），或新建一个存储桶。

![](https://qcloudimg.tencent-cloud.cn/raw/30faa09353cdd31c537803f72bca25b2.png)

- #### 录制事件回调配置（可选）
如果您希望接收录制服务的事件回调，可以配置回调地址。操作路径：进入应用详情页面，在页面中对【语音录制服务】点击 **修改** ，在 **回调地址** 点击 **修改** ，在弹窗中输入接收回调的url地址。目前仅针对录制任务完成状态推送事件回调消息。

![](https://qcloudimg.tencent-cloud.cn/raw/cbc0275b887b6bd402f41f9f5c325a5b.png)

- #### 录制范围配置
录制范围可选自定义录制或全量录制。您此时应选中自定义录制，否则调用服务端相关接口将会失败。


完成上述配置后，点击 **保存**，录制服务即可开启。若您不再需要使用录制服务，请及时在控制台将录制服务开关置为 **关闭**， 避免产生预期之外的费用。



### 步骤二：接收录制任务回调（可选）

如果您在**步骤一**中配置了回调地址，则可以接收录制任务事件回调。


### 步骤三：调用服务端接口，定义录制范围
您需要根据业务场景实际需求来调用相关接口。在调用时序和流程的设计上，请注意：
- （1）仅支持对已存在的RoomId发起开始录制请求。若RoomId不存在，录制任务将创建失败
- （2）若您没有主动调用停止录制，在房间内有用户的情况下，录制进程将一直保持。若房间内用户已全部退房，原录制任务进程将保持12小时。在这段保持的时间内，若用户重新进房，将自动开始录制。若已超过录制进程的保持时间，用户进房将不会自动开始录制



### 步骤四：查看/管理录制文件

一个录制任务结束后的数分钟内即可生成完成的音频文件。您需要登录您的[对象存储COS控制台](https://console.tencentcloud.com/cos/bucket)对录制文件进行查看和管理。







