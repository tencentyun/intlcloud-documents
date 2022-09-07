開発者がGME製品APIのデバッグアクセスを行いやすいように、ここで、Unreal Engine開発に適用されるクイックアクセスドキュメントを説明します。

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

プロジェクトにSDKを統合するには、[Unreal SDK統合ドキュメント](https://intl.cloud.tencent.com/zh/document/product/607/17025)をご参照ください。

####　コアインターフェース

<dx-tag-link link="#Init" tag="接口：Init">GMEの初期化</dx-tag-link>
<dx-tag-link link="#Poll" tag="接口：Poll">定期的なPoll呼び出しによるコールバックのトリガー</dx-tag-link>
<dx-tag-link link="#Complete" tag="监听：QAVEnterRoomComplete">入退室の通知監視</dx-tag-link>

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
#include "tmg_sdk.h"

class UEDEMO1_API AUEDemoLevelScriptActor : public ALevelScriptActor, public ITMGDelegate
{
public:
...
private:
...
｝
```

### 3. シングルトンの設定

EnterRoom関数を呼び出す前に、ITMGContextの取得が必要です、全ての呼び出しはITMGContextから始まっており、ITMGDelegateによってコールバックでアプリケーションに返送されています、事前に設定してください。

#### サンプルコード 

```
ITMGContext* context = ITMGContextGetInstance();
context->SetTMGDelegate(this);
```



### [4. SDKを初期化する](id:Init)

- このインターフェースはGMEサービスの初期化に使用され、アプリケーションの初期化時にアプリケーション側で呼び出すことをお勧めします。
- **OpenIdはユーザーを一意に識別するために使用されます。現在はINT64のみがサポートされています。ルールはApp開発者が独自に設定し、App内で重複しないようにしてください**。
- **ユーザーがログインアカウントを切り替えた場合、Uninitを呼び出してから新しいOpenIdを使用してGMEサービスを再Initしてください**。

####  関数のプロトタイプ

```
//class ITMGContext
ITMGContext virtual int Init(const char* sdkAppId, const char* openId)
```

| パラメータ     |    タイプ     | 意味                                                         |
| -------- | :---------: | ------------------------------------------------------------ |
| sdkAppId | const char* | [Tencent Cloudコンソール](https://console.cloud.tencent.com/gamegme)のGME サービスが提供するAppId。|
| OpenId   | const char* | OpenIdはInt64型のみをサポートします（stringに変換されて渡されます）。               |

#### サンプルコード 

```
std::string appid = TCHAR_TO_UTF8(CurrentWidget->editAppID->GetText().ToString().operator*());
std::string userId = TCHAR_TO_UTF8(CurrentWidget->editUserID->GetText().ToString().operator*());
ITMGContextGetInstance()->Init(appid.c_str(), userId.c_str());
```

### [5. イベントコールバックのトリガー](id:Poll)

updateで周期的にPollを呼び出すことで、イベントのコールバックをトリガできます。GMEは定期的にPoll APIを呼び出してイベントコールバックをトリガしてください。Pollが呼び出されないと、SDKサービス全体が異常に動作します。
詳細については、DemoのUEDemoLevelScriptActor.cppファイルをご参照ください。

####  サンプルコード

```
//ヘッダファイルにおける宣言
virtual void Tick(float DeltaSeconds);

void AUEDemoLevelScriptActor::Tick(float DeltaSeconds) {
  Super::Tick(DeltaSeconds);  
  ITMGContextGetInstance()->Poll();
}
```

### [6. コールバックの設定](id:Complete)

インターフェースなどは、Delegate方式でアプリケーションにコールバック通知を送信します、メッセージタイプはITMG_MAIN_EVENT_TYPEを参考してください、Windowsプラットフォームにおけるdataはjson文字列の形であり、具体的なkey-valueは、説明ドキュメントを参考してください。

#### サンプルコード  

```
//関数の実現：
//UEDemoLevelScriptActor.h:
class UEDEMO1_API AUEDemoLevelScriptActor : public ALevelScriptActor, public SetTMGDelegate
{
public:
  void OnEvent(ITMG_MAIN_EVENT_TYPE eventType, const char* data);
｝

//UEDemoLevelScriptActor.cpp:
void AUEDemoLevelScriptActor::OnEvent(ITMG_MAIN_EVENT_TYPE eventType, const char* data){
  //ここで、eventTypeの判断と操作を行います
}
```

### 7. 認証情報

関連する機能の暗号化と認証のためのAuthBufferを生成します。    
音声メッセージやテキスト変換の認証を取得する場合、ルーム番号のパラメータをnullに設定してください。

#### 関数のプロトタイプ

```
int  QAVSDK_AuthBuffer_GenAuthBuffer(unsigned int dwSdkAppID, const char* strRoomID, const char* strOpenID,
  const char* strKey, unsigned char* strAuthBuffer, unsigned int bufferLength);
```

| 参数          | タイプ  | 意味                                                         |
| ------------- | :---: | ------------------------------------------------------------ |
| dwSdkAppID    |  int  | Tencent CloudコンソールからのAppId番号                                |
| strRoomID     | char* | ルーム番号です。最大127バイトまでをサポートします                                      |
| strOpenID     | char* | ユーザーID。Initの場合のopenIDと同じです。                        |
| strKey        | char* | Tencent Cloud[コンソール](https://console.cloud.tencent.com/gamegme)からの権限キー |
| strAuthBuffer | char* | 返されたauthbuff                                              |
| bufferLength  |  int  | 渡されるauthbuffの長さです。推奨値は500です                             |



#### サンプルコード  

```
unsigned int bufferLen = 512;
unsigned char retAuthBuff[512] = {0};
QAVSDK_AuthBuffer_GenAuthBuffer(atoi(SDKAPPID3RD), roomId, "10001", AUTHKEY,retAuthBuff,bufferLen);
```

## リアルタイム音声アクセス

### [1. ルームに参加](id:EnterRoom)

生成された認証情報を用いて入室します。ルームに参加するとき、デフォルトでマイクとスピーカーはオフです。インターフェースの戻り値が0の場合は、正常に入室することでなく、呼び出しインタフェースが正常に終了したことを意味します。

ルームオーディオタイプについては、[音質選択](https://intl.cloud.tencent.com/zh/document/product/607/18522)をご参照ください。

#### 関数のプロトタイプ

```
ITMGContext virtual int EnterRoom(const char*  roomID, ITMG_ROOM_TYPE roomType, const char* authBuff, int buffLen)

```

| パラメータ       |      タイプ      | 意味                    |
| ---------- | :------------: | ----------------------- |
| roomID     |     char*      | ルーム番号であり、最大127バイトまでをサポートします |
| roomType   | ITMG_ROOM_TYPE | ルームオーディオタイプ            |
| authBuffer |     char*      | 認証コード                  |
| buffLen    |      int       | 認証コードの長さ              |

#### サンプルコード  

```
ITMGContext* context = ITMGContextGetInstance();
context->EnterRoom(roomID, ITMG_ROOM_TYPE_FLUENCY, (char*)retAuthBuff,bufferLen);
```

#### 入室イベントのコールバック

入室が完了すると入室通知が届き、監視処理関数で判断して処理します。err=0のコールバックは成功を意味し、つまりこの時点の入室が成功しました。**課金**が開始されます。本日の合計通話時間が700分未満の場合は無料です。

<dx-fold-block title="计费问题参考">
[購入ガイド。](https://intl.cloud.tencent.com/zh/document/product/607/36276)
[課金に関するよくあるご質問。](https://intl.cloud.tencent.com/zh/document/product/607/30255)
[リアルタイム音声を使用した後、クライアントの接続が切れた場合課金は継続されますか？](https://intl.cloud.tencent.com/zh/document/product/607/30255)
</dx-fold-block>

- **サンプルコード**  
  コールバック処理の関連参照コード
```
void UBaseViewController::OnEvent(ITMG_MAIN_EVENT_TYPE eventType, const char *data) {

  FString jsonData = FString(UTF8_TO_TCHAR(data));
  TSharedPtr<FJsonObject> JsonObject;
  TSharedRef<TJsonReader<>> Reader = TJsonReaderFactory<>::Create(FString(UTF8_TO_TCHAR(data)));
  FJsonSerializer::Deserialize(Reader, JsonObject);


  if (eventType == ITMG_MAIN_EVENT_TYPE_ENTER_ROOM) {
    int32 result = JsonObject->GetIntegerField(TEXT("result"));
    FString error_info = JsonObject->GetStringField(TEXT("error_info"));
    if (result == 0) {
      GEngine->AddOnScreenDebugMessage(INDEX_NONE, 20.0f, FColor::Yellow, TEXT("Enter room success."));
    }
    else {
      FString msg = FString::Printf(TEXT("Enter room failed. result=%d, info = %ls"), result, *error_info);
      GEngine->AddOnScreenDebugMessage(INDEX_NONE, 20.0f, FColor::Yellow, *msg);
    }
    onEnterRoomCompleted(result, error_info);
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

#### サンプルコード  

```
void UBaseViewController::OnEvent(ITMG_MAIN_EVENT_TYPE eventType, const char *data) {

  FString jsonData = FString(UTF8_TO_TCHAR(data));
  TSharedPtr<FJsonObject> JsonObject;
  TSharedRef<TJsonReader<>> Reader = TJsonReaderFactory<>::Create(FString(UTF8_TO_TCHAR(data)));
  FJsonSerializer::Deserialize(Reader, JsonObject);


  if (eventType == ITMG_MAIN_EVENT_TYPE_ENTER_ROOM) {
    int32 result = JsonObject->GetIntegerField(TEXT("result"));
    FString error_info = JsonObject->GetStringField(TEXT("error_info"));
    if (result == 0) {
      GEngine->AddOnScreenDebugMessage(INDEX_NONE, 20.0f, FColor::Yellow, TEXT("Enter room success."));
      // マイクの起動
      ITMGContextGetInstance()->GetAudioCtrl()->EnableMic(true);
    }
    else {
      FString msg = FString::Printf(TEXT("Enter room failed. result=%d, info = %ls"), result, *error_info);
      GEngine->AddOnScreenDebugMessage(INDEX_NONE, 20.0f, FColor::Yellow, *msg);
    }
    onEnterRoomCompleted(result, error_info);
  }
}
```

[3. スピーカーのオン/オフ](id:EnableSpeaker)

このインターフェースは、スピーカーのオン/オフに使用されます。

#### サンプルコード  

```
void UBaseViewController::OnEvent(ITMG_MAIN_EVENT_TYPE eventType, const char *data) {

  FString jsonData = FString(UTF8_TO_TCHAR(data));
  TSharedPtr<FJsonObject> JsonObject;
  TSharedRef<TJsonReader<>> Reader = TJsonReaderFactory<>::Create(FString(UTF8_TO_TCHAR(data)));
  FJsonSerializer::Deserialize(Reader, JsonObject);


  if (eventType == ITMG_MAIN_EVENT_TYPE_ENTER_ROOM) {
    int32 result = JsonObject->GetIntegerField(TEXT("result"));
    FString error_info = JsonObject->GetStringField(TEXT("error_info"));
    if (result == 0) {
      GEngine->AddOnScreenDebugMessage(INDEX_NONE, 20.0f, FColor::Yellow, TEXT("Enter room success."));
      //スピーカーをオンにする
      ITMGContextGetInstance()->GetAudioCtrl()->EnableSpeaker(true);
    }
    else {
      FString msg = FString::Printf(TEXT("Enter room failed. result=%d, info = %ls"), result, *error_info);
      GEngine->AddOnScreenDebugMessage(INDEX_NONE, 20.0f, FColor::Yellow, *msg);
    }
    onEnterRoomCompleted(result, error_info);
  }
}

```

### [4. 退室](id:ExitRoom)

このインターフェースを呼び出すと、退室することができます。処理の実行は退室のコールバックを待つ必要があります。

#### サンプルコード  

```
ITMGContext* context = ITMGContextGetInstance();
context->ExitRoom();

```

#### 退室コールバック

退室してからはコールバックが発生します、サンプルコードは次の通りです：

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
  switch (eventType) {
            case ITMG_MAIN_EVENT_TYPE_EXIT_ROOM:
    {
    //処理します
    break;
    }
  }
}

```



## 音声メッセージの導入

### [1. 認証初期化](id:ApplyPtt)

SDKを初期化してから認証の初期化を呼び出します。authBufferの取得については、前記のリアルタイム音声の認証情報インターフェースgenAuthBufferをご参照ください。

#### 関数のプロトタイプ  

```
ITMGPTT virtual int ApplyPTTAuthbuffer(const char* authBuffer, int authBufferLen)

```

| パラメータ          | タイプ  | 意味     |
| ------------- | :---: | -------- |
| authBuffer    | char* | 認証     |
| authBufferLen |  int  | 認証の長さ |

#### サンプルコード  

```
ITMGContextGetInstance()->GetPTT()->ApplyPTTAuthbuffer(authBuffer,authBufferLen);

```

### [2. ストリーミング音声認識を起動](id:StartRWSR)

このインターフェースは、ストリーミング音声識別の開始に使われています。コールバックにおいて、音声はリアルタイムでテキストに変換されて返されます。言語を指定し識別することができるし、音声から識別した情報を指定した言語に翻訳してから返すこともできます。**録音の停止にはStopRecording**を呼び出します。停止後にコールバックが発生します。

#### 関数のプロトタイプ  

```
ITMGPTT virtual int StartRecordingWithStreamingRecognition(const char* filePath) 
ITMGPTT virtual int StartRecordingWithStreamingRecognition(const char* filePath,const char* translateLanguage,const char* translateLanguage) 

```

| 参数              | タイプ  | 意味                                                         |
| ----------------- | :---: | ------------------------------------------------------------ |
| filePath          | char* | ボイスの保存パス                                               |
| speechLanguage    | char* | 指定した言語のテキストに識別するパラメータです。パラメータについては、[音声のテキスト変換の言語パラメータ参照リスト](https://intl.cloud.tencent.com/zh/document/product/607/30260)をご参照ください |
| translateLanguage | char* | 指定した言語のテキストに翻訳するパラメータです。パラメータについては、[音声のテキスト変換の言語パラメータ参照リスト](https://intl.cloud.tencent.com/zh/document/product/607/30260)をご参照ください。（このパラメータは一時的に無効です。speechLanguageと同じのパラメータを入力してください） |

#### サンプルコード  

```
ITMGContextGetInstance()->GetPTT()->StartRecordingWithStreamingRecognition(filePath,"cmn-Hans-CN","cmn-Hans-CN");

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
void UBaseViewController::OnEvent(ITMG_MAIN_EVENT_TYPE eventType, const char *data) {

  FString jsonData = FString(UTF8_TO_TCHAR(data));
  TSharedPtr<FJsonObject> JsonObject;
  TSharedRef<TJsonReader<>> Reader = TJsonReaderFactory<>::Create(FString(UTF8_TO_TCHAR(data)));
  FJsonSerializer::Deserialize(Reader, JsonObject);
  ...
  else if(eventType == ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE)
    {
        int32 nResult = JsonObject->GetIntegerField(TEXT("result"));
        FString text = JsonObject->GetStringField(TEXT("text"));
        FString fileid = JsonObject->GetStringField(TEXT("file_id"));
        FString file_path = JsonObject->GetStringField(TEXT("file_path"));
        onPttStreamRecognitionCompleted(nResult,file_path, fileid, text);
    }
    else if(eventType == ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_IS_RUNNING)
    {
        int32 nResult = JsonObject->GetIntegerField(TEXT("result"));
        FString text = JsonObject->GetStringField(TEXT("text"));
        FString fileid = TEXT("STREAMINGRECOGNITION_IS_RUNNING");
        FString file_path = JsonObject->GetStringField(TEXT("file_path"));
        onPttStreamRecognitionisRunning(nResult,file_path, fileid, text);
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
ITMGPTT virtual int StopRecording()
```

#### サンプルコード  

```
ITMGContextGetInstance()->GetPTT()->StopRecording();
```
