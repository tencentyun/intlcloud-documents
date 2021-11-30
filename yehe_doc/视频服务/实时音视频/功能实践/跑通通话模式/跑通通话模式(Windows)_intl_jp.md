## ドキュメントガイド
このドキュメントでは、主にTRTC SDKをベースに簡単なビデオ通話機能を実現する方法を紹介します。ここでは最もよく使われるインターフェースを幾つかリストアップしただけですので、より多くのインターフェース関数を理解したい場合は、[API ドキュメント](https://intl.cloud.tencent.com/document/product/647/35119)をご参照ください。


## サンプルコード

| 属するプラットフォーム | サンプルコード |
|---------|---------|
| Windows（MFC） | [TRTCMainViewController.cpp](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/MFCDemo/TRTCMainViewController.cpp) |
| Windows(Duilib) | [TRTCMainViewController.cpp](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/DuilibDemo/TRTCMainViewController.cpp) |
| Windows(C#) | [TRTCMainForm.cs](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/CSharpDemo/TRTCMainForm.cs) |

## ビデオ通話
### 1. SDKの初期化
TRTC SDKを使用する第1ステップは、`getTRTCShareInstance`エクスポートインターフェースによって、 `TRTCCloud`シングルインスタンスのオブジェクトポインタ `ITRTCCloud*`を取得し、SDKのイベントをモニタリングするコールバックを登録することです。

- `ITRTCCloudCallback`のイベントコールバックインターフェースクラスを継承し、キーとなるイベントのコールバックインターフェースをリライトします。これには、ローカルユーザーの入室/退室イベント、リモートユーザーの参加/退出イベント、エラーイベント、アラームイベントなどが含まれます。
- `addCallback`インターフェースを呼び出して、SDKのイベントの監視を登録します。

>!`addCallback`でN回登録すると、同一イベントに対して、SDKがN回コールバックします、`addCallback`を1回のみ呼び出すことをお勧めします。

<dx-codeblock>
::: C++ C++
// TRTCMainViewController.h

// ITRTCCloudCallbackのイベントコールバックインターフェースクラスを継承します
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
    virtual void onRemoteUserLeaveRoom(const char* userId, int reason);
    virtual void onUserVideoAvailable(const char* userId, bool available);
    virtual void onUserAudioAvailable(const char* userId, bool available);
...
private:
	ITRTCCloud * m_pTRTCSDK = NULL；
...
}

// TRTCMainViewController.cpp

TRTCMainViewController::TRTCMainViewController()
{
    // TRTCCloud インスタンスの作成
    m_pTRTCSDK = getTRTCShareInstance();
    
    // SDK イベントコールバックの登録
    m_pTRTCSDK->addCallback(this);
}

TRTCMainViewController::~TRTCMainViewController()
{
    // SDK イベントのモニタリング のキャンセル
    if(m_pTRTCSDK) {
        m_pTRTCSDK->removeCallback(this);
    }
    
    // TRTCCloud インスタンスのリリース
      if(m_pTRTCSDK != NULL) {
       destroyTRTCShareInstance();
        m_pTRTCSDK = null;
    }
}

// エラー通知はモニタリングする必要があります。エラー通知は、SDKの実行を継続できないことを意味します
virtual void TRTCMainViewController::onError(TXLiteAVError errCode, const char* errMsg, void* arg)
{
    if (errCode == ERR_ROOM_ENTER_FAIL) {
        LOGE(L"onError errorCode[%d], errorInfo[%s]", errCode, UTF82Wide(errMsg).c_str());
		    exitRoom();
	 }
}
:::
::: C# C#
// TRTCMainForm.cs

// ITRTCCloudCallback イベントコールバックインターフェースクラスを継承します
public partial class TRTCMainForm : Form, ITRTCCloudCallback, ITRTCLogCallback
{
	...
	private ITRTCCloud mTRTCCloud; 
	...
	
	public TRTCMainForm(TRTCLoginForm loginForm)
	{
		InitializeComponent();
		this.Disposed += new EventHandler(OnDisposed);
		// TRTCCloudインスタンスを作成
		mTRTCCloud = ITRTCCloud.getTRTCShareInstance();
		// SDKコールバックイベントを登録
		mTRTCCloud.addCallback(this);
		...
	}
	
	private void OnDisposed(object sender, EventArgs e)
	{
		if (mTRTCCloud != null)
		{
			// SDKイベントモニタリングのキャンセル
			mTRTCCloud.removeCallback(this);
			// TRTCCloudインスタンスをリリース
			ITRTCCloud.destroyTRTCShareInstance();
			mTRTCCloud = null;
		}
		...
	}
	...
	//  エラー通知はモニタリングする必要があります。エラー通知は、SDKの実行を継続できないことを意味します
	public void onError(TXLiteAVError errCode, string errMsg, IntPtr arg)
	{
	     if (errCode == TXLiteAVError.ERR_ROOM_ENTER_FAIL) {
		    exitRoom();
		}
	     ...
	}
	...
}
:::
</dx-codeblock>

### 2. TRTCParamsの組み立て

TRTCParams は SDK で最も重要なパラメータであり、SDKAppID、userId、userSig 、roomIdの4つの記入必須のフィールドがあります。

- **SDKAppID**
  Tencent CloudのTencent Real-Time Communication[コンソール](https://console.cloud.tencent.com/rav)にアクセスします。まだアプリケーションをお持ちでない場合、作成してください。SDKAppIDが表示されます。
  
- **userId**
  自由に指定することができ、文字列タイプのため、お客様の既存のアカウント体系と同じのものにすることが可能です。但し、**同じ音声/ビデオルームには2つの同名の userIdが存在できません**ので、ご注意ください。

- **userSig**
  SDKAppIDとuserIdを基に、userSigを計算できます。計算方法については、[UserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

- **roomId**
  ルームナンバーは数字タイプとなり、自由に指定できます。但し、**同じアプリケーション内の2つの音声/ビデオルームに、同じroomIdをアサインすることはできません**ので、ご注意ください。文字列形式のルームナンバーを使用したい場合は、TRTCParamsのstrRoomIdをご使用ください。

### 3. ルームへの入室（または作成）
`enterRoom` を呼び出し、 TRTCParams パラメータの中の roomIdが指定する音声/ビデオルームに参加できます。該当するルームが存在しない場合、SDK は roomId をルームナンバーとする新しいルームを自動作成します。

**appScene** パラメータは、SDK のユースケースを指定します。ここでは、`TRTCAppSceneVideoCall`（ビデオ通話）を使用しますが、このシナリオにおいては、SDK 内部のコーディックおよびネットワークコンポーネントは、映像のスムーズさをより重視し、通話のディレーとラグ率を低減させるものとなっています。
				
- 入室に成功すると、SDKが`onEnterRoom` インターフェースのコールバックを行います。パラメータ：`result`が0を上回る時は、入室に成功し、数値は入室に要した時間を表しています（単位はミリ秒（ms））。`result`が0を下回る時は、入室に失敗し、数値は入室失敗のエラーコードを表しています。
- 入室に失敗した場合、SDK は同時に `onError` インターフェースをコールバックします。パラメータは、`errCode`（エラーコード：`ERR_ROOM_ENTER_FAIL`、エラーコードは `TXLiteAVCode.h`を参照のこと）、`errMsg`（エラー原因）、`extraInfo`（保留パラメータ）です。
- すでに特定のルームにいる場合は、まず`exitRoom`を呼び出して現在のルームを退出すると、もう一つのルームに入ることができるようになります。 

<dx-codeblock>
::: C++ C++
// TRTCMainViewController.cpp

void TRTCMainViewController::enterRoom()
{
    // TRTCParamsの定義はヘッダーファイル TRTCCloudDef.hを参照
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
    if(errCode == ERR_ROOM_ENTER_FAIL)
    {
        LOGE(L"onError errorCode[%d], errorInfo[%s]", errCode, UTF82Wide(errMsg).c_str());
        // userSigが合法か、ネットワークが正常かなどをチェックします
    }
}

...

void TRTCMainViewController::onEnterRoom(int result)
{
    LOGI(L"onEnterRoom result[%d]", result);
    if(result >= 0)
	{
		//入室に成功 
	}
	else
	{
		//入室失敗、エラーコード = result；
	}
}
:::
::: C# C#
// TRTCMainForm.cs

public void EnterRoom()
{
    // TRTCParamsの定義はヘッダーファイルTRTCCloudDef.hを参照
    TRTCParams @params = new TRTCParams();
    @params.sdkAppId = sdkappid;
    @params.userId   = userid;
    @params.userSig  = usersig;
    @params.roomId   = 908; // 入室したいルームを入力します
    if(mTRTCCloud != null)
    {
    	mTRTCCloud.enterRoom(@params, TRTCAppSceneVideoCall);
    }
}

...
    
public void onError(TXLiteAVError errCode, string errMsg, IntPtr arg)
{
    if(errCode == TXLiteAVError.ERR_ROOM_ENTER_FAIL)
    {
        Log.E(String.Format("errCode : {0}, errMsg : {1}, arg = {2}", errCode, errMsg, arg));
        // userSigが合法であるか、ネットワークが正常かなどをチェックします
    }
}

...

public void onEnterRoom(int result)
{
    if(result >= 0)
	{
		//入室に成功 
	}
	else
	{
		//入室失敗、エラーコード = result；
	}
}
:::
</dx-codeblock>


>!
>- ユースケースに基づき適切なsceneパラメータを選択してください。誤った選択をすると、ラグ率または画面の解像度が想定のレベルに到達しなくなります。
>- 各端末のユースケースappSceneについては、統一する必要があります。統一していない場合、想定外のトラブルが生じる恐れがあります。

### 4. リモート側オーディオストリームの視聴
TRTC SDKは、デフォルトの状態でリモートの音声ストリームを受信するようになっています。このため追加コードを作成する必要はありません。特定の useridの音声ストリームを受信したくない場合は、 `muteRemoteAudio`を使用し、ミュートにすることができます。

### 5. リモートビデオストリームの視聴

TRTC SDKは、デフォルトの状態ではリモートのビデオストリームをプルしません。ルーム内のユーザーに上りビデオデータがあるときに、ルーム内の他のユーザーは、ITRTCCloudCallbackの中の`onUserVideoAvailable` のコールバックによって当該ユーザーのuseridを取得できます。その後、`startRemoteView`のメソッドを呼び出せば当該ユーザーのビデオ画面を表示できます。

`setRemoteViewFillMode`によって、ビデオ表示モードを `Fill` または `Fit` モードに指定することができます。この2種類のモードはビデオサイズはいずれも同じ比率で拡大縮小します。違いは以下のとおりです。
- `Fill`モード：ビューウィンドウが全てコンテンツで埋まることを優先的に保証します。拡大縮小後のビデオサイズがビューウィンドウのサイズと一致しない場合、はみ出たビデオの部分はカットされます。
- `Fit`モードでは、すべてのビデオコンテンツを確実に表示することが優先されます。拡大・縮小されたビデオサイズと表示ウィンドウのサイズが一致しない場合、塗りつぶされていないウィンドウ領域は黒で塗りつぶされます。

<dx-codeblock>
::: C++ C++
// TRTCMainViewController.cpp
void TRTCMainViewController::onUserVideoAvailable(const char* userId, bool available){
    if (available) {
        // レンダリングウィンドウのハンドルを取得します。
        CWnd *pRemoteVideoView = GetDlgItem(IDC_REMOTE_VIDEO_VIEW);
        HWND hwnd = pRemoteVideoView->GetSafeHwnd();  
        
        // リモートユーザーのビデオのレンダリングモードを設定します。
        m_pTRTCSDK->setRemoteViewFillMode(TRTCVideoFillMode_Fill);
        // SDK インターフェースを呼び出し、リモートユーザーのストリーミングを再生します。
        m_pTRTCSDK->startRemoteView(userId、 hwnd);
    } else {
        m_pTRTCSDK->stopRemoteView(userId);
    }    
}
:::
::: C# C#
// TRTCMainForm.cs
public void onUserVideoAvailable(string userId, bool available)
{
    if (available)
	{
		// ウィンドウのハンドルを取得します
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
:::
</dx-codeblock>


### 6. ローカル集音のオン/オフ

TRTC SDKは、デフォルトではローカルのマイクによる集音がオンになっていません。`startLocalAudio`で、ローカルの集音をオンにして音声ビデオデータを発信することができ、`stopLocalAudio`でこれをオフにします。
>?`startLocalPreview`の後に引き続き`startLocalAudio`を呼び出すことができます。

### 7. ローカルビデオ撮影のオン/オフ

TRTC SDK は、デフォルトではローカルのWebカメラの撮影が有効になっていません。`startLocalPreview` でローカルのWebカメラをオンにしてプレビュー画面を表示でき、`stopLocalPreview`でこれをオフにします。

- `startLocalPreview`を呼び出して、ローカルビデオのレンダリングウィンドウを指定します。**SDKがウィンドウのサイズをダイナミックに検出して、`rendHwnd` が表示する全てのウィンドウでレンダリングを行います**。
-  `setLocalViewFillMode`インターフェースを呼び出し、ローカルのビデオレンダリングモードを `Fill` または `Fit`に設定します。2種類のモードは、ビデオサイズはいずれも同じ比率で拡大縮小します。違いは次のとおりです。 
  - `Fill`  モード：ウィンドウ全てにコンテンツを表示することを優先的に保証します。拡大縮小後のビデオサイズがビューウィンドウのサイズと一致しない場合、はみ出た部分はカットされます。
  - `Fit`モードでは、すべてのビデオコンテンツを確実に表示することが優先されます。拡大・縮小されたビデオサイズとウィンドウのサイズが一致しない場合、塗りつぶされていないウィンドウ領域は黒で塗りつぶされます。

<dx-codeblock>
::: C++ C++
// TRTCMainViewController.cpp

void TRTCMainViewController::onEnterRoom(uint64_t elapsed)
{
    ...
    
	// レンダリングウィンドウのハンドルを取得します。
	CWnd *pLocalVideoView = GetDlgItem(IDC_LOCAL_VIDEO_VIEW);
	HWND hwnd = pLocalVideoView->GetSafeHwnd();
	
	if(m_pTRTCSDK)
	{
	    // SDKインターフェースを呼び出し、レンダリングモードおよびレンダリングウィンドウを設定します。
	    m_pTRTCSDK->setLocalViewFillMode(TRTCVideoFillMode_Fit);
	    m_pTRTCSDK->startLocalPreview(hwnd);
	}
	
	...
}
:::
::: C# C#
// TRTCMainForm.cs

public void onEnterRoom(int result)
{
	...
	// レンダリングウィンドウのハンドルを取得します。
	IntPtr ptr = GetHandle();
    if (mTRTCCloud != null)
    {
        // SDKインターフェースを呼び出し、レンダリングモードおよびレンダリングウィンドウを設定します。
        mTRTCCloud.setLocalViewFillMode(TRTCVideoFillMode_Fit);
        mTRTCCloud.startLocalPreview(ptr);
    }
	...
}
:::
</dx-codeblock>


### 8. オーディオ・ビデオデータストリームの遮断

- **ローカルビデオデータの遮断**
  ユーザーが通話の途中に、プライバシーを守る目的で、ローカルのビデオデータを隠したい場合は、`muteLocalVideo`を呼び出して、一時的に、ルーム内の他のユーザーが当該ユーザーの画面を視聴できなくすることができます。
  
- **ローカル音声データの遮断**
  ユーザーが通話の途中に、プライバシーを守る目的で、ローカルの音声データを遮断したい場合は、 `muteLocalAudio`を呼び出して、一時的に、ルーム内の他のユーザーに当該ユーザーの音声を聞こえなくすることができます。
  
- **リモートビデオデータの遮断**
  `stopRemoteView`によって特定の userid のビデオデータを遮断することができます。
  `stopAllRemoteView`によって全てのリモートユーザーのビデオデータを遮断することができます。
  
- **リモート音声データの遮断**
  `muteRemoteAudio` によって特定のuseridの音声データを遮断することができます。
  `muteAllRemoteAudio`によって全てのリモートユーザーの音声データを遮断することができます。

### 9. ルームからの退出

`exitRoom`メソッドを呼び出してルームを退出します。通話中かどうかにかかわらず、このメソッドを呼び出せば、ビデオ通話に関するすべてのリソースがリリースされます。
>?`exitRoom`を呼び出した後、SDKは複雑な退室のハンドシェイクのプロセスに進みます。SDKが`onExitRoom`メソッドをコールバックした時に、リソースのリリースが完了します。
<dx-codeblock>
::: C++ C++
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
:::
::: C# C#
// TRTCMainForm.cs

public void OnExit()
{
    if(mTRTCCloud != null)
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
:::
</dx-codeblock>

