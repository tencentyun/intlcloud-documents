## 機能説明
IM SDKを初期化した後、SDKログインインターフェースを呼び出して、アカウントのIDを確認し、アカウントの機能を使用する権限を取得する必要があります。メッセージ、セッションなどの機能は、IM SDKへのログインに成功して初めて正常に使用できます。

<dx-alert infotype="notice" title="">
ログインインターフェースを呼び出した直後に、セッションを取得したインターフェースのみを呼び出すことができます。他の機能のインターフェースは、SDKへのログインに成功した後にのみ呼び出すことができます。したがって、他の機能を使用する前に、**必ずログインし、ログインに成功したことを確認してください**。そうでない場合、機能が異常または使用できない可能性があります。
</dx-alert>


## ログイン
初めてIMアカウントにログインする場合、最初にアカウントを登録する必要はありません。ログインに成功すると、IMはこのアカウントの登録を自動的に完了します。
`login`([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/login.html)) インターフェースを呼び出して、ログインできます。

`login`インターフェースのキーパラメータは次のとおりです：

| パラメータ | 意味                       | 説明                                                         |
| ---------- | -------------------------- | ------------------------------------------------------------ |
| UserID     | ログインユーザーの固有識別 | 大文字と小文字の英字（a-z、A-Z）、数字（0-9）、アンダースコア（_）およびハイフン（-)のみを含めることをお勧めします。長さは32バイトを超えることはできません。 |
| UserSig    | ログインチケット           | セキュリティのために業務サーバーによって計算されます。計算方法については、[UserSig 后台 API](https://intl.cloud.tencent.com/document/product/1047/34385)をご参照ください。 |

次のシナリオでは、`login`インターフェースを呼び出す必要があります：
* App起動後、初めてIM SDK機能を使用する場合。
* ログイン時にチケットの有効期限が切れる場合：`login`インターフェースのコールバックは`ERR_USER_SIG_EXPIRED（6206）`または`ERR_SVR_ACCOUNT_USERSIG_EXPIRED（70001）`エラーコードが返されます。この場合は、新しいuserSigを生成し、再度ログインしてください。
* オンライン時にチケットの有効期限が切れる場合：ユーザーがオンライン時に`onUserSigExpired`([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Class/Listener/V2TimSDKListener.html?h=onUserSigExpired))コールバックを受信することもできます。この場合は、新しいuserSigを生成し、再度ログインする必要があります。
* オンライン時にオフラインでキックされる：ユーザーがオンライン中にキックされ、IM SDKは`onKickedOffline`([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Class/Listener/V2TimSDKListener.html?h=onKickedOffline))コールバックを通じて通知します。この場合は、UIでユーザーにプロンプトを表示し、`login`を呼び出して再度ログインすることができます。

次のシナリオでは、`login`インターフェースを呼び出す必要はありません。
* ユーザーのネットワークが切断され、再接続された後、`login`関数を呼び出す必要はなく、IM SDKは自動的にオンラインになります。
* ログインプロセスが進行中の場合、繰り返しログインを実行する必要はありません。

>?
>1. IM SDKインターフェースを呼び出してログインに成功すると、DAUの計算が開始されます。過剰なDAUを避けるために、サービスケースに従って適切にログインインターフェースを呼び出してください。
>2. Appでは、IM SDKは複数のアカウントが同時にオンラインになることをサポートしません。複数のアカウントが同時にログインした場合、最後にログインしたアカウントのみがオンラインになります。

サンプルコードは次のとおりです：[](id:login_code)


```dart
String userID = "your user id";
String userSig = "userSig from your server";
V2TimCallback res = await TencentImSDKPlugin.v2TIMManager.login(userID: userID, userSig: userSig);
if(res.code == 0){
	// ログインに成功するロジック
}else{
 	// ログインに失敗するロジック
}
```


### ログインユーザーの取得

ログインに成功すると、`getLoginUser`([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/getLoginUser.html))を呼び出して、ログインユーザーUserIDを取得します。
ログインに失敗する場合は、取得したログインユーザーUserIDは空になります。

サンプルコードは次のとおりです：


```dart
    // ユーザーがログインに成功した後に呼び出すことができます
    // getLoginUserを呼び出して、ログインに成功したユーザーUserIDを取得します
    V2TimValueCallback<String> getLoginUserRes =
        await TencentImSDKPlugin.v2TIMManager.getLoginUser();
    if (getLoginUserRes.code == 0) {
      //取得に成功
      getLoginUserRes.data; // getLoginUserRes.dataはクエリーされたログインユーザーUserIDです
    }
```



### ログイン状態の取得

`getLoginStatus`([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/getLoginStatus.html))を呼び出して、ログイン状態を取得します。ユーザーがすでにログインしているか、ログイン中の場合は、ログインインターフェースを頻繁に呼び出してログインしないでください。IM SDKでサポートされているログイン状態を次の表に示します。

| ログイン状態              | 意味               |
| ------------------------- | ------------------ |
| V2TIM_STATUS_LOGINED (1)  | ログインしている   |
| V2TIM_STATUS_LOGINING (2) | ログイン中         |
| V2TIM_STATUS_LOGOUT (3)   | ログインしていない |

サンプルコードは次のとおりです。


```dart
    // ユーザーがログインに成功した後に呼び出すことができます
    // getLoginStatusを呼び出して、ログインに成功したユーザー状態を取得します
    V2TimValueCallback<int> getLoginStatusRes =
        await TencentImSDKPlugin.v2TIMManager.getLoginStatus();
    if (getLoginStatusRes.code == 0) {
      int? status = getLoginStatusRes.data; // getLoginStatusRes.dataはユーザーのログイン状態の値です
      if (status == 1) {
        // ログインしている
      } else if (status == 2) {
        // ログイン中
      } else if (status == 3) {
        // ログインしていない
      }
    }
```



## 多端末ログインと相互キック
Tencent CloudコンソールでIM SDKの多端末ログインポリシーを設定することができます。
多端末ログイン戦略には、「モバイルまたはデスクトッププラットフォームで1つのプラットフォームをオンラインにすることができる + Webで同時にオンラインにすることができる」、「異なるプラットフォームを同時にオンラインにすることができる」など、多くのオプションがあります。
関連する構成については、[ログイン設定](https://intl.cloud.tencent.com/document/product/1047/34419)をご参照ください。

Tencent Cloudコンソールで同じプラットフォームにログインできるIM SDKインスタンスの数を構成できます。つまり、同じプラットフォームのデバイスは同時に複数のオンラインをサポートできます。
この機能はUltimate Editionでのみ使用できます。現在、Web上で同時にオンラインにできる最大数は10です。Android、iPhone、iPad、Windows、Mac（Flutterは実際のコンパイル結果に依存します）プラットフォームで、同時にオンラインにできるデバイスの最大数は3です。
関連する構成については、[ログイン設定](https://intl.cloud.tencent.com/document/product/1047/34419)をご参照ください。

`login`([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/login.html))インターフェースを呼び出すとき、同じアカウントの多端末ログインポリシーが制限を超えた場合、新しくログインしたインスタンスは、以前にログインしたインスタンスをオフラインにします。
オフラインにキックされた側は、`onKickedOffline`([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Class/Listener/V2TimSDKListener.html?h=onKickedOffline))コールバックを受信します。


## ログアウト
通常の状況では、アプリケーションのライフサイクルがIM SDKのライフサイクルと一致している場合、アプリケーションを終了する前にログアウトする必要はなく、直接終了するだけで済みます。
ただし、一部の特別なシナリオ、たとえば、特定のインターフェースに入った後にのみIM SDKを使用し、インターフェースを終了した後は使用しなくなる場合では、`logout`([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/logout.html))インターフェースを呼び出して、SDKからログアウトすることができます。ログアウトに成功すると、他のユーザーからの新しいメッセージは受信されなくなります。この場合、ログアウトに成功した後、`unInitSDK`([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/unInitSDK.html))を呼び出して、SDKの未初期化を実行する必要があることに注意してください。

サンプルコードは次のとおりです：


```dart
V2TimCallback logoutRes = await TencentImSDKPlugin.v2TIMManager.logout();
if(logoutRes.code == 0){

}
```


## アカウントの切り替え
アプリケーションでアカウント切り替えのニーズを実現したい場合は、アカウントを切り替えるたびに、`login`([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/login.html))を呼び出すだけで済みます。

たとえば、すでにaliceにログインし、bobに切り替えたい場合は、直接login bobだけで済みます。[login](#login_code) bobの前に、logout aliceを明示式に呼び出す必要はなく、IM SDK内部で自動的に処理します。
