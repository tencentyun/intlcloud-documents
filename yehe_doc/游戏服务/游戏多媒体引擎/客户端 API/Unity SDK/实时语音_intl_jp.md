Unityを使う開発者たちがTencent Cloud Gaming Multimedia EngineのクライアントAPIのデバッグ・アクセスを手軽に実行できるように、このドキュメントはUnityのリアルタイムボイス機能に適した開発導入技術ドキュメントについて説明します。

## GME利用上の重要事項

GMEはリアルタイム音声サービス、音声メッセージおよびボイスツーテキスト変換サービスを提供しており、GMEサービスの利用はInitやPollなどのコアインターフェースに依存しています。

#### 重要注意

- GMEアプリケーションの作成が完了し、SDK AppIDとKeyを取得しました。[サービス有効化ガイド](https://intl.cloud.tencent.com/document/product/607/10782)をご参照ください。
- **GMEリアルタイムボイスサービス、ボイスメッセージサービうおよびボイスツーテキスト変換サービス**が既に有効にされました。[サービス有効化ガイド](https://intl.cloud.tencent.com/document/product/607/10782)をご参照ください。
- GMEを利用する前にプロジェクトを構成してください。構成しないと、SDKが有効になりません。
- GMEのインターフェースが正常に呼び出された後、戻り値はQAVError.OKになり、値は0になります。
- GMEのインターフェースの呼び出しは、同じスレッドで行う必要があります。
- GMEは周期的にPollインターフェースを呼び出して、イベントのコールバックをトリガーする必要があります。
- エラーコードの詳細については、<dx-tag-link link="https://cloud.tencent.com/document/product/607/15173" tag="ErrorCode">エラーコード</dx-tag-link>をご参照ください。
- GMEは、Unity- WebGLプラットフォームでは簡単なリアルタイム音声通話のみをサポートしています。詳細については[H5プロジェクト設定](https://intl.cloud.tencent.com/document/product/607/30261)をご参照ください。

## SDKへのアクセス

### 重要な手順

SDKへのアクセスの重要な手順は次のとおりです：

<img src="https://qcloudimg.tencent-cloud.cn/raw/c8758a24fe68fc084b8d12b09de5e27a.jpg"  width="70%" /></img>

<dx-steps>
- <dx-tag-link link="#Init" tag="接口：Init">GMEの初期化</dx-tag-link>
- <dx-tag-link link="#Poll" tag="接口：Poll">定期的なPoll呼び出しによるコールバックのトリガー</dx-tag-link>
-<dx-tag-link link="#EnterRoom" tag="接口：EnterRoom">リアルタイムボイスルームへの参加</dx-tag-link>
- <dx-tag-link  tag="回调：QAVEnterRoomComplete">入室のコールバック処理</dx-tag-link>
-<dx-tag-link link="#EnableMic" tag="接口：EnableMic">マイクをオンにする</dx-tag-link>
-<dx-tag-link link="#EnableSpeaker" tag="接口：EnableSpeaker">スピーカーをオンにする</dx-tag-link>
-<dx-tag-link link="#ExitRoom" tag="接口：ExitRoom">音声ルーム退出</dx-tag-link>
- <dx-tag-link link="#UnInit" tag="接口：UnInit">GMEの未初期化</dx-tag-link>
</dx-steps>

### C#クラス

| クラス                  |        意味        |
| ------------------- | :----------------: |
| ITMGContext         |      コアインターフェース      |
| ITMGRoom            |    ルーム関連インターフェース    |
| ITMGRoomManager     |    ルーム管理インターフェース    |
| ITMGAudioCtrl       |    オーディオ関連インターフェース    |
| ITMGAudioEffectCtrl | サウンドと伴奏関連インターフェース |

##　コアインターフェース

|インターフェース     | インターフェースの意味   |
| ------ | :----------: |
|Init    |GMEを初期化します |
|Poll    |イベントコールバックをトリガーします|
|Pause   |システムを一時停止します|
|Resume |システムをリカバーします|
|Uninit    |GMEを未初期化にします |

###　ヘッダファイルのインクルード

```
using GME;
```

### インスタンスの取得

QAVContext.GetInstance()の直接呼び出しでインスタンスを取得するのではなく、ITMGContextのメソッドでContextのインスタンスを取得してください。

[](id:Init)
### SDKの初期化

初期化前のSDKは初期化されていない状態です。リアルタイム音声サービス、音声メッセージサービスおよびボイスツーテキスト変換サービスを使用するには、**インターフェースInitを使用してSDKを初期化する必要があります**。Initインターフェースを呼び出すスレッドは、他のインターフェースと同じスレッドである必要があります。すべてのメインスレッドでインターフェースを呼び出すことをお勧めします。

#### インターフェースのプロトタイプ

```
//class ITMGContext
public abstract int Init(string sdkAppID, string openID);
```

| パラメータ     |  タイプ  | 意味                                                         |
| -------- | :----: | ------------------------------------------------------------ |
| sdkAppId | string | [Tencent Cloud Console](https://console.cloud.tencent.com/gamegme)のGMEサービスが提供するAppIDです。取得については[ボイスサービス有効化ガイド](https://intl.cloud.tencent.com/document/product/607/10782#.E9.87.8D.E7.82.B9.E5.8F.82.E6.95.B0)をご参照ください。|
| openID   | string | openIDはInt64型（stringに変換して渡す）のみに対応しており、ルールはApp開発者が独自に定め、App内で重複しなければよい。文字列をOpenidとして渡す必要がある場合は、[チケットを提出](https://console.cloud.tencent.com/workorder/category?level1_id=438&level2_id=445&source=0&data_title=%E6%B8%B8%E6%88%8F%E5%A4%9A%E5%AA%92%E4%BD%93%E5%BC%95%E6%93%8EGME&step=1)をして開発者に連絡してください。|

#### 戻り値

| 戻り値                          | 処理                                          |
| ------------------------------- | --------------------------------------------- |
| QAVError.OK= 0                  | SDKの初期化に成功しました                               |
| AV_ERR_SDK_NOT_FULL_UPDATE=7015 | SDKファイルが完全であるかどうかをチェックし、削除後にSDKを再インポートすることをお勧めします |

<dx-alert infotype="notice" title="关于7015错误提示">

- 7015エラーコードはmd5で判断されます。アクセス中にこのエラーが発生した場合は、お知らせメッセージに従ってSDKファイルが完全であるかどうか、SDKファイルのバージョンが一致しているかどうかを確認してください。
- 戻り値AV_ERR_SDK_NOT_FULL_UPDATEが表示された場合、この戻り値は**お知らせメッセージ**として機能し、初期化に失敗することはありません。
- サードパーティの堅牢性、Unityパッケージングなどの要因がライブラリファイルmd5に影響を与え、正しくない判断を下すため、**リリース時にはこのエラーをロジックで無視してください**。UIでは表示されないようにしてください。
  </dx-alert>

####  サンプルコード 

```
int ret = ITMGContext.GetInstance().Init(sdkAppId, openID);
//戻り値で初期化が成功したかどうかを判断する
if (ret != QAVError.OK)
    {
        Debug.Log("SDK初期化失敗:"+ret);
        return;
    }
```

[](id:Poll)
### イベントのコールバックをトリガーします

updateで周期的にPollを呼び出すことで、イベントのコールバックをトリガできます。PollはGMEのメッセージポンプであり、GMEはイベントのコールバックをトリガするためにPollインターフェースを定期的に呼び出す必要があります。Pollが呼び出されないと、SDKサービス全体が異常に動作します。詳細については、[Sample Project](https://intl.cloud.tencent.com/document/product/607/18521)のEnginePollHelperファイルをご参照ください。

<dx-alert infotype="alarm" title="务必周期性调用 Poll 接口">
インターフェースのコールバックに異常が発生しないよう、定期的にメインスレッドで呼び出してください。
</dx-alert>

#### インターフェースのプロトタイプ

```
ITMGContext public abstract int Poll();
```

####  サンプルコード

```
public void Update()
    {
        ITMGContext.GetInstance().Poll();
    }
```

### システムの一時停止

システムでPauseイベントが発生したら、Pauseを実行するようエンジンに通知する必要があります。例えば、アプリケーションがバックグラウンドに戻ったとき（OnApplicationPause,isPause=True）、ルーム内のサウンドをバックグラウンドで再生しない場合は、Pauseインターフェースを呼び出してGMEサービス全体を一時停止します。

#### インターフェースのプロトタイプ

```
ITMGContext public abstract int Pause()
```

### システムリカバー

システムにResumeイベントが発生した場合、エンジンに通知を出し、Resumeを実行させる必要があります。Resumeインターフェースはリアルタイム音声のみをリカバーします。

#### インターフェースのプロトタイプ

```
ITMGContext  public abstract int Resume()
```

[](id:UnInit)
### SDKの未初期化

SDKを逆初期化し、未初期化状態にします。**ゲームサービス側のアカウントとopenidが紐付けられている場合、ゲームアカウントを切り替えるにはGMEを逆初期化し、新しいopenidで初期化する**必要があります。

#### インターフェースのプロトタイプ

```
ITMGContext public abstract int Uninit()
```

## リアルタイム音声ルームの関連インターフェース

リアルタイム音声通話を行うには、初期化してから、SDKの入室インタフェースを呼び出し、入室する必要があります。
利用上の問題について、[リアルタイムボイス関連問題](https://intl.cloud.tencent.com/document/product/607/39524)をご参照ください。

![](https://qcloudimg.tencent-cloud.cn/raw/02f98895d0b7bfe1bac774d5983289c1.jpg)

|インターフェース     | インターフェースの意味   |
| ------------- | :------------------: |
| GenAuthBuffer |     ローカル認証の計算     |
| EnterRoom     |       入室します       |
|ExitRoom |退室します|
| IsRoomEntered | 入室していますか |
| SwitchRoom    |     ルームの素早い切り替え     |

###　　ローカル認証の計算

AuthBufferを生成し、関連機能の暗号化と認証に使用します。本格なリリースについてバックグラウンドのデプロイキーを使用してください。バックグラウンドのデプロイについては、[認証キー](https://intl.cloud.tencent.com/document/product/607/12218)をご参照ください。    

#### インターフェースのプロトタイプ

```
QAVAuthBuffer GenAuthBuffer(int appId, string roomId, string openId, string key)
```

| パラメータ   | タイプ   | 意味                                                         |
| ------ | :----: | ------------------------------------------------------------ |
| appId  |  int   | Tencent CloudコンソールからのAppID番号。                              |
| roomId|string    |ルーム番号は最大127文字まで対応しています。|
| openId | string | ユーザーID。Initの場合のopenIDと同じです。                        |
| key    | string | Tencent Cloud[コンソール](https://console.cloud.tencent.com/gamegme)からの権限キー。 |

####  サンプルコード  

```
public static byte[] GetAuthBuffer(string AppID, string RoomID,string OpenId, string AuthKey){
        return QAVAuthBuffer.GenAuthBuffer(int.Parse(AppID), RoomID, OpenId, AuthKey);
}

```

####　WebGL側のフィット
- WebGLプラットフォームでは、ローカル認証関数を呼び出した後、認証値はjsコードに保存され、認証されたauthBufferをC#層に返すことはなく、ユーザーはGetAuthBufferインターフェースを呼び出してローカル認証を行った後、入室時に認証コードの値を空か任意の値に入力してください。
- 認証をバックグラウンドで計算するスキームを使用する場合、GetAuthBufferインターフェースを呼び出す必要はありません。


[](id:EnterRoom)
### 入室

生成した認証情報を用いてルームに参加します。ルームに参加するとき、デフォルトでマイクとスピーカーはオフです。

<dx-alert infotype="alarm" title="注意">
- 入室イベントのコールバック結果resultが0の場合は、入室が成功したことを示します。入室インターフェースEnterRoomの戻り値が0の場合でも、入室が成功したことを示しません。
- ルームのオーディオタイプは最初にルームに入った人によって決定され、その後、ルームのメンバーがルームのタイプを変更すると、そのルームのすべてのメンバーに適用されます。例えば、最初にルームに入った人が使っているルームのオーディオタイプは滑らかな音質で、2番目にルームに入った人はルームに入ったときに呼び出すインターフェースのオーディオタイプのパラメータが高精細な音質であっても、ルームに入ってからは滑らかな音質になります。ルームのオーディオタイプを変更するには、メンバーがChangeRoomTypeを呼び出す必要があります。
</dx-alert>

#### インターフェースのプロトタイプ

```
ITMGContext EnterRoom(string roomId, int roomType, byte[] authBuffer)

```

| パラメータ          | タイプ                    | 意味                                                  |
| ---------- | :----------: | ------------------------------------------ |
| roomId    		|string   		|ルームID、127文字まで入力可能					|
| roomType   | ITMGRoomType | ルームタイプです。ゲームではITMG_ROOM_TYPE_FLUENCYを使用することを推奨します。ルームオーディオのタイプについては、[音質選択](https://intl.cloud.tencent.com/document/product/607/18522)をご参照ください。|
| authBuffer 	|Byte[] 	|認証コード					|

####  サンプルコード  

```
ITMGContext.GetInstance().EnterRoom(strRoomId, ITMGRoomType.ITMG_ROOM_TYPE_FLUENCY, byteAuthbuffer);

```

#### 入室イベントのコールバック

ルーム参加が完了するとコールバックにより入室結果が返され、入室結果イベントを監視して処理が行われます。コールバックが成功した場合は、その時点で入室が成功し、**課金**が開始されます。

<dx-fold-block title="计费问题参考">
[購入ガイド。](https://intl.cloud.tencent.com/document/product/607/50009)
[課金に関するよくあるご質問。](https://intl.cloud.tencent.com/document/product/607/30255)
[リアルタイム音声を使用した後、クライアントの接続が切れた場合課金は継続されますか。](https://intl.cloud.tencent.com/document/product/607/30255#.E4.BD.BF.E7.94.A8.E5.AE.9E.E6.97.B6.E8.AF.AD.E9.9F.B3.E5.90.8E.EF.BC.8C.E5.A6.82.E6.9E.9C.E5.AE.A2.E6.88.B7.E7.AB.AF.E6.8E.89.E7.BA.BF.E4.BA.86.EF.BC.8C.E6.98.AF.E5.90.A6.E8.BF.98.E4.BC.9A.E7.BB.A7.E7.BB.AD.E8.AE.A1.E8.B4.B9.EF.BC.9F)
</dx-fold-block>

#### インターフェースのプロトタイプ

```
public delegate void QAVEnterRoomComplete(int result, string error_info);
public abstract event QAVEnterRoomComplete OnEnterRoomCompleteEvent;
```

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
	}else{
		//入室に成功 
    }
}
```

#### Dataの詳細

|メッセージ     | Data         |例|
| ------------------------------------ | :----------------: | ------------------------------------------------------------ |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    				|result; error_info					|{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT    	|result; error_info  			|{"error_info":"waiting timeout, please check your network","result":0}|

ネットワークが切断されると、切断されたコールバックのメッセージ`ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT`が表示され、この場合、SDKは自動的に再接続され、コールバックは`ITMG_MAIN_EVENT_TYPE_RECONNECT_START`です。再接続が成功すると`ITMG_MAIN_EVENT_RECONNECT_SUCCESS`がコールバックされます。

#### エラーコード

| エラーコード | 原因と解決策                       |
| -------- | ------------------------------------------------------------ |
| 7006     | 認証失敗の原因：<li>AppIDが存在しないか、エラーが発生しました<li>authbuff認証エラー<li>認証期限切れです <li>OpenIdが適切なものではありません |
| 7007     | 他のルームに入っています                                               |
|　1001　　　　|　ルーム参加中でこの操作を繰り返しています。入室のコールバックが戻るまで、ルーム参加インターフェースを呼び出さないことをお勧めします|
|1003　　　　|　ルームに参加してルームにいますが、もう1回ルーム参加インターフェースを呼び出しました　|
|　1101　　　|　SDKが初期化されていること、OpenIDがルールに準拠していること、またはインターフェースが同じスレッドで呼び出されていること、およびPollインターフェースが正常に呼び出されていることを確認してください|

[](id:ExitRoom)	
### 退室

このインターフェースを呼び出すと、退室することができます。これは非同期インターフェースであり、戻り値がAV_OKの場合は非同期配信が成功したことを示します。アプリケーション内にルームから退出後すぐにルールに参加するシナリオがある場合、開発者はAPI呼び出しフローで、ExitRoomのRoomExitCompleteコールバック通知を待つ必要がなく、APIを直接呼び出すことが可能です。

#### インターフェースのプロトタイプ  

```
ITMGContext ExitRoom()
```

####  サンプルコード  

```
ITMGContext.GetInstance().ExitRoom();
```

#### 退室イベントのコールバック

退室しコールバックを完成して、委託関数でメッセージを送信します。

#### インターフェースのプロトタイプ  

```
public delegate void QAVExitRoomComplete();
public abstract event QAVExitRoomComplete OnExitRoomCompleteEvent; 
```

####  サンプルコード  

```
イベントを監視します。
ITMGContext.GetInstance().OnExitRoomCompleteEvent += new QAVExitRoomComplete(OnExitRoomComplete);
監視処理：
void OnExitRoomComplete(){
    //退室した後の処理
}
```

### 入室しているかの判断

このインターフェースを呼び出すことで、入室しているかを判断できます。戻り値はbool型です。入室中に呼び出さないでください。

#### インターフェースのプロトタイプ  

```
ITMGContext abstract bool IsRoomEntered()
```

####  サンプルコード  

```
ITMGContext.GetInstance().IsRoomEntered();
```

###　ルームのすばやい切り替え

このインターフェースを呼び出して、リアルタイム音声ルームをすばやく切り替えることができます。このインターフェースはルームに入ってから呼び出されます。ルームを切り替えた後、デバイスはリセットされません。つまり、ルームでマイクがオンになっている場合は、ルームを切り替えた後もマイクがオンのままです。
素早いルーム切り替えのコールバックはITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_SWITCH_ROOMで、フィールドはerror_infoとresultです。

#### インターフェースのプロトタイプ

```
public abstract int SwitchRoom(string targetRoomID, byte[] authBuffer);
```

#### タイプの説明

| パラメータ          | タイプ                    | 意味                                                  |
| ------------ | ------ | ------------------------------ |
| targetRoomID | String | 参加するルーム番号               |
| authBuffer   | byte[] | 入室するルーム番号で生成された新しい認証 |

##　ルーム内の状態のメンテナンス

このインターフェースは、サービス層で発話メンバー、入退室メンバーを示し、ルーム内のあるメンバーの発話をミュートする機能に使用されます。

![](https://main.qcloudimg.com/raw/33eecfcd9e18a361aa0b732ffd0fb7dd.png)

| インターフェース/通知                        |       意味       |
| -------------------------------- | :--------------: |
| ITMG_MAIN_EVNET_TYPE_USER_UPDATE | メンバー状態の変更通知通知 |
| AddAudioBlackList                | ルームではメンバーの発話をミュートします |
| RemoveAudioBlackList             |     発話ミュートを解除します     |

###　メンバー入室、発話状況通知イベント

- このイベントは、ルーム内で話している人を取得してUIに表示したり、音声ルームに参加したり退出したりする通知を送ることに使用されます。
-　このイベントは状態が変化した場合のみ通知され、状態変化がない場合は通知されません。メンバーの状態をリアルタイムに取得するには、業務層で通知を受けたとき、キャッシュしてください。イベントメッセージはITMG_MAIN_EVNET_TYPE_USER_UPDATEであり、その中にevent_id、countとopenIdListがありまして、イベントメッセージがOnEvent通知の中で判断されています。
- オーディオイベントEVENT_ID_ENDPOINT_NO_AUDIOの通知にはしきい値があり、このしきい値を超えると通知が送信されます。つまり、ルームの他のメンバは、自端末が何も集音しなくなってから2秒後、自端末の発話停止の通知を受けます。
- オーディオイベントはメンバーの発話状態のみを返し、特定の音量は返さません。ルーム内のメンバー音量は、GetVolumeByIdインターフェースを使用して取得できます。

|event_id     | 意味         |保守内容|
| --------------------------- | :---------------------------------------------------: | ---------------------- |
| EVENT_ID_ENDPOINT_ENTER     |         入室したメンバーがいる場合。入室時のopenidが返されます         | アプリケーション側でメンバーリストのメンテナンスを行います     |
| EVENT_ID_ENDPOINT_EXIT      |         退室したメンバーがいる場合。退出時のopenidが返されます         | アプリケーション側でメンバーリストのメンテナンスを行います     |
| EVENT_ID_ENDPOINT_HAS_AUDIO |     オーディオパケットを送信するメンバーがいる場合、その時点でルーム内で発話しているopenidが返されます。このイベントでユーザーが発話しているか否かを判断し、声紋効果を示します     | アプリケーション側で通話メンバーリストのメンテナンスを行います     |
| EVENT_ID_ENDPOINT_NO_AUDIO  | オーディオパケットの送信を停止したメンバーがいる場合、その時点でルーム内で発話を停止しているopenidが返されます | アプリケーション側で通話メンバーリストのメンテナンスを行います |

####  サンプルコード

```
public delegate void QAVEndpointsUpdateInfo(int eventID, int count, [MarshalAs(UnmanagedType.LPArray, SizeParamIndex = 1)]string[] openIdList);
public abstract event QAVEndpointsUpdateInfo OnEndpointsUpdateInfoEvent;

//イベントを監視します：
ITMGContext.GetInstance().OnEndpointsUpdateInfoEvent += new QAVEndpointsUpdateInfo(OnEndpointsUpdateInfo);
//監視処理：
void OnEndpointsUpdateInfo(int eventID, int count, string[] openIdList)
{
				//処理します
		    switch (eventID)
 		    {
 		    case EVENT_ID_ENDPOINT_ENTER:
  			    //メンバーが入室しました
  			    break;
 		    case EVENT_ID_ENDPOINT_EXIT:
  			    //メンバーが退室しました
			    break;
		    case EVENT_ID_ENDPOINT_HAS_AUDIO:
			    //メンバーがオーディオパッケージを送信しています
			    break;
		    case EVENT_ID_ENDPOINT_NO_AUDIO:
			    //メンバーがオーディオパッケージの送信を停止しました
			    break;
		  
		    default:
			    break;
 		    }
		break;
}
```

### ルーム内の特定のメーバー発話をミュート

あるIDをオーディオデータのブラックリストに追加します。つまり、その人の音声を受信しません。これは自端末にのみ有効で、他端末には影響を与えません。返り値が0の場合、呼び出しが成功したことを示します。例えば、A、B、Cが同じルームで話をしています。 

- AがCのブラックリストを設定している場合、AがBの声しか聞こえません。
- Bがブラックリストを設定していないため、AとCの声が聞こえます。
- Cもブラックリストを設定していないため、AとBの声が聞こえます。

このインターフェースは、音声ルームで特定のユーザー発話をミュートするシナリオに使用されます。

#### インターフェースのプロトタイプ  

```
ITMGContext ITMGAudioCtrl AddAudioBlackList(String openId)
```

| パラメータ          | タイプ                    | 意味                                                  |
| ------ | :----: | ------------------------- |
| openId | String | ブラックリストに追加するユーザーのopenid |

####  サンプルコード  

```
ITMGContext.GetInstance().GetAudioCtrl ().AddAudioBlackList (openId);
```

###　発話ミュートの解除

あるIDをオーディオデータブラックリストから削除します。戻り値が0の場合、呼び出成功を表します。

#### インターフェースのプロトタイプ  

```
ITMGContext ITMGAudioCtrl RemoveAudioBlackList(string openId)
```

| パラメータ          | タイプ                    | 意味                                                  |
| ------ | :----: | ------------------------- |
| openId    |String   |　ブラックリストから削除するユーザーのopenidです|

####  サンプルコード  

```
ITMGContext.GetInstance().GetAudioCtrl ().RemoveAudioBlackList (openId);
```



## リアルタイムボイス収集に関するインターフェース

-　SDKを初期化し入室してから、ルームの中でリアルタイムボイスの関連インターフェースを呼び出すことができます。
- ユーザーインターフェースで「マイク/スピーカーのオン/オフ」ボタンをクリックした場合は、EnableMicインターフェースとEnableSpeakerインターフェースを呼び出すことをお勧めします。
- ユーザーインターフェースでマイクボタンを長押しすると発言し、ボタンを放すと発言しないようにする場合は、ルームに入るときに一度EnableAudioCaptureDeviceを呼び出し、その後長押し発言時にEnableAudioSendを呼び出すことをお勧めします。

|インターフェース     | インターフェースの意味   |
| --------------------------- | :------------------: |
|　EnableMic    |マイクをオン/オフにします|
|GetMicState    |マイクの状態を取得します|
|EnableAudioCaptureDevice    |採集デバイスをオン/オフにします|
|IsAudioCaptureDeviceEnabled    |採集デバイスの状態を取得します|
|EnableAudioSend    |オーディオの上りをオン/オフにします|
|IsAudioSendEnabled    |オーディオの上り状態を取得します|
|GetMicLevel    |マイクのリアルタイムボリュームを取得します|
|GetSendStreamLevel|オーディオの上りのリアルタイムボリュームを取得します|
|　SetMicVolume    |マイクのボリュームを設定します|
|GetMicVolume    |マイクのボリュームを取得します|


[](id:EnableMic)	
### マイクのオン/オフ

このコネクタはマイクのオン/オフを切り替えます。ルームに参加するとき、デフォルトでマイクとスピーカーはオフです。**EnableMic = EnableAudioCaptureDevice + EnableAudioSend**

#### インターフェースのプロトタイプ  

```
ITMGAudioCtrl EnableMic(bool isEnabled)
```

| パラメータ          | タイプ                    | 意味                                                  |
| --------- | :-----: | ------------------------------------------------------------ |
| isEnabled   |　boolean     |　マイクをオンにする場合、渡されたパラメータはtrueであり、マイクをオフにする場合、パラメータはfalseになります|

####  サンプルコード  

```
// マイクの起動
ITMGContext.GetInstance().GetAudioCtrl().EnableMic(true);
```

### マイク状態の取得

このインターフェースはマイクの状態の取得に使われています。戻り値0はマイクをオフにすることであり、戻り値1はマイクをオンにすることです。

#### インターフェースのプロトタイプ  

```
ITMGAudioCtrl GetMicState()
```

####  サンプルコード  

```
micToggle.isOn = ITMGContext.GetInstance().GetAudioCtrl().GetMicState();
```

### 収集デバイスのオン/オフ

このインターフェースは、採集デバイスのオン/オフに使われています。入室に際し、デバイスはデフォルトでオフになっています。

- このインターフェースは、入室後にのみ呼び出すことができます、退室した後、デバイスは自動的にオフになります。
- モバイル端末では、採集デバイスの起動は一般的に権限申請やボリュームタイプの調整を伴っています。

#### インターフェースのプロトタイプ  

```
ITMGAudioCtrl int EnableAudioCaptureDevice(bool isEnabled)
```

| パラメータ          | タイプ                    | 意味                                                  |
| --------- | :--: | ------------------------------------------------------------ |
| isEnabled    |　bool     |　収集デバイスをオンにする場合、渡されたパラメータはtrueであり、収集デバイスをオフにする場合、パラメータはfalseです|

####  サンプルコード

```
//収集デバイスをオンにします
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioCaptureDevice(true);
```

### 採集デバイス状態の取得

このインターフェースは、採集デバイス状態の取得に使われています。

#### インターフェースのプロトタイプ

```
ITMGAudioCtrl bool IsAudioCaptureDeviceEnabled()
```

####  サンプルコード

```
bool IsAudioCaptureDevice = ITMGContext.GetInstance().GetAudioCtrl().IsAudioCaptureDeviceEnabled();
```

### オーディオ上りのオン/オフ

このインターフェースは、オーディオ上りのオン/オフに使われています。収集デバイスがオンになっている場合は、収集したオーディオデータを送信します。収集デバイスがオフになっている場合は、ミュート状態が続きます。収集デバイスのオン/オフは、インターフェースEnableAudioCaptureDeviceをご参照ください。

#### インターフェースのプロトタイプ

```
ITMGAudioCtrl int EnableAudioSend(bool isEnabled)
```

| パラメータ          | タイプ                    | 意味                                                  |
| --------- | :--: | ------------------------------------------------------------ |
| isEnabled    |bool     |オーディオ送信をオンにする場合、渡されたパラメータはtrueであり、オーディオ送信をオフにする場合、パラメータはfalseです|

####  サンプルコード  

```
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioSend(true);
```

### オーディオ上り状態の取得

このインターフェースは、オーディオ上り状態の取得に使われています。

#### インターフェースのプロトタイプ  

```
ITMGAudioCtrl bool IsAudioSendEnabled()
```

####  サンプルコード  

```
bool IsAudioSend = ITMGContext.GetInstance().GetAudioCtrl().IsAudioSendEnabled();
```

### マイクのリアルタイムボリュームの取得

このAPIはマイクリアルタイム音量の取得に使用されます。20msに一度取得することをお勧めします。値の範囲は0～100で、このインターフェースを使用するとマイクで収集したリアルタイムの音量を取得できます。

 

#### インターフェースのプロトタイプ  

```
ITMGAudioCtrl int GetMicLevel
```

####  サンプルコード  

```
ITMGContext.GetInstance().GetAudioCtrl().GetMicLevel();
```

### オーディオ上りのリアルタイムボリュームの取得

このインターフェースは、自分のオーディオ上りのリアルタイムボリュームの取得に使われています。その戻り値はint型であり、数値範囲は0～100です。

 

#### インターフェースのプロトタイプ  

```
ITMGAudioCtrl int GetSendStreamLevel()
```

####  サンプルコード  

```
int Level = ITMGContext.GetInstance().GetAudioCtrl().GetSendStreamLevel();
```

### マイク音量ソフトウェアの設定

このインターフェースはマイクの音量を設定するために使用されます。パラメータvolumeは、マイクの音量を設定するために使用されます。これは、集音した音声を減衰またはゲインすることに相当します。

 

#### インターフェースのプロトタイプ  

```
ITMGAudioCtrl SetMicVolume(int volume)
```

| パラメータ   | タイプ   | 意味                                                         |
| ------ | :--: | ------------------------------------------------------------ |
| volume | int  | 値の範囲は0～200です。値が0の場合はミュート、値が100の場合は音量が増減しないことを示します。デフォルト値は100です。|

####  サンプルコード  

```
int micVol = (int)(value * 100);
ITMGContext.GetInstance().GetAudioCtrl().SetMicVolume (micVol);
```

###  マイクソフトウェアの音量取得

このインターフェースは、マイクボリュームの取得に使われています。戻り値はint型であり、戻り値が101である場合は、インターフェースSetMicVolumeを呼び出したことがないことを示しています。

 

#### インターフェースのプロトタイプ  

```
ITMGAudioCtrl GetMicVolume()
```

####  サンプルコード  

```
ITMGContext.GetInstance().GetAudioCtrl().GetMicVolume();
```

## リアルタイムボイス関連インターフェース

|インターフェース     | インターフェースの意味   |
| ------------------------ | :----------------------------: |
|EnableSpeaker    					|スピーカーのオン/オフ |
|GetSpeakerState    				|スピーカー状態の取得|
|　EnableAudioPlayDevice    |　再生デバイスをオン/オフにします|
|IsAudioPlayDeviceEnabled    |再生デバイスの状態を取得します|
|EnableAudioRecv    |オーディオの下りをオン/オフにします|
|IsAudioRecvEnabled    |オーディオの下りの状態を取得します|
|　GetSpeakerLevel    |　スピーカーのリアルタイムボリュームを取得します|
|GetRecvStreamLevel|ほかのルームメンバーのリアルタイムの下りボリュームを取得します|
|　SetSpeakerVolume    |　スピーカーのボリュームを設定します|
|　GetSpeakerVolume    |　スピーカーのボリュームを取得します|


[](id:EnableSpeaker)	
### スピーカーのオン/オフ

このインターフェースはスピーカーのオン/オフに使用されます。**EnableSpeaker = EnableAudioPlayDevice +  EnableAudioRecv**

#### インターフェースのプロトタイプ  

```
ITMGAudioCtrl EnableSpeaker(bool isEnabled)
```

| パラメータ          | タイプ                    | 意味                                                  |
| --------- | :--: | ------------------------------------------------------------ |
| isEnabled    |bool        |スピーカーをオフにする必要があれば、渡されたパラメータはfalseです。スピーカーをオンにすれば、パラメータはtrueです|

####  サンプルコード  

```
//スピーカーをオンにする
ITMGContext.GetInstance().GetAudioCtrl().EnableSpeaker(true);
```

### スピーカー状態の取得

このインターフェースは、スピーカー状態の取得に使われています。戻り値が0の場合、スピーカー状態をオフにし、戻り値が1の場合、スピーカー状態をオンにします。

#### インターフェースのプロトタイプ  

```
ITMGAudioCtrl GetSpeakerState()
```

####  サンプルコード  

```
speakerToggle.isOn = ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerState();
```



### 再生デバイスのオン/オフ

このインターフェースは、再生デバイスのオン/オフに使われています。

#### インターフェースのプロトタイプ  

```
ITMGAudioCtrl EnableAudioPlayDevice(bool isEnabled)
```

| パラメータ          | タイプ                    | 意味                                                  |
| --------- | :--: | ------------------------------------------------------------ |
| isEnabled    |bool   |再生デバイスをオフにする場合、渡すパラメータはfalseであり、再生デバイスをオンにする場合、パラメータはtrueです|

####  サンプルコード  

```
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioPlayDevice(true);
```

### 再生デバイスの状態の取得

このインターフェースは、再生デバイスの状態の取得に使われています。

#### インターフェースのプロトタイプ

```
ITMGAudioCtrl bool IsAudioPlayDeviceEnabled()
```

####  サンプルコード  

```
bool IsAudioPlayDevice = ITMGContext.GetInstance().GetAudioCtrl().IsAudioPlayDeviceEnabled();
```

### オーディオ下りのオン/オフ

このインターフェースは、オーディオ下りのオン/オフに使われています。再生デバイスがオンになっている場合は、ほかのルームメンバーのオーディオデータを再生できます。再生デバイスがオフになっている場合は、ミュート状態が続きます。再生デバイスのオン/オフは、EnableAudioPlayDeviceをご参照ください。

#### インターフェースのプロトタイプ  

```
ITMGAudioCtrl int EnableAudioRecv(bool isEnabled)
```

| パラメータ          | タイプ                    | 意味                                                  |
| --------- | :--: | ------------------------------------------------------------ |
| isEnabled    |bool     |オーディオ受信をオンにする場合、渡すパラメータはtrueであり、オーディオ受信をオフにする場合、パラメータはfalseです|

####  サンプルコード  

```
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioRecv(true);
```



### オーディオ下り状態の取得

このインターフェースは、オーディオ下り状態の取得に使われています。

#### インターフェースのプロトタイプ  

```
ITMGAudioCtrl bool IsAudioRecvEnabled()
```

####  サンプルコード  

```
bool IsAudioRecv = ITMGContext.GetInstance().GetAudioCtrl().IsAudioRecvEnabled();
```

### スピーカーのリアルタイムボリュームの取得

このインターフェースはスピーカーのリアルタイムボリュームの取得に使われています。戻り値はint型の数値であり、スピーカーのリアルタイムボリュームを示します。20msに1回取得することをおすすめします。

#### インターフェースのプロトタイプ  

```
ITMGAudioCtrl GetSpeakerLevel()
```

####  サンプルコード  

```
ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerLevel();
```

### ほかのルームメンバーの下りリアルタイムボリュームの取得

このインターフェースはルームのほかのメンバーの下りリアルタイムボリュームの取得に使われています。その戻り値はint型であり、数値範囲は0～200です。

#### インターフェースのプロトタイプ  

```
ITMGAudioCtrl int GetRecvStreamLevel(string openId)
```

| パラメータ          | タイプ                    | 意味                                                  |
| ------ | :----: | --------------------- |
| openId    |string       |ほかのルームメンバーのopenIdです|

####  サンプルコード  

```
int Level = ITMGContext.GetInstance().GetAudioCtrl().GetRecvStreamLevel(openId);
```

### スピーカーボリュームの設定

このインターフェースは、スピーカーボリュームの設定に使われています。

#### インターフェースのプロトタイプ  

```
ITMGAudioCtrl SetSpeakerVolume(int volume)
```

| パラメータ   | タイプ   | 意味                                                         |
| ------ | :--: | ------------------------------------------------------------ |
| volume | int  | 音量を0～200で設定します。値が0の場合はミュート、値が100の場合は音量が増減しないことを示します。デフォルト値は100です。|

####  サンプルコード  

```
int speVol = (int)(value * 100);
ITMGContext.GetInstance().GetAudioCtrl().SetSpeakerVolume(speVol);
```

### スピーカーボリュームの取得

このインターフェースは、スピーカーボリュームの取得に使われています。戻り値はint型であり、スピーカーボリュームを示しています。戻り値が101の場合は、インターフェースSetSpeakerVolumeを呼び出したことがないことを示しています。
Levelはリアルタイムボリュームであり、Volumeはスピーカーボリュームであり、最終の音声ボリュームは、Level×Volume%となります。例えば、リアルタイムボリュームが100で、Volume値が60である場合、最終の音声ボリューム値も60です。

#### インターフェースのプロトタイプ  

```
ITMGAudioCtrl GetSpeakerVolume()
```

####  サンプルコード  

```
ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerVolume();
```

##　デバイス選択関連インターフェース

デバイス選択関連インターフェースはPC側でのみ使用できます。

|インターフェース     | インターフェースの意味   |
| --------------------------- | :------------------: |
|　GetMicListCount           |　マイクデバイスの数を取得します|
|　GetMicList          |　マイクデバイスを列挙します|
|　GetSpeakerListCount          |　スピーカーデバイスの数を取得します|
|　GetSpeakerList          |　スピーカーデバイスを列挙します|
|SelectMic          |マイクデバイスを選びます|
|SelectSpeaker    |スピーカーデバイスを選びます|

### マイクデバイスの数の取得

このインターフェースは、マイクデバイスの数の取得に使われています。

####  関数のプロトタイプ  

```
public abstract int GetMicListCount()

```

####  サンプルコード  

```
ITMGContext.GetInstance().GetAudioCtrl().GetMicListCount();
```

### マイクデバイスの列挙

このインターフェースは、GetMicListCountインターフェースと連携して、マイクの列挙に使われています。

####  関数のプロトタイプ 

```
public abstract int GetMicList(out List<TMGAudioDeviceInfo> devicesInfo, int count)

```

| パラメータ          | タイプ                    | 意味                                                  |
| ---------------- | :----------------: | -------------------- |
| ppDeviceInfoList    |　TMGAudioDeviceInfo 　|　デバイスリストです|
| nCount    |　int   |　取得したマイクデバイスの数です|

| TMGAudioDeviceInfoパラメータ             |        タイプ        | 意味                 |
| ---------------- | :----------------: | ------------------- |
| m_strDeviceID | string | デバイス名|
| m_strDeviceID | string |デバイスID |

####  サンプルコード  

```
ITMGContext.GetInstance().GetAudioCtrl().GetMicList(devicesInfo,count);
```



### マイクデバイスの選択

このインターフェースは、マイクデバイスの選択に使われています。「DEVICEID_DEFAULT」をパラメータとして渡し、またはこのインターフェースを呼び出しないの場合、システムのデフォルトデバイスが選択されます。
GetMicListインターフェースで返される0番目のデバイスIDがデフォルトのデバイスであり、デバイスが選択されていない場合は通話デバイスがデフォルトのデバイスであり、選択された場合はサービス層で通話デバイスのメンテナンスを行います。この通話デバイスが抜かれた場合には、その時点での通話デバイスがデフォルトのデバイスとなり、抜かれた通話デバイスが挿入されると、その時点での通話デバイスが挿入された通話デバイスに復元します。

####  関数のプロトタイプ  

```
public abstract int SelectMic(string micID);
```

| パラメータ          | タイプ                    | 意味                                                  |
| ------ | :---: | ------------- |
| pMicID | string | マイクデバイスIDです。デバイスIDはGetMicListから返されたリストに含まれます。|

####  サンプルコード  

```
string deviceID = DEVICE_ID_DEFAULT;
                if (index != 0)
                {
                    deviceID = listMicInfo[index - 1].m_strDeviceID;
                }
                ITMGContext.GetInstance().GetAudioCtrl().SelectMic(deviceID);
                selectedMicID = deviceID;
```

このインターフェースは、スピーカーデバイスの数の取得に使われています。

####  関数のプロトタイプ  

```
public abstract int GetSpeakerListCount();

```

####  サンプルコード  

```
ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerListCount();

```

### スピーカーデバイスの列挙

このインターフェースは、GetSpeakerListCountインターフェースと連携しスピーカーデバイスの列挙に使われています。

####  関数のプロトタイプ  

```
public abstract int GetSpeakerList(out List<TMGAudioDeviceInfo> devicesInfo, int count)
```

| パラメータ          | タイプ                    | 意味                                                  |
| ---------------- | :----------------: | -------------------- |
| ppDeviceInfoList    |　TMGAudioDeviceInfo 　|　デバイスリストです|
| count           |        int         | 取得したスピーカーデバイスの数 |

| TMGAudioDeviceInfoパラメータ             |        タイプ        | 意味                 |
| ---------------- | :----------------: | ------------------- |
| m_strDeviceID | string | デバイス名|
| m_strDeviceID | string |デバイスID |

####  サンプルコード  

```
int speakerCount = ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerListCount();
Debug.LogFormat("speakerCount = {0}", speakerCount);
if (speakerCount > 0)
	{
		int ret = ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerList(out listSpeakerInfo, speakerCount);
		Debug.LogFormat("GetSpeakerList ret = {0}", ret);
		if (ret != 0)
		{
			listSpeakerInfo = null;
		}
	}
}
```

### スピーカーデバイスの選択

このインターフェースは、再生デバイスの選択に使われています。「DEVICEID_DEFAULT」をパラメータとして渡し、またはこのインターフェースを呼び出しないの場合、システムのデフォルト再生デバイスが選択されます。

####  関数のプロトタイプ  

```
public abstract int SelectSpeaker(string speaker);

```

| パラメータ          | タイプ                    | 意味                                                  |
| ---------- | :---: | ------------- |
| speaker | string | スピーカーのデバイスIDです。デバイスIDはGetSpeakerListから返されたリストに含まれます。|

####  サンプルコード  

```
speakerDropdown = transform.Find("DevicePanel/SpeakerSelect").GetComponent<Dropdown>();
        if (speakerDropdown != null)
        {
            speakerDropdown.onValueChanged.AddListener(delegate (int index)
            {
                string deviceID = DEVICE_ID_DEFAULT;
                if (index != 0)
                {
                    deviceID = listSpeakerInfo[index - 1].m_strDeviceID;
                }
                ITMGContext.GetInstance().GetAudioCtrl().SelectSpeaker(deviceID);
                selectedSpeakerID = deviceID;
            });
        }
```


## 高度なAPI

### インイヤ・モニタリングの起動

このインターフェースはインイヤーモニターを起動するために使用されます。自分の声を聞くにはEnableLoopBack+EnableSpeakerが必要です。

#### インターフェースのプロトタイプ  

```
ITMGContext GetAudioCtrl EnableLoopBack(bool enable)
```

| パラメータ   | タイプ   | 意味    |
| ------ | :--: | ------------ |
| enable    |bool    |　起動するかどうかを設定します|

####  サンプルコード  

```
ITMGContext.GetInstance().GetAudioCtrl().EnableLoopBack(true);
```

### デバイス占用とリリースイベントのコールバック

ルームで、デバイスの占用またはリリースが発生すると、このコールバックが呼び出されます、委託関数でイベントの関連情報を渡します。

```
public delegate void QAVOnDeviceStateChangedEvent(int deviceType, string deviceId, bool openOrClose);
public abstract event QAVOnDeviceStateChangedEvent OnDeviceStateChangedEvent;
```

| パラメータ          | タイプ                    | 意味                                                  |
| ----------- | :----: | ----------------------------------------------------- |
| deviceType    |int　　　　　　　　|<li>1は収集デバイス、<li>2は再生デバイスを表す   |
| deviceId    |　string |　デバイスGUIDであり、デバイスを標識することに使用されます。Windows側とMac側のみで有効です|
| openOrClose    |bool  |収集デバイス/再生デバイスを占用またはリリースします|

####  サンプルコード  

```
イベントを監視します。
ITMGContext.GetInstance().GetAudioCtrl().OnDeviceStateChangedEvent += new QAVAudioDeviceStateCallback(OnAudioDeviceStateChange);
監視処理：
void QAVAudioDeviceStateCallback(int deviceType, string deviceId, bool openOrClose){
    //デバイス占用とリリースイベント関連のコールバック処理
}
```

### ユーザールームのオーディオタイプの取得

このインターフェースはユーザールームのオーディオタイプを取得するするために使用されます、戻り値がルームのオーディオタイプです。戻り値が0であることは、ユーザールームのオーディオタイプの取得にエラーが発生したことを示します。ルームのオーディオタイプについてはEnterRoomインターフェースをご参照ください。

#### インターフェースのプロトタイプ  

```
ITMGContext ITMGRoom public  int GetRoomType()
```

####  サンプルコード  

```
ITMGContext.GetInstance().GetRoom().GetRoomType();
```

###　ルームタイプの変更

このAPIは、ユーザールームのオーディオタイプを変更するために使用されます。結果については、コールバックイベントを参照してください。イベントタイプはITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPEです。ルームのオーディオタイプは最初にルームに入った人によって決定され、その後、ルームのメンバーがルームのタイプを変更すると、そのルームのすべてのメンバーに適用されます。
#### インターフェースのプロトタイプ  

```
ITMGContext ITMGRoom public int ChangeRoomType(ITMGRoomType roomtype)
```

| パラメータ     | タイプ                                      | 意味                       |
| -------- | :----------: | ----------------------------------------------------- |
| roomtype    |　ITMGRoomType    |　切り替えたいルームタイプです。ルームのオーディオタイプについて、EnterRoomインターフェースをご参照ください|

####  サンプルコード  

```
ITMGContext.GetInstance().GetRoom().ChangeRoomType(ITMG_ROOM_TYPE_FLUENCY);
```

#### コールバックイベント

ルームのタイプを主動的に設定します、ルームタイプを設定した後、委託関数で修正完了の関連情報を渡します。

|戻ったパラメータ     | 意味  |
| ---------- | :------------------------: |
| roomtype   | 切り替え後のroomtypeタイプを返します |

```
public abstract event QAVCallback OnChangeRoomtypeCallback;
public abstract event QAVOnRoomTypeChangedEvent OnRoomTypeChangedEvent;
```

####  サンプルコード  

```
//イベントを監視します：
ITMGContext.GetInstance().OnRoomTypeChangedEvent += new QAVOnRoomTypeChangedEvent(OnRoomTypeChangedEvent);
//監視処理：
void OnRoomTypeChangedEvent(int roomtype)
{
        ShowWarnning (string.Format ("RoomTypeChanged current:{0}",roomtype));
}
```

#### ルームタイプ変更の通知

ユーザーまたはルーム内の他のユーザーは主動的にルームタイプを変更する場合、ルームタイプの変更がありましたら、ルームタイプの変更がこの通知イベントでサービス層に通知されています、戻り値はルームのタイプであり、詳細についてEnterRoomインターフェースをご参照ください。

```
public delegate void QAVOnRoomTypeChangedEvent(int roomtype);
public abstract event QAVOnRoomTypeChangedEvent OnRoomTypeChangedEvent;	
```

####  サンプルコード  

```
//イベントを監視します：
ITMGContext.GetInstance().OnRoomTypeChangedEvent += new QAVOnRoomTypeChangedEvent(OnRoomTypeChangedEvent);
//監視処理：
void OnRoomTypeChangedEvent(int roomtype){
    //ルームタイプ変更後の処理
}
```



###　ルーム通話品質監視イベント

品質監視イベント。この通知イベントは、ネットワーク品質をリッスンするために使用されます。ユーザーがネットワーク接続に問題がある場合、サービス層でUIを介してユーザーにネットワークの切り替えを通知します。入室後にトリガーされ、イベントは2秒に1回コールバックされます。イベントメッセージはITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITYで、返されるパラメータはweight、loss、およびdelayで、次の情報を表します：

| パラメータ   | タイプ   | 意味                                                         |
| ------ | ------ | ------------------------------------------------------------ |
| weight | int    | 範囲は1～50で、数値が50の場合、音質評点は優秀、数値が1の場合、音質評点は不可で、ほとんど使えません。数値が0の場合は初期値（意味なし）を示します通常、数値が30以下になると、ネットワークが悪いから、切り替えたほうがいいとユーザーに通知します。|
| loss   | double | 上りパケット損失率。|
| delay  | int    | オーディオ到達遅延時間（ms）。                                     |




### バージョン番号の取得

分析を行うためのSDKのバージョンを取得します。

#### インターフェースのプロトタイプ

```
ITMGContext  abstract string GetSDKVersion()
```

####  サンプルコード  

```
ITMGContext.GetInstance().GetSDKVersion();
```



### ログのプリントレベルの設定

プリントするログレベルの設定に使用されます。デフォルトのレベルのままにすることをお勧めします。Initの前に呼び出す必要があります。

#### インターフェースのプロトタイプ

```
ITMGContext  SetLogLevel(ITMG_LOG_LEVEL levelWrite, ITMG_LOG_LEVEL levelPrint)
```

#### パラメータの意味

| パラメータ          | タイプ                    | 意味                                                  |
| ---------- | -------------- | ------------------------------------------------------------ |
|levelWrite|ITMG_LOG_LEVEL|ログへの書き込みレベルの設定です。TMG_LOG_LEVEL_NONEは書き込まないことを示します、デフォルトはTMG_LOG_LEVEL_INFOです。|
|levelPrint|ITMG_LOG_LEVEL|ログのプリントレベルの設定です。TMG_LOG_LEVEL_NONEはプリントしないことを示します、デフォルトはTMG_LOG_LEVEL_ERRORです。|

ITMG_LOG_LEVELの説明は次のとおりです。

| ITMG_LOG_LEVEL        | 意味                 |
| --------------------- | -------------------- |
|TMG_LOG_LEVEL_NONE|ログをプリントしません|
|TMG_LOG_LEVEL_ERROR|エラーログをプリントします（デフォルト）|
|TMG_LOG_LEVEL_INFO|ヒントログをプリントします|
|TMG_LOG_LEVEL_DEBUG|開発デバッグログをプリントします|
|TMG_LOG_LEVEL_VERBOSE|高頻度ログをプリントします|

####  サンプルコード  

```
ITMGContext.GetInstance().SetLogLevel(TMG_LOG_LEVEL_INFO,TMG_LOG_LEVEL_INFO);
```



### プリントするログのパスの設定

プリントするログのパスを設定するために使用されます。デフォルトルートは次のとおりです。Initの前に呼び出す必要があります。

| フラットフォーム    | パス                                                         |
| ------- | ------------------------------------------------------------ |
| Windows | %appdata%\Tencent\GME\ProcessName                           |
| iOS    | Application/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/Documents   |
| Android | /sdcard/Android/data/xxx.xxx.xxx/files                       |
| Mac     | /Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents |

#### インターフェースのプロトタイプ

```
ITMGContext  SetLogPath(string logDir)

```

| パラメータ   | タイプ   | 意味   |
| ------ | :----: | ---- |
| logDir | String | パス |

####  サンプルコード  

```
ITMGContext.GetInstance().SetLogPath(path);

```

### 診断情報の取得

オーディオ・ビデオ通信のリアルタイム通信品質の関連情報を取得します。このインターフェースは、主にリアルタイムの通信品質の確認、問題のトラブルシューティングに使われています。セールス側としては、これを無視しても構いません。

#### インターフェースのプロトタイプ  

```
ITMGRoom GetQualityTips()
```

####  サンプルコード  

```
string tips = ITMGContext.GetInstance().GetRoom().GetQualityTips();

```
