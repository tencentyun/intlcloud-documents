在线教育、秀场直播、视频会议、在线医疗、远程银行等应用场景中，考虑内容审核、录像存档和视频回放等需求，常需要将整个视频通话或互动直播过程录制和存储下来的情况，可以通过云端录制功能实现。

## 功能概述
通过 TRTC 的云端录制功能，您可以通过调用 REST API 接口，启动云端录制任务订阅需要录制的音视频流，实时灵活控制。并且无需开发者自行部署服务器和录制相关模块，更轻量便捷易用。

- 录制模式：单流录制可以将房间中的每一个用户的音视频流都录制成独立的文件；混流录制可以把同一个房间的音视频媒体流混流录制成一个文件

* 订阅流：支持通过制定订阅用户的黑白名单的方式来指定您需要订阅的用户媒体流
* 转码参数：混流的场景下，支持通过设置编解码的参数来指定录制的视频文件的质量
* 混流参数：混流的场景下，支持多种灵活可变的自动多画面布局模板和自定义布局模板
* 文件存储：支持指定录制的文件保存在云存储/云点播，当前云存储厂商支持腾讯云的 COS 存储，云点播厂商支持腾讯云点播
  （未来会支持其他云厂商的存储和点播服务，届时需要您提供云服务账号，云存储服务需要提供存储参数）
* 回调通知：支持回调通知的能力，通过配置回调域名，云端录制的事件状态会通知到您的回调服务器

### 单流录制

