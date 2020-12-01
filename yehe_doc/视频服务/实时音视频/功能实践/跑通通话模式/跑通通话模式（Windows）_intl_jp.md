## ドキュメントガイド
ここでは主に、 TRTC SDK をベースとして簡単なビデオ通話機能を実現する方法についてご紹介します。本稿では最もよく用いられるインターフェースのみをリストアップしています。インターフェース関数に関する詳しい情報をご希望の場合、 [APIドキュメント](https://intl.cloud.tencent.com/document/product/647/35119)をご参照ください。


## サンプルコード

| 属するプラットフォーム | サンプルコード |
|---------|---------|
| Windows（MFC） | [TRTCMainViewController.cpp](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/MFCDemo/TRTCMainViewController.cpp) |
| Windows（Duilib） | [TRTCMainViewController.cpp](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/DuilibDemo/TRTCMainViewController.cpp) |
| Windows（C#） | [TRTCMainForm.cpp](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/CSharpDemo/TRTCMainForm.cs) |

## ビデオ通話
### 1. SDKの初期化
TRTC SDK を使用する第1ステップとして、始めに`getTRTCShareInstance` エクスポートインターフェースによって、 `TRTCCloud` のシングルインスタンスオブジェクトの `ITRTCCloud*`ポインタを取得し、 SDK イベントをモニターするコールバックを登録します。

- `ITRTCCloudCallback`イベントのコールバックインターフェースクラスを継承して、ローカルユーザーの入室/退室イベント、リモートユーザーの入室/退室イベント、エラーイベント、警告イベントなど、重要なイベントのコールバックインターフェースを書き換えます。
- `addCallback`インターフェースをコールして、SDKイベントを登録、監視します。

>!`addCallback`がN回登録されている場合、SDKは同じイベントに対してコールバックをN回トリガーするので、`addCallbackを1回だけ呼び出すことをお勧めします。

C++ 版：

```c++
// TRTCMainViewController.h

// ITRTCCloudCallbackイベントコールバックインターフェースクラスを継承します
class TRTCMainViewController : public ITRTCCloudCallback
{
public:
	TRTCMainViewController();
	virtual ~TRTCMainViewController();

    virtual void onError(TXLiteAVError errCode, const char* errMsg, void* arg);
    virtual void onWarning(TXLiteAVWarning warningCode, const char* warningMsg, void* arg);
    virtual void onEnterRoom(int result);
    virtual void onExitRoom(int reason);
    virtual void onRemoteUserEnterRoom(const char* userId);
    virtual void onRemoteUserLeaveRoom(const char* userId,int reason);
    virtual void onUserVideoAvailable(const char* userId, boo1 available);
    virtual void onUserAudioAvailable(const char* userId, boo1 available);
...
private:
	ITRTCCloud * m_pTRTCSDK = NULL；
...
}

// TRTCMainViewController.cpp

TRTCMainViewController::TRTCMainViewController()
{
    //  TRTCCloud インスタンスを作成
    m_pTRTCSDK = getTRTCShareInstance();
    
    // SDKコールバックイベントを登録
    m_pTRTCSDK->addCallback(this);
}

TRTCMainViewController::~TRTCMainViewController()
{
    // SDKイベントの監視をキャンセル
    if(m_pTRTCSDK) {
        m_pTRTCSDK->removeCallback(this);
    }
    
    //  TRTCCloud インスタンスをリリース
	  if(m_pTRTCSDK != NULL) {
       destroyTRTCShareInstance();
        m_pTRTCSDK = null;
    }
}

// エラー通知は監視されるべきもので、エラー通知はSDKの実行を継続できないことを意味します
virtual void TRTCMainViewController::onError(TXLiteAVError errCode, const char* errMsg, void* arg)
{
    if (errCode == ERR_ROOM_ENTER_FAIL) {
        LOGE(L"onError errorCode[%d], errorInfo[%s]", errCode, UTF82Wide(errMsg).c_str());
		    exitRoom();
	 }
}
```

C# 版：

```c#
// TRTCMainForm.cs

// ITRTCCloudCallbackイベントコールバックインターフェースクラスを継承します
public partial class TRTCMainForm : Form, ITRTCCloudCallback, ITRTCLogCallback
{
	...
	private ITRTCCloud mTRTCCloud; 
	...
	
	public TRTCMainForm(TRTCLoginForm loginForm)
    {
    	InitializeComponent();
    	this.Disposed += new EventHandler(OnDisposed);
    	//  TRTCCloud インスタンスを作成
    	mTRTCCloud = lTRTCCloud.getTRTCShareInstance();
    	// SDKコールバックイベントを登録
    	mTRTCCloud.addCallback(this);
    	...
    }
    
    private void OnDisposed(object sender, EventArgs e)
    {
    	if (mTRTCCloud != null)
    	{
    		// SDKイベントの監視をキャンセル
    		mTRTCCloud.removeCallback(this);
    		//  TRTCCloud インスタンスをリリース
    		ITRTCCloud.destroyTRTCShareInstance();
    		mTRTCCloud = null;
    	}
    	...
    }
    ...
    // エラー通知は監視されるべきもので、エラー通知はSDKの実行を継続できないことを意味します
    public void onError(TXLiteAVError errCode, string errMsg, IntPtr arg)
    {
         if (errCode == TXLiteAVError.ERR_ROOM_ENTER_FAIL) {
		    exitRoom();
		}
         ...
    }
    ...
}
```

### 2.  TRTCParamsの組み立て

TRTCParamsは、SDKの最も重要なパラメータであり、sdkAppId、userId、userSig及びroomIdという4つの必須フィールドが含まれます。

- **SDKAppID**
  Tencent CloudのTencent Real-Time Communication[コンソール](https://console.cloud.tencent.com/rav)にアクセスします。まだアプリケーションをお持ちでない場合、作成してください。SDKAppIDが表示されます。
  
- **userId**
  自由に指定できます。文字列型なので、直接お客様の既存のアカウントシステムとの一致を維持することができます。ただし、**同じオーディオ・ビデオルームには、同じ名前のuserIdが2つないようにご注意ください**。

- **userSig**
  userSigはuserIdをもとに算出することができます。計算方法は、[UserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

- **roomId**
  ルーム番号は数値型で、自由に指定できます。ただし、**同じアプリケーション内の2つのオーディオ・ビデオルームに、同じroomIdを割り当てることはできませんので、ご注意ください**。

### 3. ルームへの入室（または作成）
 `enterRoom` をコールして、 TRTCParams パラメータの roomId で指定されたオーディオ・ビデオルームに参加できます。そのルームが存在しない場合は、SDK は roomId をルームナンバーとする新しいルームを自動的に作成します。

**appScene** パラメータは、SDK のユースケースを指定します。このドキュメントでは、 `TRTCAppSceneVideoCall`（ビデオ通話）を使用して、そのユースケースにおいて、 SDK 内部コーデック及びネットワークコンポーネントが、ビデオの流暢さをより重視して、通話遅延とラグ率を低下させます。
				
- 入室に成功した場合、SDK は `onEnterRoom` インターフェースをコールバックします。パラメータ： `result`が0より大きいときは入室成功で、数値はルーム入室にかかった時間を示します。単位はミリ秒（ms）です。 `result`が0より小さいときは、入室失敗で、数値は入室失敗のエラーコードを示します。
- 入室に失敗した場合、SDK は同時に `onError` インターフェースをコールバックします。パラメータは、`errCode`（エラーコードは `ERR_ROOM_ENTER_FAIL`、エラーコードは `TXLiteAVCode.h`を参照できます）、`errMsg`（エラー原因）、`extraInfo`（保留パラメータ）です。
>- 既にルームにいる場合は、 `exitRoom` の方法をコールして現在のルームを退出すると、次のルームに入ることができるようになります。 

C++ 版：

```c++
// TRTCMainViewController.cpp

void TRTCMainViewController::enterRoom()
{
    // TRTCParams 参照用ヘッダーファイルの定義 TRTCCloudDef.h
    TRTCParams params;
    params.sdkAppId = sdkappid;
    params.userId   = userid;
    params.userSig  = usersig;
    params.roomId   = 908; // 入室したいルームを入力します
    if(m_pTRTCSDK) 
    {
    	m_pTRTCSDK->enterRoom(params, TRTCAppSceneVideoCall);
    }
}

...
    
void TRTCMainViewController::onError(TXLiteAVError errCode, const char* errMsg, void* arg)
{
    if (errCode == ERR_ROOM_ENTER_FAIL) 
    {
        LOGE(L"onError errorCode[%d], errorInfo[%s]", errCode, UTF82Wide(errMsg).c_str());
        // userSigが合法であるか、ネットワークが正常かなどをチェックします
    }
}

...

void TRTCMainViewController::onEnterRoom(int result)
{
    LOGI(L"onEnterRoom result[%d]", result);
    if (result >= 0) 
	{
		//入室に成功
	}
	else
	{
		//入室に失敗。エラーコード = result；
	}
}
```

C# 版：

```c#
// TRTCMainForm.cs

public void EnterRoom() 
{
    // TRTCParams 参照用ヘッダーファイルの定義 TRTCCloudDef.h
    TRTCParams @params = new TRTCParams();
    @params.sdkAppId = sdkappid;
    @params.userId   = userid;
    @params.userSig  = usersig;
    @params.roomId   = 908; // 入室したいルームを入力します
    if (mTRTCCloud != null)
    {
    	mTRTCCloud.enterRoom(@params, TRTCAppSceneVideoCall);
    }
}

...
    
public void onError(TXLiteAVError errCode, string errMsg, IntPtr arg)
{
    if (errCode == TXLiteAVError.ERR_ROOM_ENTER_FAIL) 
    {
        Log.E(String.Format("errCode : {0}, errMsg : {1}, arg = {2}", errCode, errMsg, arg));
        // userSigが合法であるか、ネットワークが正常かなどをチェックします
    }
}

...

public void onEnterRoom(int result) 
{
    if (result >= 0) 
	{
		//入室に成功
	}
	else
	{
		//入室に失敗。エラーコード = result；
	}
}
```

2. ユースケースに基づき適切な　scene　パラメータを設定してください。誤った選択をすると、ラグ率または画面の解像度が想定のレベルに到達しなくなります。

### 4. リモートオーディオストリームの視聴
TRTC SDK は、デフォルトではリモートのオーディオストリームを受信します。このために追加でコードを作成する必要はありません。特定の userid のオーディオストリームを聴きたくない場合は、 `muteRemoteAudio` を使用してミュートにすることができます。

### 5. リモートビデオストリーミングの視聴

TRTC SDK は、デフォルトではリモートのビデオストリーミングをプルすることはありません。ルーム内でユーザーのアップストリーミングビデオデータがある場合、ルーム内のその他のユーザーは ITRTCCloudCallback の `onUserVideoAvailable` コールバックによって、そのユーザーの userid。 を取得でき、 `startRemoteView` メソッドをコールしてそのユーザーのビデオ画面を表示することができます。

`setRemoteViewFillMode`を介して、ビデオ表示モードを` Fill`または`Fit`モードに指定することができます。この2種類のモードでは、ビデオサイズは同じ比率のまま拡大・縮小され、次のような違いがあります。
- `Fill`モードでは、ウィンドウを確実に塗りつぶすことが優先されます。拡大・縮小されたビデオサイズと表示ウィンドウのサイズが一致しない場合、余分なビデオ部分は削除されます。
- `Fit`モードでは、すべてのビデオコンテンツを確実に表示することが優先されます。拡大・縮小されたビデオサイズと表示ウィンドウのサイズが一致しない場合、塗りつぶされていないウィンドウ領域は黒で塗りつぶされます。

C++ 版：

```c++
// TRTCMainViewController.cpp
void TRTCMainViewController::onUserVideoAvailable(const char* userId, bool available){
    if (available) {
        // レンダリングウィンドウのハンドルを取得します。
        CWnd *pRemoteVideoView = GetDlgItem(IDC_REMOTE_VIDEO_VIEW);
        HWND hwnd = pRemoteVideoView->GetSafeHwnd();  
        
        // リモートユーザーのビデオのレンダリングモードを設定します。
        m_pTRTCSDK->setRemoteViewFillMode(TRTCVideoFillMode_Fill);
        // SDKインターフェースを呼び出して、リモートユーザーストリームを再生します。
        m_pTRTCSDK->startRemoteView(userId， hwnd);
    }else{
        m_pTRTCSDK->stopRemoteView(userId);
    }    
}
```

C# 版：

```c#
// TRTCMainForm.cs
public void onUserVideoAvailable(string userId, bool available)
{
    if (available) 
	{
		// ウィンドウのハンドルを取得します。
		IntPtr ptr = GetHandleAndSetUserId(pos, userId, false);
		SetVisableInfoView(pos, false);
		// リモートユーザーのビデオのレンダリングモードを設定します。
		mTRTCCloud.setRemoteViewFillMode(userId, TRTCVideoFillMode.TRTCVideoFillMode_Fit);
		// SDKインターフェースを呼び出して、リモートユーザーストリームを再生します。
		mTRTCCloud.startRemoteView(userId, ptr);
	}
	else
	{
		mTRTCCloud.stopRemoteView(userId);
		...
	}
}
```

### 6. ローカル音声集音スイッチ

TRTC SDK は、デフォルトではローカルのマイクによる集音を有効にしません。`startLocalAudio` は、ローカルの集音を有効にして、音声ビデオデータを放送します。`stopLocalAudio` はそれを停止します。
>? `startLocalPreview` の後に引き続き `startLocalAudio`をコールすることができます。

### 7. ローカルビデオ収録スイッチ

TRTC SDKは、デフォルトではローカルのカメラキャプチャがオンになりません。`startLocalPreview`でローカルカメラを起動してプレビュー画面を表示することができ、`stopLocalPreview`はその機能をオフにします。

-  `startLocalPreview`をコールして、ローカルビデオのレンダリングウィンドウを指定します。**SDK はウィンドウのサイズを動的に検出し、 `rendHwnd` で表示されるウィンドウ全体をレンダリングします**。
-  `setLocalViewFillMode` インターフェースをコールして、ローカルのビデオレンダリングモードを `Fill` または `Fit`に設定します。2種類のモードでは、ビデオサイズはみな同じ比率で拡大縮小します。違いは次のとおりです。
  - `Fill`モードでは、ウィンドウを確実に塗りつぶすことが優先されます。拡大・縮小されたビデオサイズとウィンドウのサイズが一致しない場合、余分な部分は削除されます。
  - `Fit`モードでは、すべてのビデオコンテンツを確実に表示することが優先されます。拡大・縮小されたビデオサイズと表示ウィンドウのサイズが一致しない場合、塗りつぶされていないウィンドウ領域は黒で塗りつぶされます。

C++ 版：

```c++
// TRTCMainViewController.cpp

void TRTCMainViewController::onEnterRoom(uint64_t elapsed)
{
    ...
    
	// レンダリングウィンドウのハンドルを取得します。
    CWnd *pLocalVideoView = GetDlgItem(IDC_LOCAL_VIDEO_VIEW);
    HWND hwnd = pLocalVideoView->GetSafeHwnd();
    
    if(m_pTRTCSDK) 
    {
        // SDKインターフェースをコールして、レンダリングモードとレンダリングウィンドウを設定します。
        m_pTRTCSDK->setLocalViewFillMode(TRTCVideoFillMode_Fit);
        m_pTRTCSDK->startLocalPreview(hwnd);
    }
    
	...
}
```

C# 版：

```c#
// TRTCMainForm.cs

public void onEnterRoom(int result) 
{
	...
	// レンダリングウィンドウのハンドルを取得します。
	IntPtr ptr = GetHandle();
    if (mTRTCCloud != null)
    {
        // SDKインターフェースをコールして、レンダリングモードとレンダリングウィンドウを設定します。
        mTRTCCloud.setLocalViewFillMode(TRTCVideoFillMode_Fit);
        mTRTCCloud.startLocalPreview(ptr);
    }
	...
}
```

### 8. 音声ビデオデータストリーミングのブロック

- **ローカルビデオデータのブロック**
  ユーザーが通話の途中に個人的な目的からローカルのビデオデータのブロックを希望し、ルーム内のその他のユーザーに対し一時的に当該ユーザーの画面を閲覧できなくさせる場合は、 `muteLocalVideo`をコールすることができます。
  
- **ローカル音声データのブロック**
  ユーザーが通話の途中に個人的な目的からローカルの音声データのブロックを希望し、ルーム内のその他のユーザーに対し一時的に当該ユーザーの音声をミュートさせる場合は、 `muteLocalAudio`をコールすることができます。
  
- **リモートビデオデータのブロック**
   `stopRemoteView` によって、特定の userid のビデオデータをブロックすることができます。
   `stopAllRemoteView` によって、すべてのリモートユーザーのビデオデータをブロックすることができます。
  
- **リモート音声データのブロック**
   `muteRemoteAudio` によって、特定の userid の音声データをブロックすることができます。
   `muteAllRemoteAudio` によって、すべてのリモートユーザーの音声データをブロックすることができます。

### 9.ルームからの退出

 `exitRoom` のメソッドをコールして退室します。現在まだ通話中かどうかに関わらず、このメソッドをコールすると、ビデオ通話に関するすべてのリソースをリリースします。
>? `exitRoom` をコール後、SDK は複雑な退室のハンドシェイクフローに入ります。SDK が `onExitRoom` メソッドをコールバックするとき、リソースのリリースが実際に完了したものとみなします。

C++ 版：

```c++
// TRTCMainViewController.cpp

void TRTCMainViewController::exitRoom()
{
    if(m_pTRTCSDK) 
    {
    	m_pTRTCSDK->exitRoom();
    }
}
....
void TRTCMainViewController::onExitRoom(int reason)
{
	// 退室に成功しました。reasonパラメータは保留され、まだ使用されていません。

    ...
}
```

C# 版：

```c#
// TRTCMainForm.cs

public void OnExit()
{
    if (mTRTCCloud != null)
    {
    	mTRTCCloud.exitRoom();
    }
}
...
public void onExitRoom(int reason) 
{
    // 退室に成功しました
    ...
}
```

