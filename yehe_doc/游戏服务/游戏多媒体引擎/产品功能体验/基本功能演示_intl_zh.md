腾讯云游戏多媒体引擎（Game Multimedia Engine，GME）提供高质量的一站式语音解决方案，全面覆盖游戏行业应用场景。支持多人实时语音、3D 位置语音、语音消息、语音转文本和语音内容安全等功能。
>!此处演示的 Demo 需要使用 Android 或者 iOS 系统手机进行体验。

<table>
  <tbody><tr>
    <th style="text-align:center;" width="150px"><b>Android<br></b>使用摄像机扫码</th>
    <th style="text-align:center;" width="150px"><b>iOS<br></b>使用摄像机扫码</th>
  </tr>
  <tr>
    <td style="
    text-align: center;
"><img style="width:150px; max-width: inherit;" src="https://main.qcloudimg.com/raw/17b2a65547432f5d81391fce1fa17a90.png" class="zoom-img-hover"></td>
    <td style="
    text-align: center;
"><img style="width:150px; max-width: inherit;" src="https://main.qcloudimg.com/raw/17b2a65547432f5d81391fce1fa17a90.png" class="zoom-img-hover"></td>
  </tr>
</tbody></table>


## Demo 功能
Demo 演示的 GME 基础功能如下：

<table>
   <tr>
      <th>基础功能</th>
      <th>可体验的功能</th>
   </tr>
   <tr>
      <td  rowspan="4">实时语音功能</td>
      <td>音质体验：流畅音质、标准音质以及高清音质</td>
   </tr>
   <tr>
      <td>房间内实时通话语音功能</td>
   </tr>
	    <tr>
      <td>3D 音效功能</td>
   </tr>
      <td>实时语音变声音效功能（基础变声）</td>
   </tr>
      <td>语音消息功能</td>
			<td>按住录制、上传语音消息，点击播放语音消息</td>
   </tr>
      <td>语音转文本功能</td>
			<td>Demo 中上传的语音消息自动转换为文本，可选择多种语言</td>
   </tr>
</table>

<span id="test"></span>

## 登录界面

### 1. 登录系统

输入 UserId，单击 **Login**，系统则会使用设置的 UserId 进行登录。登录后，界面将会新增 **Voice Chat** 和 **Voice Message** 两个按钮。

<img src="https://main.qcloudimg.com/raw/dbacd4455622253ddb07d53e1bc785b8.png"  width="50%" /></img><br>

### 2. 选择使用功能

- 单击 **Voice Chat**，将会进入 [实时语音](#test1) 功能。
- 单击 **Voice Message**，将会进入 [语音消息](#test2) 功能。

<span id="test1"></span>


## 体验实时语音功能

### 1. 进入语音房间 

 [登录](#test) 之后，单击 **Voice Chat** 进入语音聊天界面：

 <img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/IMB_KuI8ov.gif"    width="50%"/></img><br>

- **RoomId**：房间号 ID，房间号相同的成员会进入同一个房间。
- **RoomType**：用于控制语音质量。
  - Fluency：流畅音质。流畅优先、超低延迟实时语音，应用在游戏内开黑场景，适用于 FPS、MOBA 等类型的游戏。
  - Standard：标准音质。音质较好，延时适中，适用于狼人杀、棋牌等休闲游戏的实时通话场景。
  - Hign Quality：高清音质。超高音质，延时相对较大，适用于播放音乐等有高音质要求的游戏场景。

### 2. 语音聊天操作

在语音聊天界面，单击 **JoinRoom** 进入房间：

<img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/IMB_8zP4w2.gif"  width="50%"/><br>

- **Talking Members**：房间内正在说话的成员，界面将会显示正在说话的成员 ID。
- **Mic**：麦克风，勾选表示打开。 
- **Speaker**：扬声器，勾选表示打开。
- **3D Voice Effect**：3D 音效，勾选表示打开，可通过设置以下参数进行配置：
  - Range：设置语音接收范围，单位为游戏引擎单位。
  - X：自身 X 轴。
  - Y：自身 Y 轴。
  - Z：自身 Z 轴。
  - XR：绕 X 坐标轴旋转的方向。
  - YR：绕 Y 坐标轴旋转的方向。
  - ZR：绕 Z 坐标轴旋转的方向。
- **Voice Change**：实时语音音效，可通过选择不同的参数类型，改变播放音效特性，详情可参考 [实时语音音效](https://intl.cloud.tencent.com/document/product/607/31503)。
- **QuitRoom**：退出实时语音房间，回到上一界面。

<span id="test2"></span>

## 体验语音消息功能及转文本功能

### 1. 进入语音消息功能界面

[登录](#test) 之后，单击 **Voice Message** 进入语言消息界面：

<img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/IMB_DsvaLv.gif"  width="50%"/></img><br>

### 2. 界面操作

- **Language**：选择所录制的语言，录制后将转换为对应语言的文本，显示在 **Audio-to-Text** 一栏中。
- **Push To Talk**：长按 **Push To Talk**，开始录制；松开 **Push To Talk**，结束录制。
- **Audio**：录制的语音消息和语音时长。单击 <img src="https://main.qcloudimg.com/raw/7d268c4b1bb7e1998792b19a23e7bb63.png" width="3%"></img> 按钮播放录音，播放过程中再次单击，结束播放。
- **Audio-to-Text**：语音转换成的文字。