![单流录制](https://qcloudimg.tencent-cloud.cn/raw/cd843d26b27ed6f4179ebbff401ae6e3.png)

如图所示为单流录制的场景，房间1234里面主播1和主播2都上行了音视频流，假设您订阅了主播1和主播2的音视频流，并设置录制模式为单流录制，录制后台会分别拉取主播1和主播2的音视频流，并把他们录制成独立的媒体文件，包含：

1.  主播1的一个视频M3U8索引文件；
2.  主播1的若干个视频TS切片文件；
3.  主播1的一个音频M3U8索引文件；
4.  主播1的若干个音频TS切片文件；
5.  主播2的一个视频M3U8索引文件；
6.  主播2的若干个视频TS切片文件；
7.  主播2的一个音频M3U8索引文件；
8.  主播2的若干个音频TS切片文件；

录制后台会把这些文件上传到您指定的云存储服务器，您的业务后台需要把这些录制文件拉取下来，并根据业务的需求对这些文件进行合并转码操作，我们会提供[音视频合并转码脚本](https://intl.cloud.tencent.com/zh/document/product/647/45169#.E5.8D.95.E6.B5.81.E6.96.87.E4.BB.B6.E5.90.88.E5.B9.B6.E8.84.9A.E6.9C.AC)。

### 混流录制

![混流录制](https://qcloudimg.tencent-cloud.cn/raw/3a29f4527601abe3ac981759bf44ad07.png)

如图所示为混流录制的场景，房间1234里面有主播1和主播2都上行了音视频流，假设您订阅了主播1和主播2的音视频流，设置录制模式为混流录制，录制后台会分别拉取主播1和主播2的音视频流，并把他们的视频流按照您配置多画面模板进行混流，音频流进行混音，最后把媒体流混合成一路媒体文件，包含：

1.  混流后的的一个视频M3U8索引文件；
2.  混流后的若干个视频TS切片文件；

录制后台会把这些文件上传到您指定的云存储服务器，您的业务后台需要把这些录制文件拉取下来，并根据业务的需求对这些文件进行合并转码操作，我们会提供[音视频合并转码脚本](https://intl.cloud.tencent.com/zh/document/product/647/45169#.E5.8D.95.E6.B5.81.E6.96.87.E4.BB.B6.E5.90.88.E5.B9.B6.E8.84.9A.E6.9C.AC)。

> !
>- 录制接口的调用频率限制为20qps
>- 单个接口超时时间为6秒
>- 默认并发录制支持100路，如果需要更多路数，请[提交工单](https://console.intl.cloud.tencent.com/workorder/category?step=0&source=14)联系我们。
>- 单录制任务最大支持同时订阅的单房间内音视频流为25路。

## 调用流程
### 1. 启动录制

通过您的后台服务调用REST API （CreateCloudRecording）来启动云端的录制，需要重点关注的参数如下：

#### 任务ID（TaskId）

这个参数是本次录制任务的唯一标识，您需要保存下这个任务ID作为后续针对这个录制任务接口操作的输入参数。

#### 录制的模式（RecordMode）
- 单流录制，分别录制房间中的您所订阅的主播的音频和视频文件并将录制文件（M3U8/TS）上传至云存储；
- 混流录制，将房间内您所订阅所有主播的音视频流混录成一个音视频文件并将录制文件[M3U8/TS]上传至云存储；

#### 录制用户的黑白名单（SubscribeStreamUserIds）
默认情况下，云端录制会订阅房间内所有的媒体流（最多25路），您也可以通过该参数指定订阅的主播用户的黑白名单信息，当然我们也支持在录制的过程中进行更新操作。

#### 云存储参数（StorageParams）
通过指定云存储参数，我们会为您把录制后的文件上传到您所开通的指定云存储/云点播服务，请关注云存储/云点播空间的参数的有效性和保持非欠费状态。这里需要注意的是录制文件名称是有固定的规则

##### 录制文件名命名规则

* 单流录制M3U8文件名规则：
\<Prefix>/\<TaskId>/\<SdkAppId>\_\<RoomId>\_\_UserId\_s\_\<UserId>\_\_UserId\_e\_\<MediaId>\_\<Type>.m3u8

* 单流录制TS文件名规则为：
\<Prefix>/\<TaskId>/\<SdkAppId>\_\<RoomId>\_\_UserId\_s\_\<UserId>\_\_UserId\_e\_\<MediaId>\_\<Type>\_\<UTC>.ts

* 单流录制mp4文件名规则为：
\<Prefix>/\<TaskId>/\<SdkAppId>\_\<RoomId>\_\_UserId\_s\_\<UserId>\_\_UserId\_e\_\<MediaId>\_\<Index>.mp4

* 混流录制M3U8文件名规则：
\<Prefix>/\<TaskId>/\<SdkAppId>\_\<RoomId>.m3u8

* 混流录制TS文件名规则：
\<Prefix>/\<TaskId>/\<SdkAppId>\_\<RoomId>\_\<UTC>.ts

* 混流录制mp4文件名规则为：
\<Prefix>/\<TaskId>/\<SdkAppId>\_\<RoomId>\_\<Index>.mp4

* 高可用拉起后的文件名规则
云录制服务在机房故障的时候会通过高可用的方案对录制任务进行恢复，这种情况下为了不覆盖原有的录制文件，拉起后会加上一个前缀ha<1/2/3>，表示发生高可用的次数。一个录制任务最大允许拉起的次数为3次。

* 单流录制M3U8 文件名规则：
\<Prefix>/\<TaskId>/ha\<1/2/3>\_\<SdkAppId>\_\<RoomId>\_\_UserId\_s\_\<UserId>\_\_UserId\_e\_\<MediaId>\_\<Type>.m3u8

* 单流录制TS文件名规则为：
\<Prefix>/\<TaskId>/ha\<1/2/3>\_\<SdkAppId>\_\<RoomId>\_\_UserId\_s\_\<UserId>\_\_UserId\_e\_\<MediaId>\_\<Type>\_\<UTC>.ts

* 混流录制M3U8 文件名规则：
\<Prefix>/\<TaskId>/ha\<1/2/3>\_\<SdkAppId>\_\<RoomId>.m3u8

* 混流录制TS文件名规则：
\<Prefix>/\<TaskId>/ha\<1/2/3>\_\<SdkAppId>\_\<RoomId>\_\<UTC>.ts

#### 字段含义说明：
\<Prefix>: 录制参数中设置的文件名前缀，如果没有设置那么就不存在；
\<TaskId>: 录制的任务ID，全局唯一，启动录制后返回参数中有携带；
\<SdkAppId>: 录制任务的SdkAppId；
\<RoomId>: 录制的房间号；
\<UserId>: 特殊的base64处理后的录制流的用户ID，见下面注意事项；
\<MediaId>: 主辅流标识，main或者aux；
\<Type>: 录制流的类型，audio或者video；
\<UTC>: 该文件开始的UTC录制时间，时区UTC+0，由年、月、日、小时、分钟、秒和毫秒组成；
\<Index>: 如果没有触发mp4切片逻辑（大小超过2GB或时长超过24小时）则无该字段，否则为切片的索引号，从1开始递增;
ha\<1/2/3>：高可用的拉起的前缀，比如第一次拉起会变成\<Prefix>/\<TaskId>/ha1\_\<SdkAppId>\_\<RoomId>.m3u8
>! 如果这里\<RoomId>如果是字符串房间ID，我们会对房间ID先做base64操作，再把base64后的字符串中符号'/'替换成 '-' (中划线), 符号'='替换成 '.' ；
录制流的\<UserId>会先做base64操作，再把base64后的字符串中符号'/'替换成 '-' (中划线), 符号'='替换成 '.' 。

#### 录制开始的时间的获取
录制开始的时间定义为第一次收到主播的音视频数据，并启动录制第一个文件的服务器unix时间。
您可以通过以下三个方法获取到录制开始的时间戳：

* 查询录制文件接口（DescribeCloudRecording）中的BeginTimeStamp字段

比如下面这个查询接口返回的信息看到BeginTimeStamp为1622186279144ms：

```json
{
  "Response": {
    "Status": "xx",
    "StorageFileList": [
      {
        "TrackType": "xx",
        "BeginTimeStamp": 1622186279144,
        "UserId": "xx",
        "FileName": "xx"
      }
    ],
    "RequestId": "xx",
    "TaskId": "xx"
  }
}
```

* 读取M3U8文件中对应的标签项（\#EXT-X-TRTC-START-REC-TIME）

比如下面这个M3U8文件表示起始录制的unix时间戳为1622425551884ms：

```m3u8
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-ALLOW-CACHE:NO
#EXT-X-MEDIA-SEQUENCE:0
#EXT-X-TARGETDURATION:70
#EXT-X-TRTC-START-REC-TIME:1622425551884
#EXT-X-TRTC-VIDEO-METADATA:WIDTH:1920 HEIGHT:1080
#EXTINF:12.074
1400123456_12345__UserId_s_MTY4NjExOQ..__UserId_e_main_video_20330531094551825.ts
#EXTINF:11.901
1400123456_12345__UserId_s_MTY4NjExOQ..__UserId_e_main_video_20330531094603825.ts
#EXTINF:12.076
1400123456_12345__UserId_s_MTY4NjExOQ..__UserId_e_main_video_20330531094615764.ts
#EXT-X-ENDLIST
```

* 监听录制回调事件

通过订阅回调，在事件类型307中的BeginTimeStamp字段您可以获取到录制文件对应的录制起始时间戳
比如下面这个回调事件，您可以读取到这个文件的录制开始的unix时间戳是1622186279144ms：

```json
{
        "EventGroupId": 3,
        "EventType":    307,
        "CallbackTs":   1622186289148,
        "EventInfo":    {
                "RoomId":       "xx",
                "EventTs":      "1622186289",
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "FileName":     "xx.m3u8",
                        "UserId":       "xx",
                        "TrackType":    "audio",
                        "BeginTimeStamp":       1622186279144
                }
        }
}
```

#### 混流录制的水印参数 （MixWatermark）
我们支持在混流录制中添加图片水印，最大支持个数为25个，可以在画布任意位置添加水印。

|字段名|解释|
|---|---|
|Top|水印相对左上角的垂直位移|
|Left|水印相对左上角的水平位移|
|Width|水印显示的宽度|
|Height|水印显示的高度|
|url|水印文件的存储url|

#### 混流录制的布局模式参数（MixLayoutMode）
我们支持九宫格布局（默认），悬浮布局，屏幕分享布局和自定义布局四种布局

##### 九宫格布局：

根据主播的数量自动调整每个画面的大小，每个主播的画面大小一致，最多支持25个画面。

* 子画面为1个时：
每个小画面的宽和高分别为整个画布宽和高;

* 子画面为2个时：
每个小画面的宽为整个画布宽的1/2;
每个小画面的高为整个画布高;

* 子画面小于等于4个时：
每个小画面的宽和高分别为整个画布宽和高的 1/2;

* 子画面小于等于9个时：
每个小画面的宽和高分别为整个画布宽和高的 1/3;

* 子画面小于等于16个时：
每个小画面的宽和高分别为整个画布宽和高的 1/4;

* 子画面大于16个时：
每个小画面的宽和高分别为整个画布宽和高的1/5;

 九宫格布局随着订阅的子画面增加按照下图进行变化：

![九宫格布局1](https://qcloudimg.tencent-cloud.cn/raw/9d989363167bd9231a1ebf3097b8fb5c.jpg)
![九宫格布局2](https://qcloudimg.tencent-cloud.cn/raw/cd5437606f3a5dceb723d6e63eb283ee.jpg)
![九宫格布局3](https://qcloudimg.tencent-cloud.cn/raw/98295756807b1aba1457f668f85d7fd9.jpeg)
![九宫格布局4](https://qcloudimg.tencent-cloud.cn/raw/87b3d8d21d3e22704c379a534faf37b8.jpeg)
![九宫格布局5](https://qcloudimg.tencent-cloud.cn/raw/3418887536457bfa607ecdfb34a71b7f.jpeg)
![九宫格布局6](https://qcloudimg.tencent-cloud.cn/raw/ae3aa97ee2cbe5678f1672b34a610d20.jpeg)

##### 悬浮布局：
默认第一个进入房间的主播（也可以指定一个主播）的视频画面会铺满整个屏幕。其他主播的视频画面从左下角开始依次按照进房顺序水平排列，显示为小画面，小画面悬浮于大画面之上。当画面数量小于等于17个时，每行4个（4 x 4排列）。当画面数量大于17个时，重新布局小画面为每行5个（5 x 5）排列。最多支持25个画面，如果用户只发送音频，仍然会占用画面位置。

* 子画面小于等于17个时：
       每个小画面的宽和高分别为整个画布宽和高的 0.235；
       相邻小画面的左右和上下间距分别为整个画布宽和高的 0.012；
       小画面距离画布的水平和垂直边距也分别为整个画布宽和高的 0.012；

* 子画面大于17个时：
       每个小画面的宽和高分别为整个画布宽和高的 0.188；
       相邻小画面的左右和上下间距分别为整个画布宽和高的 0.01；
       小画面距离画布的水平和垂直边距也分别为整个画布宽和高的 0.01；

  悬浮布局随着订阅的子画面增加按照下图进行变化：
   ![悬浮布局1](https://qcloudimg.tencent-cloud.cn/raw/96a531ba9f6a69297ea4f1a5a365794a.jpg)
   ![悬浮布局2](https://qcloudimg.tencent-cloud.cn/raw/be91b17b6b557fcd7d1d76c589e15917.jpg)


##### 屏幕分享布局：
指定一个主播在屏幕左侧的大画面位置（如果不指定，那么大画面位置为背景色），其他主播自上而下依次垂直排列于右侧。当画面数量少于17个的时候，右侧每列最多8人，最多占据两列。当画面数量多于17个的时候，超过17个画面的主播从左下角开始依次水平排列。最多支持24个画面，如果主播只发送音频，仍然会占用画面位置。

* 子画面小于等于5个时:
右侧小画面的宽为整个画布宽的1/5, 右侧小画面的高为整个画布高的1/4；
左侧大画面的宽为整个画布宽的4/5, 左侧大画面的高为整个画布高;

* 子画面大于5且小于等于7个时:
右侧小画面的宽为整个画布宽的1/7, 右侧小画面的高为整个画布高的1/6；
左侧大画面的宽为整个画布宽的6/7, 左侧大画面的高为整个画布高;
* 子画面大于7且小于等于9个时:
右侧小画面的宽为整个画布宽的1/9, 右侧小画面的高为整个画布高的1/8；
左侧大画面的宽为整个画布宽的8/9, 左侧大画面的高为整个画布高;

* 子画面大于9小于等于17个时:
右侧小画面的宽为整个画布宽的1/10,右侧小画面的高为整个画布高的1/8；
左侧大画面的宽为整个画布宽的4/5,左侧大画面的高为整个画布高;

* 子画面大于17个时:
右（下）侧小画面的宽为整个画布宽的1/10,右（下）侧小画面的高为整个画布高的1/8；
左侧大画面的宽为整个画布宽的4/5,左侧大画面的高为整个画布高的7/8;

屏幕分享布局随着订阅的子画面增加按照下图进行变化：
   ![屏幕分享布局1](https://qcloudimg.tencent-cloud.cn/raw/d64e7e705060d21ec24d7392f8d43728.png)
   ![屏幕分享布局2](https://qcloudimg.tencent-cloud.cn/raw/695683aecb62c29976f16124d6e9b29b.png)
   ![屏幕分享布局3](https://qcloudimg.tencent-cloud.cn/raw/8423e777eb1a5bfb80e384e7b97db49d.png)
   ![屏幕分享布局4](https://qcloudimg.tencent-cloud.cn/raw/538faeb7d2f993427b7ab1db548cb633.png)
   ![屏幕分享布局4](https://qcloudimg.tencent-cloud.cn/raw/f911eb5a849da0aa22ed9b69ebe2f63a.png)

##### 自定义布局：
根据您的业务需要在 MixLayoutList 内自己定制每个主播画面的布局信息。

### 2. 查询录制（DescribeCloudRecording）
如果需要，您可以调用该接口查询录制服务的状态，注意，只有录制任务存在的时候才能查询到信息，如果录制任务已经结束会返回错误。
录制的文件列表（StorageFile）会包含本次录制的所有M3U8索引文件和录制的起始Unix时间戳信息。注意，如果是上传云点播任务，该接口返回的StorageFile为空。

### 3. 更新录制（ModifyCloudRecording）
如果需要，您可以调用该接口修改录制服务的参数，如订阅黑白名单SubscribeStreamUserIds（单流和混流录制有效），录制的模板参数MixLayoutParams（混流录制有效），注意更新操作是全量覆盖的操作，并不是增量更新的操作，您每次更新都需要携带全量的信息，包括模板参数MixLayoutParams和黑白名单SubscribeStreamUserIds，因此您需要保存之前的启动录制的参数或者重新计算完整的录制相关参数。

### 4. 停止录制（DeleteCloudRecording）
在录制结束之后需要调用停止录制（DeleteCloudRecording）的接口来结束录制任务，否则录制任务会等待到达预设的超时时间MaxIdleTime后自动结束。需要注意MaxIdleTime的定义是房间内持续没有主播的状态超过MaxIdleTime的时长，这里如果房间是存在有主播，但是主播没有上行数据是不会进入超时的计时状态的。建议业务在录制结束的时候调用此接口结束录制任务。

## 高级功能

### 录制mp4文件

如果希望录制的输出文件格式是mp4格式，可以在启动录制的参数(OutputFormat)指定录制文件输出格式为hls+mp4。默认依然会录制hls文件，在hls录制完成后会立即触发转mp4任务，从hls所在的cos内拉流进行mp4封装，再上传到客户的cos中。
注意这里需要提供COS的文件下拉权限，否则转mp4任务会因为下拉hls文件失败而终止。
mp4文件将在以下情况下强制分片。

1. 录制时长超过24小时;
2. 单个mp4文件大小达到2GB;
   <br>具体的流程如图所示
   <br>![输出mp4](https://qcloudimg.tencent-cloud.cn/raw/d3a3f5121e9832cc8a39b8d9ec6f7b1a.png)

### 录制上传点播

如果希望将录制的输出文件上传至点播平台，可以在启动录制的存储参数(StorageParams)中指定CloudVod成员参数。录制后台会在录制结束后将录制的mp4文件通过您指定的方式上传到点播平台，并通过回调的形式把播放地址发送给您。如果录制模式为单流录制模式，每一个订阅的主播都会有一个对应的播放地址；如果录制模式为混流录制模式，只有一个混流后媒体的播放地址。上传点播任务有以下几个注意事项。

1. 存储参数中的CloudVod和CloudStorage只能同时指定一个，否则发起录制将失败；
2. 上传点播任务的过程中使用DescribeCloudRecording查询到的任务状态，不会携带录制文件的信息；
   <br>具体的流程如图所示，这里的云存储为录制内部云存储，客户不用填写相关参数。
   <br>![输出vod](https://qcloudimg.tencent-cloud.cn/raw/28da00ba87fc1b9be2030f96d2dfd820.png)



### 单流文件合并脚本

我们提供了[合并单流音视频文件的脚本]()，用于把单流录制的音视频文件合并成MP4文件。

>? 如果两个切片之间的时间间隔超过15秒，间隔时间内没有任何音频/视频信息（如果禁用了辅流，则会忽略辅流信息），我们把这两个切片看作两个不同的分段。其中录制时间较早的切片看作前一个分段的结束切片，录制时间较晚的切片看作后一个分段的开始切片。

 - 分段模式（-m 0）
此模式下，脚本将每个UserId下的录制文件按分段合并，一个UserId下的分段被独立合并为一个个文件。
 - 合并模式（-m 1）
把同一个UserId下的所有分段合并为一个音视频文件。可利用 -s 选项选择是否填充各个分段之间的间隔。

#### 依赖环境

Python3

-   Centos：sudo yum install python3
-   Ubuntu：sudo apt-get install python3

Python3 依赖包

-	sortedcontainers：pip3 install sortedcontainers

#### 使用方法

 1.运行合并脚本：python3 TRTC_Merge.py [option]
 2.会在录制文件目录下生成合并后的mp4文件
例如：python3 TRTC_Merge.py -f /xxx/file -m 0

可选参数和对应功能见下表:

|参数| 功能 |
|---|---|
|-f | 指定待合并文件的存储路径。如果有多个UserId的录制文件，脚本会分别进行合并操作。 |
|-m   | 0：分段模式(默认设置)，此模式下，脚本将每个UserId下的录制文件按分段合并，每个UserId有可能产生多个文件。 <br>1：合并模式，一个UserId下的所有音视频文件合并为一个文件。|
|-s|保存模式。如果设置了该参数，则合并模式下的分段之间的空白部分被删除，文件的实际时常小于物理时常。|
|-a|0: 主流合并(默认设置)，同一个UserId的主流和音频做合并，辅流不会和音频做合并。 <br>1: 自动合并，如果主流存在则主流和音频合并，如果主流不存在辅流存在则辅流和音频做合并。 <br>2: 辅流合并，同一个UserId的辅流和音频做合并，主流不会和音频做合并|
|-p|指定输出视频的fps。默认为15 fps，有效范围5-120 fps，低于5 fps计为5 fps，高于120 fps计为120 fps。|
|-r|指定输出视频的分辨率。如 -r 640 360，表示输出视频的宽为640，高为360。|

**文件名规则**

- 音视频文件名规则：UserId\_timestamp\_av.mp4
- 纯音频文件名规则：UserId\_timestamp.m4a

>? 这里的UserId为录制流的用户ID特殊的base64值，详见启动录制中文件名命名规则相关说明。timestamp为每个分段的首个ts切片启动录制的时间。



## 回调接口

您可以提供一个接收回调的Http/Https 服务网关来订阅回调消息。当相关事件发生时，云录制系统会回调事件通知到您的消息接收服务器。

### 事件回调消息格式

事件回调消息以 HTTP/HTTPS POST 请求发送给您的服务器，其中：
字符编码格式：UTF-8。
请求：body 格式为 JSON。
应答：HTTP STATUS CODE = 200，服务端忽略应答包具体内容，为了协议友好，建议客户应答内容携带 JSON： {"code":0}。

### 参数说明

事件回调消息的 header 中包含以下字段：


| 字段名       | 值                 |
| ------------ | ------------------ |
| Content-Type | application/json   |
| Sign         | 签名值             |
| SdkAppId     | sdk application id |

事件回调消息的 body 中包含以下字段：

| 字段名       | 类型        | 含义                                                         |
| ------------ | ----------- | ------------------------------------------------------------ |
| EventGroupId | Number      | 事件组 ID， 云端录制固定为3                                  |
| EventType    | Number      | 回调通知的事件类型                                           |
| CallbackTs   | Number      | 事件回调服务器向您的服务器发出回调请求的 Unix 时间戳，单位为毫秒 |
| EventInfo    | JSON Object | 事件信息                                                     |

事件类型说明

| 字段名                                                | 类型 | 含义                                                    |
| ----------------------------------------------------- | ---- | ------------------------------------------------------- |
| EVENT\_TYPE\_CLOUD\_RECORDING\_RECORDER\_START        | 301  | 云端录制 录制模块启动                                   |
| EVENT\_TYPE\_CLOUD\_RECORDING\_RECORDER\_STOP         | 302  | 云端录制 录制模块退出                                   |
| EVENT\_TYPE\_CLOUD\_RECORDING\_UPLOAD\_START          | 303  | 云端录制 上传模块启动                                   |
| EVENT\_TYPE\_CLOUD\_RECORDING\_FILE\_INFO             | 304  | 云端录制 生成m3u8索引文件，第一次生成并且上传成功后回调 |
| EVENT\_TYPE\_CLOUD\_RECORDING\_UPLOAD\_STOP           | 305  | 云端录制 上传结束                                       |
| EVENT\_TYPE\_CLOUD\_RECORDING\_FAILOVER               | 306  | 云端录制 发生迁移，原有的录制任务被迁移到新负载上时触发 |
| EVENT\_TYPE\_CLOUD\_RECORDING\_FILE\_SLICE            | 307  | 云端录制 生成M3U8文件(切出第一个ts分片) 生成后回调      |
| EVENT\_TYPE\_CLOUD\_RECORDING\_UPLOAD\_ERROR          | 308  | 云端录制 上传模块发生错误                               |
| EVENT\_TYPE\_CLOUD\_RECORDING\_DOWNLOAD\_IMAGE\_ERROR | 309  | 云端录制 下载解码图片文件发生错误                       |
| EVENT\_TYPE\_CLOUD\_RECORDING\_MP4\_STOP              | 310  | 云端录制 mp4录制任务结束，回调包含录制的mp4文件名       |
| EVENT\_TYPE\_CLOUD\_RECORDING\_VOD\_COMMIT            | 311  | 云端录制 vod录制任务上传媒体资源完成                    |
| EVENT\_TYPE\_CLOUD\_RECORDING\_VOD\_STOP              | 312  | 云端录制 vod录制任务结束                                |


事件信息说明

| 字段名  | 类型          | 含义                                 |
| ------- | ------------- | ------------------------------------ |
| RoomId  | String/Number | 房间名（类型与客户端房间号类型一致） |
| EventTs | Number        | 时间发生的 Unix 时间戳，单位为秒     |
| UserId  | String        | 录制机器人的用户 ID                  |
| TaskId  | String        | 录制ID，一次云端录制任务唯一的ID     |
| Payload | JsonObject    | 根据不同事件类型定义不同             |

事件类型为301 EVENT\_TYPE\_CLOUD\_RECORDING\_RECORDER\_START 时Payload的定义

| 字段名 | 类型   | 含义                                               |
| ------ | ------ | -------------------------------------------------- |
| Status | Number | 0：代表录制模块启动成功，1：代表录制模块启动失败。 |

```json
{
        "EventGroupId": 3,
        "EventType":    301,
        "CallbackTs":   1622186275913,
        "EventInfo":    {
                "RoomId":       "xx",
                "EventTs":      "1622186275",
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Status":       0
                }
        }
}
```

事件类型为302 EVENT\_TYPE\_CLOUD\_RECORDING\_RECORDER\_STOP 时Payload的定义

| 字段名    | 类型   | 含义                                                         |
| --------- | ------ | ------------------------------------------------------------ |
| LeaveCode | Number | 0：代表录制模块正常调用停止录制退出；<br>1: 录制机器人被客户踢出房间；<br>2：客户解散房间；<br>3：服务器将录制机器人踢出；<br>4：服务器解散房间；<br>99：代表房间内除了录制机器人没有其他用户流，超过指定时间退出；<br>100：房间超时退出；<br>101：同一用户重复进入相同房间导致机器人退出 |

```json
{
        "EventGroupId": 3,
        "EventType":    302,
        "CallbackTs":   1622186354806,
        "EventInfo":    {
                "RoomId":       "xx",
                "EventTs":      "1622186354",
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "LeaveCode":    0
                }
        }
}
```

事件类型为303 EVENT\_TYPE\_CLOUD\_RECORDING\_UPLOAD\_START 时Payload的定义

| 字段名 | 类型   | 含义                                                   |
| ------ | ------ | ------------------------------------------------------ |
| Status | Number | 0：代表上传模块正常启动<br>1：代表上传模块初始化失败。 |

```json
{
        "EventGroupId": 3,
        "EventType":    303,
        "CallbackTs":   1622191965320,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191965,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Status":       0
                }
        }
}
```

事件类型为304 EVENT\_TYPE\_CLOUD\_RECORDING\_FILE\_INFO 时Payload的定义

| 字段名   | 类型   | 含义             |
| -------- | ------ | ---------------- |
| FileList | String | 生成的M3U8文件名 |

```json
{
        "EventGroupId": 3,
        "EventType":    304,
        "CallbackTs":   1622191965350,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191965,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "FileList":     "xx.m3u8"
                }
        }
}
```


事件类型为305 EVENT\_TYPE\_CLOUD\_RECORDING\_UPLOAD\_STOP 时Payload的定义

| 字段名 | 类型   | 含义                                                         |
| ------ | ------ | ------------------------------------------------------------ |
| Status | Number | 0: 代表此次录制上传任务已经完成，所有的文件均已上传到指定的第三方云存储<br>1：代表此次录制上传任务已经完成，但至少有一片文件滞留在服务器或者备份存储上<br>2: 代表滞留在服务器或者备份存储上的文件已经恢复上传到指定的第三方云存储 |

```json
{
        "EventGroupId": 3,
        "EventType":    305,
        "CallbackTs":   1622191989674,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191989,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Status":       0
                }
        }
}
```

事件类型为306 EVENT\_TYPE\_CLOUD\_RECORDING\_FAILOVER 时Payload的定义

| 字段名 | 类型   | 含义                    |
| ------ | ------ | ----------------------- |
| Status | Number | 0: 代表此次迁移已经完成 |

```json
{
        "EventGroupId": 3,
        "EventType":    306,
        "CallbackTs":   1622191989674,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191989,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Status":       0
                }
        }
}
```

事件类型为307 EVENT\_TYPE\_CLOUD\_RECORDING\_FILE\_SLICE 时Payload的定义

| 字段名         | 类型   | 含义                                |
| -------------- | ------ | ----------------------------------- |
| FileName       | String | m3u8文件名                          |
| UserId         | String | 本录制文件对应的用户ID              |
| TrackType      | String | audio/video/audio_video             |
| BeginTimeStamp | Number | 录制开始时，服务器Unix时间戳（毫秒) |


```json
{
        "EventGroupId": 3,
        "EventType":    307,
        "CallbackTs":   1622186289148,
        "EventInfo":    {
                "RoomId":       "xx",
                "EventTs":      "1622186289",
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "FileName":     "xx.m3u8",
                        "UserId":       "xx",
                        "TrackType":    "audio",
                        "BeginTimeStamp":       1622186279144
                }
        }
}
```

事件类型为308 EVENT\_TYPE\_CLOUD\_RECORDING\_UPLOAD\_ERROR 时Payload的定义

| 字段名  | 类型   | 含义                       |
| ------- | ------ | -------------------------- |
| Code    | String | 第三方云存储的返回code     |
| Message | String | 第三方云存储的返回消息内容 |


```json
{
  "Code": "InvalidParameter",
  "Message": "AccessKey invalid"
}

{
        "EventGroupId": 3,
        "EventType":    308,
        "CallbackTs":   1622191989674,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191989,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Code":       "xx",
                        "Message":    "xx"
                }
        }
}
```

事件类型为309 EVENT\_TYPE\_CLOUD\_RECORDING\_DOWNLOAD\_IMAGE\_ERROR 时Payload的定义

| 字段名 | 类型   | 含义          |
| ------ | ------ | ------------- |
| Url    | String | 下载失败的url |


```json
{
        "EventGroupId": 3,
        "EventType":    309,
        "CallbackTs":   1622191989674,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191989,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Url":       "http://xx",
                }
        }
}
```

事件类型为310 EVENT\_TYPE\_CLOUD\_RECORDING\_MP4\_STOP 时Payload的定义

| 字段名   | 类型   | 含义                                                         |
| -------- | ------ | ------------------------------------------------------------ |
| Status   | Number | 0: 代表此次录制mp4任务已经正常退出，所有的文件均已上传到指定的第三方云存储<br>1：代表此次录制mp4任务已经正常退出，但至少有一片文件滞留在服务器或者备份存储上<br>2: 代表此次录制mp4任务异常退出(可能原因是拉取cos的hls文件失败) |
| FileList | String | 生成的M3U8文件名                                             |


```json
{
        "EventGroupId": 3,
        "EventType":    310,
        "CallbackTs":   1622191989674,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191989,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Status":       0,
                        "FileList": ["xxxx1.mp4", "xxxx2.mp4"]
                }
        }
}
```

事件类型为311 EVENT\_TYPE\_CLOUD\_RECORDING\_VOD\_COMMIT 时Payload的定义

| 字段名    | 类型   | 含义                                                         |
| --------- | ------ | ------------------------------------------------------------ |
| Status    | Number | 0: 代表本录制文件正常上传至点播平台<br>1：代表本录制文件滞留在服务器或者备份存储上<br>2: 代表本录制文件上传点播任务异常 |
| UserId    | String | 本录制文件对应的用户ID（当录制模式为混流模式时，此字段为空） |
| TrackType | String | audio/video/audio_video                                      |
| MediaId   | String | main/aux                                                     |
| FileId    | String | 本录制文件在点播平台的唯一id                                 |
| VideoUrl  | String | 本录制文件在点播平台的播放地址                               |
| CacheFile | String | 本录制文件对应的mp4文件名（未上传点播之前）                  |
| Errmsg    | String | statue不为0时，对应的错误信息                                |


上传成功的回调：

```json
{
        "EventGroupId": 3,
        "EventType":    311,
        "CallbackTs":   1622191965320,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191965,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Status":       0,
                        "TencentVod":   {
                            "UserId":       "xx",
                            "TrackType":    "audio_video",
                            "MediaId":      "main",
                            "FileId":       "xxxx",
                            "VideoUrl":     "http://xxxx"
                        }
                }
        }
}
```

上传失败的回调：

```json
{
        "EventGroupId": 3,
        "EventType":    311,
        "CallbackTs":   1622191965320,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191965,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Status":       1,
                        "Errmsg":       "xxx",
                        "TencentVod":   {
                            "UserId":       "123",
                            "TrackType":    "audio_video",
                            "CacheFile":    "xxx.mp4"
                        }
                }
        }
}
```

事件类型为312 EVENT\_TYPE\_CLOUD\_RECORDING\_VOD\_STOP 时Payload的定义

| 字段名 | 类型   | 含义                                                         |
| ------ | ------ | ------------------------------------------------------------ |
| Status | Number | 0: 代表本次上传vod任务已经正常退出<br>1：代表本次上传vod任务异常退出 |


```json
{
        "EventGroupId": 3,
        "EventType":    312,
        "CallbackTs":   1622191965320,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191965,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Status":       0
                }
        }
}
```





## 最佳实践

为了保障录制的高可用，建议客户在集成Restful API的同时注意以下几点：

1. 调用CreateCloudRecording请求后，请关注http response, 如果请求失败，那么需要根据具体的状态码采取相应的重试策略。

   错误码是由“一级错误码”和“二级错误码”组合而成，例如"InvalidParameter.SdkAppId"。

   - **如果返回的Code是InternalError.xxxxx，说明遇到了服务端错误，可以使用相同的参数重试多次，直到返回正常，拿到taskid为止。建议使用退避重试策略，如第一次3s重试，第二次6s重试，第三次12s重试，以此类推。**
   - 如果返回的Code是InValidParameter.xxxxx，说明输入的参数有误，请根据提示检查参数。
   - 如果返回的Code是FailedOperation.RestrictedConcurrency，说明客户的并发录制任务数，超过了后台预留的资源(默认是100路)，请联系腾讯云技术支持来调整最高并发路数限制。

2. 调用CreateCloudRecording接口时，指定的UserId/UserSig是录制作为单独的机器人用户加入房间的id，请不要和TRTC房间内的其他用户重复。同时，TRTC客户端加入的房间类型必须和录制接口指定的房间类型保持一直，比如SDK创建房间用的是字符串房间号，那么云端录制的房间类型也需要相应设置成字符串房间号。

3. 录制状态查询，客户可以通过以下几种方式来得到录制相应的文件信息。

   - 成功发起CreateCloudRecording任务后15s左右，调用DescribeCloudRecording接口查询录制文件对应的信息，如果查询到状态为idle说明录制没有拉到上行的音视频流，请检查房间内是否有主播上行。
   - 成功发起CreateCloudRecording后，在确保房间有上行音视频的情况下，可以按照录制文件名的生成规则来拼接录制文件名称。具体文件名规则请看上面(这里链接到文件名规则)。
   - 录制文件的状态会通过回调发送到客户的服务器，如果订阅了相关回调，将会收到录制文件的状态信息。（这里链接到回调页面）
   - 通过Cos来查询录制文件，发起云端录制的时候可以指定存储在cos的目录，录制任务结束以后，可以找到对应的目录来找到录制文件。

4. 录制用户(userid)的usersig过期时间应该设置成比录制任务生命周期更长的时间。防止录制任务机器断网，在内部高可用生效的时候，恢复录制因为usersig过期而失败

