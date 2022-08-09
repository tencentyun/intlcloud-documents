[](id:toc)
ここでは、Flutter SDKの統合方法についてご説明します。

## 環境要件

|   | バージョン |
|---------|---------|
| Flutter | IM SDKの最低要件はFlutter 2.2.0バージョン、TUIKit統合コンポーネントリポジトリの最低要件はFlutter 2.10.0バージョンです。|
|Android|Android Studio 3.5以降のバージョン。Appの要件はAndroid 4.1以降のバージョンのデバイスです。|
|iOS|Xcode 11.0以降のバージョン。プロジェクトに有効な開発者署名を設定済みであることを確認してください。|

## 前提条件

1. [Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)を行い、[実名認証](https://intl.cloud.tencent.com/document/product/378/3629)が完了していること。
2. [アプリケーションの作成とアップグレード](https://intl.cloud.tencent.com/document/product/1047/34577)を参照してアプリケーションを作成し、`SDKAppID`を記録していること。

[](id:part1)

## その1：テストユーザーの作成

[IMコンソール](https://console.cloud.tencent.com/im)でご自分のアプリケーションを選択し、左側ナビゲーションバーで**支援ツール**->**UserSig生成&検証**の順にクリックし、2つのUserIDおよびそれに対応するUserSigを作成します。`UserID`、`署名（Key）`、`UserSig`の3つをコピーし、その後のログインで使用します。

>? このアカウントは開発テストのみに使用します。アプリケーションのリリース前の`UserSig`の正しい発行方法は、サーバーで生成し、Appのインターフェース向けに提供する方法となります。`UserSig`が必要なときは、Appから業務サーバーにリクエストを送信し動的に`UserSig`を取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/1047/34385)をご参照ください。

![](https://main.qcloudimg.com/raw/2286644d987d24caf565142ae30c4392.png)

[](id:part2)

## その2：適切な方法を選択してFlutter SDKを統合


IMは3種類の統合方法を提供しており、最適な方法を選択して統合を行うことができます。

|   | 適用ケース |
|---------|---------|
| [DEMOの使用](#part3) | IM Demoは完全なチャットAppであり、コードはオープンソース化されています。チャットライクなユースケースを実装したい場合は、Demoを使用して二次開発を行うことができます。今すぐ[Demo体験](https://intl.cloud.tencent.com/document/product/1047/34279)が可能です。 |
| [UIを含む統合](#part4) | IMのUIコンポーネントリポジトリ`TUIKit`は、セッションリスト、チャットインターフェース、連絡先リストなどの共通のUIコンポーネントを提供しています。開発者は実際の業務ニーズに応じて、このコンポーネントリポジトリによってカスタムIMアプリケーションをスピーディーにビルドすることができます。**この方法を優先して用いることを推奨します**。 |
| [UI統合を自身で実装](#part5) | アプリケーションインターフェースのニーズがTUIKitでは満たせない場合、または多くのカスタマイズが必要な場合は、この方法を用いることができます。 |


IM SDKの各APIについてより深くご理解いただけるよう、各APIの呼び出しおよび監視のトリガーのデモンストレーションを行う[ API Example](https://github.com/TencentCloud/TIMSDK/tree/master/Flutter/IMSDK/im-flutter-plugin/tencent_im_sdk_plugin/example)もご提供しています。


[](id:part3)

## その3：Demoの使用

### Demoクイックスタート

1. Demoソースコードのダウンロード、依存のインストール：
```shell
#コードをcloneします
git clone https://github.com/TencentCloud/TIMSDK.git

#flutterのdemoディレクトリに進みます
cd TIMSDK/Flutter/Demo/im-flutter-uikit

#依存のインストール
flutter pub get
```

2. Demoプロジェクトの実行：
```shell
#demoプロジェクトを起動します。SDK_APPID、KEYの2つのパラメータを置き換えてください
flutter run --dart-define=SDK_APPID={YOUR_SDKAPPID} --dart-define=ISPRODUCT_ENV=false --dart-define=KEY={YOUR_KEY}
```

>?
>
>- `--dart-define=SDK_APPID={YOUR_SDKAPPID}`の中の`{YOUR_SDKAPPID}`をご自分のアプリケーションのSDKAppIDに置き換える必要があります。
>- `--dart-define=ISPRODUCT_ENV=false`は開発環境か本番環境かを判断します。開発環境の場合、falseとしてください。
>- `--dart-define=KEY={YOUR_KEY}`の中の`{YOUR_KEY}`を、[その1：テストユーザーの作成](#part1)の`キー（Key）`情報に置き換える必要があります。
>

#### IDEを使用して実行することも可能です。（オプションの手順）

<dx-tabs>
::: Androidプラットフォーム[](id:android)
1. Android Studioでdiscuss/andoridディレクトリを開きます。
![](https://qcloudimg.tencent-cloud.cn/raw/6516f9b17c58915c4ebc93c5c8829831.png)
2. Androidのエミュレーターを起動し、**Build And Run**をクリックすると、Demoが実行可能となります。ランダムなUserID（数字とアルファベットの組み合わせ）を入力できます。
>?UIは部分的に調整され更新される可能性があります。最新バージョンを基準としてください。
:::
::: iOSプラットフォーム[](id:ios)
1. Xcodeを開き、discuss/ios/Runner.xcodeprojファイルを開きます。
![](https://qcloudimg.tencent-cloud.cn/raw/6d74814ba9bce54c7439e8b3cea53e73.png)
2. iPhoneの実機に接続して、**Build And Run**をクリックします。iOSプロジェクトのコンパイルが終了すると、新しいウィンドウにXcodeプロジェクトが表示されます。
3. iOSプロセスを開き、メインTargetのSigning & Capabilities（Apple開発者アカウントが必要）を設定すると、プロジェクトをiPhoneの実機で実行可能になります。
4. プロジェクトを起動し、実機でDemoのデバッグを実行します。
![](https://qcloudimg.tencent-cloud.cn/raw/3fe6bbac88bb21ad7a7822bb297793b3.png)
:::
</dx-tabs>

#### Demoコードの構造の概要

>? DemoのUIおよび業務ロジックの部分には、Flutter TUIKitを使用しています。Demo層自体は、Appのビルド、ナビゲーションリダイレクトの処理およびインスタンス化されたTUIKit内の各コンポーネントの呼び出しのみに用いられます。


|  フォルダ  | 説明 |
|---------|---------|
| lib | プログラムのコアディレクトリ |
| lib/i18n | 国際化関連コードです。ここでの国際化には、TUIKit自体の機能の国際化や多言語対応は含まれません。必要に応じてインポートできます |
| lib/src | プロジェクトのメインディレクトリ |
| lib/src/pages | このDemoのいくつかの重点ナビゲーションページです。プロジェクトの初期化完了後、`app.dart`はアニメーションをロードして表示し、ログインセッションを判断して、ユーザーを`login.dart`または`home_page.dart`に誘導します。ユーザーのログイン後、ログイン情報は`shared_preference`プラグインを通じてローカルに保存されます。その後、毎回のアプリケーション起動の際、ローカルに保存されたログイン情報を発見すると、自動的にその情報を使用してログインし、情報がない場合やログインに失敗した場合はログインページに誘導します。自動ログイン中、ユーザーはまだ`app.dart`で、ロードしたアニメーションを見ることができます。`home_page.dart`にはボトムTabが含まれ、このDemoの4つの主要機能ページの切り替えを担います。 |
| lib/utils | いくつかのツール関数クラス |


基本的に、`lib/src`内の各dartファイルはTUIKitコンポーネントをインポートしており、ファイル内でコンポーネントをインスタンス化すると ページレンダリングが可能になります。

主要なファイルは次のとおりです。


|  lib/srcの主要なファイル  | ファイルの説明 |
|---------|---------|
| add_friend.dart | フレンド追加申請ページです。`TIMUIKitAddFriend`コンポーネントを使用します|
| add_group.dart | グループ参加申請ページです。`TIMUIKitAddGroup`コンポーネントを使用します|
| blacklist.dart| ブラックリスト一覧ページです。`TIMUIKitBlackList`コンポーネントを使用します |
| chat.dart | メインチャットページです。TUIKitのフルセットのチャット機能、`TIMUIKitChat`コンポーネントを使用します |
| chatv2.dart | メインチャットページです。アトミック機能、`TIMUIKitChat`コンポーネントを使用します |
| contact.dart | 連絡先ページです。`TIMUIKitContact`コンポーネントを使用します|
| conversation.dart | セッションリストインターフェースです。`TIMUIKitConversation`コンポーネントを使用します |
| create_group.dart | グループチャット開始ページです。Demoのみで実装でき、コンポーネントは使用しません |
| group_application_list.dart | グループ参加申請リストページです。`TIMUIKitGroupApplicationList`コンポーネントを使用します |
| group_list.dart | グループリストページです。`TIMUIKitGroup`コンポーネントを使用します  |
| group_profile.dart | グループプロファイルおよびグループ管理ページです。`TIMUIKitGroupProfile`コンポーネントを使用します |
| newContact.dart | 連絡先フレンド申請ページです。`TIMUIKitNewContact`コンポーネントを使用します |
| routes.dart | Demoのルートです。ログインページ`login.dart`またはホームページ`home_page.dart`にナビゲートします。 |
| search.dart | グローバル検索およびセッション内検索ページです。`TIMUIKitSearch`（グローバル検索）および`TIMUIKitSearchMsgDetail`（セッション内検索）コンポーネントを使用します |
| user_profile.dart | ユーザー情報およびリレーションシップチェーン保守ページです。`TIMUIKitProfile`コンポーネントを使用します|

大部分のTUIKitコンポーネントはナビゲーションリダイレクトのメソッドに渡す必要があります。そのため、Demo層での`Navigator`の処理が必要です。

Demoの説明は以上です。Demoを直接変更して二次開発を行うか、またはこれを参照し、業務ニーズに合わせて実装することができます。

[](id:part4)

## その4：UIを含む統合、TUIKitコンポーネントリポジトリの使用、IM機能埋め込みを半日で完了

TUIKitはTencent Cloud IM SDKのUIコンポーネントリポジトリであり、セッションリスト、チャットインターフェース、連絡先リストなどの共通のUIコンポーネントを提供しています。開発者は実際の業務ニーズに応じて、このコンポーネントリポジトリによってカスタムIMアプリケーションをスピーディーにビルドすることができます。[TUIKitの詳細な説明](https://intl.cloud.tencent.com/document/product/1047/46576)をご参照ください。

### 前提条件

Flutterプロジェクトの作成が完了している、またはベースになるFlutterプロジェクトがすでにあること。

### 統合の手順

#### IM TUIkitのインストール

TUIkitにはIM SDKが含まれているため、`tim_ui_kit`をインストールすれば、基本のIM SDKをインストールする必要はありません。

```shell
#コマンドラインでの実行：
flutter pub add tim_ui_kit
```

#### 初期化

1. アプリケーションを起動する際にTUIKitを初期化します。
2. 必ず先に`TIMUIKitCore.getInstance()`を実行してから初期化関数`init()`を呼び出し、`sdkAppID`を渡してください。
```dart
/// main.dart
import 'package:tim_ui_kit/tim_ui_kit.dart';

final CoreServicesImpl _coreInstance = TIMUIKitCore.getInstance();
  @override
 void initState() {
   _coreInstance.init(
     sdkAppID: 0, // Replace 0 with the SDKAppID of your IM application when integrating
     loglevel: LogLevelEnum.V2TIM_LOG_DEBUG,
     listener: V2TimSDKListener());    
   super.initState();
 }
}
```

#### テストユーザーのログイン
1. この時点で、最初にコンソール上で作成したテストアカウントを使用して、ログイン検証を完了することが可能です。
2. `_coreInstance.login`メソッドを呼び出し、テストアカウントにログインします。
```dart
import 'package:tim_ui_kit/tim_ui_kit.dart';

final CoreServicesImpl _coreInstance = TIMUIKitCore.getInstance();
_coreInstance.login(userID: userID, userSig: userSig);
```

>? このアカウントは開発テストのみに使用します。アプリケーションのリリース前の`UserSig`の正しい発行方法は、サーバーで生成し、Appのインターフェース向けに提供する方法となります。`UserSig`が必要なときは、Appから業務サーバーにリクエストを送信し動的に`UserSig`を取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/1047/34385)をご参照ください。

#### 実装：セッションリストページ

セッションリストをIM機能のトップページにし、チャット記録のあるすべてのユーザーとのセッションおよびグループチャットセッションをカバーすることができます。

<img style="width:300px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/279da6d5d41ec1ce0b0cf7fca9a697b8.jpg" />

`Conversation`クラスを作成し、`body`で`TIMUIKitConversation`コンポーネントを使用して、セッションリストをレンダリングしてください。

具体的なセッションチャットページにリダイレクトするためのナビゲーションに用いる、`onTapItem`イベントの処理関数を渡すだけです。`Chat`クラスに関しては、次の手順で説明します。

```dart
import 'package:flutter/material.dart';
import 'package:tim_ui_kit/tim_ui_kit.dart';

class Conversation extends StatelessWidget {
const Conversation({Key? key}) : super(key: key);
@override
Widget build(BuildContext context) {
return Scaffold(
  appBar: AppBar(
    title: const Text(
      "Message",
      style: TextStyle(color: Colors.black),
    ),
  ),
  body: TIMUIKitConversation(
    onTapItem: (selectedConv) {
      Navigator.push(
          context,
          MaterialPageRoute(
            builder: (context) => Chat(
              selectedConversation: selectedConv,
            ),
          ));
    },
  ),
);
}
}
```

#### 実装：セッションチャットページ

このページはトップのメインチャット履歴と、ボトムのメッセージ送信モジュールで構成されます。
<img style="width:300px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/0c361254fa5117f7580f39e8b523e472.png" />

`Chat`クラスを作成し、`body`で`TIMUIKitChat`コンポーネントを使用して、チャットページをレンダリングしてください。

連絡先の詳細情報ページへのリダイレクトに用いる、`onTapAvatar`イベントの処理関数を渡すとよいでしょう。`UserProfile`クラスに関しては、次の手順で説明します。

```dart
import 'package:flutter/material.dart';
import 'package:tim_ui_kit/tim_ui_kit.dart';

class Chat extends StatelessWidget {
final V2TimConversation selectedConversation;
const Chat({Key? key, required this.selectedConversation}) : super(key: key);
String? _getConvID() {
return selectedConversation.type == 1
    ? selectedConversation.userID
    : selectedConversation.groupID;
}
@override
Widget build(BuildContext context) {
return TIMUIKitChat(
  conversationID: _getConvID() ?? '', // groupID or UserID
  conversationType: selectedConversation.type ?? 1, // Conversation type
  conversationShowName: selectedConversation.showName ?? "", // Conversation display name
  onTapAvatar: (_) {
        Navigator.push(
            context,
            MaterialPageRoute(
             builder: (context) => UserProfile(userID: userID),
        ));
  }, // Callback for the clicking of the message sender profile photo. This callback can be used with `TIMUIKitProfile`.
);
}
```

#### 実装：ユーザー詳細ページ

このページはデフォルトで、`userID`を渡すだけで、フレンドかどうかに基づいて自動的にユーザー詳細ページを生成できるものです。

`UserProfile`クラスを作成し、`body`で`TIMUIKitProfile`コンポーネントを使用し、ユーザー詳細およびリレーションシップチェーンページをレンダリングしてください。

>? このページをカスタマイズしたい場合は、`profileWidgetBuilder`を使用して、カスタマイズしたいprofileコンポーネントを渡し、`profileWidgetsOrder`を併用して縦方向の配列順を決定することを優先してご検討ください。それでご満足いただけない場合のみ、`builder`をご使用ください。

<img style="width:300px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/5f2e67ffb31adc738165e2c4ce58218c.jpg" />

```dart
import 'package:flutter/material.dart';
import 'package:tim_ui_kit/tim_ui_kit.dart';

class UserProfile extends StatelessWidget {
    final String userID;
    const UserProfile({required this.userID, Key? key}) : super(key: key);

    @override
    Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
       title: const Text(
         "Message",
         style: TextStyle(color: Colors.black),
       ),
     ),
     body: TIMUIKitProfile(
          userID: widget.userID,
     ),
    );
  }
}
```

この時点で、アプリケーションはメッセージの送受信、フレンドシップの管理、ユーザー詳細情報の表示、セッションリストの表示ができるようになっています。

#### その他の機能

引き続き以下のTUIKitプラグインを使用して、完全なIM機能をスピーディーに実装することができます。

[TIMUIKitContact](https://intl.cloud.tencent.com/document/product/1047/46297#timuikitcontact): 連絡先リストページです。

[TIMUIKitGroupProfile](https://intl.cloud.tencent.com/document/product/1047/46297#timuikitgroupprofile): グループプロファイルページです。使用する方式は`TIMUIKitProfile`と基本的に同じです。

[TIMUIKitGroup](https://intl.cloud.tencent.com/document/product/1047/46297#timuikitgroup): グループリストインターフェースです。

[TIMUIKitBlackList](https://intl.cloud.tencent.com/document/product/1047/46297#timuikitblacklist): ブラックリストインターフェースです。

[TIMUIKitNewContact](https://intl.cloud.tencent.com/document/product/1047/46297#timuikitnewcontact): 連絡先（フレンド）申請リストです。外部に赤い点を表示させたい場合は、`TIMUIKitUnreadCount`のレッドドットコンポーネントを使用すると、リスナーを自動的にマウントします。

[TIMUIKitSearch](https://pub.dev/documentation/tim_ui_kit/latest/ui_views_TIMUIKitSearch_tim_uikit_search/TIMUIKitSearch-class.html): 検索コンポーネントです。連絡先/グループ/チャット記録のグローバル検索のほか、特定のセッションにおけるチャット記録の検索もサポートします。2つのモードは`conversation`を渡すかどうかによって決まります。

UIプラグインガイドの詳細については、[このドキュメント](https://intl.cloud.tencent.com/document/product/1047/46297)または[プラグインREADME](https://pub.dev/packages/tim_ui_kit)をご参照ください。

[](id:part5)

## その5：UI統合を自身で実装

### 前提条件

Flutterプロジェクトの作成が完了している、またはベースになるFlutterプロジェクトがすでにあること。

### 統合の手順

#### IM SDKのインストール

[このセグメントの詳細なドキュメント](https://intl.cloud.tencent.com/document/product/1047/46264)

次のコマンドを使用して、Flutter IM SDKの最新バージョンをインストールします。

コマンドラインでの実行：

```shell
flutter pub add tencent_im_sdk_plugin
```

#### SDKの初期化完了

[このセグメントの詳細なドキュメント](https://intl.cloud.tencent.com/document/product/1047/47966)

`initSDK`を呼び出して、SDKの初期化を完了します。

お客様の`sdkAppID`を渡します。

```Dart
import 'package:tencent_im_sdk_plugin/enum/V2TimSDKListener.dart';
import 'package:tencent_im_sdk_plugin/enum/log_level_enum.dart';
import 'package:tencent_im_sdk_plugin/tencent_im_sdk_plugin.dart';
    TencentImSDKPlugin.v2TIMManager.initSDK(
    sdkAppID: 0, // Replace 0 with the SDKAppID of your IM application when integrating
    loglevel: LogLevelEnum.V2TIM_LOG_DEBUG, // Log
    listener: V2TimSDKListener(),
  );
```

この手順ではIM SDKにいくつかのリスナーをマウントすることができます。これには主に、ネットワーク状態およびユーザー情報の変更などが含まれます。詳細については、[このドキュメント](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/enum_V2TimSDKListener/V2TimSDKListener-class.html)をご参照ください。

#### テストユーザーのログイン

[このセグメントの詳細なドキュメント](https://cloud.tencent.com/document/product/269/75296)

この時点で、最初にコンソール上で作成したテストアカウントを使用して、ログイン検証を完了することが可能です。

`TencentImSDKPlugin.v2TIMManager.login`メソッドを呼び出し、テストアカウントにログインします。

戻り値`res.code`が0の場合、ログインは成功です。

```dart
import 'package:tencent_im_sdk_plugin/tencent_im_sdk_plugin.dart';
 V2TimCallback res = await TencentImSDKPlugin.v2TIMManager.login(
    userID: userID,
    userSig: userSig, 
  );
```

>? このアカウントは開発テストのみに使用します。アプリケーションのリリース前の`UserSig`の正しい発行方法は、`UserSig`の計算コードをサーバーに統合し、Appのインターフェース向けに提供する方法となります。`UserSig`が必要なときは、Appから業務サーバーにリクエストを送信し動的に`UserSig`を取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/1047/34385)をご参照ください。

#### メッセージの送信

[このセグメントの詳細なドキュメント](https://intl.cloud.tencent.com/document/product/1047/47992)

ここでは、テキストメッセージの送信を例に挙げます。そのフローは次のとおりです。

1. `createTextMessage(String)`を呼び出してテキストメッセージを作成します。
2. 戻り値に基づいて、メッセージIDを取得します。
3. `sendMessage()`を呼び出して、このIDのメッセージを送信します。`receiver`には、その前に作成した別のテストアカウントIDを入力できます。シングルチャットメッセージを送信する場合は`groupID`の入力は不要です。

サンプルコード：

```dart
import 'package:tencent_im_sdk_plugin/tencent_im_sdk_plugin.dart';

V2TimValueCallback<V2TimMsgCreateInfoResult> createMessage =
      await TencentImSDKPlugin.v2TIMManager
          .getMessageManager()
          .createTextMessage(text: "The text to create");
          
String id = createMessage.data!.id!; // The message creation ID 

V2TimValueCallback<V2TimMessage> res = await TencentImSDKPlugin.v2TIMManager
      .getMessageManager()
      .sendMessage(
          id: id, // Pass in the message creation ID to
          receiver: "The userID of the destination user",
          groupID: "The groupID of the destination group",
          );
```

>?送信に失敗した場合は、sdkAppIDが知らない人宛てのメッセージ送信をサポートしていないことが原因の可能性があります。コンソールで有効にしてからテストに使用してください。
>
> [このリンクをクリック](https://console.cloud.tencent.com/im/login-message)して、フレンドリレーションシップチェーンのチェックを無効にしてください。

#### セッションリストの取得

[このセグメントの詳細なドキュメント](https://intl.cloud.tencent.com/document/product/1047/48321)

前の手順でテストメッセージの送信が完了しましたので、別のテストアカウントでログインし、セッションリストをプルできるようになりました。
<img style="width:300px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/e2fdd7632ebc0c5cde68c91afa914201.jpg" />


セッションリストの取得には2つの方法があります。

1. 長時間接続コールバックを監視し、セッションリストをリアルタイムに更新します。
2. APIをリクエストし、ページごとに一括でセッションリストを取得します。

一般的なユースケースは次のようなものです。

アプリケーションの起動後すぐにセッションリストを取得し、その後は長時間接続を監視して、セッションリストの変更をリアルタイムに更新します。

##### セッションリストの一括リクエスト

セッションリストを取得するためには`nextSeq`を保守し、現在の位置を記録する必要があります。

```dart
import 'package:tencent_im_sdk_plugin/tencent_im_sdk_plugin.dart';

String nextSeq = "0";

getConversationList() async {
  V2TimValueCallback<V2TimConversationResult> res = await TencentImSDKPlugin
      .v2TIMManager
      .getConversationManager()
      .getConversationList(nextSeq: nextSeq, count: 10);
  
  nextSeq = res.data?.nextSeq ?? "0";
}
```

この時点で、前の手順で別のテストアカウントを使用して送信したメッセージのセッションを見ることができるようになりました。

##### 長時間接続の監視によるセッションリストのリアルタイム取得

この手順では、先にSDKにリスナーをマウントしてからコールバックイベントを処理し、UIを更新する必要があります。

1. リスナーをマウントします。
```dart
await TencentImSDKPlugin.v2TIMManager
      .getConversationManager()
      .setConversationListener(
        listener: new V2TimConversationListener(
          onConversationChanged: (List<V2TimConversation> list){
            _onConversationListChanged(list);
    },
          onNewConversation:(List<V2TimConversation> list){
            _onConversationListChanged(list);
    },
```

2. コールバックイベントを処理し、最新のセッションリストをインターフェース上に表示します。
```dart
import 'package:tencent_im_sdk_plugin/tencent_im_sdk_plugin.dart';

List<V2TimConversation> _conversationList = [];

_onConversationListChanged(List<V2TimConversation> list) {
  for (int element = 0; element < list.length; element++) {
    int index = _conversationList.indexWhere(
        (item) => item!.conversationID == list[element].conversationID);
    if (index > -1) {
      _conversationList.setAll(index, [list[element]]);
    } else {
      _conversationList.add(list[element]);
    }
  }
```

#### メッセージの受信

[このセグメントの詳細なドキュメント](https://intl.cloud.tencent.com/document/product/1047/47997)

Tencent Cloud IM Ffltter SDKによるメッセージの受信には2つの方法があります。

1. 長時間接続コールバックを監視し、メッセージの変更をリアルタイムに取得し、メッセージ履歴リストを更新してレンダリングします。
2. APIをリクエストし、ページごとに一括でメッセージ履歴を取得します。

一般的なユースケースは次のようなものです。

1. インターフェースが新しいセッションに入ると、まず一定量のメッセージ履歴を一括でリクエストし、メッセージ履歴リストの表示に用います。
2. 長時間接続を監視し、新しいメッセージをリアルタイムに受信してメッセージ履歴リストに追加します。

##### メッセージ履歴リストの一括リクエスト

ページごとに取得するメッセージ数が多すぎると取得速度に影響しますので、多すぎてはなりません。20通前後に設定することをお勧めします。

次のリクエストの際に使用できるよう、現在のページ数を動的に記録しなければなりません。

サンプルコードは次のとおりです。

```dart
import 'package:tencent_im_sdk_plugin/tencent_im_sdk_plugin.dart';

  V2TimValueCallback<List<V2TimMessage>> res = await TencentImSDKPlugin
      .v2TIMManager
      .getMessageManager()
      .getGroupHistoryMessageList(
        groupID: "groupID",
        count: 20,
        lastMsgID: "",
      );
      
  List<V2TimMessage> msgList = res.data ?? [];
  
  // here you can use msgList to render your message list
    }
```

##### 長時間接続の監視による新メッセージのリアルタイム取得

メッセージ履歴リストを初期化すると、新しいメッセージは長時間接続`V2TimAdvancedMsgListener.onRecvNewMessage`から受信します。

`onRecvNewMessage`コールバックがトリガーされると、必要に応じて新しいメッセージをメッセージ履歴リストに追加することができます。

リスナーをバインドするサンプルコードは次のとおりです。

```dart
import 'package:tencent_im_sdk_plugin/tencent_im_sdk_plugin.dart';

final adVancesMsgListener = V2TimAdvancedMsgListener(
onRecvNewMessage: (V2TimMessage newMsg) {
  _onReceiveNewMsg(newMsg);
},
/// ... other listeners related to message
);

TencentImSDKPlugin.v2TIMManager
    .getMessageManager()
    .addAdvancedMsgListener(listener: adVancesMsgListener);
```

この時点で、IMモジュールの開発は基本的に完了し、メッセージの送受信や様々なセッションに入ることが可能になりました。

続いて、[グループ](https://intl.cloud.tencent.com/document/product/1047/48169)，[ユーザープロファイル](https://intl.cloud.tencent.com/document/product/1047/48160)、[リレーションシップチェーン](https://intl.cloud.tencent.com/document/product/1047/48157)、[オフラインプッシュ](https://intl.cloud.tencent.com/document/product/1047/46306)、[ローカル検索](https://intl.cloud.tencent.com/document/product/1047/48135)などの関連機能の開発を完了することができます。



## よくあるご質問

### サポートされているプラットフォームはどれですか。
- 現在、[IM SDK(tencent_im_sdk_plugin)](https://intl.cloud.tencent.com/document/product/1047/46264)はiOS 、Android、Webの3つのプラットフォームをサポートしています。このほかにWindowsおよびMac版も開発中ですので、ご期待ください。
- [TUIKit](https://intl.cloud.tencent.com/document/product/1047/46576)および[完全版付属インタラクションDemo](https://github.com/TencentCloud/TIMSDK/tree/master/Flutter/Demo/im-flutter-uikit)はiOSとAndroidの両方のモバイルプラットフォームをサポートしています。

### AndroidでBuild And Runをクリックすると、使用できるデバイスが見つからないというエラーが発生します。

デバイスが他のリソースに使用されないことを保証するか、または**Build**をクリックしてAPKパッケージを生成してから、エミュレーター内にドラッグして実行します。

### iOSで初回実行時にエラーが発生します。

実行を設定後、エラーが発生した場合は、**Product** > **Clean Build Folder**をクリックし、生成物を削除してから再度`pod install`または`flutter run`を行うことができます。

![20220714152720](https://tuikit-1251787278.cos.ap-guangzhou.myqcloud.com/20220714152720.png)

### Apple Watchを装着した際、 実機デバッグでiOSのエラーが発生します。

![20220714152340](https://tuikit-1251787278.cos.ap-guangzhou.myqcloud.com/20220714152340.png)

Apple Watchを機内モードに設定し、iPhoneのBluetooth機能を`設定 => Bluetooth`で完全にオフにしてください。

Xcodeを再起動し（オンになっている場合）、再び`flutter run`を実行します。

### Flutter環境の問題

Flutterの環境に問題のないことを確認する場合、Flutter doctorを実行してFlutter環境が適切にインストールされているかチェックしてください。

### Flutterを使用して自動生成したプロジェクトをTUIKitにインポートし、Android端末で実行するとエラーが発生します。

![](https://qcloudimg.tencent-cloud.cn/raw/d95efdd4ae50f13f38f4c383ca755ae7.png)

1. `android\app\src\main\AndroidManifest.xml`を開き、下記に従って、`xmlns:tools="http://schemas.android.com/tools"` / `android:label="@string/android_label"`および`tools:replace="android:label"`への入力を補完します。
```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="Android端末のパッケージ名に置き換える"
    xmlns:tools="http://schemas.android.com/tools">
    <application
        android:label="@string/android_label"
        tools:replace="android:label"
        android:icon="@mipmap/ic_launcher" // iconパスを指定する
        android:usesCleartextTraffic="true"
        android:requestLegacyExternalStorage="true">
```

2. `android\app\build.gradle`を開き、`defaultConfig`の`minSdkVersion`および`targetSdkVersion`への入力を補完します。
```gradle
defaultConfig {
  applicationId "" // Android端末のパッケージ名に置き換える
  minSdkVersion 21
  targetSdkVersion 30
}
```

## お問い合わせ
統合と使用の過程でご不明な点がありましたら、QQグループ：788910197に参加してお問い合わせください。
