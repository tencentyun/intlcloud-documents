## ドキュメントガイド
ここでは主に、TRTC SDKをベースとしてビデオ・マイク接続をサポートするだけでなく、万人単位に及ぶ同時視聴をサポートするオンラインライブストリーミング機能についてご紹介します。本稿では最もよく用いられるインターフェースのみをリストアップしています。インターフェース関数に関する詳しい情報をご希望の場合、[APIドキュメント](https://intl.cloud.tencent.com/document/product/647/35119)をご参照ください。


## サンプルコード

| 属するプラットフォーム | サンプルコード |
|---------|---------|
| Windows（MFC） | [TRTCMainViewController.cpp](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/MFCDemo/TRTCMainViewController.cpp) |
| Windows（Duilib） | [TRTCMainViewController.cpp](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/DuilibDemo/TRTCMainViewController.cpp) |
| Windows(C#) | [TRTCMainForm.cs](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/CSharpDemo/TRTCMainForm.cs) |


## オンラインライブストリーミング
### 1. SDKの初期化

TRTC SDKを使用するときの最初のステップでは、まず`TRTCCloud`のシングルトンオブジェクトを取得し、SDKイベントを監視するためのコールバックを登録します。

- `ITRTCCloudCallback`イベントのコールバックインターフェースクラスを継承して、ローカルユーザーの入室/退室イベント、リモートユーザーの入室/退室イベント、エラーイベント、警告イベントなど、重要なイベントのコールバックインターフェースを書き換えます。
- `addCallback`インターフェースをコールして、SDKイベントを登録、監視します。

>!`addCallback`でN回登録すると、同一イベントに対して、SDKがN回コールバックします。`addCallback`を1回のみ呼び出すことをお勧めします。

<dx-codeblock>
::: C++版 C++
// TRTCMainViewController.h

// ITRTCCloudCallbackのイベントコールバックインターフェースクラスを継承します
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
::: C#版 C#
// TRTCMainForm.cs

// ITRTCCloudCallbackのイベントコールバックインターフェースクラスを継承します
public partial class TRTCMainForm : Form, ITRTCCloudCallback, ITRTCLogCallback
{
	...
	private ITRTCCloud mTRTCCloud; 
	...
	
	public TRTCMainForm(TRTCLoginForm loginForm)
	{
		InitializeComponent();
		this.Disposed += new EventHandler(OnDisposed);
		// TRTCCloud インスタンスの作成
		mTRTCCloud = ITRTCCloud.getTRTCShareInstance();
		// SDK イベントコールバックの登録
		mTRTCCloud.addCallback(this);
		...
	}
	
	private void OnDisposed(object sender, EventArgs e)
	{
		if (mTRTCCloud != null)
		{
			// SDK イベントのモニタリング のキャンセル
			mTRTCCloud.removeCallback(this);
			// TRTCCloud インスタンスのリリース
			ITRTCCloud.destroyTRTCShareInstance();
			mTRTCCloud = null;
		}
		...
	}
	...
	// エラー通知はモニタリングする必要があります。エラー通知は、SDKの実行を継続できないことを意味します
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

TRTCParamsは、SDKの最も重要なパラメータであり、sdkAppId、userId、userSig、roomIdという4つの入力必須フィールドが含まれます。

- **SDKAppID**
Tencent Cloud TRTC [コンソール](https://console.cloud.tencent.com/rav)に入ります。アプリケーションがない場合は、作成してください。作成するとSDKAppIDが確認できます。

- **userId**
  自由に指定することができ、文字列タイプのため、お客様の既存のアカウント体系と同じのものにすることが可能です。但し、**同じ音声/ビデオルームには2つの同名の userIdが存在できません**ので、ご注意ください。

- **userSig**
  SDKAppIDとuserIdを基に、userSigを計算できます。計算方法については、[UserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

- **roomId**
  ルーム番号は数字タイプであり、自由に指定できますが、**同一のアプリケーション内の2つのオーディオビデオルームに同じroomIdを割り当てることはできません**ので、ご注意ください。文字列形式のルーム番号を使用したい場合は、TRTCParamsのstrRoomIdをご使用ください。

### 3.キャスターのプレビューカメラ画面
TRTC SDK は、デフォルトではローカルのWebカメラの撮影が有効になっていません。`startLocalPreview` でローカルのWebカメラをオンにしてプレビュー画面を表示でき、`stopLocalPreview`でこれをオフにします。

ローカルプレビューを起動する前に、`setLocalViewFillMode`を呼び出して、ビデオ表示モードを`Fill`または`Fit`モードに指定することができます。この2種類のモードでは、ビデオサイズは同じ比率のまま拡大・縮小され、次のような違いがあります。
- `Fill`モードでは、ウィンドウを確実に塗りつぶすことが優先されます。拡大・縮小されたビデオサイズと表示ウィンドウのサイズが一致しない場合、余分なビデオ部分は削除されます。
- `Fit`モードでは、すべてのビデオコンテンツを確実に表示することが優先されます。拡大・縮小されたビデオサイズと表示ウィンドウのサイズが一致しない場合、塗りつぶされていないウィンドウ領域は黒で塗りつぶされます。

<dx-codeblock>
::: C++版 C++
void TRTCMainViewController::onEnterRoom(uint64_t elapsed)
{
	// レンダリングウィンドウのハンドルを取得します。
    CWnd *pLocalVideoView = GetDlgItem(IDC_LOCAL_VIDEO_VIEW);
    HWND hwnd = pLocalVideoView->GetSafeHwnd();
    
    if(m_pTRTCSDK)
    {
        // SDKインターフェースを呼び出し、レンダリングモードおよびレンダリングウィンドウを設定します。
        m_pTRTCSDK->setLocalViewFillMode(TRTCVideoFillMode_Fit);
        m_pTRTCSDK->startLocalPreview(hwnd);
    }

}
:::
::: C#版 C#
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

### 4.キャスターによるマイク集音の起動

TRTC SDKは、デフォルトではローカルのマイク集音がオンになりません。キャスターは`startLocalAudio`を呼び出してローカルの集音を起動し、オーディオビデオデータを配信することができます。`stopLocalAudio`はその機能をオフにします。`startLocalPreview`の後、続いて`startLocalAudio`を呼び出すことができます。

>?`startLocalAudio`はマイクの使用権限をチェックします。マイクの権限がない場合、SDKはユーザーに起動の申請をします。

### 5.キャスターによるルームの新規作成、配信の開始

キャスターは`enterRoom`を使用してオーディオビデオルームを作成することができます。パラメータ`TRTCParams`の`roomId`は、ルーム番号を指定するために使用します。同時に、`role`フィールドを`TRTCRoleAnchor`（キャスター）に指定する必要もあります。

`appScene`パラメータは、SDKのユースケースを指定します。ここでは、`TRTCAppSceneLIVE`（オンラインライブストリーミング）を使用します。

- 作成に成功すると、SDKは`onEnterRoom`インターフェースをコールバックします。パラメータ`elapsed`は入室の所要時間を表し、単位はmsです。
- 作成に失敗すると、SDKは`onError`インターフェースをコールバックします。パラメータは、`errCode`（エラーコード `ERR_ROOM_ENTER_FAIL`、エラーコードは`TXLiteAVCode.h`を参照できます）、`errMsg`（エラー原因）、`extraInfo`（保留用パラメータ）です。

<dx-codeblock>
::: C++版 C++
// TRTCMainViewController.cpp

void TRTCMainViewController::startBroadCasting()
{
    // TRTCParamsの定義はヘッダーファイル TRTCCloudDef.hを参照
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
        // userSigが合法か、ネットワークが正常かなどをチェックします
    }
}

...

void TRTCMainViewController::onEnterRoom(uint64_t elapsed)
{
    LOGI(L"onEnterRoom elapsed[%lld]", elapsed);
    
	// ローカルのビデオプレビューを起動します。以下のドキュメントを参照して、ビデオコーデックパラメータを設定し、ローカルのカメラ画面の内容をプレビューしてください
}
:::
::: C#版 C#
// TRTCMainForm.cs

public void createRoom()
{
    // TRTCParamsの定義はヘッダーファイルTRTCCloudDef.hを参照
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
        // userSigが合法か、ネットワークが正常かなどをチェックします
    }
}

...

public void onEnterRoom(int result)
{
    // ローカルのビデオプレビューを起動します。以下のドキュメントを参照して、ビデオコーデックパラメータを設定し、ローカルのカメラ画面の内容をプレビューしてください
}
:::
</dx-codeblock>

### 6.キャスターによるプライバシーモードのオン・オフ

キャスターはライブストリーミング中、プライバシーを保護するために、ローカルのオーディオビデオデータをブロックしたい場合が出てきます。このような場合、`muteLocalVideo`を呼び出せばローカルのビデオ収集をブロックでき、`muteLocalAudio`を呼び出せばローカルのオーディオ収集をブロックできます。

### 7.視聴者が入室して視聴

視聴者は`enterRoom`を呼び出すことでオーディオビデオルームに入室することができます。パラメータTRTCParamsの`roomId`は、ルームナンバーを指定するために使用されます。
`appScene`は、同様に`TRTCAppSceneLIVE`（オンラインライブストリーミング）にも入力しますが、`role`フィールドは`TRTCRoleAudience`（視聴者）と指定する必要があります。

<dx-codeblock>
::: C++版 C++
void TRTCMainViewController::startPlaying()
{
    // TRTCParamsの定義はヘッダーファイル TRTCCloudDef.hを参照
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
:::
::: C#版 C#
public void startPlaying()
{
    // TRTCParamsの定義はヘッダーファイルTRTCCloudDef.hを参照
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
:::
</dx-codeblock>

キャスターがルーム内にいる場合、視聴者はTRTCCloudDelegateの`onUserVideoAvailable`コールバックを介してキャスターのuseridを取得します。次に、視聴者が`startRemoteView`メソッドを呼び出すと、キャスターのビデオ画面が表示されます。

`setRemoteViewFillMode`によって、ビデオ表示モードを `Fill` または `Fit` モードに指定することができます。この2種類のモードはビデオサイズはいずれも同じ比率で拡大縮小します。違いは以下のとおりです。
- `Fill`モード：ビューウィンドウが全てコンテンツで埋まることを優先的に保証します。拡大縮小後のビデオサイズがビューウィンドウのサイズと一致しない場合、はみ出たビデオの部分はカットされます。
- `Fit`モード：ビデオのコンテンツが全て表示されることを優先的に保証します。拡大縮小後のビデオサイズがビューウィンドウのサイズと一致しない場合、欠けているウィンドウエリアは黒色で補填されます。

<dx-codeblock>
::: C++版 C++
void TRTCMainViewController::onUserVideoAvailable(const char* userId, bool available){
    if (available)  {
        // レンダリングウィンドウのハンドルを取得します。
        CWnd *pRemoteVideoView = GetDlgItem(IDC_REMOTE_VIDEO_VIEW);
        HWND hwnd = pRemoteVideoView->GetSafeHwnd();  
        
        // リモートユーザーのビデオのレンダリングモードを設定します。
        m_pTRTCSDK->setRemoteViewFillMode(TRTCVideoFillMode_Fill);
        // SDK インターフェースを呼び出し、リモートユーザーのストリーミングを再生します。
        m_pTRTCSDK->startRemoteView(userId、 hwnd);
    }else{
        m_pTRTCSDK->stopRemoteView(userId);
    }    
}
:::
::: C#版 C#
public void onUserVideoAvailable(string userId, bool available)
{
    if (available)
	{
		// ウィンドウのハンドルを取得します
		IntPtr ptr = GetHandleAndSetUserId(pos, userId, false);
		SetVisableInfoView(pos, false);
		// リモートユーザーのビデオのレンダリングモードを設定します。
		mTRTCCloud.setRemoteViewFillMode(userId, TRTCVideoFillMode.TRTCVideoFillMode_Fit);
		// SDK インターフェースを呼び出し、リモートユーザーのストリーミングを再生します。
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

>!
>- TRTCAppSceneLIVEモードでは、同じルームにいる視聴者(TRTCRoleAudience)人数に制限はありません。
>- 各端末のユースケースappSceneについては、統一する必要があります。統一していない場合、想定外のトラブルが生じる恐れがあります。

### 8.視聴者とキャスターとのマイク接続
キャスターと視聴者のいずれも、TRTCCloudが提供する`switchRole`を介して、ロールを相互に切り替えることができます。最もよくあるのは、視聴者とキャスターとのマイク接続シナリオです。視聴者はこのインターフェースを通じて「アシスタントキャスター」に切り替わった上で、ルーム内のもとの「メインキャスター」と双方向のマイク接続を行うことができます。

### 9. ルームからの退出
`exitRoom`メソッドを呼び出してルームを退出します。通話中か否かにかかわらず、このメソッドを呼び出すと、ビデオ通話に関するすべてのリソースがリリースされます。`exitRoom`をコールした後、SDKは複雑な退室ハンドシェイクフローに進みます。SDKが`onExitRoom`メソッドをコールバックすると、リソースのリリースが完全に終了します。

<dx-codeblock>
::: C++版 C++
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
	// 退出に成功、reason パラメータは保留され、現在使用されていません。

}
:::
::: C#版 C#
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
    // 退出に成功
    ...
}
:::
</dx-codeblock>
