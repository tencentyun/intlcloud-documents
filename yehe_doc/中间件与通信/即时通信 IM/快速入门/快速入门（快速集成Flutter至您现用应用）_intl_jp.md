1. [](id:toc)
   このドキュメントを読むと、既存のAndroid/iOSネイティブ開発プロジェクトに、Tencent Cloud IM Flutterを統合する方法を知ることができます。

   Flutterを使って既存のアプリケーションを書き換えるのは現実的ではない場合もあります。既存のAPPで、Tencent Cloud IMの機能を使用したい場合は、Flutterモジュールをネイティブ開発APPプロジェクトに組み込むハイブリッド開発スキームをお勧めします。

   **作業量を大幅に削減し、IM通信機能をデュアルエンドのネイティブAPPに速やかに組み込むことができます。**

   ![](https://qcloudimg.tencent-cloud.cn/raw/0a54bc281851a147b0f034a74c6001e5.png)

   ## 環境要件

   | 環境                  | バージョン                                                   |
   | --------------------- | ------------------------------------------------------------ |
   | Flutter               | SDKの最低要件はFlutter 2.2.0バージョン、TUIKit統合コンポーネントリポジトリの最低要件はFlutter 2.10.0バージョンです。 |
   | Android               | Android Studio 3.5以降のバージョン。Appの要件はAndroid 4.1以降のバージョンのデバイスです。 |
   | iOS                   | Xcode 11.0以降のバージョン。プロジェクトに有効な開発者署名を設定済みであることを確認してください。 |
   | Tencent Cloud　IM SDK | [tencent_im_sdk_plugin](https://pub.dev/packages/tencent_im_sdk_plugin) 5.0以降、 [tim_ui_kit](https://pub.dev/packages/tim_ui_kit) 0.2以降。 |

   >?
   >
   >　上記のDemoプロジェクトのソースコードは、[GitHubウェアハウス](https://github.com/TencentCloud/tencentchat-add-flutter-to-app)にありますので、ぜひご利用ください。

   ##　始める前に知るべきこと

   始める前に、Tencent CloudのIM Flutter SDKとTUIKitの使用方法、そしてFlutter-ネイティブハイブリッド開発原理を理解しておく必要があります。

   ###　Tencent Cloud IM

   ####　入門全般

   始める前に、Tencent Cloud IM FlutterのSDK構成と使用方法を理解しておく必要があります。

   主に、[UIなしバージョン](https://cloud.tencent.com/document/product/269/68823#.E7.AC.AC.E4.BA.94.E9.83.A8.E5.88.86.EF.BC.9A.E8.87.AA.E5.AE.9E.E7.8E.B0-ui-.E9.9B.86.E6.88.90)と[UIありコンポーネントライブラリ](https://cloud.tencent.com/document/product/269/70747)の2つのSDKがあります。このドキュメントでは、[UIありコンポーネントライブラリ（TUIKit）](https://cloud.tencent.com/document/product/269/70747)を例に、ハイブリッド開発スキームを紹介します。

   **Tencent CloudのIM Flutterの詳細な使用方法については、[クイックスタートドキュメント](https://cloud.tencent.com/document/product/269/68823)をご参照ください。**

   [](id:modules)

   #### 2つのモジュール

   Tencent Cloud IMには主にChatチャットモジュールとCall通話モジュールの2つの部分があります。

   Chatモジュールには主にメッセージ受送信、セッション管理、ユーザー関係管理などが含まれます。

   Call通話モジュールは主に、一対一通話とグループでの複数人トークを含むオーディオ・ビデオ通話があります。

   ###　Flutterハイブリッド開発

   核となる原理は、module形式のFlutterプロジェクトを、Native側の実行可能プログラムとしてパッケージ化し、Nativeプロジェクトに組み込むことです。Flutter moduleは共通化されているため、Flutter moduleを1回書くだけでAndroid/iOSアプリに埋め込むことができます。

   既存のアプリケーションでTencent Cloud IM関連ページを表示する必要がある場合は、Flutterを搭載するためのActivity (Android)またはViewController (iOS)を読み込むことができます。

   [Method Channel](https://docs.flutter.dev/development/platform-integration/platform-channels#channels-and-platform-threading)は、現在のユーザ情報の配信、オディオ/ビデオ通話データの配信、オフラインプッシュデータのトリガなど、双方向通信が必要な場合に使用できます。他側のメソッドをトリガするには`invokeMethod`を使用し、他側からのメソッド呼び出しをリッスンするには[プリマウントされたMethod Channel Listener](https://docs.flutter.dev/development/platform-integration/platform-channels#executing-channel-handlers-on-background-threads)を使用します。

   [](id:android)

   ####　AndroidプロジェクトにFlutterモジュールを追加

   [詳しく学ぶ](https://docs.flutter.dev/development/add-to-app/android/project-setup)

   Gradle内の既存のアプリケーションの依存関係としてFlutter moduleを追加します。これを実現するには2つの方式があります。

   ####　Android方式その1：Android Archive (AAR)への依存

   AARメカニズムは、Flutter moduleのパッケージングのための媒介として汎用Android AARを作成します。頻繁にビルドする場合は、ビルド手順が1つ追加されます。

   このオプションは、Flutterライブラリを、AARおよびPOMS Widgetで構成される汎用のローカルMavenリポジトリとしてパッケージ化します。このオプションにより、あなたのチームがFlutter SDKをインストールせずにホストアプリケーションを構築できます。その後、ローカルまたはリモートリポジトリからWidgetを配布できます。

   そのため、オンラインの本番環境でこのソリューションを使用することをお勧めします。

   **具体的な手順：**

   Flutter moduleで次の操作を実行します：

   ```shell
   flutter build aar
   ```

   次に、画面の指示に従って統合を行います。

   ![](https://qcloudimg.tencent-cloud.cn/raw/32e9376de02da10e97a8c54b9ab2b51c.png)

   あなたのアプリケーションには依存関係としてFlutterモジュールが含まれるようになりました。

   #####　Android方式その2：Flutter moduleのソースコードへの依存

   ソースコードのサブプロジェクトメカニズムは、簡単なワンタッチのビルドプロセスですが、Flutter SDKが必要です。これはAndroid Studio IDEプラグインで使われている仕組みです。

   この方式は、あなたのAndroidプロジェクトとFlutterプロジェクトの両方を1ステップで構築できます。このオプションは、2つの部分を同時に処理して高速でイテレーションする場合に便利ですが、あなたのチームがアプリケーションを構築するためのFlutter SDKをインストールする必要があります。

   そのため、開発テスト環境では、本ソリューションを用いることをお勧めします。

   **具体的な手順：**

   Flutter moduleをサブプロジェクトとして、ホストAPPの`settings.gradle`に追加します。

   ```gradle
   // Include the host app project.
   include ':app'                                    // assumed existing content
   setBinding(new Binding([gradle: this]))                                // new
   evaluate(new File(                                                     // new
     settingsDir.parentFile,                                              // new
     'tencent_chat_module/.android/include_flutter.groovy'                // new
   ))                                                                     // new
   ```

   お客様のアプリケーションの`app/build.gradle => dependencies`に、Flutter moduleに対する`implementation`を導入する：

   ```gradle
   dependencies{
     implementation project(':flutter')
   }
   ```

   あなたのアプリケーションには依存関係としてFlutterモジュールが含まれるようになりました。

   [](id:ios)

   ####　iOSプロジェクトにFlutterモジュールを追加

   [詳しく学ぶ](https://docs.flutter.dev/development/add-to-app/ios/project-setup#embed-the-flutter-module-in-your-existing-application)

   既存のアプリケーションにFlutterを埋め込む方法は2つあります。

   #####　iOS方式その1：CocoaPodsとFlutter SDKを埋め込む

   CocoaPods依存関係マネージャを使用し、Flutter SDKをインストールします。この方法では、プロジェクトに携わるすべての開発者がFlutter SDKのバージョンをローカルにインストールする必要があります。

   アプリケーションをXcodeにビルドするだけで、DARTとプラグインコードを埋め込むスクリプトが自動的に実行されます。これにより、Xcode以外で他のコマンドを実行することなく、最新バージョンのFlutterモジュールを高速でイテレーションすることができます。

   そのため、開発テスト環境では、本ソリューションを用いることをお勧めします。

   **具体的な手順：**

   次のコードをPodfileに追加します：

   ```
   // 前のステップで構築したFlutter Moduleのパス
   flutter_chat_application_path = '../tencent_chat_module'
   
   load File.join(flutter_chat_application_path, '.ios', 'Flutter', 'podhelper.rb')
   ```

   Flutterを組み込む[Podfile target](https://guides.cocoapods.org/syntax/podfile.html#target)に対し、`install_all_flutter_pods(flutter_chat_application_path)`を呼び出します。

   ```
   target 'MyApp' do
     install_all_flutter_pods(flutter_chat_application_path)
   end
   ```

   Podfileの`post_install`ブロックで`flutter_post_install(installer)`を呼び出し、[Tencent Cloud IM TUIKit](https://cloud.tencent.com/document/product/269/70747)に必要な権限宣言（マイク/カメラ/アルバムの権限を含む）を行います。

   ```
   post_install do |installer|
     flutter_post_install(installer) if defined?(flutter_post_install)
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

   `pod install`を実行します。
   > ?
   >
   > - `tencent_chat_module/pubspec.yaml`でFlutterプラグインの依存関係を変更する場合は、Flutter　Module目ディレクトリで`flutter pub get`を実行して、`podhelper.rb`スクリプトによって読み込まれたプラグインのリストを更新してください。次に、iOSアプリケーションのルートディレクトリから「pod install」を再度実行します。
   > 　–　Apple Siliconチップarm64アーキテクチャのMacでは、`arch-x86_64 pod install--repo-update`を実行する場合があります。

   `podhelper.rb`スクリプトは、あなたのプラグイン/`Flutter.framework`/`App.framework`を該当するプロジェクトに移植します。

   #####　iOS方式その2：Xcodeにframeworksを埋め込む

   Flutterエンジン、コンパイルされたDARTコード、およびすべてのFlutterプラグインのために必要なフレームワークを作成します。フレームワークを手動で埋め込み、Xcodeで既存のアプリケーションのビルド設定を更新します。

   既存のXcodeプロジェクトを手動で編集することで、必要なframeworkを生成してアプリケーションに埋め込むことができます。あなたのチームメンバーがFlutter SDKとCocoaPodsをローカルにインストールできない場合や、既存のアプリケーションでCocoaPodsを依存関係マネージャとして使用したくない場合に、このように行うことができます。Flutterモジュールでコードを変更するたびに、`flutter buildios-framework`.を実行しなければなりません。

   そこで、オンライン環境でこのソリューションを用いることをお勧めします。

   **具体的な手順：**

   Flutter moduleで、次のコードを実行します。

   次の例では、frameworkを`some/path/MyApp/Flutter/`に生成するとします。

   ```shell
   flutter build ios-framework --output=some/path/MyApp/Flutter/
   ```

   生成されたframeworksをXcodeで既存のアプリケーションに統合します。例えば、`some/path/MyApp/Flutter/Release/`ディレクトリで、frameworksをあなたのアプリケーションのtargetコンパイル設定の「General　>　Frameworks,Libraries,and Embedded Content」の下にドラッグし、「Embed」ドロップダウンリストから「Embed&Sign」を選択することができます。


   ##　ハイブリッド開発オプション

   ハイブリッド開発の統合を行うためにFlutter Module方式を使用することをお勧めします。

   Nativeプロジェクトでは、Flutterエンジンを構築し、FlutterのChatおよびCallモジュールを搭載します。2つのモジュールについては、[こちらをご参照ください](#modules)。

   Flutterエンジンの作成管理には、現在、単一のFlutterエンジンと複数のFlutterエンジンの2つの方法があります。

   | エンジンモード                     | 紹介                                                         | メリット                                                     | デメリット                                                   | Demoソースのダウンロード                                     |
   | ---------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
   | [Flutter単一エンジン](#single)     | ChatモジュールとCallモジュールは、同じFlutterエンジンで搭載されます。 | すべてのFlutterコードの統一的なメンテナンスに便利です。      | Callプラグインにより、電話の着信があった場合には、自動的に着信ページを表示する必要があります。同じエンジンでは、Flutterのあるページに強制的にジャンプする必要があり、体験がよくない。 | [クリックしてダウンロードする](https://github.com/TencentCloud/tencentchat-add-flutter-to-app/tree/main/Single%20Flutter%20Engines) |
   | [Flutterマルチエンジン](#multiple) | ChatモジュールとCallモジュールはそれぞれ異なるFlutterエンジンに搭載され、Flutterエンジングループを使用して両エンジンを一元的に管理します。 | Callプラグインは独立して1つのFlutterエンジンの中に存在し、個別ページで制御されます。着信時に、直接このページをポップアップすることができ、ユーザーの現在のページに影響しないで、比較的好ましい体験を得られます。 | 通話モジュールをフローティングウインドーに最小化することはできません。 | [クリックしてダウンロードする](https://github.com/TencentCloud/tencentchat-add-flutter-to-app/tree/main/Multiple%20Flutter%20Engines) |

   また、Tencent Cloud IM Native SDKとFlutter SDKを組み合わせて使用するソリューションも用意されています。[ユースケースと手順の説明についてはこちらをご参照ください](#native)。[Demoソースのダウンロード](https://github.com/TencentCloud/tencentchat-add-flutter-to-app/tree/main/Initialize%20from%20Native)。

   [](id:multiple)

   ##　ソリューション1：Flutterマルチエンジンソリューション【推奨】

   このソリューションでは、ChatモジュールとCallモジュールはそれぞれ異なるFlutterエンジンから独立しています。

   複数のFlutterエンジンを使用する利点は、各インスタンスが独立したもので、独自の内部ナビゲーションスタック、UI、およびアプリケーションステータスを維持することです。これにより、アプリケーションコード全体の状態維持責任が合理化され、モジュール機能が向上します。

   ![](https://qcloudimg.tencent-cloud.cn/raw/87cc37d846388fb3c66aab6743cfede2.png)

   AndroidとiOSに複数のFlutterエンジンを追加し、主に1つのFlutterEngineGroupクラス（Android API、iOS API）に基づいて複数のFlutterEngine（Flutterエンジン）を構築・管理します。

   このプロジェクトでは、統合されたFlutterEngineGroupに基づいて、ChatモジュールとCallingモジュールを搭載する2つのFlutterEngine（Flutterエンジン）を管理しています。

   [![](https://github.com/TencentCloud/tencentchat-add-flutter-to-app/tree/main/Multiple%20Flutter%20Engines)

   ###　Flutter Moduleの開発

   既存のアプリケーションにFlutterを埋め込むには、まずFlutterモジュールを作成します。

   プロジェクトのルートディレクトリの外層で次を実行します。

   ```
   cd some/path/
   flutter create --template module tencent_chat_module
   ```

   これにより、some/path/tencent_chat_module/にFlutterモジュールプロジェクトが作成されます。このディレクトリでは、`flutter run--debug`や`flutter buildios`など、他のFlutterプロジェクトと同じFlutterコマンドを実行できます。FlutterおよびDartプラグインを使用して、Android Studio、IntelliJまたはVS Codeでこのモジュールを実行することもできます。このプロジェクトには、既存のアプリケーションに埋め込む前にモジュールの単一ビューのサンプルバージョンが含まれています。これは、コードのFlutterのみの部分をテストするのに有効です。

   `tencent_chat_module`モジュールディレクトリ構造は、通常のFlutterアプリケーションに似ています：

   ```
   tencent_chat_module/
   ├── .ios/
   │   ├── Runner.xcworkspace
   │   └── Flutter/podhelper.rb
   ├── lib/
   │   └── main.dart
   ├── test/
   └── pubspec.yaml
   ```

   これで`lib/`に、コードを書くことができるようになりました。

   ####　Flutter libディレクトリを整理

   >?
   >
   >　以下のコード構造は参考までに記載されています。必要に応じてTencent Cloud IM Flutterを導入するために柔軟に構成することができます。

   `lib/`で`call`,`chat`,`common`という3つのディレクトリを作成します。それぞれ通話エンジン、IMエンジン、汎用modelクラスを置くために用いられます。

   ```
   tencent_chat_module/
   ├── lib/
   │   └── call/
   │   └── chat/
   │   └── common/
   ```

   ####　汎用modelクラスモジュール

   以下に示すように、`common/common_model.dart`ファイルを新規作成し、Flutterとネイティブアプリケーションの通信仕様を定義する2つのclassを作成します。

   ```dart
   class ChatInfo {
     String? sdkappid;
     String? userSig;
     String? userID;
   
     ChatInfo.fromJSON(Map<String, dynamic> json) {
       sdkappid = json["sdkappid"].toString();
       userSig = json["userSig"].toString();
       userID = json["userID"].toString();
     }
   
     Map<String, String> toMap(){
       final Map<String, String> map = {};
       if(sdkappid != null){
         map["sdkappid"] = sdkappid!;
       }
       if(userSig != null){
         map["userSig"] = userSig!;
       }
       if(userID != null){
         map["userID"] = userID!;
       }
       return map;
     }
   }
   
   class CallInfo{
     String? userID;
     String? groupID;
   
     CallInfo();
   
     CallInfo.fromJSON(Map<String, dynamic> json) {
       groupID = json["groupID"].toString();
       userID = json["userID"].toString();
     }
   
     Map<String, String> toMap(){
       final Map<String, String> map = {};
       if(userID != null){
         map["userID"] = userID!;
       }
       if(groupID != null){
         map["groupID"] = groupID!;
       }
       return map;
     }
   }
   ```

   #### Chatモジュール

   **まずIMエンジンを作成します。このモジュールのすべてのコードとファイルは`lib/chat`ディレクトリにあります。**

   1.　`model.dart`という名前のグローバル状態管理Modelを新規作成します。
      このModelはTencent Cloud IM Flutterモジュールのマウント、初期化、管理、オフラインプッシュ機能、グローバル状態管理、Nativeとの間の通信の維持を行うために使用されます。
      Chatモジュール全体の中心となるものです。
      詳細コードについてはDemoソースコードをご参照ください。次の3つの部分に重点を置きます：
       -　Future<dynamic>_handleMessage(MethodCall call)：ログイン情報やクリックプッシュイベントなど、Nativeからのイベントを動的に監視します。
       -　Future<void> handleClickNotification(Map<String, dynamic>　msg)：通知をクリックしてイベントを処理します。Nativeからのパススルー、Mapからのデータの取り出し、特定のセッションなど、対応するサブモジュールへジャンプします。
       -　Future<void> initChat()：Tencent Cloud IMを初期化/Tencent Cloud IM/にログイン/オフラインプッシュの初期化とToken送信を完了します。このメゾットはスレッドロック機構を使用し、同時に1つしか実行できなく、初期化が成功した後、繰り返し実行しないことを保証します。

   > ?
   >
   > 　[オフラインプッシュの導入ガイドライン](https://cloud.tencent.com/document/product/269/74605)に従って、ベンダーのオフラインプッシュ機能の導入を完了してから、プッシュTokenを正常に送信し、プッシュ機能を使用してください。

   2.　Chatモジュールのメインエントリー用に新しい`chat_main.dart`ファイルを作成します。
      -　このページは、Flutter Chatモジュールの最初のページでもあります。
      -　Demoで、このページはログインする前に読み込み状態であり、ログインするとセッションリストが表示されます。
      -　また、ここで`didChangeAppLifecycleState`監視とフォアグラウンドバックグラウンド切り替えイベントの送信を行う必要があります。詳細については、[オフラインプッシュプラグインのドキュメント手順5](https://cloud.tencent.com/document/product/269/74605#.E6.AD.A5.E9.AA.A45.EF.BC.9A.E5.89.8D.E5.90.8E.E5.8F.B0.E5.88.87.E6.8D.A2.E7.9B.91.E5.90.AC.3Ca-id.3D.22step_5.22.3E.3C.2Fa.3E)をご参照ください。
      -　詳細コードについて、Demoソースコードをご参照ください。

   3.　[オフラインプッシュプラグイン](https://cloud.tencent.com/document/product/269/74605)機能を単一のインスタンスで管理するために、新しい`push.dart`ファイルを作成します。Tokenの取得・送信/プッシュ権限の取得などの操作に使用されます。詳細コードについてはDemoソースコードをご参照ください。

   4.　TUIKitのセッションモジュールコンポーネント`TIMUIKitConversation`を搭載するための新しい`conversation.dart`ファイルを作成します。詳細コードについてはDemoソースコードをご参照ください。

   5.　TUIKitの履歴メッセージリストを記載し、メッセージモジュールコンポーネント`TIMUIKitChat`を送信するための新しい`chat.dart`ファイルを作成します。
      このページには、「Profile」および「Group Profile」ページにジャンプする機能もあります。
      詳細コードについてはDemoソースコードをご参照ください。

   6.　TUIKitのユーザー情報とリレーショナルチェーン管理モジュールコンポーネント`TIMUIKitProfile`を記載するための新しい`user_profile.dart`ファイルを作成します。詳細コードについてはDemoソースコードをご参照ください。

   7.　TUIKitのグループ情報とグループ管理モジュールコンポーネント`TIMUIKitGroupProfile`を搭載するための`group_profile.dart`ファイルを新規作成します。詳細コードについてはDemoソースコードをご参照ください。

   これで、Chatモジュールの開発が完了しました。最終的な構造は次のとおりです：

   ```
   tencent_chat_module/
   ├── lib/
   │   └── call/
   │       └── chat.dart
   │       └── model.dart
   │       └── chat_main.dart
   │       └── push.dart
   │       └── conversation.dart
   │       └── user_profile.dart
   │       └── group_profile.dart
   │   └── chat/
   │   └── common/
   ```

   #### Callモジュール

   このモジュールは、[オディオビデオ通話プラグイン](https://pub.dev/packages/tim_ui_kit_calling_plugin)によって提供されるオディオビデオ通話機能を搭載するために使用されます。

   このモジュールの中核は、リスナーが新たな通話の招待を受けると、Nativeメソッドを呼び出すことで、自動的に通話ページをポップアップするとともに、Native経由で転送されたChatモジュールからの通話要求を受け、自発的に通話を開始します。

   **まずIMエンジンを作成します。このモジュールのすべてのコードとファイルは`lib/call`ディレクトリにあります。**

   1.　`model.dart`という名前のグローバル状態管理Modelを新規作成します。
      このModelは[オディオビデオ通話プラグイン](https://pub.dev/packages/tim_ui_kit_calling_plugin)のマウント、初期化、管理、グローバル状態管理、Nativeとの間の通信維持を行います。
      Callモジュール全体のコアです。
      詳細コードについてはDemoソースコードをご参照ください。次の2つの部分に重点を置きます。
       -　_onRtcListener=TUICallingListener(...)：通話イベントを定義するリスナーは、Method Channelを介してNative層に通知し、Callモジュールが属するViewController(iOS)/Activity(Android)のフロントエンドを表示するかどうかを動的に制御します。
       -　Future<dynamic>_handleMessage(MethodCall call)：Nativeからのアクティブな通話開始要求、Callモジュールからの呼び出しを動的に監視し、自主的に通話を開始します。

   2.　Callモジュールのメインエントリー用に新しい`call_main.dart`ファイルを作成します。
         このコンポーネントは、[オディオ・ビデオ通話プラグインのバインドに必要なnavigatorKey](https://pub.dev/packages/tim_ui_kit_calling_plugin)を注入するために使用されます。
         詳細コードについてはDemoソースコードをご参照ください。


   ####　各Flutterエンジンのエントリーを設定

   上記の3つのモジュールを開発した後、Flutterエンジンへのエントリーとして、最終的に外部に露出するmainメソッドを完成させます。

   1.　デフォルトのエントリー

   `lib/main.dart`ファイルを開き、`main()`メソッドを空のMaterialAppに変更します。

   このメソッドは、Flutter Moduleへのデフォルトのエントリーとして、Flutterマルチエンジン、FlutterEngineGroupで管理されている背景で、サブFlutter Engineがなければ何もentry pointが設定されない限り、このメソッドは利用されません。

   例えば、このデフォルトの`main()`メソッドは、私たちのシナリオでは使用されていません。

   ```dart
   void main() {
     WidgetsFlutterBinding.ensureInitialized();
   
     runApp(MaterialApp(
       title: 'Flutter Demo',
       theme: ThemeData(
         primarySwatch: Colors.blue,
       ),
       home: Container(),
     ));
   }
   ```

   2.　Chatモジュールのエントリーを設定

   `@pragma('vm:entry-point')`コメントを使用して、このメソッドを`entry-point`としてマークします。メソッド名`chatMain`は、このエントリの名前であり、Nativeでは、対応するFlutterエンジンを作成するためにも使用されます。

   グローバルな`ChangeNotifierProvider`状態管理を使用して、`ChatInfoModel`データとビジネスロジックを維持します。

   ```dart
   @pragma('vm:entry-point')
   void chatMain() {
     // This call ensures the Flutter binding has been set up before creating the
     // MethodChannel-based model.
     WidgetsFlutterBinding.ensureInitialized();
   
     final model = ChatInfoModel();
   
     runApp(
       ChangeNotifierProvider.value(
         value: model,
         child: const ChatAPP(),
       ),
     );
   }
   ```

   3.　Callモジュールのエントリーを設定

   同様に、このエントリーは`callMain`という名前が付けられています。

   グローバルな`ChangeNotifierProvider`状態管理を使用して、`CallInfoModel`データとビジネスロジックを維持します。

   ```dart
   @pragma('vm:entry-point')
   void callMain() {
     // This call ensures the Flutter binding has been set up before creating the
     // MethodChannel-based model.
     WidgetsFlutterBinding.ensureInitialized();
   
     final model = CallInfoModel();
   
     runApp(
       ChangeNotifierProvider.value(
         value: model,
         child: const CallAPP(),
       ),
     );
   }
   ```

   これでFlutter Moduleの部分のDartコードが作成されました。

   次に、Nativeコードの作成を開始します。

   ###　iOS Native開発

   このドキュメントでは、Swift言語を例にします。

   >?
   >
   >　次のコード構造は参照用です。必要に応じて柔軟に設定できます。

   iOSのプロジェクトディレクトリに移動します。

   もし既存のアプリケーションが`MyApp`とし、Podfileがなければ、[CocoaPods入門ガイドライン](https://guides.cocoapods.org/using/using-cocoapods.html)を参照して`Podfile`をプロジェクトに追加してください。

   ####　Flutter Moduleの導入

   ネイティブアプリケーションにFlutter moduleを導入するには、[この部分](#ios)をご参照ください。方式1を使用することをお勧めします。

   ####　iOSプロジェクトで、Flutterエンジンを管理

   ![](https://qcloudimg.tencent-cloud.cn/raw/039ec36a5696f2188f9fa8ab11071210.png)

   **複数のエンジンインスタンスを統合管理する`FlutterEngineGroup`を作成します。**

   `AppDelegate.swift`ファイルに、次のコードを追加します：

   ```swift
   @UIApplicationMain
   class AppDelegate: FlutterAppDelegate {
     lazy var flutterEngines = FlutterEngineGroup(name: "chat.flutter.tencent", project: nil)
     ...
   }
   ```

   **Flutterエンジンを管理する単一のインスタンスオブジェクトを作成します。**

   このSwift単一のインスタンスオブジェクトは、Flutterインスタンスの一元管理に使用され、プロジェクト内のあらゆる場所で直接呼び出すことができます。

   Demoコードのロジックは、新しいルーティングを使用し、ChatのViewControllerを搭載します。CallのViewControllerは、presentとdismissの動的ウィンドウでメンテナンスを行います。

   新しい`FlutterUtils.swift`ファイルを作成し、コードを書きます。この部分の詳細コードについてDemoソースコードをご参照ください。

   重点は次のとおりです：
   -　private override init()：Flutterエンジンの各インスタンスを初期化し、Method Channelを登録し、イベントを監視します。
   -　func reportChatInfo()：Flutter層を初期化してTencent Cloud IMにログインできるよう、ユーザーログイン情報とSDKAPPIDをFlutter Moduleにパススルーします。
   -　func launchCallFunc()：CallのFlutterページを引き上げるために使用されます。Callモジュールが通話招待を受けるときにトリガーされ、またはChatモジュールが自主的な通話を開始するときにトリガーされます。
   - func triggerNotification(msg: String)：iOS　Native層が受信したオフラインプッシュメッセージクリックイベントとそれに含まれるext情報を、JSON String形式でFlutter層にバインドされた監視処理イベントに送信します。例えば、対応するセッションへのオフラインプッシュクリックジャンプを処理するために使用されます。

   **オフラインプッシュクリックイベントの監視と転送**

   オフラインプッシュの初期化/Token送信/クリックイベントに対するセッションジャンプ処理は、Flutter Chatモジュールで行われているので、Native領域はクリック通知イベントのextをパススルーするだけでよいです。

   これは、クリック通知イベントがNativeでブロックされて消費されているため、Flutter層が直接取得することができず、Native経由で転送しなければならないからです。

   `AppDelegate.swift`ファイルに、次のコードを追加します。具体的なコードについてはDemoソースコードをご参照ください。

   ![](https://qcloudimg.tencent-cloud.cn/raw/9c816ae4745e5a8d2b9b1d64167e1fc5.png)

   この時点で、iOS Native層の作成が完了しました。

   ###　Android Native開発

   このドキュメントはKotlin言語を例にします。

   >?
   >
   >　次のコード構造は参照用です。必要に応じて柔軟に設定できます。

   ####　Flutter Moduleの導入

   ネイティブアプリケーションにFlutter moduleを導入するには、[この部分]（#android）をご参照ください。方式2を使用することをお勧めします。

   ####　AndroidプロジェクトでFlutterエンジンを管理

   **Flutterエンジンを管理する単一のインスタンスオブジェクトを作成します。**

   このKotlin単一のインスタンスオブジェクトは、Flutterインスタンスの一元管理に使用され、プロジェクト内のあらゆる場所で直接呼び出すことができます。

   新しい`FlutterUtils.kt`ファイルを作成し、`FlutterUtils`静的クラスを定義します。

   ```kotlin
   @SuppressLint("StaticFieldLeak")
   object FlutterUtils {}
   ```

   **「FlutterEngineGroup」(Flutterエンジングループ)を作成して、複数のエンジンインスタンスを統合管理します。**

   「FlutterUtils.kt」ファイルで、「FlutterEngineGroup」を定義し、各Flutter EngineインスタンスとMethod Channelをセットにして、初期化時に初期化します。

   ```kotlin
   lateinit var context : Context
   lateinit var flutterEngines: FlutterEngineGroup
   private lateinit var chatFlutterEngine:FlutterEngine
   private lateinit var callFlutterEngine:FlutterEngine
   
   lateinit var chatMethodChannel: MethodChannel
   lateinit var callMethodChannel: MethodChannel
   
   // 初期化
   flutterEngines = FlutterEngineGroup(context)
   ...
   ```

   **Flutterエンジンを管理するために使用される単一のオブジェクトを完成させます。**

   Demoコードのロジックは新しいルーティングを使用して、ChatとCallのActivityを搭載することです。

   ChatのActivityはユーザーが自主的に入ったり退出したりします。CallのActivityは、リスナーまたはアクティブな外部発呼で自動的にナビゲーションにより入ったり退出します。

   重点は次のとおりです：
   -　fun init()：Flutterエンジンの各インスタンスを初期化し、Method Channelを登録し、イベントを受信します。
   -　fun reportChatInfo()：Flutter層を初期化してTencent Cloud IMにログインできるよう、ユーザーログイン情報とSDKAPPIDをFlutter Moduleにパススルーします。
   -　fun launchCallFunc()：CallのFlutterページを引き上げるために使用されます。Callモジュールが通話招待を受けるときにトリガーされ、またはChatモジュールが自主的な通話を開始するときにトリガーされます。
   - fun triggerNotification(msg: String)：iOS　Native層が受信したオフラインプッシュメッセージクリックイベントとそれに含まれるext情報を、JSON String形式でFlutter層にバインドされた監視処理イベントに送信します。例えば、対応するセッションへのオフラインプッシュクリックジャンプを処理するために使用されます。

   この単一インスタンスobjectの詳細コードについては、Demoソースコードをご参照ください。

   **マスターエントリー`MyApplication`で、上記のオブジェクトを初期化します**

   `MyApplication.kt`ファイルで単一インスタンスオブジェクトにグロバールcontextを渡し、初期化を実行します。

   ```kotlin
   class MyApplication : MultiDexApplication() {
   
       override fun onCreate() {
           super.onCreate()
           FlutterUtils.context = this // new
           FlutterUtils.init()         // new
       }
   }
   ```

   **オフラインプッシュクリックイベントの監視と転送**

   オフラインプッシュの初期化/Token送信/クリックイベントに対するセッションジャンプ処理は、Flutter Chatモジュールで行われているので、Native領域はクリック通知イベントのextをパススルーするだけでです。

   これは、クリック通知イベントがNativeでブロックされて消費されているため、Flutter層が直接取得することができず、Native経由で転送しなければならないからです。

   >! オフラインプッシュの導入手順はベンダーによって異なるため、このドキュメントではOPPOを例にします。すべてのベンダーの導入方法については[このドキュメント](https://www.tencentcloud.com/document/product/1047/39156)をご参照ください。

   Tencent Cloud IMコンソールでは、OPPOのプッシュ証明書が追加され、`次のアクションをクリック`して`アプリケーション内の指定されたページを開く`を選択し、`アプリケーション内のページ`で`Activity`方式を用いて、オフラインプッシュ情報を処理するためのページを設定します。アプリケーションの最初のページにすることをお勧めします。例えば、Demoは`com.tencent.chat.android.MainActivity`に設定されます。

   ![](https://qcloudimg.tencent-cloud.cn/raw/fd384ea1140199113d01a6650c0c8f3d.png)

   上のコンソールで設定されたオフラインプッシュ用のActivityファイルに、次のコードを追加します。

   このコードの役割は、ベンダーが該当するActivityを引き上げると、BundleからHashMap形式のextメッセージを取り出し、単一のインスタンスオブジェクト中のメソッドをトリガーし、そのメッセージを手動でFlutterに転送することです。具体的なコードについてはDemoソースコードをご参照ください。

   ![](https://qcloudimg.tencent-cloud.cn/raw/2ec45c1a8b3bd952bcb86a8095f91515.png)

   この時点で、Android Native層の作成が完了しました。


   [](id:single)

   ##　ソリューション2：Flutter単一エンジンソリューション

   このソリューションは、ChatモジュールとCallモジュールを、同じFlutterエンジンインスタンスに記述します。

   ![](https://qcloudimg.tencent-cloud.cn/raw/115b917df15da5d84ea6794774a3b080.png)

   この2つのモジュールは、Flutterエンジンを維持するだけで、同時に表示および非表示にすることができます。

   ![](https://github.com/TencentCloud/tencentchat-add-flutter-to-app/tree/main/Single%20Flutter%20Engines)

   ###　Flutter Moduleの開発

   既存のアプリケーションにFlutterを埋め込むには、まずFlutterモジュールを作成します。

   プロジェクトのルートディレクトリの外層で次を実行します。

   ```
   cd some/path/
   flutter create --template module tencent_chat_module
   ```

   これにより、some/path/tencent_chat_module/にFlutterモジュールプロジェクトが作成されます。このディレクトリでは、`flutter run--debug`や`flutter buildios`など、他のFlutterプロジェクトと同じFlutterコマンドを実行できます。FlutterおよびDartプラグインを使用して、Android Studio、IntelliJまたはVS Codeでこのモジュールを実行することもできます。このプロジェクトには、既存のアプリケーションに埋め込む前にモジュールの単一ビューのサンプルバージョンが含まれています。これは、コードのFlutterのみの部分をテストするのに役立ちます。

   `tencent_chat_module`モジュールディレクトリ構造は、通常のFlutterアプリケーションに似ています。

   ```
   tencent_chat_module/
   ├── .ios/
   │   ├── Runner.xcworkspace
   │   └── Flutter/podhelper.rb
   ├── lib/
   │   └── main.dart
   ├── test/
   └── pubspec.yaml
   ```

   これで`lib/`に、コードを書くことができるようになりました。

   #### main.dart

   `main.dart`ファイルを変更して、[TUIKit](https://cloud.tencent.com/document/product/269/70747)、[オフラインプッシュプラグイン](https://cloud.tencent.com/document/product/269/74605)および[オディオビデオ通話プラグイン](https://pub.dev/packages/tim_ui_kit_calling_plugin)を導入します。

   グローバル状態、我々のIM SDKおよびMethod ChannelとNativeが通信している状態は、`ChatInfoModel`で管理されています。

   Nativeからユーザ情報とSDKAPPIDを受信したら、`_coreInstance.init()`および`_coreInstance.login()`を呼び出してTencent Cloud IMの初期化・ログインを行います。また、オーディオビデオプッシュプラグインおよびオフラインプッシュプラグインを初期化し、プッシュTokenの送信を完了します。

   > ?
   >
   > 　[オフラインプッシュの導入ガイドライン](https://cloud.tencent.com/document/product/269/74605)に従って、ベンダーのオフラインプッシュ機能の導入を完了してから、プッシュTokenを正常に送信し、プッシュ機能を使用してください。

   オディオビデオ通話プラグインの場合は、次の点に注意してください：
   -　リスナーで新しい通話招待を受信したときにNativeメソッドを呼び出すと、Nativeはユーザーが現在Flutterモジュールのページにいるかどうかを検出します。いない場合は、フロントエンドのページを強制的にこのモジュールに調整して着信ページを表示する必要があります。

   オフラインプッシュプラグインの場合は、次の点に注意してください：
   -　通知をクリックしてイベントを処理します。Nativeからのパススルー、Mapからのデータの取り出し、特定のセッションなど、対応するサブモジュールへジャンプします。

   トップページの制作を完了し、ログインしていないときにロードしたアニメーションを表示します。ログインに成功すると、セッション一覧ページが表示されます。

   また、ここで`didChangeAppLifecycleState`の監視とフォアグラウンドバックグラウンド切り替えイベントの送信を完了する必要があります。詳細は[オフラインプッシュプラグインドキュメント手順5](https://cloud.tencent.com/document/product/269/74605#.E6.AD.A5.E9.AA.A45.EF.BC.9A.E5.89.8D.E5.90.8E.E5.8F.B0.E5.88.87.E6.8D.A2.E7.9B.91.E5.90.AC.3Ca-id.3D.22step_5.22.3E.3C.2Fa.3E)をご参照ください。

   詳細コードについてはDemoソースコードをご参照ください。

   ####　他のTUIKitモジュールの導入

   1.　新しい`push.dart`ファイルを作成し、[オフラインプッシュプラグイン](https://cloud.tencent.com/document/product/269/74605)機能を単一のインスタンスで管理します。Tokenの取得・送信/プッシュ権限の取得などの操作に使用されます。詳細コードについてはDemoソースコードをご参照ください。

   2.　TUIKitのセッションモジュールコンポーネント`TIMUIKitConversation`を搭載するための新しい`conversation.dart`ファイルを作成します。詳細コードについてはDemoソースコードをご参照ください。

   3.　TUIKitの履歴メッセージリストを記載し、メッセージモジュールコンポーネント`TIMUIKitChat`を送信するための新しい`chat.dart`ファイルを作成します。
      このページには、「Profile」および「Group Profile」ページにジャンプする機能もあります。
      詳細コードについてはDemoソースコードをご参照ください。

   4.　TUIKitのユーザー情報およびリレーショナルチェーン管理モジュールコンポーネント`TIMUIKitProfile`を搭載するための新しい`user_profile.dart`ファイルを作成します。詳細コードについてはDemoソースコードをご参照ください。

   5.　TUIKitのグループ情報とグループ管理モジュールコンポーネント`TIMUIKitGroupProfile`を搭載する`group_profile.dart`ファイルを新規作成します。詳細コードについてはDemoソースコードをご参照ください。

   これで統一されたFlutter Moduleの開発が完了しました。

   ###　iOS Native開発

   このドキュメントでは、Swift言語を例にします。

   >?
   >
   >　次のコード構造は参照用です。必要に応じて柔軟に設定できます。

   iOSのプロジェクトディレクトリに移動します。

   もしあなたの既存のアプリケーションが`MyApp`とし、Podfileがなければ、[CocoaPods入門ガイドライン](https://guides.cocoapods.org/using/using-cocoapods.html)を参照して`Podfile`をプロジェクトに追加してください。

   ####　Flutter Moduleの導入

   ネイティブアプリケーションにFlutter moduleを導入するには、[この部分](#ios)をご参照ください。方式1を使用することをお勧めします。

   ####　iOSプロジェクトで、Flutterエンジンを管理

   **FlutterEngineを作成します。**

   FlutterEngineを作成する場所は、メインアプリケーションのエントリーに固有です。例として、`AppDelegate`内のappの起動時にFlutterEngineを作成し、プロパティとして公開する方法を示しました。

   ```swift
   import UIKit
   import Flutter
   import FlutterPluginRegistrant
   
   @UIApplicationMain
   class AppDelegate: FlutterAppDelegate { // More on the FlutterAppDelegate.
     lazy var flutterEngine = FlutterEngine(name: "tencent cloud chat")
   
     override func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
       // Runs the default Dart entrypoint with a default Flutter route.
       flutterEngine.run();
       GeneratedPluginRegistrant.register(with: self.flutterEngine);
       return super.application(application, didFinishLaunchingWithOptions: launchOptions);
     }
   }
   ```

   **Flutterエンジンを管理する単一のインスタンスオブジェクトを作成します。**

   このSwift単一インスタンスオブジェクトは、Flutter Method Channelを一元管理し、Flutter Moduleと通信するための一連のメソッドを提供し、プロジェクト内のあらゆる場所で直接呼び出すことができます。

   次のようなメソッドがあります：
   -　private override init()：Method Channelを初期化し、イベントリスニングメソッドをバインドします。
   -　func reportChatInfo()：Flutter層を初期化してTencent Cloud IMにログインできるよう、ユーザーログイン情報とSDKAPPIDをFlutter Moduleにパススルーします。
   -　func launchChatFunc()：Flutter Moduleが置かれるViewControllerを引き上げるか、ナビゲーションします。
   - func triggerNotification(msg: String)：iOS　Native層が受信したオフラインプッシュメッセージクリックイベントとそれに含まれるext情報を、JSON String形式でFlutter層にバインドされた監視処理イベントに送信します。例えば、対応するセッションへのオフラインプッシュクリックジャンプを処理するために使用されます。

   詳細コードについてはDemoソースコードをご参照ください。

   **オフラインプッシュクリックイベントの監視と転送**

   オフラインプッシュの初期化/Token送信/クリックイベントに対するセッションジャンプ処理は、Flutter Chatモジュールで行われているので、Native領域はクリック通知イベントのextをパススルーするだけでよい。

   これは、クリック通知イベントがNativeでブロックされて消費されているため、Flutter層が直接取得することができず、Native経由で転送しなければならないからです。

   `AppDelegate.swift`ファイルに、次のコードを追加します。具体的なコードについてはDemoソースコードをご参照ください。

   ![](https://qcloudimg.tencent-cloud.cn/raw/0ea48d21696a1e696ab98091983168f9.png)

   この時点で、iOS Native層の作成が完了しました。

   ###　Android Native開発

   このドキュメントはKotlin言語を例にします。

   >?
   >
   >　次のコード構造は参照用です。必要に応じて柔軟に設定できます。

   ####　Flutter Moduleの導入

   ネイティブアプリケーションにFlutter moduleを導入するには、[この部分]（#android）をご参照ください。方式2を使用することをお勧めします。

   ####　AndroidプロジェクトでFlutterエンジンを管理

   **Flutterエンジンを管理する単一のインスタンスオブジェクトを作成します。**

   このKotlinの単一インスタンスオブジェクトは、Flutter Method Channelの一元管理に使用され、Flutter Moduleと通信するための一連のメソッドを提供し、プロジェクト内のあらゆる場所で直接呼び出すことができます。

   新しい`FlutterUtils.kt`ファイルを作成し、`FlutterUtils`静的クラスを定義します。

   ```kotlin
   @SuppressLint("StaticFieldLeak")
   object FlutterUtils {}
   ```

   **`FlutterEngine`(Flutterエンジン)を作成します。**

   `FlutterUtils.kt`ファイルに`FlutterEngine'を定義し、初期化時に初期化します。

   ```kotlin
   lateinit var context : Context
   private lateinit var flutterEngine:FlutterEngine
   
   // 初期化
   flutterEngine = FlutterEngine(context)
   ```

   **Flutterエンジンを管理するために使用される単一のオブジェクトを完成させます。**

   Demoコードのロジックは新しいルーティングを使用して、ChatとCallのActivityを搭載することです。

   ChatのActivityはユーザーが自主的に入ったり退出したりします。CallのActivityは、リスナーまたはアクティブな外部発呼で自動的にナビゲーションにより入ったり退出します。

   重点に置くところは次のとおりです。
   -　fun init()：Method Channelを初期化し、イベントリスニングメソッドをバインドします。
   -　fun reportChatInfo()：Flutter層を初期化してTencent Cloud IMにログインできるよう、ユーザーログイン情報とSDKAPPIDをFlutter Moduleにパススルーします。
   -　fun launchChatFunc()：Flutter Moduleが置かれるViewControllerに引き上げるか、ナビゲーションします。
   - fun triggerNotification(msg: String)：iOS　Native層が受信したオフラインプッシュメッセージクリックイベントとそれに含まれるext情報を、JSON String形式でFlutter層にバインドされた監視処理イベントに送信します。例えば、対応するセッションへのオフラインプッシュクリックジャンプを処理するために使用されます。

   この単一インスタンスobjectの詳細コードについては、Demoソースコードをご参照ください。

   **マスターエントリー`MyApplication`で、上記のオブジェクトを初期化します**

   `MyApplication.kt`ファイルで単一インスタンスオブジェクトにグロバールcontextを渡し、初期化を実行します。

   ```kotlin
   class MyApplication : MultiDexApplication() {
   
       override fun onCreate() {
           super.onCreate()
           FlutterUtils.context = this // new
           FlutterUtils.init()         // new
       }
   }
   ```

   **オフラインプッシュクリックイベントの監視と転送**

   オフラインプッシュの初期化/Token送信/クリックイベントに対するセッションジャンプ処理は、Flutter Chatモジュールで行われているので、Native領域はクリック通知イベントのextをパススルーするだけでよいです。

   これは、クリック通知イベントがNativeでブロックされて消費されているため、Flutter層が直接取得することができず、Native経由で転送しなければならないからです。

   >! オフラインプッシュの導入手順はベンダーによって異なるため、このドキュメントではOPPOを例にします。すべてのベンダーの導入方法については[このドキュメント](https://cloud.tencent.com/document/product/269/75428)をご参照ください。

   Tencent Cloud IMコンソールでは、OPPOのプッシュ証明書が追加され、`次のアクションをクリック`して`アプリケーション内の指定されたページを開く`を選択し、`アプリケーション内のページ`で`Activity`方式を用いて、オフラインプッシュ情報を処理するためのページを設定します。アプリケーションの最初のページにすることをお勧めします。例えば、Demoは`com.tencent.chat.android.MainActivity`に設定されます。

   ![](https://qcloudimg.tencent-cloud.cn/raw/fd384ea1140199113d01a6650c0c8f3d.png)

   上のコンソールで設定されたオフラインプッシュ用のActivityファイルに、次のコードを追加します。

   このコードの役割は、ベンダーが該当するActivityを引き上げると、BundleからHashMap形式のextメッセージを取り出し、単一のインスタンスオブジェクト中のメソッドをトリガーし、そのメッセージを手動でFlutterに転送することです。具体的なコードについてはDemoソースコードをご参照ください。

   ![](https://qcloudimg.tencent-cloud.cn/raw/2ec45c1a8b3bd952bcb86a8095f91515.png)

   この時点で、Android Native層の作成が完了しました。

   [](id:native)

   ##　追加ソリューション：Native層でTencent Cloud IMの初期化・ログインを行います

   ChatとCallのモジュール機能については、高頻度の単純なユースケースを既存のビジネスロジックに深く組み込みたい場合があります。

   例えば、ゲームシーンについて、対局内で、直接セッションを立ち上げてほしい。

   Flutterを使用して実装された完全な機能Chatモジュールは、APPの重要度の低いサブモジュールであるだけなので、最初から完全なFlutter Moduleを開始することは望ましくありません。

   この時点で、Native層からTencent Cloud IM Native SDKの初期化およびログインメソッドを呼び出すことができます。その後、必要な高頻度で簡単なシナリオで、Tencent Cloud IM Native SDKを直接使用してIn-App Chat機能を構築することができます。

   >?
   >　もちろん、その場合は事前にFlutterでTencent Cloud IMを初期化してログインするという選択肢もありますが、その時点でNative層で再度初期化してログインする必要はなくなります。両方とも一度初期化してログインするだけで、両方のエンドで使用できるようになります。

   Flutter SDKにはNative SDKが組み込まれているため、Native層で再度導入する必要はなく、直接使用できます。

   ###　Native初期化とログイン

   iOS Swiftコードを例に、Native層で初期化してログインする方法を示します。

   ```swift
   import ImSDK_Plus
   
   
   func initTencentChat(){
           if(isLoginSuccess == true){
               return
           }
           let data = V2TIMManager.sharedInstance().initSDK(あなたのSDKAPPID , config: nil);
           if (data == true){
               V2TIMManager.sharedInstance().login(
                   chatInfo.userID,
                   userSig: chatInfo.userSig,
                   succ: {
                       self.isLoginSuccess = true
                       self.reportChatInfo()
                   },
                   fail: onLoginFailed()
               )
           }
   }
   ```

   Native層で、Native SDKを直接使用してビジネス機能モジュールを構築できます。詳細については[iOSクイックスタート]()または[Androidクイックスタート](https://cloud.tencent.com/document/product/269/36838)をご参照ください。

   ###　Flutter TUIKitの初期化

   Native層で初期化・ログインを実行した場合、Flutter層で再度実行する必要はありませんが、TUIKitの`_coreInstance.setDataFromNative()`を呼び出して、現在のユーザ情報を渡す必要があります。

   ```dart
   final CoreServicesImpl _coreInstance = TIMUIKitCore.getInstance();
   _coreInstance.setDataFromNative(userId: chatInfo?.userID ?? "");
   ```
   **コードの詳細については、Demoソースをご参照ください。**

   [![](https://qcloudimg.tencent-cloud.cn/raw/9ab7dc1c98627885eea01ddfd1803bb3.png)](https://github.com/TencentCloud/tencentchat-add-flutter-to-app/tree/main/Initialize%20from%20Native)

   -----

   これにより、Tencent Cloud　IM Flutter-Nativeハイブリッド開発方式のすべてを紹介しました。

   このドキュメントに記載されたソリューションにより、既存のネイティブ開発Android/iOSアプリで、Flutter SDKを使用して、同じFlutterコードセットを使用して、ChatとCallモジュール機能を迅速に移植することができます。

   ご不明の点があれば、いつでもお気軽にお問い合わせをしてください。
   - [Telegram Group](https://t.me/+1doS9AUBmndhNGNl)
   - [WhatsApp Group](https://chat.whatsapp.com/Gfbxk7rQBqc8Rz4pzzP27A)


   ## Reference

   1. [Integrate a Flutter module into your Android project](https://docs.flutter.dev/development/add-to-app/android/project-setup).
   2. [Integrate a Flutter module into your iOS project](https://docs.flutter.dev/development/add-to-app/ios/project-setup).
   3. [Adding a Flutter screen to an iOS app](https://docs.flutter.dev/development/add-to-app/ios/add-flutter-screen?tab=no-engine-vc-swift-tab).
   4. [Multiple Flutter screens or views](https://docs.flutter.dev/development/add-to-app/multiple-flutters).
