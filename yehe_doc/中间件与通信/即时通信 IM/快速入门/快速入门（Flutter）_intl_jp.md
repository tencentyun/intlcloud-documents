- [](id:toc)
  ここでは、Flutter SDKの統合方法についてご説明します。

  ## 環境要件

  | 環境    | バージョン                                                   |
  | ------- | ------------------------------------------------------------ |
  | Flutter | IM SDKの最低要件はFlutter 2.2.0バージョン、TUIKit統合コンポーネントリポジトリの最低要件はFlutter 2.10.0バージョンです。 |
  | Android | Android Studio 3.5以降のバージョン。Appの要件はAndroid 4.1以降のバージョンのデバイスです。 |
  | iOS     | Xcode 11.0以降のバージョン。プロジェクトに有効な開発者署名を設定済みであることを確認してください。 |

  ## サポートするプラットフォーム

  FlutterのすべてのプラットフォームをサポートするIM SDKとTUIKitの構築に取り組み、1つのコードセットですべてのプラットフォームで実行することを支援します。

  | プラットフォーム                                             | UI SDK ([tencent_cloud_chat_sdk](https://pub.dev/packages/tencent_cloud_chat_sdk))なし | UIおよび基本業務ロジックTUIKit ([tencent_cloud_chat_uikit](https://pub.dev/packages/tencent_cloud_chat_uikit))を含めます |
  | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
  | iOS                                                          | 対応可                                                       | 対応可                                                       |
  | Android                                                      | 対応可                                                       | 対応可                                                       |
  | [Web](#web)                                                  | 対応可、4.1.1+2以降のバージョンは対応可                      | 対応可、0.1.5とそれ以降のバージョンは対応可                  |
  | [macOS](#pc)                                                 | 対応可、4.1.9以降のバージョンは対応可                        | 近日リリース                                                 |
  | [Windows](#pc)                                               | 対応可、4.1.9以降のバージョンは対応可                        | 近日リリース                                                 |
  | [混合開発](https://www.tencentcloud.com/document/product/1047/51456) （Flutter SDKを既存のネイティブアプリケーションに追加します） | 5.0.0以降のバージョンは対応可                                | 1.0.0とそれ以降のバージョンは対応可                          |

  >? Web/macOS/Windowsプラットフォームでは、わずかなステップで簡単に導入する必要があります。詳細については、この記事の[その他のプラットフォームを展開](#more)をご参照ください。

  ## Demo体験

  アクセス前に、DEMOを体験して、Tencent Cloud IM FlutterクロスプラットフォームSDKとTUIKit機能をすばやく理解できます。

  **以下の各バージョンのDEMOは、すべてTUIKitを同じFlutterプロジェクトに導入して制作・パッケージ化しています。**Desktop(macOS/Windows)プラットフォームは、SDKでサポートされています。DEMOは近日リリースされます。

  <table style="text-align:center; vertical-align:middle; max-width: 800px">
    <tr>
      <th style="text-align:center;">モバイル端末 APP</th>
      <th style="text-align:center;">WEB - H5</th>
    </tr>
    <tr>
      <td><div style="display: flex; justify-content: center; align-items: center; flex-direction: column; padding-top: 10px">iOS/Android APP、プラットフォームのダウンロードを自動的に判断します<img style="max-width:200px; margin: 20px 0 20px 0" src="https://qcloudimg.tencent-cloud.cn/raw/ca2aaff551410c74fce48008c771b9f6.png"/></div></td>
      <td><div style="display: flex; justify-content: center; align-items: center; flex-direction: column; padding-top: 10px">携帯電話でコードをスキャンしてオンラインWeb版DEMOを体験します<img style="max-width:200px; margin: 20px 0 20px 0" src="https://qcloudimg.tencent-cloud.cn/raw/3c79e8bb16dd0eeab35e894a690e0444.png"/></div></td>
    </tr>
  </table>

  ## 予備作業

  1. [Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)を行い、[実名認証](https://intl.cloud.tencent.com/document/product/378/3629)が完了していること。
  2. [アプリケーションの作成とアップグレード](https://intl.cloud.tencent.com/document/product/1047/34577)を参照してアプリケーションを作成し、`SDKAppID`を記録していること。
  3. [IMコンソール](https://console.cloud.tencent.com/im)でご自分のアプリケーションを選択し、左側ナビゲーションバーで**支援ツール**->**UserSig生成&検証**の順にクリックし、2つのUserIDおよびそれに対応するUserSigを作成します。`UserID`、`署名（Key）`、`UserSig`の3つをコピーし、その後のログインで使用します。
  ![](https://main.qcloudimg.com/raw/2286644d987d24caf565142ae30c4392.png)

  >? このアカウントは開発テストのみに使用します。アプリケーションのリリース前の`UserSig`の正しい発行方法は、サーバーで生成し、Appのインターフェース向けに提供する方法となります。`UserSig`が必要なときは、Appから業務サーバーにリクエストを送信し動的に`UserSig`を取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/1047/34385)をご参照ください。

  [](id:part2)

  ## 適切な方法を選択してFlutter SDKを統合

  IMは3種類の統合方法を提供しており、最適な方法を選択して統合を行うことができます。

  | 統合方法                     | 適用シナリオ                                                 |
  | ---------------------------- | ------------------------------------------------------------ |
  | [DEMOによる修正](#part3)     | IM Demoは完全なチャットAppであり、コードはオープンソース化されています。チャットライクなユースケースを実装したい場合は、Demoを使用して二次開発を行うことができます。今すぐ[Demo体験](https://intl.cloud.tencent.com/document/product/1047/34279)が可能です。 |
  | [UIを含む統合](#part4)       | IMのUIコンポーネントリポジトリ`TUIKit`は、セッションリスト、チャットインターフェース、連絡先リストなどの共通のUIコンポーネントを提供しています。開発者は実際の業務ニーズに応じて、このコンポーネントリポジトリによってカスタムIMアプリケーションをスピーディーにビルドすることができます。**この方法を優先して用いることを推奨します**。 |
  | [UI統合を自身で実装](#part5) | アプリケーションインターフェースのニーズがTUIKitでは満たせない場合、または多くのカスタマイズが必要な場合は、この方法を用いることができます。 |

  IM SDKの各APIについてより深くご理解いただけるよう、各APIの呼び出しおよび監視のトリガーのデモンストレーションを行う[API Example](https://github.com/TencentCloud/tc-chat-sdk-flutter/tree/main/example)も提供しています。

  [](id:part3)

  ## ソリューション1：Demoによる修正

  ### Demoクイックスタート

  1. Demoソースコードのダウンロード、依存関係のインストール：
  ```shell
  # Clone the code
  git clone https://github.com/TencentCloud/tc-chat-demo-flutter.git
  
  # Install dependencies
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

  #### IDEを使用して実行することも可能です：（オプションの手順）

  <dx-tabs>
  ::: Androidプラットフォーム[](id:android)
  1. Android Studioでは、FlutterとDartプラグインをインストールします。
   - Macプラットフォーム：プラグイン設定を開く（v3.6.3.0以降のシステムでPreferences > Pluginsを開く） => Flutterプラグインを選択してインストールをクリックする => Dartプラグインをインストールするといったプロンプトが表示されると、Yesをクリックする => 再起動といったプロンプトが表示されると、Restartをクリックする。
   - LinuxまたはWindowsプラットフォーム：プラグイン設定を開く（File > Settings > Pluginsにある） => Marketplace（拡張ストア）を選択し、Flutter pluginを選択してから、Install（インストール）をクリックする。
  ![](https://qcloudimg.tencent-cloud.cn/raw/481bc19b55b40051daa8e669325cd123.png)
  2. プロジェクトを開いて、依存関係を取得します。
  Android Studioでは、`im-flutter-uikit`ディレクトリを開きます。
  このパスでコマンドを実行して、依存関係を実行します。
  ```shell
  flutter pub get
  ```
  3. 環境変数の設定
  右上隅の実行ボタンの横で、`main.dart`にマウスをhoverし、`Edit Configurations`を設定します。
  ![](https://qcloudimg.tencent-cloud.cn/raw/e2db56849e86dab8f6f0ccb4d3374fce.png)
  ポップアップ表示されたウィンドウでは、`Additional run args`を設定し、環境変数（SDKAPPIDなどの情報）を入力します。例：
  ```shell
  # SDK_APPID、KEYの2つのパラメータを置き換えてください
  --dart-define=SDK_APPID={YOUR_SDKAPPID} --dart-define=ISPRODUCT_ENV=false --dart-define=KEY={YOUR_KEY}
  ```
  ![](https://qcloudimg.tencent-cloud.cn/raw/f022441399d2d6057b86e489593768ad.png)
  4. Androidシミュレータを作成します。
  インストールしたばかりのシミュレータを起動し、それを選択します。
  ![](https://qcloudimg.tencent-cloud.cn/raw/e3aebdd2f6018c8f1fa10d5b5fb62c79.png)
  画面の右上隅にあるDevice ManagerをクリックしてCreate devicesを完了し、シミュレータを作成します。Google FCMプッシュ機能を使用するには、できるだけGoogle Play Storeをサポートするデバイスをインストールすることをお勧めします。
  ![](https://qcloudimg.tencent-cloud.cn/raw/9db005b86f9ffa1052826fe5e11d219a.png)
  5. プロジェクトを実行します。
  必要に応じて、下図左側のRunまたは右側のDebugをクリックしてプロジェクトを実行します。
  ![](https://qcloudimg.tencent-cloud.cn/raw/7b0d4d008f71e1d0d805c9fb3a5de437.png)
  >?UIは部分的に調整され更新される可能性があります。最新バージョンを基準としてください。
  >:::
  >::: iOSプラットフォーム[](id:ios)

  1. Xcodeでは、`im-flutter-uikit/ios`ディレクトリを開きます。
  2. iPhoneの実機に接続して、**Build And Run**をクリックします。iOSプロジェクトのコンパイルが終了すると、新しいウィンドウにXcodeプロジェクトが表示されます。
  3. iOSプロセスを開き、メインTargetのSigning & Capabilities（Apple開発者アカウントが必要）を設定すると、プロジェクトをiPhoneの実機で実行可能になります。
  4. プロジェクトを起動し、実機でDemoのデバッグを実行します。
  ![](https://qcloudimg.tencent-cloud.cn/raw/911935cf419e4298edb45cd93bf10852.png)
  :::
  </dx-tabs>

  #### Demoコードの構造の概要

  >? DemoのUIおよび業務ロジックの部分には、Flutter TUIKitを使用しています。Demo層自体は、Appのビルド、ナビゲーションリダイレクトの処理およびインスタンス化されたTUIKit内の各コンポーネントの呼び出しのみに用いられます。

  | フォルダ      | 説明                                                         |
  | ------------- | ------------------------------------------------------------ |
  | lib           | プログラムのコアディレクトリ                                 |
  | lib/i18n      | 国際化関連コードです。ここでの国際化には、TUIKit自体の機能の国際化や多言語対応は含まれません。必要に応じてインポートできます |
  | lib/src       | プロジェクトのメインディレクトリ                             |
  | lib/src/pages | このDemoのいくつかの重点ナビゲーションページです。プロジェクトの初期化完了後、`app.dart`はアニメーションをロードして表示し、ログインセッションを判断して、ユーザーを`login.dart`または`home_page.dart`に誘導します。ユーザーのログイン後、ログイン情報は`shared_preference`プラグインを通じてローカルに保存されます。その後、毎回のアプリケーション起動の際、ローカルに保存されたログイン情報を発見すると、自動的にその情報を使用してログインし、情報がない場合やログインに失敗した場合はログインページに誘導します。自動ログイン中、ユーザーはまだ`app.dart`で、ロードしたアニメーションを見ることができます。`home_page.dart`にはボトムTabが含まれ、このDemoの4つの主要機能ページの切り替えを担います。 |
  | lib/utils     | いくつかのツール関数クラス                                   |

  基本的に、`lib/src`内の各dartファイルはTUIKitコンポーネントをインポートしており、ファイル内でコンポーネントをインスタンス化すると、ページレンダリングが可能になります。

  主要なファイルは次のとおりです：

  | lib/srcの主要なファイル     | ファイルの説明                                               |
  | --------------------------- | ------------------------------------------------------------ |
  | add_friend.dart             | フレンド追加申請ページです。`TIMUIKitAddFriend`コンポーネントを使用します |
  | add_group.dart              | グループ参加申請ページです。`TIMUIKitAddGroup`コンポーネントを使用します |
  | blacklist.dart              | ブラックリスト一覧ページです。`TIMUIKitBlackList`コンポーネントを使用します |
  | chat.dart                   | メインチャットページです。TUIKitのフルセットのチャット機能、`TIMUIKitChat`コンポーネントを使用します |
  | chatv2.dart                 | メインチャットページです。アトミック機能、`TIMUIKitChat`コンポーネントを使用します |
  | contact.dart                | 連絡先ページです。`TIMUIKitContact`コンポーネントを使用します |
  | conversation.dart           | セッションリストインターフェースです。`TIMUIKitConversation`コンポーネントを使用します |
  | create_group.dart           | グループチャット開始ページです。Demoのみで実装でき、コンポーネントは使用しません |
  | group_application_list.dart | グループ参加申請リストページです。`TIMUIKitGroupApplicationList`コンポーネントを使用します |
  | group_list.dart             | グループリストページです。`TIMUIKitGroup`コンポーネントを使用します |
  | group_profile.dart          | グループプロファイルおよびグループ管理ページです。`TIMUIKitGroupProfile`コンポーネントを使用します |
  | newContact.dart             | 連絡先フレンド申請ページです。`TIMUIKitNewContact`コンポーネントを使用します |
  | routes.dart                 | Demoのルートです。ログインページ`login.dart`またはホームページ`home_page.dart`にナビゲートします。 |
  | search.dart                 | グローバル検索およびセッション内検索ページです。`TIMUIKitSearch`（グローバル検索）および`TIMUIKitSearchMsgDetail`（セッション内検索）コンポーネントを使用します |
  | user_profile.dart           | ユーザー情報およびリレーションシップチェーン保守ページです。`TIMUIKitProfile`コンポーネントを使用します |

  大部分のTUIKitコンポーネントはナビゲーションリダイレクトのメソッドに渡す必要があります。そのため、Demo層での`Navigator`の処理が必要です。

  Demoの説明は以上です。Demoを直接変更して二次開発を行うか、またはこれを参照し、業務ニーズに合わせて実装することができます。

  [](id:part4)

  ## ソリューション2：UIを含む統合、TUIKitコンポーネントリポジトリの使用、IM機能埋め込みを半日で完了

  TUIKitはTencent Cloud IM SDKのUIコンポーネントリポジトリであり、セッションリスト、チャットインターフェース、連絡先リストなどの共通のUIコンポーネントを提供しています。開発者は実際の業務ニーズに応じて、このコンポーネントリポジトリによってカスタムIMアプリケーションをすばやくビルドすることができます。[TUIKitのグラフィックとテキストの説明](https://intl.cloud.tencent.com/document/product/1047/50059)をご参照ください。

  この部分は、TUIKitの使用について簡単に説明します。入門ガイドの詳細については、[TUIKit統合基本機能](https://intl.cloud.tencent.com/document/product/1047/50054)をご参照ください。

  ![](https://qcloudimg.tencent-cloud.cn/raw/f140dd76be01a65abfb7e6ba2bf50ed5.png)

  ### 前提条件

  Flutterプロジェクトの作成が完了している、またはベースになるFlutterプロジェクトがすでにあること。

  ### 統合の手順

  #### 権限の設定

  TUIKitの実行には、撮影/アルバム/録音/ネットワークなどの権限が必要なため、関連の機能を正常に使用するにはNativeファイルに手動でステートメントを作成する必要があります。

  **Android**

  `android/app/src/main/AndroidManifest.xml`を開き、`<manifest></manifest>`に次の権限を追加します。

  ```xml
      <uses-permission
          android:name="android.permission.INTERNET"/>
      <uses-permission
          android:name="android.permission.RECORD_AUDIO"/>
      <uses-permission
          android:name="android.permission.FOREGROUND_SERVICE"/>
      <uses-permission
          android:name="android.permission.ACCESS_NETWORK_STATE"/>
      <uses-permission
          android:name="android.permission.VIBRATE"/>
      <uses-permission
          android:name="android.permission.ACCESS_BACKGROUND_LOCATION"/>
      <uses-permission
          android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
      <uses-permission
          android:name="android.permission.READ_EXTERNAL_STORAGE"/>
      <uses-permission
          android:name="android.permission.CAMERA"/>
  ```

  **iOS**

  `ios/Podfile`を開き、ファイルの末尾に次の権限コードを追加します。

  ```
  post_install do |installer|
    installer.pods_project.targets.each do |target|
      flutter_additional_ios_build_settings(target)
      target.build_configurations.each do |config|
            config.build_settings['GCC_PREPROCESSOR_DEFINITIONS'] ||= [
              '$(inherited)',
              'PERMISSION_MICROPHONE=1',
              'PERMISSION_CAMERA=1',
              'PERMISSION_PHOTOS=1',
            ]
          end
    end
  end
  ```

  >?プッシュ機能を使用する必要がある場合は、プッシュに関する権限も追加する必要があります。詳細については、Flutterメーカーメッセージプッシュプラグイン統合ガイドをご確認ください。

  #### IM TUIkitのインストール

  TUIkitにはIM SDKが含まれているため、`tencent_cloud_chat_uikit`をインストールすれば、基本のIM SDKをインストールする必要はありません。

  ```shell
  #コマンドラインでの実行：
  flutter pub add tencent_cloud_chat_uikit
  ```

  プロジェクトでWebをサポートする必要がある場合は、次の手順を実行する前に、[Web互換性セクションを参照](#web)して、JSファイルを導入してください。

  #### 初期化

  1. アプリケーションを起動する際にTUIKitを初期化します。
  2. [`TIMUIKitCore.getInstance()`](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitCore/getInstance.html)を実行してから、初期化関数[`init()`](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitCore/init.html)を呼び出し、`sdkAppID`を渡すよう、必ず確認してください。
  3. APIエラーメッセージと、ユーザーに思い出させるための提案を取得しやすくするために、ここでonTUIKitCallbackListenerのリッスンをマウントすることをお勧めします。[詳細については、この部分を参照](https://intl.cloud.tencent.com/document/product/1047/50054#onTUIKitCallbackListener)してください。

  ```dart
  /// main.dart
  import 'package:tencent_cloud_chat_uikit/tencent_cloud_chat_uikit.dart';
  
  final CoreServicesImpl _coreInstance = TIMUIKitCore.getInstance();
    @override
   void initState() {
     _coreInstance.init(
       sdkAppID: 0, // Replace 0 with the SDKAppID of your IM application when integrating
       // language: LanguageEnum.en, // インターフェース言語の設定です。設定されていない場合は、システム言語に従います
       loglevel: LogLevelEnum.V2TIM_LOG_DEBUG,
       onTUIKitCallbackListener:  (TIMCallback callbackValue){}, // [設定をお勧めします。詳細については、この部分を参照](https://intl.cloud.tencent.com/document/product/1047/50054#onTUIKitCallbackListener)してください
       listener: V2TimSDKListener());
     super.initState();
   }
  }
  ```

  >?それ以降のステップは、このステップでawaitの初期化が完了した後にのみ実行できます。

  #### テストユーザーのログイン

  1. この時点で、最初にコンソール上で作成したテストアカウントを使用して、ログイン検証を完了することが可能です。
  2. [`_coreInstance.login`](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitCore/login.html)メソッドを呼び出して、テストアカウントにログインします。

  ```dart
  import 'package:tencent_cloud_chat_uikit/tencent_cloud_chat_uikit.dart';
  
  final CoreServicesImpl _coreInstance = TIMUIKitCore.getInstance();
  _coreInstance.login(userID: userID, userSig: userSig);
  ```

  >? このアカウントは開発テストのみに使用します。アプリケーションのリリース前の`UserSig`の正しい発行方法は、サーバーで生成し、Appのインターフェース向けに提供する方法となります。`UserSig`が必要なときは、Appから業務サーバーにリクエストを送信し動的に`UserSig`を取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/1047/34385)をご参照ください。

  #### 実装：セッションリストページ

  セッションリストをIM機能のトップページにし、チャット記録のあるすべてのユーザーとのセッションおよびグループチャットセッションをカバーすることができます。

  <img style="width:300px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/279da6d5d41ec1ce0b0cf7fca9a697b8.jpg" />

  `Conversation`クラスを作成してください。`body`では、[`TIMUIKitConversation`](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitConversation/)コンポーネントを使用してセッションリストをレンダリングします。

  具体的なセッションチャットページにリダイレクトするためのナビゲーションに用いる、`onTapItem`イベントの処理関数を渡すだけです。`Chat`クラスに関しては、次の手順で説明します。

  ```dart
  import 'package:flutter/material.dart';
  import 'package:tencent_cloud_chat_uikit/tencent_cloud_chat_uikit.dart';
  
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

  `Chat`クラスを作成してください。`body`では、[`TIMUIKitChat`](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitChat/)コンポーネントを使用して、チャットページをレンダリングします。

  連絡先の詳細情報ページへのリダイレクトに用いる、`onTapAvatar`イベントの処理関数を渡すとよいでしょう。`UserProfile`クラスに関しては、次の手順で説明します。

  ```dart
  import 'package:flutter/material.dart';
  import 'package:tencent_cloud_chat_uikit/tencent_cloud_chat_uikit.dart';
  
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

  `UserProfile`クラスを作成してください。`body`では、[`TIMUIKitProfile`](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitProfile/)コンポーネントを使用して、ユーザーの詳細およびリレーションシップチェーンページをレンダリングします。

  >? このページをカスタマイズしたい場合は、[`profileWidgetBuilder`](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitProfile/ProfileWidgetBuilder.html)でカスタマイズが必要なprofileを渡すことを優先し、`profileWidgetsOrder`に合わせて垂直方向の配置順序を決定します。満足できない場合は、`builder`を使用できます。

  <img style="width:300px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/5f2e67ffb31adc738165e2c4ce58218c.jpg" />

  ```dart
  import 'package:flutter/material.dart';
  import 'package:tencent_cloud_chat_uikit/tencent_cloud_chat_uikit.dart';
  
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

  - [TIMUIKitContact](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitContact/)：連絡先リストページです。
  - [TIMUIKitGroupProfile](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitGroupProfile/)：グループ情報ページです。使用方法は`TIMUIKitProfile`と基本的に同じです。
  - [TIMUIKitGroup](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitGroup/)：グループリストインターフェースです。
  - [TIMUIKitBlackList](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitBlackList/)：ブラックリストインターフェースです。
  - [TIMUIKitNewContact](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/TIMUIKitNewContact/)：連絡先（友達）申請リストです。小さな赤い点を外部に表示する必要がある場合は、監視を自動的にマウントする`TIMUIKitUnreadCount`小さな赤い点コンポーネントを使用できます。
  - [ローカル検索](https://intl.cloud.tencent.com/document/product/1047/50036)：`TIMUIKitSearch`グローバル検索コンポーネントです。連絡先/グループ/チャット記録のグローバル検索をサポートし、`TIMUIKitSearchMsgDetail`を使用して特定のセッションでチャット記録を検索することもサポートします。2つのモードは、`conversation`が渡されるかどうかによって異なります。

  UIコンポーネントの概要は、[このグラフィックとテキストの概要](https://intl.cloud.tencent.com/document/product/1047/50059)または[詳細のドキュメント](https://comm.qq.com/im/doc/flutter/uikit-sdk-api/)をご参照ください。

  [](id:part5)

  ## ソリューション3：UI統合の自己実装

  ### 前提条件

  Flutterプロジェクトの作成が完了している、またはベースになるFlutterプロジェクトがすでにあること。

  ### 統合の手順

  #### IM SDKのインストール

  [このセグメントの詳細なドキュメント](https://intl.cloud.tencent.com/document/product/1047/46264)

  次のコマンドを使用して、Flutter IM SDKの最新バージョンをインストールします。

  コマンドラインでの実行：

  ```shell
  flutter pub add tencent_cloud_chat_sdk
  ```

  >?
  >プロジェクトが[Web](#web)または[デスクトップ端末(macOS、Windows)](#pc)も対象とする場合は、いくつかの追加手順が必要です。詳細については、それぞれのリンクをご参照ください。

  #### SDKの初期化完了

  [このセグメントの詳細なドキュメント](https://intl.cloud.tencent.com/document/product/1047/47966)

  `initSDK`を呼び出して、SDKの初期化を完了します。

  お客様の`sdkAppID`を渡します。

  ```Dart
  import 'package:tencent_cloud_chat_sdk/enum/V2TimSDKListener.dart';
  import 'package:tencent_cloud_chat_sdk/enum/log_level_enum.dart';
  import 'package:tencent_cloud_chat_sdk/tencent_cloud_chat_sdk.dart';
  TencentImSDKPlugin.v2TIMManager.initSDK(
    sdkAppID: 0, // Replace 0 with the SDKAppID of your IM application when integrating
    loglevel: LogLevelEnum.V2TIM_LOG_DEBUG, // Log
    listener: V2TimSDKListener(),
  );
  ```

  このステップでは、IM SDKに対して、ネットワーク状態やユーザー情報の変更などを含むいくつかの監視をマウントできます。詳細については、[このドキュメント](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/enum_V2TimSDKListener/V2TimSDKListener-class.html)をご参照ください。

  #### テストユーザーのログイン

  [このセグメントの詳細なドキュメント](https://intl.cloud.tencent.com/document/product/1047/47969)

  この時点で、最初にコンソール上で作成したテストアカウントを使用して、ログイン検証を完了することが可能です。

  `TencentImSDKPlugin.v2TIMManager.login`メソッドを呼び出し、テストアカウントにログインします。

  戻り値`res.code`が0の場合、ログインは成功です。

  ```dart
  import 'package:tencent_cloud_chat_sdk/tencent_cloud_chat_sdk.dart';
  V2TimCallback res = await TencentImSDKPlugin.v2TIMManager.login(
    userID: userID,
    userSig: userSig,
  );
  ```

  >? このアカウントは開発テストのみに使用します。アプリケーションのリリース前の`UserSig`の正しい発行方法は、`UserSig`の計算コードをサーバーに統合し、Appのインターフェース向けに提供する方法となります。`UserSig`が必要なときは、Appから業務サーバーにリクエストを送信し動的に`UserSig`を取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/1047/34385)をご参照ください。

  #### メッセージの送信

  [このセグメントの詳細なドキュメント](https://intl.cloud.tencent.com/document/product/1047/47992)

  ここでは、テキストメッセージの送信を例に挙げます。そのフローは次のとおりです：

  1. `createTextMessage(String)`を呼び出してテキストメッセージを作成します。
  2. 戻り値に基づいて、メッセージIDを取得します。
  3. `sendMessage()`を呼び出して、このIDのメッセージを送信します。`receiver`には、その前に作成した別のテストアカウントIDを入力できます。シングルチャットメッセージを送信する場合は`groupID`の入力は不要です。

  サンプルコード：

  ```dart
  import 'package:tencent_cloud_chat_sdk/tencent_cloud_chat_sdk.dart';
  
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
  >[このリンクをクリック](https://console.cloud.tencent.com/im/login-message)して、フレンドリレーションシップチェーンのチェックを無効にしてください。

  #### セッションリストの取得

  [このセグメントの詳細なドキュメント](https://intl.cloud.tencent.com/document/product/1047/48324)

  前の手順でテストメッセージの送信が完了しましたので、別のテストアカウントでログインし、セッションリストをプルできるようになりました。
  <img style="width:300px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/e2fdd7632ebc0c5cde68c91afa914201.jpg" />

  セッションリストの取得には2つの方法があります：

  1. 長時間接続コールバックを監視し、セッションリストをリアルタイムに更新します。
  2. APIをリクエストし、ページごとに一括でセッションリストを取得します。

  一般的なユースケースは次のようなものがあります：

  アプリケーションの起動後すぐにセッションリストを取得し、その後は長時間接続を監視して、セッションリストの変更をリアルタイムに更新します。

  ##### セッションリストの一括リクエスト

  セッションリストを取得するためには`nextSeq`を保守し、現在の位置を記録する必要があります。

  ```dart
  import 'package:tencent_cloud_chat_sdk/tencent_cloud_chat_sdk.dart';
  
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

  1. 監視をマウントします。
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
  import 'package:tencent_cloud_chat_sdk/tencent_cloud_chat_sdk.dart';
  
  List<V2TimConversation> _conversationList = [];
  
  _onConversationListChanged(List<V2TimConversation> list) {
    for (int element = 0; element < list.length; element++) {
      int index = _conversationList.indexWhere(
          (item) => item!.conversationID == list[element].conversationID);
      if (index > -1) {
        _conversationList.setAll(index, [list[element]]);
      }else{
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

  サンプルコードは次のとおりです：

  ```dart
  import 'package:tencent_cloud_chat_sdk/tencent_cloud_chat_sdk.dart';
  
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

  リスナーをバインドするサンプルコードは次のとおりです：

  ```dart
  import 'package:tencent_cloud_chat_sdk/tencent_cloud_chat_sdk.dart';
  
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

  続いて、[グループ](https://intl.cloud.tencent.com/document/product/1047/48169)、[ユーザー個人情報](https://intl.cloud.tencent.com/document/product/1047/48160)、[リレーションシップチェーン](https://intl.cloud.tencent.com/document/product/1047/48157)、[オフラインプッシュ](https://www.tencentcloud.com/document/product/1047/46306)、[ローカル検索](https://intl.cloud.tencent.com/document/product/1047/48135)などの関連機能の開発を完了することができます。

  詳細については、[UI統合SDKの自己実装ドキュメント](https://www.tencentcloud.com/document/product/1047/34299)をご確認ください。

  ## 高度な機能統合

  ### その他のプラグインを使用してFlutter IM使用体験を強化

  SDKとTUIKitの基本的な機能に加えて、IM機能を強化するのに役立つ4つのオプションのプラグインも提供しています。

  - [メッセージプッシュプラグイン](https://intl.cloud.tencent.com/document/product/1047/50032)：メーカーのネイティブオフラインプッシュ機能およびオンラインプッシュ機能をサポートし、その他の業務メッセージのプッシュもサポートし、メッセージの到達率を向上させることができます。
  - 統合コードについては、[Demo](https://github.com/TencentCloud/tc-chat-demo-flutter/blob/main/lib/src/pages/app.dart)をご参照ください。

  >?良いアイデアや提案があれば、気軽に[お問い合わせ](https://www.tencentcloud.com/contact-us)ください。

  [](id:more)

  ## その他のプラットフォームを展開

  Tencent Cloud IM for Flutter関連SDKは、デフォルトでAndroid / iOSプラットフォームをサポートします。その他のプラットフォーム(Web/Desktop)を展開するには、この部分をご参照ください。

  ### Flutter for Webサポート[](id:web)

  SDK、TUIKit(tencent_cloud_chat_uikit) 0.1.5バージョンは、UIなし SDK(tencent_cloud_chat_sdk) 4.1.1+2とそれ以降のバージョンは、Webとの完全な互換性があります。

  AndroidとiOS端末と比べて、いくつかの追加手順が必要です。次のとおりです：

  #### Flutter 3.xバージョンをアップグレード

  Flutter 3.xバージョンは、Web性能をさらに最適化します。これを使用してFlutter Webプロジェクトを開発することを強くお勧めします。

  #### Flutter for Webを導入してSDKを追加

  ```dart
  flutter pub add tencent_im_sdk_plugin_web
  ```

  #### JSを導入

  >?既存のFlutterプロジェクトがWebをサポートしない場合は、ルートディレクトリで`flutter create .`を実行してWebサポートを追加してください。
  >

  プロジェクトの`web/`に進み、`npm`または`yarn`を使用して関連するJSの依存関係をインストールします。プロジェクトを初期化するときは、画面指示に従って進めてください。

  ```shell
  cd web
  
  npm init
  
  npm i tim-js-sdk
  
  npm i tim-upload-plugin
  ```

  `web/index.html`を開き、`<head> </head>`にJSファイルを導入します。次のとおりです。

  ```html
  <script src="./node_modules/tim-upload-plugin/index.js"></script>
  <script src="./node_modules/tim-js-sdk/tim-js-friendship.js"></script>
  ```

  ![](https://qcloudimg.tencent-cloud.cn/raw/a4d25e02c546e0878ba59fcda87f9c76.png)

  ### Flutter for Desktop(PC) サポート[](id:pc)

  UIなしSDK(tencent_cloud_chat_sdk) 4.1.9とそれ以降のバージョンは、macOS、Windows端末との完全な互換性があります。AndroidとiOS端末と比べて、いくつかの追加手順が必要です。次のとおりです：

  #### Flutter 3.xバージョンをアップグレード

  Flutter 3.0以降のバージョンにのみ、desktop端末のパッケージが適用されるため、使用する必要がある場合は、Flutter 3.xバージョンにアップグレードしてください。

  #### Flutter for Desktopを導入してSDKを追加

  ```dart
  flutter pub add tencent_im_sdk_plugin_desktop
  ```

  #### macOS修正

  `macos/Runner/DebugProfile.entitlements`ファイルを開きます。

  `<dict></dict>`に次の`key-value`キーと値のペアを追加します。

  ```
  <key>com.apple.security.app-sandbox</key>
  <false/>
  ```

  ## よくあるご質問

  ### iOS側のPod依存関係を正常にインストールできません

  #### **試行ソリューション1：**設定を実行した後、エラーが発生した場合は、**Product** > **Clean Build Folder**をクリックし、生成物を削除してから再度`pod install`または`flutter run`を行うことができます

  ![](https://qcloudimg.tencent-cloud.cn/raw/d495b2e8be86dac4b430e8f46a15cef4.png)

  #### **試行ソリューション2：**`ios/Pods`フォルダおよび`ios/Podfile.lock` ファイルを手動で削除し、次のコマンドを実行して、依存関係を再インストールします

  1. M1など、新規Apple SiliconのMacデバイスを搭載します。
  ![](https://staticintl.cloudcachetci.com/yehe/backend-news/vAsQ099_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_327a198c-bc61-433a-991f-0124e7b0d2e2.png)
  ```shell
  cd ios
  sudo arch -x86_64 gem install ffi
  arch -x86_64 pod install --repo-update
  ```
  2. 古いIntelチップのMacデバイスを搭載します。
  ```shell
  cd ios
  sudo gem install ffi
  pod install --repo-update
  ```

  ### Apple Watchを装着した際、 実機デバッグでiOSのエラーが発生します

  ![](https://qcloudimg.tencent-cloud.cn/raw/1ffcfe39a18329c86849d7d3b34b9a0e.png)

  Apple Watchを機内モードに設定し、iPhoneのBluetooth機能を`設定 => Bluetooth`で完全にオフにしてください。

  Xcodeを再起動し（オンになっている場合）、再び`flutter run`を実行します。

  ### Flutter環境の問題

  Flutterの環境に問題のないことを確認する場合、Flutter doctorを実行してFlutter環境が適切にインストールされているかチェックしてください。

  ### Flutterを使用して自動生成したプロジェクトをTUIKitにインポートし、Android端末で実行するとエラーが発生します

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

  ### エラーコードのクエリー方法

  - IM SDKのAPIレベルのエラーコードについては、[このドキュメント](https://intl.cloud.tencent.com/document/product/1047/34348)をご確認ください。
  - TUIKitのシナリオコードは、インターフェースポップアップ表示に使用されます。[onTUIKitCallbackListener監視](https://intl.cloud.tencent.com/document/product/1047/50054#callback)を通じて取得します。すべてのシナリオコードリストについては、[このドキュメント](https://intl.cloud.tencent.com/document/product/1047/50054#infoCode)をご確認ください。
