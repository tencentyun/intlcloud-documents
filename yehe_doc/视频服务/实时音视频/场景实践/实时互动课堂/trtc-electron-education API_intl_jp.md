コンポーネント trtc-electron-education は、リアルタイム双方向対話型授業のシーンで使用するTencent Real-Time Communication（TRTC）とInstant Messaging（IM)の機能を対象として、二次パッケージングしたものです。基本の音声・ビデオチャット、画面共有の機能をパッケージングすると同時に、eラーニングのシーンを対象に教師のQA開始、学生の挙手、教師が学生を招待して皆の前で回答させる、回答の終了などの関連機能もパッケージングされています。
trtc-electron-educationは、1つのオープンソースのnpm コンポーネントであり、Tencent Cloudの2つのクローズドソースであるSDKに依存しています。具体的な実現プロセスは、[リアルタイム双方向対話型授業(Electron)](https://intl.cloud.tencent.com/document/product/647/37278)をご参照ください。
* TRTC SDK：[TRTC SDK](https://intl.cloud.tencent.com/document/product/647)を低レイテンシーのオーディオビデオ通話コンポーネントとして使用しています。
* IM SDK： [IM SDK](https://intl.cloud.tencent.com/document/product/1047)をシグナリング情報の送信と処理に利用します。

## コンポーネントの接続
```
// yarn方式の導入
yarn add trtc-electron-education
// npm方式の導入
npm i trtc-electron-education --save
```

## コンポーネントのパラメータ

入力必須となる主要パラメータは下表で示すとおりです。

| パラメータ |タイプ|説明|
| ----- | ----- | ----- |
|sdkAppId|number|入力必須のパラメータ。<a href="https://console.cloud.tencent.com/trtc/app">TRTCコンソール</a> の中でSDKAppIDを確認できます。|
|userID|string|入力が必要なパラメータ。ユーザーIDは、お客様のアカウント体系から指定することが可能です。|
|userSig|string|入力が必要なパラメータ。ID署名（ログインパスワードに相当）は、userIDから算出します。具体的な計算方法は、[UserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。|

## 初期化の例示

```typescript
import TrtcElectronEducation from 'trtc-electron-education';
const rtcClient = new TrtcElectronEducation({
     sdkAppId: 1400***803,
     userID: '123'
     userSig: 'eJwtzM9****-reWMQw_'
 });
```

## コンポーネントの概要
### 基本関数

#### on(EventCode, handler, context)
コンポーネントが配布するイベントのモニタリングに利用します。  
パラメータ：

|パラメータ名|タイプ|説明|
| ----- | ----- | ----- |
|EventCode|String|イベントコード|
|handler|Function|モニタリング関数|
|context|Object|現在実行しているコンテキスト|

例示：
```typescript
const EVENT = rtcClient.EVENT
rtcClient.on(EVENT.MESSAGE_RECEIVED, onMessageReceived);
```

#### off(EventCode, handler)
イベントモニタリングの取消。  
パラメータ：

|パラメータ名|	タイプ	|説明|
| ----- | ----- | ----- |
|EventCode|String|イベントコード|
|handler|Function|取消が必要な名前付きモニタリング関数|

例示：
```typescript
const EVENT = rtcClient.EVENT
rtcClient.off(EVENT.MESSAGE_RECEIVED, onMessageReceived);
```

<span id="createRoom"></span>
#### createRoom(params: CreateRoomParams)
教師のクラス作成。  
パラメータ：

|パラメータ名|	タイプ	|説明|
| ----- | ----- | ----- |
|classId|	number|	教室 ID|
|nickName|string|ニックネーム|
|avatar|string|プロファイル写真URL（未入力可）|

例示：
```typescript
interface CreateRoomParams {
  classId: number; // 教室 ID
  nickName: string; // ニックネーム
  avatar?:string; // プロファイル画像URL
}
rtcClient.createRoom(params).then(() => {
})
```

#### destroyRoom(classId: number)
教師がクラスから退出し、ルームを廃棄します。
パラメータ：

|パラメータ名|	タイプ	| 説明|
| ----- | ----- | ----- |
|classId|	number|	 教室 ID|

例示：
```typescript
rtcClient.destroyRoom(classId)
```

<span id="enterRoom"></span>
#### enterRoom(params: EnterRoomParams)
教師が授業を開始し、学生は教室に入り、聴講の準備をします。
パラメータ：

|パラメータ名|	タイプ	| 説明|
| ----- | ----- | ----- |
|classId|	number|	 教室 ID|
|nickName|	string| ニックネーム|
|role|string| ロール。teacherは教師、studentは学生を表します。|
|avatar|string| プロファイル写真URL（未入力可）|

例示：
```typescript
interface EnterRoomParams {
  role: string; // ロール
  classId: number; // 教室 ID
  nickName?: string; // ニックネーム
  avatar?:string; // プロファイル画像URL
}
rtcClient.enterRoom(params).then(() => {
})
```

#### exitRoom(role:string, classId: number)
教師が授業を終了させ、学生は教室から退出します。
パラメータ：

|パラメータ名|	タイプ	| 	説明|
| ----- | ----- | ----- |
|classId|	number|	 教室 ID|
|role|string| ロール。teacherは教師、studentは学生を表します。|

例示：
```typescript
rtcClient.exitRoom(role, classId);
```

### 挙手の操作部分の関数
<span id="startQuestionTime"></span>
#### startQuestionTime(classId: number)
教師がQA時間を開始。教師側が通知を発信し、学生がQA開始のイベントを受信して、挙手の機能を起動します。
パラメータ：

|パラメータ名|	タイプ	| 説明|
| ----- | ----- | ----- |
|classId|	number|	 教室 ID|

例示：
```typescript
rtcClient.startQuestionTime(classId)
```

<span id="raiseHand"></span>
#### raiseHand()
学生の挙手。学生が挙手の通知を送信し、教師側が学生の挙手の通知を受信します。  
パラメータ：無
例示：
```typescript
rtcClient.raiseHand()
```

<span id="inviteToPlatform"></span>
#### inviteToPlatform(userID: string)
教師が皆の前で回答させるために学生を招待。教師側が挙手リストの中の学生userIDを選択し、招待の通知を送信します。学生側は皆の前で回答する招待のイベントを受信し、招待を受けた学生のマイクが起動します。挙手する学生がいない場合は、教師が回答する学生を直接指名します。学生側が皆の前で回答する招待のイベントを受信し、指名された学生のマイクが起動します。
パラメータ：

|パラメータ名|	タイプ	|説明|
| ----- | ----- |  ----- |
|userID|string| ユーザーID|

例示：
```typescript
rtcClient.inviteToPlatform(userID).then(() => {
})
```

<span id="finishAnswering"></span>
#### finishAnswering(userID: string)
回答の終了。教師側が学生側の回答を終了します。学生は回答終了の通知を受信し、指定された学生のマイク接続が停止します。
パラメータ：

|パラメータ名|	タイプ	| 説明|
| ----- | ----- |   ----- |
|userID|string| ユーザーID|

例示：
```typescript
rtcClient.finishAnswering(userID).then(() => {
})
```

#### stopQuestionTime(classId: number)
QA時間の停止。教師側がQA時間を停止します。学生側は回答時間停止の通知を受信します。マイク接続済みの学生はマイク接続を停止し、挙手の機能をオフにする必要があります。
パラメータ：

|パラメータ名|	タイプ	|説明|
| ----- | ----- | ----- |
|classId|	number|	教室 ID|

例示：
```typescript
rtcClient.stopQuestionTime(classId)
```

### プッシュプルストリーム操作に関する関数
<span id="getScreenShareList"></span>
#### getScreenShareList()
画面共有のウィンドウのリストを取得。
パラメータ：無
例示：
```typescript
rtcClient.getScreenShareList();
```


<span id="startScreenCapture"></span>
#### startScreenCapture(source: SourceParam)
画面共有を選択し、プッシュを開始。
パラメータ：

|パラメータ名|	タイプ	|説明|
| ----- | ----- | ----- |
|type|number|キャプチャソースタイプ|
|sourceId|string|ソースIDの収集。ウィンドウについては、当該フィールドにウィンドウのハンドルを表示します。画面については、当該フィールドに画面IDを表示します。|
|sourceName|string|ソース名の収集、UTF8 エンコーディング|

例示：
```typescript
interface SourceParam {
  type: number; // キャプチャソースタイプ
  sourceId: string; // ソースIDの収集
  sourceName: string; // ソース名の収集、UTF8 エンコーディング
}
rtcClient.startScreenCapture({
   type,
   sourceId,
   sourceName
 })
```

<span id="startRemoteView"></span>
#### startRemoteView(params: RemoteParams) 
リモートのビデオ画面または画面共有の画面の表示を開始。
パラメータ：

|パラメータ名|	タイプ	| 説明|
| ----- | ----- |  ---- |
|userID|	string|	 ユーザーID|
|streamType|number| 画面タイプ。1は大画面、2は小画面、3は画面共有を表します。|
|view|HTMLElement| 表示画面をローディングするDOM|

例示：
```typescript
interface RemoteParams {
  userID: string; // ユーザーID
  streamType: number; // 画面タイプ。1-大画面、2-小画面、3-画面共有
  view: HTMLElement; //表示画面をロードするDOM
}
const view = document.getElementById('localVideo');
rtcClient.startRemoteView({
  userID: userID,
  streamType: 1,//1-大画面、2-小画面、3-画面共有
  view: view
});
```

#### stopRemoteView(params: StopRemoteParams)
リモートのビデオ画面または画面共有の画面の表示を停止すると、同時に当該リモートユーザーのデータストリームを再びプルしなくなります。
パラメータ：

|パラメータ名|	タイプ	| 説明|
| ----- | ----- |  ----- |
|userID|	string|	 ユーザーID|
|streamType|number| 画面タイプ。1は大画面、2は小画面、3は画面共有を表します。|

例示：
```typescript
interface StopRemoteParams {
  userID: string; // ユーザーID
  streamType: number; // 画面タイプ。1-大画面、2-小画面、3-画面共有
}
rtcClient.stopRemoteView({
   userID: userID,
   streamType: 1 //1-大画面、2-小画面、3-画面共有
 });
```

### メッセージ送受信に関する関数
#### sendTextMessage(params: MessageParams) 
チャットルームのメッセージ送信。
パラメータ：

|パラメータ名|	タイプ	| 説明|
| ----- | ----- |  ----- |
|classId|number| 教室 ID|
|message|string| テキストメッセージ|

例示：
```typescript
interface MessageParams {
  classId: number; // 教室 ID
  message: string; // メッセージテキスト
}
rtcClient.sendTextMessage(params).then(() => {
})
```

#### sendCustomMessage(userID: string, data: string)
カスタマイズ C2C メッセージの送信。 
パラメータ：

|パラメータ名|	タイプ	|	説明|
| ----- | ----- | ----- |
|userID|string| ユーザーID |
|data|string| カスタマイズメッセージ|

例示：
```typescript
rtcClient.sendCustomMessage(userID, JSON.stringify(params)
```

#### sendGroupCustomMessage(classId: number, data: string)
カスタマイズグループメッセージの送信。  
パラメータ：

|パラメータ名|	タイプ	| 説明|
| ----- | ----- | ----- |
|classId|number| 教室 ID|
|data|string| カスタマイズメッセージ|

例示：
```typescript
rtcClient.sendGroupCustomMessage(classId, JSON.stringify(params))
```

### デバイス操作に関する関数
<span id="openCamera"></span>
#### openCamera(view: HTMLElement)
カメラの起動。
パラメータ：

|パラメータ名|	タイプ	| 説明|
| ----- | ----- | ----- |
|view|HTMLElement| 表示画面をロードするDOM|

例示：
```typescript
const domEle = document.getElementById('localVideo');
rtcClient.openCamera(domEle);
```

#### closeCamera()
カメラの停止。 
パラメータ：無
例示：
```typescript
rtcClient.closeCamera();
```

<span id="getCameraList"></span>
#### getCameraList()
カメラリストの取得。
パラメータ：無
例示：
```typescript
rtcClient.getCameraList()
```

<span id="setCurrentCamera"></span>
#### setCurrentCamera(deviceId:string)
カメラの設定。パラメータは getCameraDevicesListの中から取得できるデバイスIDです。
パラメータ：

|パラメータ名|	タイプ	| 説明|
| ----- | ----- |  ---- |
|deviceId|string| デバイスID|

例示：
```typescript
rtcClient.setCurrentCamera(deviceId)
```

<span id="openMicrophone"></span>
#### openMicrophone()
マイクをオンにします。
パラメータ：無
例示：
```typescript
rtcClient.openMicrophone();
```

<span id="closeMicrophone"></span>
#### closeMicrophone()
マイクをオフにします。
パラメータ：無
例示：
```typescript
rtcClient.closeMicrophone();
```


<span id="getMicrophoneList"></span>
#### getMicrophoneList()
マイクのデバイスリストを取得します。  
パラメータ：無
例示：
```typescript
rtcClient.getMicrophoneList()
```
#### setCurrentMicDevice(micId:string)
マイクの設定。パラメータは getMicDevicesListの中から取得できるデバイスIDです。
パラメータ：

|パラメータ名|	タイプ	| 	説明|
| ----- | ----- | ----- |
|micId|string| デバイスID|

例示：
```typescript
rtcClient.setCurrentMicDevice(micId)
```

<span id="setBeautyStyle"></span>
#### setBeautyStyle(params: BeautyParams) 
美顔、美白、肌の色調補正効果のランクを設定します。 
パラメータ：

|パラメータ名|	タイプ	| 説明|
| ----- | ----- |  ----- |
|beautyStyle|number| 1はすべすべのつや感。綺麗な女性のショーに適用します。効果はかなりはっきりと出ます。<br>2はナチュラル。肌質補正アルゴリズムで、顔の細部をもっと多く残しますので、主観的によりナチュラルな感じを受けます。|
|beauty|number| 美顔レベル。数値の範囲は0～9です。0はオフを意味し、1～9まで数値が大きくなるほど効果が高くなります|
|white|number| 美白レベル。数値の範囲は0～9です。0はオフを意味し、1～9まで数値が大きくなるほど効果が高くなります|
|ruddiness|number| 肌色補正レベル。数値の範囲は0～9です。0はオフを意味し、1～9まで数値が大きくなるほど効果が高くなります。このパラメータは、Windowsプラットフォームではまだ有効ではありません|

例示：
```typescript
interface BeautyParams {
  beautyStyle: number;//スムース、ナチュラル
  beauty: number; //美顔レベル
  white: number; //美白レベル
  ruddiness: number; //肌色補正レベル
}
rtcClient.setBeautyStyle({
	beautyStyle: 1,
	beauty: 5,
	white: 5,
	ruddiness: 5
})
```

## コンポーネントイベント
### 例示
```typescript
const EVENT = rtcClient.EVENT
rtcClient.on(EVENT.STUDENT_RAISE_HAND, () => {
   //学生の挙手
})
```
### 詳細イベント

| CODE |説明|
| ----- | ----- |
|ENTER_ROOM_SUCCESS|入室の成功|
|LEAVE_ROOM_SUCCESS|退室の成功|
|TEACHER_ENTER|教師の入室|
|TEACHER_LEAVE|教師の退室|
|STUDENT_ENTER|学生の入室|
|STUDENT_LEAVE|学生の退室|
|SCREEN_SHARE_ADD|教師の画面共有開始|
|SCREEN_SHARE_REMOVE|教師の画面共有終了|
|REMOTE_VIDEO_ADD|リモートビデオストリームのイベントの追加。リモートユーザーがビデオストリームを公開すると、この通知を受け取ります。|
|REMOTE_VIDEO_REMOVE|リモートビデオストリームのイベントの削除。リモートユーザーがビデオストリームの公開をキャンセルすると、この通知を受け取ります。|
|REMOTE_AUDIO_ADD|リモートオーディオストリームのイベントの追加|
|REMOTE_AUDIO_REMOVE|リモートオーディオストリームのイベントの削除|
|ROOM_DESTROYED|ルームの廃棄|
|QUESTION_TIME_STARTED|QA時間の開始|
|QUESTION_TIME_STOPPED|QA時間の終了|
|STUDENT_RAISE_HAND|学生の挙手|
|BE_INVITED_TO_PLATFORM|招待されて質問に回答、指名|
|ANSWERING_FINISHED|回答の終了、音声禁止|
|MESSAGE_RECEIVED|メッセージの受信|
|KICKED_OUT|同じアカウントが他の場所でログインすると、追放されてオフラインになります。
|ERROR|異常|
|WARNING|警告|
