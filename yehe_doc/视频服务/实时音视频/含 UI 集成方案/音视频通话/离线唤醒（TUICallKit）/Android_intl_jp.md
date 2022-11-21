オフライン通知機能は、アプリケーションが「バックエンドで実行中」または「オフライン状態」の場合でも、オーディオビデオ通話の着信を受信できる機能です。TUICallKitはTUIOfflinePushコンポーネントを統合することでオフライン通知機能を実現しています。ここでは、オーディオビデオ通話プロジェクトで`TUIOfflinePush`コンポーネントを統合する方法についてご説明します。

## 事前準備

1. **アプリケーションをメーカーのプッシュプラットフォームに登録する** オフラインプッシュ機能はメーカーオリジナルのチャネルに依存します。ご自身のアプリケーションを各メーカーのプッシュプラットフォームに登録し、APPIDおよびAPPKEYなどのパラメータを取得する必要があります。

>! **次の2つのファイルはこの後の手順で使用します**
>- Huaweiプラットフォームに登録する場合は、`agconnect-services.json`ファイルをダウンロードして保存します。
>- Googleプラットフォームに登録する場合は、`google-services.json`ファイルをダウンロードして保存します。
> | Google FCM                                                   |
   > | ------------------------------------------------------------ |
   > | ![img](https://qcloudimg.tencent-cloud.cn/raw/aa734c4d4a8c1c2580b964360ad66304.png) |


2. **IMコンソールで設定を行う** 

メーカーのチャネルに登録するにはご自身のパッケージ名を渡す必要があります。メッセージの相互運用のため、各メーカーで入力するパッケージ名は一致させる必要があります。生成したID、APPIDおよびAPPKEYを記録します。これらはこの後の手順で使用します。 



## ステップ1：コンポーネントのダウンロードとインポート

1. [Github](https://github.com/tencentyun/TUICalling)でコードをクローン/ダウンロードした後、下図のように、Androidディレクトリ下のtuiofflinepushサブディレクトリを現在のプロジェクトのappの同階層のディレクトリにコピーします。

![img](https://qcloudimg.tencent-cloud.cn/raw/8ce4eb830c8880f523e3aa833150c864.png)﻿﻿

2. プロジェクトのルートディレクトリ下で`setting.gradle`ファイルを見つけ、その中に次のコードを追加します。

```java
include ':tuiofflinepush'
```

3. appディレクトリ下で`build.gradle`ファイルを見つけ、その中に次のコードを追加します。その役割は、現在のappの新たに追加したtuiofflinepushコンポーネントへの依存を宣言するものです。

```java
api project(':tuiofflinepush')
```

## ステップ2：プロジェクト設定の完了

1. appディレクトリ下で`build.gradle`ファイルを見つけ、アプリケーションパッケージ名をご自身のパッケージ名に変更します。

```java
applicationId 'com.****.trtc'
```

2. appディレクトリ下で`build.gradle`ファイルを見つけ、`ViVo`アクセスパラメータの`VIVO_APPKEY`、`VIVO_APPID`および`HONOR_APPID`を設定し、コンパイルまたは実行エラーを避けます。

```java
manifestPlaceholders = [
    "VIVO_APPKEY": "PLACEHOLDER", 
    "VIVO_APPID" : "PLACEHOLDER",
    "HONOR_APPID": "PLACEHOLDER"
]
```

3. **Huawei**および**Google**ファイルの設定： appディレクトリ下で`google-services.json`ファイルを置き換えます。このファイルは[事前準備](https://www.tencentcloud.com/document/product/647/50999#.E5.89.8D.E6.9C.9F.E5.87.86.E5.A4.87)でGoogleプラットフォームに登録した際に保存したファイルです。 appディレクトリ下に`agconnect-services.json`ファイルを追加します。このファイルは[事前準備](https://www.tencentcloud.com/document/product/647/50999#.E5.89.8D.E6.9C.9F.E5.87.86.E5.A4.87)でHuaweiプラットフォームに登録した際に保存したファイルです。

4. [事前準備](https://www.tencentcloud.com/document/product/647/50999#.E5.89.8D.E6.9C.9F.E5.87.86.E5.A4.87)で記録したID、APPID、APPKEYを`PrivateConstants`ファイルに入力し、パラメータの設定が正しいかどうかを確認します。**入力するパラメータは次のとおりです**。

```java
public class PrivateConstants {
    /****** Xiaomiオフラインプッシュパラメータstart ******/
    // Tencent Cloudコンソールで、サードパーティの証明書プッシュ後に割り当てられた証明書IDをアップロードします
    public static final long XM_PUSH_BUZID = アプリケーションが割り当てた証明書ID;
    // Xiaomiオープンプラットフォームが割り当てたアプリケーションAPPIDおよびAPPKEY
    public static final String XM_PUSH_APPID = "アプリケーションが割り当てたAPPID";
    public static final String XM_PUSH_APPKEY = "アプリケーションが割り当てたAPPKEY";
    /****** Xiaomiオフラインプッシュパラメータend ******/
}
```

>! この手順は非常に重要です。パラメータが正しく設定されているかどうかをよく確認してください。

 上記の手順が完了すると、プロジェクトに`TUICallKit`のオフライン通知機能が実装されます。

## ステップ3：オフライン通知内容のカスタマイズ

TUICallKitはデフォルトの通知スタイルを提供していますが、通知内容をカスタマイズしたい場合は、[OfflinePushInfoConfig.java](https://github.com/tencentyun/TUICallKit/blob/main/Android/tuicallkit/src/main/java/com/tencent/qcloud/tuikit/tuicallkit/config/OfflinePushInfoConfig.java)ファイルを変更してください。

```java
public static TUIOfflinePushInfo createOfflinePushInfo(Context context) {    
    TUIOfflinePushInfo pushInfo = new TUIOfflinePushInfo();    
    pushInfo.setTitle("mike");    
    pushInfo.setDesc("You have receive a new call");    
    // OPPOはChannelIDを設定するとプッシュメッセージを受信することができます。このchannelIDはコンソールと一致している必要があります    
    // OPPO must set a ChannelID to receive push messages. This channelID needs to be the same as the console.    
    pushInfo.setAndroidOPPOChannelID("tuikit");    
    pushInfo.setIgnoreIOSBadge(false);    
    pushInfo.setIOSSound("phone_ringing.mp3");  
    return pushInfo;
}
```

## よくあるご質問

オフラインプッシュ通知が受信できない場合は、お調べしますので[お問い合わせ](https://intl.cloud.tencent.com/contact-us)ください。

### 1、通知が受信できない

メーカーのコンソールを使用してプッシュテストを行い、成功した場合はメーカーのチャネルに問題がないことがわかります。さらにTUIOfflinePushコンソールのメーカーパラメータ設定が正しいかどうかを確認し、要件に従って入力します。（テストの結果、vivo x9はコンソールでメッセージのカテゴリーを設定する必要があります）。

一部のスマートフォンでは通知が「重要でない通知」に入ることがあります。ステータスバーをプルダウンし、「重要でない通知」に分類されていないかを確認してください。

TUIOfflinePushの登録が正常に行われているかどうかを確認します。次のログをフィルタリングします。

```java
TUIOfflinePush
```

### 2、画面ロック時にディスプレイが点灯しない

Androidスマートフォンはメーカーとプラットフォームの制限により、画面ロック状態での必要な権限が異なります。状況に応じて以下のトラブルシューティングを行ってください。

**メーカーのロック画面通知権限がオンになっているかを確認する** 一部のメーカーではルールの統一化を行っています。例えばXiaomiではロック画面中のオフライン通知到着時にディスプレイが点灯しない場合、**設定** > **ロック画面**で、**ロック画面中の通知受信時にディスプレイを点灯**スイッチをクリックしてオンにします。

**アプリケーションのロック画面通知権限がオンになっているかを確認する** 例：Xiaomiではロック画面表示権限が必要です。

>? この問題が起こった場合は互換性の処理が必要です。TencentのQQグループ（592465424）に参加すると、問い合わせとフィードバックを行うことができます。

### 3、オフラインプッシュ通知をクリックしても通話画面が開かない

通話リクエストが見つかるかどうかを確認する必要があります。次のログをフィルタリングできます。

```java
onReceiveNewInvitation
```

### 4、アプリケーションがバックエンドにあるとき、通話画面をフロントエンドに自動的にプルできない

**アプリケーションをバックエンドからフロントエンドに自動的にプルする場合、Appが「バックエンド自動起動」または「フローティングウィンドウ」権限を有効にしているかどうかを確認する必要があります。**

メーカーが異なる場合や、同じメーカーであってもAndroidのバージョンが異なる場合は、アプリケーションに許可する権限や権限名が一致しないことがありますのでご注意ください。例えば、Xiaomi 6では**バックエンドの画面ポップアップ**権限を有効にすればよいだけですが、Redmiでは**バックエンドの画面ポップアップ**と**フローティングウィンドウの表示**の権限を同時に有効にする必要があります。

>? 手動ですべての権限を有効化しても、通話画面のフロントエンドへの自動プルができないことをテスト中に発見した場合は、互換性の処理が必要です。
