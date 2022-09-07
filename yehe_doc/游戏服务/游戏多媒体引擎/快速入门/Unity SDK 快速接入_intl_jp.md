開発者がGME製品APIのデバッグ・アクセスを行いやすいように、ここで、Unity開発に適用されるクイックアクセス技術ドキュメントを説明させていただきます。

GMEクイックスタート文書は、ユーザーのアクセスを助けるための最も主要なアクセスインターフェースのみを提供しています。

## GME利用上の重要事項

GMEは2つの部分に分かれます。リアルタイム音声サービス、音声メッセージおよびテキスト変換サービスを提供しており、これらのサービスの利用はInitやPollなどのコアインターフェースに依存しています。

<dx-alert infotype="notice" title="关于 Init 接口">
例えば、リアルタイムの音声サービスを使用する同時に音声メッセージ・サービスも使用する場合、**Init初期化インターフェースを1回だけ呼び出す必要があります**。
</dx-alert>

###　インターフェース呼び出しのフローチャート

![image](https://main.qcloudimg.com/raw/99d612d90268a7248f5b55c385eeb8b8.png)

### 統合の手順

#### SDKの統合

プロジェクトにSDKを統合するには、[Unity SDK統合ドキュメント](https://intl.cloud.tencent.com/zh/document/product/607/10783)をご参照ください。

####　コアインターフェース

- <dx-tag-link link="#Init" tag="接口：Init">GMEの初期化</dx-tag-link>
- <dx-tag-link link="#Poll" tag="接口：Poll">定期的なPoll呼び出しによるコールバックのトリガー</dx-tag-link>
- <dx-tag-link link="#Complete" tag="监听：QAVEnterRoomComplete">入退室の通知監視</dx-tag-link>

#### リアルタイム音声

<dx-steps>
-<dx-tag-link link="#EnterRoom" tag="接口：EnterRoom">リアルタイム音声ルームへの参加</dx-tag-link>
-<dx-tag-link link="#EnableMic" tag="接口：EnableMic">マイクのオン/オフ</dx-tag-link>
-<dx-tag-link link="#EnableSpeaker" tag="接口：EnableSpeaker">スピーカーのオン/オフ</dx-tag-link>
-<dx-tag-link link="#ExitRoom" tag="接口：ExitRoom">音声ルーム退出</dx-tag-link>
</dx-steps>

#### 音声メッセージ

<dx-steps>
-<dx-tag-link link="#ApplyPtt" tag="接口：ApplyPTTAuthbuffer">認証の初期化</dx-tag-link>
-<dx-tag-link link="#StartRWSR" tag="接口：StartRecordingWithStreamingRecognition">ストリーミング音声認識の起動</dx-tag-link>
-<dx-tag-link link="#Stop" tag="接口：StopRecording">レコーディング停止</dx-tag-link>
</dx-steps>

<dx-tag-link link="#Init" tag="接口：UnInit">GMEの録画を停止</dx-tag-link>

## コアインターフェースのアクセス

### 1. SDKのダウンロード 

ダウンロード案内ページにアクセスして、必要な<dx-tag-link link="https://cloud.tencent.com/document/product/607/18521" tag="DownLoad">クライアンSDKをダウンロードします</dx-tag-link>。

### 2. ヘッダーファイルを取り込む

```
using TencentMobileGaming;
```

### 3. Contextインスタンスの取得

QAVContext.GetInstance()の直接呼び出しでインスタンスを取得するのではなく、ITMGContextのメソッドでContextのインスタンスを取得してください。

#### サンプルコード  

```
int ret = ITMGContext.GetInstance().Init(sdkAppId, openID);
```

### [4. SDKを初期化する](id:Init)

- このインターフェースはGMEサービスの初期化に使用され、アプリケーションの初期化時にアプリケーション側で呼び出すことをお勧めします。
- **OpenIdはユーザーを一意に識別するために使用されます。現在はINT64のみがサポートされています。ルールはApp開発者が独自に設定し、App内で重複しないようにしてください**。
- **ユーザーがログインアカウントを切り替えた場合、Uninitを呼び出してから新しいOpenIdを使用してGMEサービスを再Initしてください**。

#### 関数のプロトタイプ

```
//class ITMGContext
public abstract int Init(string sdkAppID, string openID);
```

| パラメータ     |  タイプ  | 意味                                                         |
| -------- | :----: | ------------------------------------------------------------ |
| sdkAppId | String | [Tencent Cloudコンソール](https://console.cloud.tencent.com/gamegme)のGMEサービスが提供するAppId。 |
| OpenId   | String | openIdはInt64型のみをサポートします（stringに変換されて渡されます）。               |

#### サンプルコード 

```
int ret = ITMGContext.GetInstance().Init(sdkAppId, openID);
//戻り値で初期化が成功したかどうかを判断する
if (ret != QAVError.OK)
 {
     Debug.Log("SDK初期化失敗:"+ret);
     return;
 }
```

### [5. イベントコールバックのトリガー](id:Poll)

updateで周期的にPollを呼び出すことで、イベントのコールバックをトリガできます。GMEは定期的にPoll APIを呼び出してイベントコールバックをトリガしてください。Pollが呼び出されないと、SDKサービス全体が異常に動作します。
詳細については、DemoのEnginePollHelperファイルをご参照ください。

#### サンプルコード

```
public void Update()
  {
      ITMGContext.GetInstance().Poll();
  }
```

### [6. 入退室の通知監視](id:Complete)

#### 入室通知

```
//委託関数：
public delegate void QAVEnterRoomComplete(int result, string error_info);
//イベント関数：
public abstract event QAVEnterRoomComplete OnEnterRoomCompleteEvent;
```

#### 退室通知

```
委託関数：
public delegate void QAVExitRoomComplete();
イベント関数：
public abstract event QAVExitRoomComplete OnExitRoomCompleteEvent;
```

### 7.認証情報

関連する機能の暗号化と認証のためのAuthBufferを生成します。    
音声メッセージやテキスト変換の認証を取得する場合、ルーム番号のパラメータをnullに設定してください。

####  関数のプロトタイプ

```
QAVAuthBuffer GenAuthBuffer(int appId, string roomId, string openId, string key)
```

| パラメータ   |  タイプ     | 意味                                                         |
| ------ | :----: | ------------------------------------------------------------ |
| appId  |  int   | Tencent CloudコンソールからのAppId番号。                              |
| roomId | string | ルーム番号であり、最大127文字まで対応しています（オフライン音声ルーム番号のパラメータをnullに設定しなければなりません）。   |
| openId | string | ユーザーID。Initの場合のopenIdと同じです。                       |
| key    | string | Tencent Cloud[コンソール](https://console.cloud.tencent.com/gamegme)からの権限キー。 |

####  サンプルコード  

```
public static byte[] GetAuthBuffer(string AppID, string RoomID,string OpenId, string AuthKey){
    return QAVAuthBuffer.GenAuthBuffer(int.Parse(AppID), RoomID, OpenId, AuthKey);
}

```

## リアルタイム音声アクセス

### [1. ルームに参加](id:EnterRoom)

生成された認証情報を用いて入室します。ルームに参加するとき、デフォルトでマイクとスピーカーはオフです。インターフェースの戻り値が0の場合は、正常に入室することでなく、呼び出しインタフェースが正常に終了したことを意味します。

ルームオーディオタイプについては、[音質選択](https://intl.cloud.tencent.com/zh/document/product/607/18522)をご参照ください。

####  関数のプロトタイプ

```
ITMGContext EnterRoom(string roomId, int roomType, byte[] authBuffer)
```

| パラメータ       |  タイプ  | 意味                    |
| ---------- | :----: | ----------------------- |
| roomId     | String | ルーム番号、127文字まで入力可能 |
| roomType   |  int   | ルームオーディオタイプ            |
| authBuffer | byte[] | 認証コード                  |

#### サンプルコード  

```
ITMGContext.GetInstance().EnterRoom(strRoomId, ITMGRoomType.ITMG_ROOM_TYPE_FLUENCY, byteAuthbuffer);
```

#### 入室イベントのコールバック

入室が完了すると入室通知が届き、監視処理関数で判断して処理します。err=0のコールバックは成功を意味し、つまりこの時点の入室が成功しました。**課金**が開始されます。本日の合計通話時間が700分未満の場合は無料です。

<dx-fold-block title="计费问题参考">
[購入ガイド。](https://intl.cloud.tencent.com/zh/document/product/607/36276)
[課金に関するよくあるご質問。](https://intl.cloud.tencent.com/zh/document/product/607/30255)
[リアルタイム音声を使用した後、クライアントの接続が切れた場合課金は継続されますか。](https://intl.cloud.tencent.com/zh/document/product/607/30255)
</dx-fold-block>

- **サンプルコード**  
  コールバック処理の関連参照コード
```
//イベントを監視します：
ITMGContext.GetInstance().OnEnterRoomCompleteEvent += new QAVEnterRoomComplete(OnEnterRoomComplete);
//監視処理：
void OnEnterRoomComplete(int err, string errInfo)
{
  if (err != 0) {
    ShowLoginPanel("エラーコード:" + err + "エラーメッセージ:" + errInfo);
    return;
  }
  else{
	//入室に成功 
  }
}
```

- **エラーコード**
<table>
<thead>
<tr>
<th>エラーコードの値</th>
<th>原因と解決策</th>
</tr>
</thead>
<tbody><tr>
<td>7006</td>
<td>次の理由で認証に失敗しました：<ul><li>AppIDが存在しないか、エラーです</li><li>authbuff認証エラーです</li><li>認証期限切れです</li><li>openIdが仕様に準拠していません</li></ul></td>
</tr>
<tr>
<td>7007</td>
<td>他のルームにいます</td>
</tr>
<tr>
<td>1001</td>
<td>ルーム参加中でこの操作を繰り返しています。コールバックが戻るまで、ルーム参加インターフェースを呼び出さないことをお勧めします</td>
</tr>
<tr>
<td>1003</td>
<td>ルームに参加してルームにいますが、もう1回ルーム参加インターフェースを呼び出しました</td>
</tr>
<tr>
<td>1101</td>
<td>SDKが初期化されていること、openIdが規則に準拠していること、またはインターフェースが同じスレッドで呼び出されていること、およびPollインタフェースが正常に呼び出されていることを確認してください</td>
</tr>
</tbody></table>





### [2. マイクのオン/オフ](id:EnableMic)

このインターフェースは、マイクのオン/オフに使用されます。入室する際、マイクとスピーカーはデフォルトでオフになっています。

####  サンプルコード  

```
//イベントを監視します：
ITMGContext.GetInstance().OnEnterRoomCompleteEvent += new QAVEnterRoomComplete(OnEnterRoomComplete);
//監視処理：
void OnEnterRoomComplete(int err, string errInfo)
{
  if (err != 0) {
    ShowLoginPanel("エラーコード:" + err + "エラーメッセージ:" + errInfo);
    return;
  }
  else{
	//入室に成功 
	// マイクの起動
    ITMGContext.GetInstance().GetAudioCtrl().EnableMic(true);
  }
}
```

### [3. スピーカーのオン/オフ](id:EnableSpeaker)

このインターフェースは、スピーカーのオン/オフに使用されます。

#### サンプルコード  

```
//イベントを監視します：
ITMGContext.GetInstance().OnEnterRoomCompleteEvent += new QAVEnterRoomComplete(OnEnterRoomComplete);
//監視処理：
void OnEnterRoomComplete(int err, string errInfo)
{
  if (err != 0) {
    ShowLoginPanel("エラーコード:" + err + "エラーメッセージ:" + errInfo);
    return;
  }
  else{
	//入室に成功 
    //スピーカーをオンにする
    ITMGContext.GetInstance().GetAudioCtrl().EnableSpeaker(true);
  }
}
```

### [4. 退室](id:ExitRoom)

このインターフェースを呼び出すと、退室することができます。処理の実行は退室のコールバックを待つ必要があります。

#### サンプルコード  

```
ITMGContext.GetInstance().ExitRoom();
```

#### 退室コールバック

退室してからはコールバックが発生します、サンプルコードは次の通りです：

```
イベントを監視します。
ITMGContext.GetInstance().OnExitRoomCompleteEvent += new QAVExitRoomComplete(OnExitRoomComplete);
監視処理：
void OnExitRoomComplete(){
//退室した後の処理
}
```



## 音声メッセージの導入

### [1. 認証初期化](id:ApplyPtt)

SDKを初期化してから認証の初期化を呼び出します。authBufferの取得については、前記のリアルタイム音声の認証情報インターフェースgenAuthBufferをご参照ください。

#### 関数のプロトタイプ  

```
ITMGPTT int ApplyPTTAuthbuffer (byte[] authBuffer)
```

| パラメータ       |  タイプ  | 意味 |
| ---------- | :----: | ---- |
| authBuffer | String | 認証 |

#### サンプルコード  

```
UserConfig.SetAppID(transform.Find ("appId").GetComponent<InputField> ().text);
UserConfig.SetUserID(transform.Find ("userId").GetComponent<InputField> ().text);
UserConfig.SetAuthKey(transform.Find("authKey").GetComponent<InputField>().text);
byte[] authBuffer = UserConfig.GetAuthBuffer(UserConfig.GetAppID(), UserConfig.GetUserID(), null,UserConfig.GetAuthKey());
ITMGContext.GetInstance().GetPttCtrl().ApplyPTTAuthbuffer(authBuffer);
```

### [2. ストリーミング音声認識を起動](id:StartRWSR)

このインターフェースは、ストリーミング音声識別の開始に使われています。コールバックにおいて、音声はリアルタイムでテキストに変換されて返されます。言語を指定し識別することができるし、音声から識別した情報を指定した言語に翻訳してから返すこともできます。**録音の停止にはStopRecording**を呼び出します。停止後にコールバックが発生します。

#### 関数のプロトタイプ  

```
ITMGPTT int StartRecordingWithStreamingRecognition(string filePath)
ITMGPTT int StartRecordingWithStreamingRecognition(string filePath, string speechLanguage,string translateLanguage)
```

| パラメータ              |  タイプ  | 意味                                                         |
| ----------------- | :----: | ------------------------------------------------------------ |
| filePath          | String | ボイスの保存パス                                               |
| speechLanguage    | String | 指定した言語のテキストに識別するパラメータです。パラメータについては、[音声のテキスト変換の言語パラメータ参照リスト](https://intl.cloud.tencent.com/zh/document/product/607/30260)をご参照ください |
| translateLanguage | String | 指定した言語のテキストに翻訳するパラメータです。パラメータについては、[音声のテキスト変換の言語パラメータ参照リスト](https://intl.cloud.tencent.com/zh/document/product/607/30260)をご参照ください。（このパラメータは一時的に無効です。speechLanguageと同じのパラメータを入力してください） |

#### サンプルコード  

```
string recordPath = Application.persistentDataPath + string.Format("/{0}.silk", sUid++);
int ret = ITMGContext.GetInstance().GetPttCtrl().StartRecordingWithStreamingRecognition(recordPath, "cmn-Hans-CN","cmn-Hans-CN");
```

#### ストリーミング音声識別コールバック

ストリーミング音声認識を開始した後、コールバック関数OnEventでコールバックメッセージを受信する必要があります。イベントメッセージは`ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE`があり、録音を停止して認識を完了した後にテキストを返します。これは、話が終わってから認識されたテキストを返すことに相当します。

OnEvent関数で、必要に応じて適切なイベントメッセージを判断します。渡されるパラメータには次の4つの情報が含まれます。

| メッセージ名称  |                    意味                     |
| --------- | :-----------------------------------------: |
| result    |    ストリーミングボイス認識が完了したかどうかを判断するための戻りコード     |
| text      |            ボイステキスト変換で認識されたテキスト             |
| file_path |             録音を保存するローカルアドレス              |
| file_id   | 録音はバックグラウンドのURLアドレスにあり、録音はサーバーで90日間保存されます |

- **サンプルコード**  
```
//イベントを監視します：
ITMGContext.GetInstance().GetPttCtrl().OnStreamingSpeechComplete +=new QAVStreamingRecognitionCallback (OnStreamingSpeechComplete);
ITMGContext.GetInstance().GetPttCtrl().OnStreamingSpeechisRunning += new QAVStreamingRecognitionCallback (OnStreamingRecisRunning);
//監視処理：
void OnStreamingSpeechComplete(int code, string fileid, string filepath, string result){
    // ストリーミングAutomatic Speech Recognitionのコールバックの起動
}
void OnStreamingRecisRunning(int code, string fileid, string filePath, string result){
    if (code == 0)
    {
        setBtnText(mStreamBtn, "ストリーミング");
        InputField field = transform.Find("recordFilePath").GetComponent<InputField>();
        field.text = filePath;
            field = transform.Find("downloadUrl").GetComponent<InputField>();
        field.text = "Stream is Running";
            field = transform.Find("convertTextResult").GetComponent<InputField>();
        field.text = result;
        showWarningText("レコーディング中");
    }    
}
```

- **エラーコード**
<table>
<thead>
<tr>
<th>エラーコード</th>
<th align="center">意味</th>
<th align="center">処理方式</th>
</tr>
</thead>
<tbody><tr>
<td>32775</td>
<td align="center">ストリーミング音声をテキストに変更できませんが、録音は成功しました</td>
<td align="center">UploadRecordedFileインターフェースを呼び出して録音をアップロードし、SpeechToTextインターフェースを呼び出して音声を文字に変換します</td>
</tr>
<tr>
<td>32777</td>
<td align="center">ストリーミング音声をテキストに変更できませんが、録音とアップロードは成功しました</td>
<td align="center">返されたメッセージには正常にアップロードしたバックグラウンドURLがあり、SpeechToTextインターフェースを呼び出して音声から文字への変換操作を行います</td>
</tr>
<tr>
<td>32786</td>
<td align="center">ストリーミング音声をテキストに変更できませんでした</td>
<td align="center">ストリーミングレコーディングステータスでは、ストリーミングレコーディングインターフェースの実行結果が返されるまで待ってください</td>
</tr>
</tbody></table>



### [3. 録音を停止](id:Stop)

このインターフェースは、録音の停止に使われています。このインターフェースが非同期インターフェースであるため、録音を停止した後には録音完了のコールバックがあります。コールバックが成功してから、録音ファイルが利用できるようになります。

#### 関数のプロトタイプ  

```
ITMGPTT int StopRecording()
```

#### サンプルコード  

```
ITMGContext.GetInstance().GetPttCtrl().StopRecording();
```
