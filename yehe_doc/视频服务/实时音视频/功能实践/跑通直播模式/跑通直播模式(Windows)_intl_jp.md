## ドキュメントガイド
ここでは主に、TRTC SDKをベースとしてビデオ・マイク接続をサポートするだけでなく、万人単位に及ぶ同時視聴をサポートするオンラインライブストリーミング機能についてご紹介します。本稿では最もよく用いられるインターフェースのみをリストアップしています。インターフェース関数に関する詳しい情報をご希望の場合、[APIドキュメント](https://intl.cloud.tencent.com/document/product/647/35119)をご参照ください。


## サンプルコード

| 属するプラットフォーム | サンプルコード |
|---------|---------|
| Windows（MFC） | [TRTCMainViewController.cpp](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/MFCDemo/TRTCMainViewController.cpp) |
| Windows（Duilib） | [TRTCMainViewController.cpp](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/DuilibDemo/TRTCMainViewController.cpp) |
| Windows（C#） | [TRTCMainForm.cs](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/CSharpDemo/TRTCMainForm.cs) |


## オンラインライブストリーミング
### 1.SDKの初期化

TRTC SDKを使用するときの最初のステップでは、まず`TRTCCloud`のシングルトンオブジェクトを取得し、SDKイベントを監視するためのコールバックを登録します。

- `ITRTCCloudCallback`イベントのコールバックインターフェースクラスを継承して、ローカルユーザーの入室/退室イベント、リモートユーザーの入室/退室イベント、エラーイベント、警告イベントなど、重要なイベントのコールバックインターフェースを書き換えます。
- `addCallback`インターフェースをコールして、SDKイベントを登録、監視します。

>`addCallback`がN回登録されている場合、SDKは同じイベントに対してコールバックをN回トリガーするので、`addCallbackを1回だけ呼び出すことをお勧めします。

C++ 版：

```c++
// TRTCMainViewController.h

// ITRTCCloudCallbackイベントのコールバックインターフェースクラスの継承
class TRTCMainViewController : public ITRTCCloudCallback
{
public:
	TRTCMainViewController();
	virtual ~TRTCMainViewController();

    virtual void onError(TXLiteAVError errCode, const char* errMsg, void* arg);
    virtual void onWarning(TXLiteAVWarning warningCode, const char* warningMsg, void* arg);
    virtual void onEnterRoom(uint64_t elapsed);
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
    //  trtcCloud インスタンスを作成
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
    
    // TRTCCloudインスタンスをリリース
	  if(m_pTRTCSDK != NULL) {
       destroyTRTCShareInstance();
        m_pTRTCSDK = null;
    }
}

// エラー通知は監視されるべきもので、、エラー通知はSDKの実行を継続できないことを意味します
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
    	//  trtcCloud インスタンスを作成
    	mTRTCCloud = ITRTCCloud.getTRTCShareInstance();
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
    		// TRTCCloudインスタンスをリリース
    		ITRTCCloud.destroyTRTCShareInstance();
    		mTRTCCloud = null;
    	}
    	...
    }
    ...
    // エラー通知は監視されるべきもので、、エラー通知はSDKの実行を継続できないことを意味します
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

### 2.TRTCParamsの組み立て

TRTCParamsは、SDKの最も重要なパラメータであり、sdkAppId、userId、userSig及びroomIdという4つの必須フィールドが含まれます。

