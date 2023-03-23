为方便 Flutter 开发者调试和接入腾讯云游戏多媒体引擎客户端 API，本文为您介绍适用于 Flutter 语音消息服务及转文本服务的接入技术文档。

## 使用 GME 重要事项

GME 提供实时语音服务、语音消息服务及转文本服务，使用 GME 服务都依赖 Init 和 Poll 等核心接口。

#### 重点提示
- 已完成 GME 应用创建，并获取 SDK AppID 和 Key。请参见 [服务开通指引](https://intl.cloud.tencent.com/document/product/607/10782)。

- 已开通 **GME 实时语音服务、语音消息服务以及转文本服务**。请参见 [服务开通指引](https://intl.cloud.tencent.com/document/product/607/10782)。

- GME 使用前请对工程进行配置，否则 SDK 不生效。

- GME 的接口调用成功后返回值为 GmeError.AV_OK，数值为 0。

- GME 的接口调用要在同一个线程下。

- GME 需要周期性的调用 Poll 接口触发事件回调。

- 错误码详情可参见 [错误码](https://intl.cloud.tencent.com/document/product/607/33223)。
  

   > **注意**
   > 

   > 语音转文本相关接口有默认频率限制，限额范围内计费方式请参见 [计费文档](https://intl.cloud.tencent.com/document/product/607/50009)；若需提升接口频率限额或了解超额计费方式，请联系商务或 [提交工单咨询](https://console.cloud.tencent.com/workorder/category?level1_id=438&level2_id=445&source=0&data_title=%E6%B8%B8%E6%88%8F%E5%A4%9A%E5%AA%92%E4%BD%93%E5%BC%95%E6%93%8EGME&step=1)。
   > 
>   - 语音消息非流式转文本接口 ***SpeechToText()*** ：默认单账号限制并发数为10路
>   - 语音消息流式转文本接口 ***StartRecordingWithStreamingRecognition()***：默认单账号限制并发数为50路


## 接入 SDK

### 重要步骤

接入 SDK 重要流程如下：

![](https://qcloudimg.tencent-cloud.cn/raw/c8758a24fe68fc084b8d12b09de5e27a.jpg)

1. [初始化 GME](https://www.tencentcloud.com/document/product/607/53819)

2. [周期性调用 Poll 触发回调](https://www.tencentcloud.com/document/product/607/53819)

3. [鉴权初始化](https://www.tencentcloud.com/document/product/607/53819)

4. [启动流式语音识别](https://www.tencentcloud.com/document/product/607/53819)

5. [停止录制](https://www.tencentcloud.com/document/product/607/53819)

6. [反初始化 GME](https://www.tencentcloud.com/document/product/607/53819)


### dart 文件
``` bash
gme.dart      GME 业务实现接口
gmeType.dart  GME 类型定义文件
gmeError.dart GME 错误类型定义文件
```

## 核心接口
<table>
<tr>
<td rowspan="1" colSpan="1" >接口</td>

<td rowspan="1" colSpan="1" >接口含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >InitSDK</td>

<td rowspan="1" colSpan="1" >初始化 GME</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Poll</td>

<td rowspan="1" colSpan="1" >触发事件回调</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Uninit</td>

<td rowspan="1" colSpan="1" >反初始化 GME</td>
</tr>
</table>


### 导入Gme模块
``` bash
import 'package:gme/gme.dart';
import 'package:gme/gmeType.dart';
```

### 获取实例

var m_context = await ITMGContext.GetInstance();

### 初始化 SDK

未初始化前，SDK 处于未初始化阶段，**需要通过接口 Init 初始化 SDK**，才可以使用实时语音服务、语音消息服务及转文本服务。调用 Init 接口的线程必须于其他接口在同一线程,建议都在主线程调用接口。

#### 接口原型
``` bash
Future<int> InitSDK(String appID, String openID)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >sdkAppId</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >来自 [腾讯云控制台](https://console.cloud.tencent.com/gamegme) 的 GME 服务提供的 AppID，获取请参见 [语音服务开通指引](https://intl.cloud.tencent.com/document/product/607/10782#.E9.87.8D.E7.82.B9.E5.8F.82.E6.95.B0)。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >openID</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >openID 只支持 Int64 类型（转为 string 传入），规则由 App 开发者自行制定，App 内不重复即可。如需使用字符串作为 Openid 传入，可 [提交工单](https://console.cloud.tencent.com/workorder/category?level1_id=438&level2_id=445&source=0&data_title=%E6%B8%B8%E6%88%8F%E5%A4%9A%E5%AA%92%E4%BD%93%E5%BC%95%E6%93%8EGME&step=1) 联系开发者。</td>
</tr>
</table>


#### 返回值
<table>
<tr>
<td rowspan="1" colSpan="1" >返回值</td>

<td rowspan="1" colSpan="1" >处理</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GmeError.AV_OK= 0</td>

<td rowspan="1" colSpan="1" >初始化 SDK 成功</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >AV_ERR_SDK_NOT_FULL_UPDATE=7015</td>

<td rowspan="1" colSpan="1" >检查 SDK 文件是否完整，建议删除后重新导入 SDK</td>
</tr>
</table>


> **关于7015错误提示**
> 
> - 7015错误码是通过 md5 进行判断，在接入过程中若出现此错误，请根据提示检查 SDK 文件是否完整、SDK 文件版本是否一致。
> - 出现返回值 AV_ERR_SDK_NOT_FULL_UPDATE 时，此返回值**只有提示作用**，并不会造成初始化失败。


#### 示例代码
``` bash
int res = await ITMGContext.GetInstance().InitSDK(_editAppID.text,_editOpenID.text);
//通过返回值判断是否初始化成功
if (ret != GmeError.AV_OK)
{
    print("SDK初始化失败:");
    return;
}
```

### 触发事件回调

通过在定时器调用 Poll 可以触发事件回调。Poll 是 GME 的消息泵，GME 需要周期性的调用 Poll 接口触发事件回调。如果没有调用 Poll ，将会导致整个 SDK 服务运行异常。详情请参见 [Sample Project](https://intl.cloud.tencent.com/document/product/607/18521)  中的 EnginePollHelper 文件。

> **注意**
> 

> 务必周期性调用 Poll 接口且在主线程调用，以免接口回调异常。
> 


#### 接口原型
``` bash
Future<void> Poll()
```

#### 示例代码
``` bash
Future<void> pollTimer() async {
  _pollTimer = Timer.periodic(Duration(milliseconds: 100), (Timer timer) {
  ITMGContext.GetInstance().Poll();
  });
}
```

### 反初始化 SDK

反初始化 SDK，进入未初始化状态。**如果游戏业务侧账号与 openid 是绑定的，那切换游戏账号需要反初始化 GME，再用新的 openid 初始化**。

#### 接口原型
``` bash
Future<int> Uninit()
```

## 语音消息服务及转文本服务

> **说明**
> 
> - 转文本服务分录音文件极速转文本以及语音消息流式转文本。
> - 使用语音消息服务不需要进入实时语音房间。
> - 语音消息最大录制时长默认为58秒，最短不能小于1秒。如果需要再加以限制，例如限制为最大录制时长为10秒，请在初始化之后调用 SetMaxMessageLength 接口进行设置。


### 语音消息服务使用流程

![](https://qcloudimg.tencent-cloud.cn/raw/24c16c71cb2fcc6cf170a6b481067564.jpg)

### 转文本服务使用流程

![](https://qcloudimg.tencent-cloud.cn/raw/8269f413756379d574a2969ac8da0158.jpg)
<table>
<tr>
<td rowspan="1" colSpan="1" >接口</td>

<td rowspan="1" colSpan="1" >接口含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GenAuthBuffer</td>

<td rowspan="1" colSpan="1" >获取鉴权信息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SetMaxMessageLength</td>

<td rowspan="1" colSpan="1" >限制最大语音信息时长</td>
</tr>
</table>


### 生成本地鉴权

生成 AuthBuffer，用于相关功能的加密和鉴权，如正式发布请使用后台部署密钥，后台部署请参见 [鉴权密钥](https://intl.cloud.tencent.com/document/product/607/12218)。    

#### 接口原型
``` bash
Future<Uint8List> GenAuthBuffer(String appID, String roomID, String openID, String key)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >appId</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >来自腾讯云控制台的 AppId 号码。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >roomId</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >填 null 或者空字符串。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >openId</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >用户标识。与 Init 时候的 OpenId 相同。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >key</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >来自腾讯云 [控制台](https://console.cloud.tencent.com/gamegme) 的权限密钥。</td>
</tr>
</table>


### 应用鉴权

生成鉴权信息后，将鉴权赋值到 SDK 中。  

#### 接口原型
``` bash
Future<int> ApplyPTTAuthbuffer(Uint8List authBuffer) 
```

#### 示例代码
``` bash
Uint8List authBuffer = await ITMGContext.GetInstance().GenAuthBuffer(_editAppID.text, _editRoomID.text, _editOpenID.text, _editKey.text);
m_context.ApplyPTTAuthbuffer(authBuffer);
```

### 限制最大语音信息时长

限制最大语音消息的长度，最大支持58秒。

#### 接口原型
``` bash
Future<int> SetMaxMessageLength(int msTime)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >msTime</td>

<td rowspan="1" colSpan="1" >number</td>

<td rowspan="1" colSpan="1" >语音时长，单位 ms，区间为 1000 < msTime < = 58000</td>
</tr>
</table>


#### 示例代码
``` bash
ITMGContext.GetInstance().GetPTT().SetMaxMessageLength(fileLen);
```

## 流式语音识别

### 语音消息及转文字相关接口
<table>
<tr>
<td rowspan="1" colSpan="1" >接口</td>

<td rowspan="1" colSpan="1" >接口含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >StartRecordingWithStreamingRecognition</td>

<td rowspan="1" colSpan="1" >启动流式录音</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >StopRecording</td>

<td rowspan="1" colSpan="1" >停止录音</td>
</tr>
</table>


### 启动流式语音识别

此接口用于启动流式语音识别，同时在回调中会有实时的语音转文字返回，可以指定语言进行识别，也可以将语音中识别到的信息翻译成指定的语言返回。**停止录音调用 **[**停止录制**](https://www.tencentcloud.com/document/product/607/53819)。

#### 接口原型
``` bash
Future<int> StartRecordingWithStreamingRecognition(String filePath, String speechLanguage, String translateLanguage) 
```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >filePath</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >存放的语音路径</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >speechLanguage</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >识别成指定文字的语言参数，参数请参见 [语言参数参考列表](https://intl.cloud.tencent.com/document/product/607/30260)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >translateLanguage</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >翻译成指定文字的语言参数，参数请参见 [语言参数参考列表](https://intl.cloud.tencent.com/document/product/607/30260)</td>
</tr>
</table>


#### 示例代码
``` bash
string filePath = "xx/xxx/xxx.silk"
int res = await ITMGContext.GetInstance().GetPTT().StartRecordingWithStreamingRecognition(filePath, strCurLanguage, strCurLanguage);
if (ret == 0) {
    this.currentStatus = "开始流式录音";
} else {
    this.currentStatus = "开始流式录音失败";
}
```

> **注意**
> 

>  翻译会收取额外费用，请参见 [购买指南](https://intl.cloud.tencent.com/document/product/607/50009)。
> 


### 流式语音识别的回调

启动流式语音识别后，需要在 OnEvent 通知中监听回调消息，事件消息分为以下两个：

ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE 是在停止录制并完成识别后才返回文字，相当于一段话说完才会返回识别的文字。
ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_IS_RUNNING 是在录音过程中就会实时返回识别到的文字，相当于边说话边返回识别到的文字。

根据需求在 回调 通知中对相应事件消息进行判断。传递的参数包含以下四个信息。
<table>
<tr>
<td rowspan="1" colSpan="1" >消息名称</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >result</td>

<td rowspan="1" colSpan="1" >用于判断流式语音识别是否成功的返回码</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >text</td>

<td rowspan="1" colSpan="1" >语音转文字识别的文本</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >file_path</td>

<td rowspan="1" colSpan="1" >录音存放的本地地址</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >file_id</td>

<td rowspan="1" colSpan="1" >录音在后台的 url 地址，录音在服务器存放90天</td>
</tr>
</table>


> **注意**
> 

> 监听 `ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_IS_RUNNING` 消息时，file_id 为空。
> 


#### 错误码
<table>
<tr>
<td rowspan="1" colSpan="1" >错误码</td>

<td rowspan="1" colSpan="1" >含义</td>

<td rowspan="1" colSpan="1" >处理方式</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >32775</td>

<td rowspan="1" colSpan="1" >流式语音转文本失败，但是录音成功</td>

<td rowspan="1" colSpan="1" >调用 UploadRecordedFile 接口上传录音，再调用 SpeechToText 接口进行语音转文字操作</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >32777</td>

<td rowspan="1" colSpan="1" >流式语音转文本失败，但是录音成功，上传成功</td>

<td rowspan="1" colSpan="1" >返回的信息中有上传成功的后台 url 地址，调用 SpeechToText 接口进行语音转文字操作</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >32786</td>

<td rowspan="1" colSpan="1" >流式语音转文本失败</td>

<td rowspan="1" colSpan="1" >在流式录制状态当中，请等待流式录制接口执行结果返回</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >32787</td>

<td rowspan="1" colSpan="1" >转文本成功，文本翻译服务未开通</td>

<td rowspan="1" colSpan="1" >需要在控制台开通文本翻译服务</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >32788</td>

<td rowspan="1" colSpan="1" >转文本成功，文本翻译语言参数不支持</td>

<td rowspan="1" colSpan="1" >重新检查传入参数</td>
</tr>
</table>


如果出现 4098 错误码，请参见 [常见问题文档](https://intl.cloud.tencent.com/document/product/607/39716) 进行解决。

#### 示例代码
``` bash
void handleEventMsg(int eventType, String data){
   switch (eventType) {
        case ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE:
        {
            HandleSTREAM2TEXTComplete(data,true);
            break;
        }
        ...
        case ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_IS_RUNNING:
        {
            HandleSTREAM2TEXTComplete(data, false);
            break;
        }
    }
}
ITMGContext.GetInstance().SetEvent(handleEventMsg);
```

## 语音消息录制

**录制的流程为：录音 > 停止录音 > 录音回调返回 > 启动下一次录音。**

### 语音消息及转文字相关接口
<table>
<tr>
<td rowspan="1" colSpan="1" >接口</td>

<td rowspan="1" colSpan="1" >接口含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >StartRecording</td>

<td rowspan="1" colSpan="1" >启动录音</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >PauseRecording</td>

<td rowspan="1" colSpan="1" >暂停录音</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ResumeRecording</td>

<td rowspan="1" colSpan="1" >恢复录音</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >StopRecording</td>

<td rowspan="1" colSpan="1" >停止录音</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >CancelRecording</td>

<td rowspan="1" colSpan="1" >取消录音</td>
</tr>
</table>


### 启动录音

此接口用于启动录音。

#### 接口原型
``` bash
Future<int> StartRecording(String filePath)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >filePath</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >存放的语音路径</td>
</tr>
</table>


#### 示例代码
``` bash
string filepath = "xxxx/xxx.silk";
int res = await ITMGContext.GetInstance().GetPTT().StartRecording(filepath);
```



### 停止录音

此接口用于停止录音。此接口为异步接口，停止录音后会有录音完成回调，成功之后录音文件才可用。

#### 接口原型
``` bash
Future<int> StopRecording() 
```

#### 示例代码
``` bash
ITMGContext.GetInstance().GetPTT().StopRecording();
```

### 启动录音的回调

录音完成的回调，通过委托传递消息。

**停止录音调用StopRecording**。停止录音后才有启动录音的回调。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >code</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >当 code 为 0 时，录制完成</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >filepath</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >录制的存放地址，必须是可以访问到的路径，不可将 fileid 作为路径</td>
</tr>
</table>


#### 错误码
<table>
<tr>
<td rowspan="1" colSpan="1" >错误码值</td>

<td rowspan="1" colSpan="1" >原因</td>

<td rowspan="1" colSpan="1" >建议方案</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >4097</td>

<td rowspan="1" colSpan="1" >参数为空</td>

<td rowspan="1" colSpan="1" >检查代码中接口参数是否正确</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >4098</td>

<td rowspan="1" colSpan="1" >初始化错误</td>

<td rowspan="1" colSpan="1" >检查设备是否被占用，或者权限是否正常，是否初始化正常</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >4099</td>

<td rowspan="1" colSpan="1" >正在录制中</td>

<td rowspan="1" colSpan="1" >确保在正确的时机使用 SDK 录制功能</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >4100</td>

<td rowspan="1" colSpan="1" >没有采集到音频数据</td>

<td rowspan="1" colSpan="1" >检查麦克风设备是否正常</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >4101</td>

<td rowspan="1" colSpan="1" >录音时，录制文件访问错误</td>

<td rowspan="1" colSpan="1" >确保文件存在，文件路径的合法性</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >4102</td>

<td rowspan="1" colSpan="1" >麦克风未授权错误</td>

<td rowspan="1" colSpan="1" >使用 SDK 需要麦克风权限，添加权限请参考对应引擎或平台的 SDK 工程配置文档</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >4103</td>

<td rowspan="1" colSpan="1" >录音时间太短错误</td>

<td rowspan="1" colSpan="1" >首先，限制录音时长的单位为毫秒，检查参数是否正确；其次，录音时长要1000毫秒以上才能成功录制</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >4104</td>

<td rowspan="1" colSpan="1" >没有启动录音操作</td>

<td rowspan="1" colSpan="1" >检查是否已经调用启动录音接口</td>
</tr>
</table>


#### 示例代码
``` bash
void handleEventMsg(int eventType, String data){
   switch (eventType) {
        case ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
        {
          //进行处理
          break;
        }
        ...
        case ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE:
        {
          //进行处理
          break;
        }
    }
}
ITMGContext.GetInstance().SetEvent(handleEventMsg);
```

### 暂停录音

此接口用于暂停录音。如需恢复录音请调用接口 ResumeRecording。

#### 接口原型
``` bash
Future<int> PauseRecording()
```

#### 示例代码
``` bash
ITMGContext.GetInstance().GetPTT().PauseRecording();
```

### 恢复录音

此接口用于恢复录音。

#### 接口原型
``` bash
Future<int> ResumeRecording()
```

#### 示例代码
``` bash
ITMGContext.GetInstance().GetPTT().ResumeRecording();
```

### 取消录音

调用此接口取消录音。**取消之后没有回调**。

#### 接口原型
``` bash
Future<int> CancelRecording()
```

#### 示例代码
``` bash
ITMGContext.GetInstance().GetPTT().CancelRecording();
```

## 语音消息上传、下载及播放
<table>
<tr>
<td rowspan="1" colSpan="1" >接口</td>

<td rowspan="1" colSpan="1" >接口含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >UploadRecordedFile</td>

<td rowspan="1" colSpan="1" >上传语音文件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >DownloadRecordedFile</td>

<td rowspan="1" colSpan="1" >下载语音文件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >PlayRecordedFile</td>

<td rowspan="1" colSpan="1" >播放语音</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >StopPlayFile</td>

<td rowspan="1" colSpan="1" >停止播放语音</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GetFileSize</td>

<td rowspan="1" colSpan="1" >语音文件的大小</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GetVoiceFileDuration</td>

<td rowspan="1" colSpan="1" >语音文件的时长</td>
</tr>
</table>


### 上传语音文件

此接口用于上传语音文件。

#### 接口原型
``` bash
Future<int> UploadRecordedFile(String filePath) 
```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >filePath</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >上传的语音路径，此路径为本地路径</td>
</tr>
</table>


#### 示例代码
``` bash
ITMGContext.GetInstance().GetPTT().UploadRecordedFile(_filePath);
```

### 上传语音完成的回调

上传语音完成后，事件消息为 ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE， 在 OnEvent 函数中对事件消息进行判断。
传递的参数包含三个信息，result，file_path 和 file_id。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >result</td>

<td rowspan="1" colSpan="1" >number</td>

<td rowspan="1" colSpan="1" >当 code 为0时，录制完成</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >filepath</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >录制的存放地址</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >fileid</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >文件的 url 路径</td>
</tr>
</table>


#### 错误码
<table>
<tr>
<td rowspan="1" colSpan="1" >错误码值</td>

<td rowspan="1" colSpan="1" >原因</td>

<td rowspan="1" colSpan="1" >建议方案</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >8193</td>

<td rowspan="1" colSpan="1" >上传文件时，文件访问错误</td>

<td rowspan="1" colSpan="1" >确保文件存在，文件路径的合法性</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >8194</td>

<td rowspan="1" colSpan="1" >签名校验失败错误</td>

<td rowspan="1" colSpan="1" >检查鉴权密钥是否正确，检查是否有初始化离线语音</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >8195</td>

<td rowspan="1" colSpan="1" >网络错误</td>

<td rowspan="1" colSpan="1" >检查设备网络是否可以正常访问外网环境</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >8196</td>

<td rowspan="1" colSpan="1" >获取上传参数过程中网络失败</td>

<td rowspan="1" colSpan="1" >检查鉴权是否正确，检查设备网络是否可以正常访问外网环境</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >8197</td>

<td rowspan="1" colSpan="1" >获取上传参数过程中回包数据为空</td>

<td rowspan="1" colSpan="1" >检查鉴权是否正确，检查设备网络是否可以正常访问外网环境</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >8198</td>

<td rowspan="1" colSpan="1" >获取上传参数过程中回包解包失败</td>

<td rowspan="1" colSpan="1" >检查鉴权是否正确，检查设备网络是否可以正常访问外网环境</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >8200</td>

<td rowspan="1" colSpan="1" >没有设置 appinfo</td>

<td rowspan="1" colSpan="1" >检查 apply 接口是否有调用，或者入参是否为空</td>
</tr>
</table>


#### 示例代码
``` bash
void handleEventMsg(int eventType, String data){
 switch (eventType) {
        ...
        case ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE:
        {
            //进行处理
            break;
        }
    }
}
ITMGContext.GetInstance().SetEvent(handleEventMsg);
```

### 下载语音文件

此接口用于下载语音文件。

#### 接口原型
``` bash
Future<int> DownloadRecordedFile(String fileId, String filePath)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >fileId</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >文件的 url 路径</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >filePath</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >文件的本地保存路径，必须是可以访问到的路径，不可将 fileid 作为路径</td>
</tr>
</table>


#### 示例代码
``` bash
ITMGContext.GetInstance().GetPTT().DownloadRecordedFile(_fileId, _filePath);
```

### 下载语音文件完成回调

下载语音完成后，事件消息为 ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE， 在 OnEvent 函数中对事件消息进行判断。
传递的参数包含三个信息，result、file_path 和 file_id。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >result</td>

<td rowspan="1" colSpan="1" >number</td>

<td rowspan="1" colSpan="1" >当 code 为0时，下载完成</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >filepath</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >录制的存放地址</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >fileid</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >文件的 url 路径，录音在服务器存放 90 天</td>
</tr>
</table>


#### 错误码
<table>
<tr>
<td rowspan="1" colSpan="1" >错误码值</td>

<td rowspan="1" colSpan="1" >原因</td>

<td rowspan="1" colSpan="1" >建议方案</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >12289</td>

<td rowspan="1" colSpan="1" >下载文件时，文件访问错误</td>

<td rowspan="1" colSpan="1" >检查文件路径是否合法</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >12290</td>

<td rowspan="1" colSpan="1" >签名校验失败</td>

<td rowspan="1" colSpan="1" >检查鉴权密钥是否正确，检查是否有初始化离线语音</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >12291</td>

<td rowspan="1" colSpan="1" >网络存储系统异常</td>

<td rowspan="1" colSpan="1" >服务器获取语音文件失败，检查接口参数 fileid 是否正确，检查网络是否正常，检查 COS 文件存不存在</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >12292</td>

<td rowspan="1" colSpan="1" >服务器文件系统错误</td>

<td rowspan="1" colSpan="1" >检查设备网络是否可以正常访问外网环境，检查服务器上是否有此文件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >12293</td>

<td rowspan="1" colSpan="1" >获取下载参数过程中，HTTP 网络失败</td>

<td rowspan="1" colSpan="1" >检查设备网络是否可以正常访问外网环境</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >12294</td>

<td rowspan="1" colSpan="1" >获取下载参数过程中，回包数据为空</td>

<td rowspan="1" colSpan="1" >检查设备网络是否可以正常访问外网环境</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >12295</td>

<td rowspan="1" colSpan="1" >获取下载参数过程中，回包解包失败</td>

<td rowspan="1" colSpan="1" >检查设备网络是否可以正常访问外网环境</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >12297</td>

<td rowspan="1" colSpan="1" >没有设置 appinfo</td>

<td rowspan="1" colSpan="1" >检查鉴权密钥是否正确，检查是否有初始化离线语音</td>
</tr>
</table>


#### 示例代码
``` bash
void handleEventMsg(int eventType, String data){
    switch (eventType) {
        ...
        case ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
        {
          //进行处理
          break;
        }
    }
}
ITMGContext.GetInstance().SetEvent(handleEventMsg);
```

### 播放语音

此接口用于播放语音。

#### 接口原型
``` bash
Future<int> PlayRecordedFile(String filePath, int voiceType)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >filePath</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >本地语音文件的路径</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >voicetype</td>

<td rowspan="1" colSpan="1" >ITMG_VOICE_TYPE</td>

<td rowspan="1" colSpan="1" >变声类型，请参见 [变声接入文档](https://intl.cloud.tencent.com/document/product/607/44995)</td>
</tr>
</table>


#### 错误码
<table>
<tr>
<td rowspan="1" colSpan="1" >错误码值</td>

<td rowspan="1" colSpan="1" >原因</td>

<td rowspan="1" colSpan="1" >建议方案</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >20485</td>

<td rowspan="1" colSpan="1" >播放未开始</td>

<td rowspan="1" colSpan="1" >确保文件存在，文件路径的合法性</td>
</tr>
</table>


#### 示例代码
``` bash
int res = await ITMGContext.GetInstance().GetPTT().PlayRecordedFile(_filePath, _nVoiceType);
```

### 播放语音的回调

播放语音的回调，事件消息为 ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE， 在 OnEvent 函数中对事件消息进行判断。
传递的参数包含两个信息，一个是 result，另一个是 file_path。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >code</td>

<td rowspan="1" colSpan="1" >number</td>

<td rowspan="1" colSpan="1" >当 code 为0时，播放完成</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >filepath</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >录制的存放地址</td>
</tr>
</table>


#### 错误码
<table>
<tr>
<td rowspan="1" colSpan="1" >错误码值</td>

<td rowspan="1" colSpan="1" >原因</td>

<td rowspan="1" colSpan="1" >建议方案</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >20481</td>

<td rowspan="1" colSpan="1" >初始化错误</td>

<td rowspan="1" colSpan="1" >检查设备是否被占用，或者权限是否正常，是否初始化正常</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >20482</td>

<td rowspan="1" colSpan="1" >正在播放中，试图打断并播放下一个失败了（正常是可以打断的）</td>

<td rowspan="1" colSpan="1" >检查代码逻辑是否正确</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >20483</td>

<td rowspan="1" colSpan="1" >参数为空</td>

<td rowspan="1" colSpan="1" >检查代码中接口参数是否正确</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >20484</td>

<td rowspan="1" colSpan="1" >内部错误</td>

<td rowspan="1" colSpan="1" >初始化播放器错误，解码失败等问题产生此错误码，需要结合日志定位问题</td>
</tr>
</table>


#### 示例代码
``` bash
void handleEventMsg(int eventType, String data){
 switch (eventType) {
    case ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE:
    {
        //进行处理
        break;
    }
   }
}
```

### 停止播放语音

此接口用于停止播放语音。停止播放语音也会有播放完成的回调。

#### 接口原型
``` bash
Future<int> StopPlayFile()
```

#### 示例代码
``` bash
ITMGContext.GetInstance().GetPTT().StopPlayFile();
```

### 获取语音文件的大小

通过此接口，获取语音文件的大小。

#### 接口原型
``` bash
Future<int> GetFileSize(String filePath)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >filePath</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >语音文件的路径，此路径为本地路径</td>
</tr>
</table>


#### 示例代码
``` bash
final int res = await ITMGContext.GetInstance().GetPTT().GetFileSize(_filePath);
```

### 获取语音文件的时长

此接口用于获取语音文件的时长，单位毫秒。

#### 接口原型
``` bash
Future<int> GetVoiceFileDuration(String filePath)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >filePath</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >语音文件的路径，此路径为本地路径</td>
</tr>
</table>


#### 示例代码
``` bash
final int res = await ITMGContext.GetInstance().GetPTT().GetVoiceFileDuration(_filePath);
```

## 录音文件极速转文

### 将指定的语音文件翻译成文字（指定语言）

此接口可以指定语言进行识别，也可以将语音中识别到的信息翻译成指定的语言返回。

> **注意**
> 

> 翻译会收取额外费用，请参见 [购买指南](https://intl.cloud.tencent.com/document/product/607/50009)。
> 


#### 接口原型
``` bash
Future<int> SpeechToText(String fileId, String speechLanguage, String translateLanguage)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >fileID</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >语音文件 url，录音在服务器存放90天</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >speechLanguage</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >识别出指定文字的语言参数，参数参见 [语言参数参考列表](https://intl.cloud.tencent.com/document/product/607/30260)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >translatelanguage</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >翻译成指定文字的语言参数，参数参见 [语言参数参考列表](https://intl.cloud.tencent.com/document/product/607/30260) 中的翻译语言参数</td>
</tr>
</table>


#### 示例代码
``` bash
ITMGContext.GetInstance().GetPTT().SpeechToText(_fileId, "cmn-Hans-CN", "cmn-Hans-CN");
```

### 识别回调

将指定的语音文件识别成文字的回调，事件消息为 ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE， 在 OnEvent 函数中对事件消息进行判断。
传递的参数包含三个信息，result、file_path 和 text，其中 text 为识别的文本。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >result</td>

<td rowspan="1" colSpan="1" >number</td>

<td rowspan="1" colSpan="1" >当 code 为0时，录制完成</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >fileid</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >语音文件 url，录音在服务器存放90天</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >text</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >转换的文本结果</td>
</tr>
</table>


#### 错误码
<table>
<tr>
<td rowspan="1" colSpan="1" >错误码值</td>

<td rowspan="1" colSpan="1" >原因</td>

<td rowspan="1" colSpan="1" >建议方案</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >32769</td>

<td rowspan="1" colSpan="1" >内部错误</td>

<td rowspan="1" colSpan="1" >分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >32770</td>

<td rowspan="1" colSpan="1" >网络失败</td>

<td rowspan="1" colSpan="1" >检查设备网络是否可以正常访问外网环境</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >32772</td>

<td rowspan="1" colSpan="1" >回包解包失败</td>

<td rowspan="1" colSpan="1" >分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >32774</td>

<td rowspan="1" colSpan="1" >没有设置 appinfo</td>

<td rowspan="1" colSpan="1" >检查鉴权密钥是否正确，检查是否有初始化离线语音</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >32776</td>

<td rowspan="1" colSpan="1" >authbuffer 校验失败</td>

<td rowspan="1" colSpan="1" >检查 authbuffer 是否正确</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >32784</td>

<td rowspan="1" colSpan="1" >语音转文本参数错误</td>

<td rowspan="1" colSpan="1" >检查代码中接口参数 fileid 是否为空</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >32785</td>

<td rowspan="1" colSpan="1" >语音转文本翻译返回错误</td>

<td rowspan="1" colSpan="1" >离线语音后台错误，请分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >32787</td>

<td rowspan="1" colSpan="1" >转文本成功，文本翻译服务未开通</td>

<td rowspan="1" colSpan="1" >需要在控制台开通文本翻译服务</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >32788</td>

<td rowspan="1" colSpan="1" >转文本成功，文本翻译语言参数不支持</td>

<td rowspan="1" colSpan="1" >重新检查传入参数</td>
</tr>
</table>


#### 示例代码
``` bash
void handleEventMsg(int eventType, String data){
 switch (eventType) {
    case ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
       {
         //进行处理
         break;
       }
       ...
       case ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE:
       {
         //进行处理
         break;
       }
    }
}
```

## 语音消息音量相关接口
<table>
<tr>
<td rowspan="1" colSpan="1" >接口</td>

<td rowspan="1" colSpan="1" >接口含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GetMicLevel</td>

<td rowspan="1" colSpan="1" >获取实时麦克风音量</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SetMicVolume</td>

<td rowspan="1" colSpan="1" >设置录制音量</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GetMicVolume</td>

<td rowspan="1" colSpan="1" >获取录制音量</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GetSpeakerLevel</td>

<td rowspan="1" colSpan="1" >获取实时扬声器音量</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SetSpeakerVolume</td>

<td rowspan="1" colSpan="1" >设置播放音量</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GetSpeakerVolume</td>

<td rowspan="1" colSpan="1" >获取播放音量</td>
</tr>
</table>


### 获取语音消息麦克风实时音量

此接口用于获取麦克风实时音量，返回值为 number 类型，值域为0 - 200。

#### 接口原型
``` bash
Future<int> GetMicLevel() 
```

#### 示例代码
``` bash
final int res = await ITMGContext.GetInstance().GetPTT().GetMicLevel();
```

### 设置语音消息录制音量

此接口用于设置离线语音录制音量，值域为0 - 200。

#### 接口原型
``` bash
Future<int> SetMicVolume(int volume)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >vol</td>

<td rowspan="1" colSpan="1" >number</td>

<td rowspan="1" colSpan="1" >取值范围为 0-200，数值为0的时候表示静音，当数值为100的时候表示音量不增不减，默认数值为100。</td>
</tr>
</table>


#### 示例代码
``` bash
final int res = await ITMGContext.GetInstance().GetPTT().SetMicVolume(100);
```

### 获取语音消息录制音量

此接口用于获取离线语音录制音量。返回值为 number 类型，值域为0 - 200。

#### 接口原型
``` bash
Future<int> GetMicVolume() 
```

#### 示例代码
``` bash
final int res = await ITMGContext.GetInstance().GetPTT().GetMicVolume();
```

### 获取语音消息扬声器实时音量

此接口用于获取扬声器实时音量。返回值为 number 类型，值域为0 - 200。

#### 接口原型
``` bash
Future<int> GetSpeakerLevel()
```

#### 示例代码
``` bash
final int res = await ITMGContext.GetInstance().GetPTT().GetSpeakerLevel();
```

### 设置语音消息播放音量

此接口用于设置离线语音播放音量，值域为0 - 200。

#### 接口原型
``` bash
Future<int> SetSpeakerVolume(int volume)
```

#### 示例代码
``` bash
final int res = await ITMGContext.GetInstance().GetPTT().SetSpeakerVolume(100);
```

### 获取语音消息播放音量

此接口用于获取离线语音播放音量。返回值为 number 类型，值域为0 - 200。

#### 接口原型
``` bash
Future<int> GetSpeakerVolume()
```

#### 示例代码
``` bash
final int res = await ITMGContext.GetInstance().GetPTT().GetSpeakerVolume();
```

## 高级 API

### 获取版本号

获取 SDK 版本号，用于分析。

#### 接口原型
``` bash
Future<String> GetSDKVersion() 
```

#### 示例代码
``` bash
_sdkVersions = await ITMGContext.GetInstance().GetSDKVersion();
```

### 设置打印日志等级

用于设置打印日志等级。建议保持默认等级。需要在 Init 之前调用。

#### 接口原型
``` bash
Future<int> SetLogLevel(int levelWrite, int levelPrint)
```

#### 参数含义
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >level</td>

<td rowspan="1" colSpan="1" >ITMG_LOG_LEVEL</td>

<td rowspan="1" colSpan="1" >设置写入日志的等级，TMG_LOG_LEVEL_NONE 表示不写入，默认为 TMG_LOG_LEVEL_INFO</td>
</tr>
</table>


level 说明如下：
<table>
<tr>
<td rowspan="1" colSpan="1" >level</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TMG_LOG_LEVEL_NONE</td>

<td rowspan="1" colSpan="1" >不打印日志</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TMG_LOG_LEVEL_ERROR</td>

<td rowspan="1" colSpan="1" >打印错误日志（默认）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TMG_LOG_LEVEL_INFO</td>

<td rowspan="1" colSpan="1" >打印提示日志</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TMG_LOG_LEVEL_DEBUG</td>

<td rowspan="1" colSpan="1" >打印开发调试日志</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TMG_LOG_LEVEL_VERBOSE</td>

<td rowspan="1" colSpan="1" >打印高频日志</td>
</tr>
</table>


#### 示例代码
``` bash
ITMGContext.GetInstance().SetLogLevel(ITMG_LOG_LEVEL.TMG_LOG_LEVEL_ERROR,ITMG_LOG_LEVEL.TMG_LOG_LEVEL_ERROR);
```

### 设置打印日志路径

用于设置打印日志路径。默认路径如下。需要在 Init 之前调用。

#### 接口原型
``` bash
Future<int> SetLogPath(String logDir)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >logPath</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >路径</td>
</tr>
</table>


#### 示例代码
``` bash
String logDir = ""//自行设置路径
ITMGContext.GetInstance().SetLogPath(curPath);
```