- **SDKAppID**
Tencent CloudのTencent Real-Time Communication[コンソール](https://console.cloud.tencent.com/rav)にアクセスします。まだアプリケーションをお持ちでない場合、作成してください。SDKAppIDが表示されます。

- **userId**
  自由に指定できます。文字列型なので、直接お客様の既存のアカウントシステムとの一致を維持することができます。ただし、**同じオーディオ・ビデオルームには、同じ名前のuserIdが2つないようにご注意ください**。

- **userSig**
  userSigはuserIdをもとに算出することができます。計算方法は、[UserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

- **roomId**
  ルーム番号は数値型で、自由に指定できます。ただし、**同じアプリケーション内の2つのオーディオ・ビデオルームに、同じroomIdを割り当てることはできませんので、ご注意ください**。

### 3.キャスターのプレビューカメラ画面
TRTC SDKは、デフォルトではローカルのカメラキャプチャがオンになりません。`startLocalPreview`でローカルカメラを起動してプレビュー画面を表示することができ、`stopLocalPreview`はその機能をオフにします。

ローカルプレビューを起動する前に、`setLocalViewFillMode`を呼び出して、ビデオ表示モードを`Fill`または`Fit`モードに指定することができます。この2種類のモードでは、ビデオサイズは同じ比率のまま拡大・縮小され、次のような違いがあります。
- `Fill`モードでは、ウィンドウを確実に塗りつぶすことが優先されます。拡大・縮小されたビデオサイズと表示ウィンドウのサイズが一致しない場合、余分なビデオ部分は削除されます。
- `Fit`モードでは、すべてのビデオコンテンツを確実に表示することが優先されます。拡大・縮小されたビデオサイズと表示ウィンドウのサイズが一致しない場合、塗りつぶされていないウィンドウ領域は黒で塗りつぶされます。

C++ 版：

```c++
void TRTCMainViewController::onEnterRoom(uint64_t elapsed)
{
	// レンダリングウィンドウのハンドルを取得します。
    CWnd *pLocalVideoView = GetDlgItem(IDC_LOCAL_VIDEO_VIEW);
    HWND hwnd = pLocalVideoView->GetSafeHwnd();
    
    if(m_pTRTCSDK)
    {
        // SDKインターフェースをコールして、レンダリングモードとレンダリングウィンドウを設定します。
        m_pTRTCSDK->setLocalViewFillMode(TRTCVideoFillMode_Fit);
        m_pTRTCSDK->startLocalPreview(hwnd);
    }
    
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

### 4.キャスターによるマイク集音の起動

TRTC SDKは、デフォルトではローカルのマイク集音がオンになりません。キャスターは`startLocalAudio`を呼び出してローカルの集音を起動し、オーディオ・ビデオデータを配信することができます。`stopLocalAudio`はその機能をオフにします。`startLocalPreview`の後、続いて`startLocalAudio`を呼び出すことができます。

>`startLocalAudio`はマイクの使用権限をチェックします。マイクの権限がない場合、SDKはユーザーに起動の申請をします。

### 5.キャスターによるルームの新規作成、配信の開始

キャスターは`enterRoom`を使用してオーディオ・ビデオルームを作成することができます。パラメータ`TRTCParams`の`roomId`は、ルーム番号を指定するために使用します。同時に、`role`フィールドを`TRTCRoleAnchor`（キャスター）に指定する必要もあります。。

`appScene`パラメータは、SDKのユースケースを指定します。ここでは、`TRTCAppSceneLIVE`（オンラインライブストリーミング）を使用します。

- 作成に成功すると、SDKは`onEnterRoom`インターフェースをコールバックします。パラメータ`elapsed`は入室の所要時間を表し、単位はmsです。
- 作成に失敗すると、SDKは`onError`インターフェースをコールバックします。パラメータは、`errCode`（エラーコード `ERR_ROOM_ENTER_FAIL`、エラーコードは`TXLiteAVCode.h`を参照できます）、`errMsg`（エラー原因）、`extraInfo`（保留用パラメータ）です。

C++ 版：

```c++
// TRTCMainViewController.cpp

void TRTCMainViewController::startBroadCasting()
{
    // TRTCParams 参照用ヘッダーファイルの定義 TRTCCloudDef.h
    TRTCParams params;
    params.sdkAppId = sdkappid;
    params.userId   = userid;
    params.userSig  = usersig;
    params.roomId   = 908; // 入室したいルームを入力します
    params.role     = TRTCRoleAnchor; //キャスター
    if(m_pTRTCSDK)
    {
    	m_pTRTCSDK->enterRoom(params, TRTCAppSceneLIVE);
    }
}

void TRTCMainViewController::onError(TXLiteAVError errCode, const char* errMsg, void* arg)
{
    if(errCode == ERR_ROOM_ENTER_FAIL)
    {
        LOGE(L"onError errorCode[%d], errorInfo[%s]", errCode, UTF82Wide(errMsg).c_str());
        // userSigが有効か、ネットワークが正常かなどをチェックします
    }
}

...

void TRTCMainViewController::onEnterRoom(uint64_t elapsed)
{
    LOGI(L"onEnterRoom elapsed[%lld]", elapsed);
    
	// ローカルのビデオプレビューを起動します。以下のドキュメントを参照して、ビデオのエンコードパラメータを設定し、ローカルのカメラ画面の内容をプレビューしてください
}
```

C# 版：

```c#
// TRTCMainForm.cs

public void createRoom()
{
    // TRTCParams 参照用ヘッダーファイルの定義 TRTCCloudDef.h
    TRTCParams @params = new TRTCParams();
    @params.sdkAppId = sdkappid;
    @params.userId   = userid;
    @params.userSig  = usersig;
    @params.roomId   = 908; // 入室したいルームを入力します
    @params.role     = TRTCRoleAnchor; //キャスター
    if(mTRTCCloud != null)
    {
    	mTRTCCloud.enterRoom(@params, TRTCAppSceneLIVE);
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
    // ローカルのビデオプレビューを起動します。以下のドキュメントを参照して、ビデオのエンコードパラメータを設定し、ローカルのカメラ画面の内容をプレビューしてください
}
```

### 6.キャスターによるプライバシーモードのオン・オフ

キャスターはライブストリーミング中、プライバシーを保護するために、ローカルのオーディオ・ビデオデータをブロックしたい場合が出てきます。このような場合、`muteLocalVideo`を呼び出せばローカルのビデオ収集をブロックでき、`muteLocalAudio`を呼び出せばローカルのオーディオ収集をブロックできます。

### 7.視聴者が入室して視聴

視聴者は`enterRoom`を呼び出すことでオーディオ・ビデオルームに入室することができます。パラメータTRTCParamsの`roomId` は、ルーム番号を指定するために使用されます。
`appScene`は、同様に`TRTCAppSceneLIVE`（オンラインライブストリーミング）にも入力しますが、`role` フィールドは`TRTCRoleAudience`（視聴者）と指定する必要があります。

C++ 版：

```c++

void TRTCMainViewController::startPlaying()
{
    // TRTCParams 参照用ヘッダーファイルの定義 TRTCCloudDef.h
    TRTCParams params;
    params.sdkAppId = sdkappid;
    params.userId   = userid;
    params.userSig  = usersig;
    params.roomId   = 908; // 入室したいルームを入力します
    params.role     = TRTCRoleAudience; //視聴者
    if(m_pTRTCSDK)
    {
    	m_pTRTCSDK->enterRoom(params, TRTCAppSceneLIVE);
    }
}
```

C# 版：

```c#
public void startPlaying()
{
    // TRTCParams 参照用ヘッダーファイルの定義 TRTCCloudDef.h
    TRTCParams @params = new TRTCParams();
    @params.sdkAppId = sdkappid;
    @params.userId   = userid;
    @params.userSig  = usersig;
    @params.roomId   = 908; // 入室したいルームを入力します
    @params.role     = TRTCRoleAudience; //視聴者
    if(mTRTCCloud != null)
    {
    	mTRTCCloud.enterRoom(@params, TRTCAppSceneLIVE);
    }
}
```

キャスターがルーム内にいる場合、視聴者は TRTCCloudDelegateの`onUserVideoAvailable`コールバックを介してキャスターのuseridを取得します。次に、視聴者が `startRemoteView`メソッドを呼び出すと、キャスターのビデオ画面が表示されます。

`setRemoteViewFillMode`を介して、ビデオ表示モードを` Fill`または`Fit`モードに指定することができます。この2種類のモードでは、ビデオサイズは同じ比率のまま拡大・縮小され、次のような違いがあります。
- `Fill`モードでは、ウィンドウを確実に塗りつぶすことが優先されます。拡大・縮小されたビデオサイズと表示ウィンドウのサイズが一致しない場合、余分なビデオ部分は削除されます。
- `Fit`モードでは、すべてのビデオコンテンツを確実に表示することが優先されます。拡大・縮小されたビデオサイズと表示ウィンドウのサイズが一致しない場合、塗りつぶされていないウィンドウ領域は黒で塗りつぶされます。

C++ 版：

```c++
void TRTCMainViewController::onUserVideoAvailable(const char* userId, bool available){
    if (available) {
        // レンダリングウィンドウのハンドルを取得します。
        CWnd *pRemoteVideoView = GetDlgItem(IDC_REMOTE_VIDEO_VIEW);
        HWND hwnd = pRemoteVideoView->GetSafeHwnd();  
        
        // リモートユーザーのビデオのレンダリングモードを設定します。
        m_pTRTCSDK->setRemoteViewFillMode(TRTCVideoFillMode_Fill);
        // SDKインターフェースを呼び出して、リモートユーザーストリームを再生します。
        m_pTRTCSDK->startRemoteView(userId， hwnd);
    } else {
        m_pTRTCSDK->stopRemoteView(userId);
    }    
}
```

C# 版：

```c#
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

>TRTCAppSceneLIVEモードでは、同じルームにいる視聴者(TRTCRoleAudience)人数に制限はありません。

### 8.視聴者とキャスターとのマイク接続
キャスターと視聴者のいずれも、TRTCCloudが提供する`switchRole`を介して、ロールを相互に切り替えることができます。最もよくあるのは、視聴者とキャスターとのマイク接続シナリオです。視聴者はこのインターフェースを通じて「アシスタントキャスター」に切り替わった上で、ルーム内のもとの「メインキャスター」と双方向のマイク接続を行うことができます。

### 9.ルームからの退出
`exitRoom`メソッドを呼び出してルームを退出します。通話中か否かにかかわらず、このメソッドを呼び出すと、ビデオ通話に関するすべてのリソースがリリースされます。`exitRoom`をコールした後、SDKは複雑な退室ハンドシェイクフローに進みます。SDKが`onExitRoom`メソッドをコールバックすると、リソースのリリースが完全に終了します。

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

}
```

C# 版：

```c#
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
```
