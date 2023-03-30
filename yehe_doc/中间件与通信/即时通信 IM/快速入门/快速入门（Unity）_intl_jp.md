- [](id:toc)
  このドキュメントを読むことで、Unity SDKを統合する方法を学ぶことができます。

  ## 環境要件

  | 環境    | バージョン                                                   |
  | ------- | ------------------------------------------------------------ |
  | Unity   | 2019.4.15f1以降のバージョン。                                |
  | Android | Android Studio 3.5以降のバージョン。AppはAndroid 4.1以降のバージョンのデバイスが必要です。 |
  | iOS     | Xcode 11.0以降のバージョン。プロジェクトに有効な開発者署名を設定済みであることを確認してください。 |

  ## サポートするプラットフォーム

  UnityのすべてのプラットフォームをサポートするIM SDKの構築に取り組み、1つのコードセットですべてのプラットフォームで実行することを支援します。

  | プラットフォーム | IM SDK                              |
  | ---------------- | ----------------------------------- |
  | iOS              | サポートあり                        |
  | Android          | サポートあり                        |
  | macOS            | サポートあり                        |
  | Windows          | サポートあり                        |
  | [Web](#web)      | サポートあり、1.8.1以降のバージョン |

  >? Webプラットフォームは、いくつかの追加手順を簡単に導入する必要があります。詳細については、このドキュメントの[その5](#web)をご確認ください。

  ##  前提条件

  1. [Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)を行い、[実名認証](https://intl.cloud.tencent.com/document/product/378/3629)が完了していること。
  2. [アプリケーションの作成とアップグレード](https://intl.cloud.tencent.com/document/product/1047/34577)を参照してアプリケーションを作成し、`SDKAppID`を記録していること。

  [](id:part1)

  ## その1：テストユーザーの作成

  [IMコンソール](https://console.cloud.tencent.com/im)でご自分のアプリケーションを選択し、左側ナビゲーションバーで**支援ツール**->**UserSig生成&検証**の順にクリックし、2つのUserIDおよびそれに対応するUserSigを作成します。`UserID`、`署名（Key）`、`UserSig`の3つをコピーし、その後のログインで使用します。

  >? このアカウントは開発テストのみに使用します。アプリケーションのリリース前の`UserSig`の正しい発行方法は、サーバーで生成し、Appのインターフェース向けに提供する方法となります。`UserSig`が必要なときは、Appから業務サーバーにリクエストを送信し動的に`UserSig`を取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/1047/34385)をご参照ください。

  ![](https://main.qcloudimg.com/raw/2286644d987d24caf565142ae30c4392.png)

  [](id:part2)

  ## その2：UnityプロジェクトへのIM SDK統合

  1. UnityからUnityプロジェクトを作成し、プロジェクトのある場所を記録しておきます。
  または、既存のUnityプロジェクトを開きます。
  2. IDE（例：Visual Studio Code）からプロジェクトを開きます。
  ![](https://qcloudimg.tencent-cloud.cn/raw/1a21933037a72a6bd4c8ed14f08c6ca7.png)
  3. ディレクトリに基づいてPackages/manifest.jsonを見つけて次のように依存を修正します：
  ```json
     {
       "dependencies":{
         "com.tencent.imsdk.unity":"https://github.com/TencentCloud/chat-sdk-unity.git#unity"
       }
     }
  ```

  IM SDKの各APIをよりよく理解させるために、[API Example](https://github.com/TencentCloud/tc-chat-sdk-unity/tree/main/Assets/IM_Api_Example)をさらに提供して、各APIの呼び出しと監視のトリガーを示します。

  [](id:part3)

  ## その3：ロードの依存性

  Unity Editorでプロジェクトを開き、依存のロードが完了してから、Tencent Cloud IMのロードが完了したことを確認します。
  ![](https://qcloudimg.tencent-cloud.cn/raw/d98dfb17bbee6c0319e370de6f2ba9dd.jpg)

  [](id:part4)

  ## その5：UI統合の自己実装

  ### 前提条件

  Unityプロジェクトの作成が完了したか、基盤となるUnityプロジェクトが作成されて、Tencent Cloud IM SDKがロードされました。

  ### SDKの初期化完了

  [このセグメントの詳細なドキュメント](https://intl.cloud.tencent.com/document/product/1047/48570)

  `TencentIMSDK.Init`を呼び出して、SDK初期化を完了します。

  お客様の`SDKAppID`を渡します。

  ```c#
  public static void Init() {
    int SDKAppID = 0; // IMコンソールからアプリケーションSDKAppIDを取得します。
    SdkConfig sdkConfig = new SdkConfig();
  
    sdkConfig.sdk_config_config_file_path = Application.persistentDataPath + "/TIM-Config";
  
    sdkConfig.sdk_config_log_file_path = Application.persistentDataPath + "/TIM-Log";
  
    TIMResult res = TencentIMSDK.Init(long.Parse(SDKAppID), sdkConfig);
  }
  ```

  `Init`の後、主にネットワークの状態やユーザー情報の変更など、IM SDK用のいくつかの監視をマウントできます。詳細については、[このドキュメント](https://intl.cloud.tencent.com/document/product/1047/48570)をご参照ください。

  ### テストアカウントのログイン

  [このセグメントの詳細なドキュメント](https://intl.cloud.tencent.com/document/product/1047/48571)

  この時点で、最初にコンソール上で作成したテストアカウントを使用して、ログイン検証を完了することが可能です。

  `TencentIMSDK.Login`メソッドを呼び出して、テストアカウントにログインします。

  戻り値`res.code`が0の場合、ログインは成功です。

  ```c#
  public static void Login() {
    if (userid == "" || user_sig == "")
    {
        return;
    }
    TIMResult res = TencentIMSDK.Login(userid, user_sig, (int code, string desc, string json_param, string user_data)=>{
      // ログインコールバックロジックを処理します
    });
  }
  ```

  >? このアカウントは開発テストのみに使用します。アプリケーションのリリース前の`UserSig`の正しい発行方法は、`UserSig`の計算コードをサーバーに統合し、Appのインターフェース向けに提供する方法となります。`UserSig`が必要なときは、Appから業務サーバーにリクエストを送信し動的に`UserSig`を取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/1047/34385)をご参照ください。

  ### メッセージの送信

  [このセグメントの詳細なドキュメント](https://intl.cloud.tencent.com/document/product/1047/48572)

  ここでテキストメッセージの送信を例に取ります

  サンプルコード：

  ```c#
  public static void MsgSendMessage() {
          string conv_id = ""; // c2cメッセージセッションIDはuserID、グループメッセージセッションIDはgroupIDです
          Message message = new Message
          {
            message_conv_id = conv_id,
            message_conv_type = TIMConvType.kTIMConv_C2C, // グループメッセージはTIMConvType.kTIMConv_Groupです
            message_elem_array = new List<Elem>
            {
              new Elem
              {
                elem_type = TIMElemType.kTIMElem_Text,
                text_elem_content =  "これは通常のテキストメッセージです"
              }
            }
          };
          StringBuilder messageId = new StringBuilder(128);
  
          TIMResult res = TencentIMSDK.MsgSendMessage(conv_id, TIMConvType.kTIMConv_C2C, message, messageId, (int code, string desc,                         string json_param, string user_data)=>{
            // メッセージ送信非同期結果
          });
                // 同期に送信されたメッセージから返されたメッセージID messageId
  }
  ```

  >?送信に失敗した場合、sdkAppIDは知らない人から送信されたメッセージをサポートしていない可能性があります。コンソールで有効にしてからテストに使用されます。
  >
  >[このリンクをクリック](https://console.cloud.tencent.com/im/login-message)して、フレンドリレーションシップチェーンのチェックを無効にしてください。

  ### セッションリストの取得

  [このセグメントの詳細なドキュメント](https://intl.cloud.tencent.com/document/product/1047/50020)

  前の手順でテストメッセージの送信が完了しましたので、別のテストアカウントでログインし、セッションリストを取得できるようになりました。

  セッションリストの取得には2つの方法があります：

  1. 長時間接続コールバックを監視し、セッションリストをリアルタイムに更新します。
  2. APIをリクエストし、ページごとに一括でセッションリストを取得します。

  一般的なユースケースは次のとおりです：

  アプリケーションの起動後すぐにセッションリストを取得し、その後は長時間接続を監視して、セッションリストの変更をリアルタイムに更新します。

  #### セッションリストの一括リクエスト

  ```c#
  TIMResult res = TencentIMSDK.ConvGetConvList((int code, string desc, List<ConvInfo> info_list, string user_data)=>{
   // 非同期ロジックを処理します
  });
  ```

  この時点で、前の手順で別のテストアカウントを使用して送信したメッセージのセッションを見ることができるようになりました。

  #### 長時間接続のリッスンによるセッションリストのリアルタイム取得

  この手順では、先にSDKにリッスンをマウントしてからコールバックイベントを処理し、UIを更新する必要があります。

  1. 監視をマウントします。
  ```c#
  TencentIMSDK.SetConvEventCallback((TIMConvEvent conv_event, List<ConvInfo> conv_list, string user_data)=>{
   // コールバックロジックを処理します
  });
  ```
  2. コールバックイベントを処理し、最新のセッションリストをインターフェース上に表示します。

  ### メッセージの受信

  [このセグメントの詳細なドキュメント](https://intl.cloud.tencent.com/document/product/1047/48573)

  Tencent Cloud IM SDKによるメッセージの受信には2つの方法があります：

  1. 長時間接続コールバックを監視し、メッセージの変更をリアルタイムに取得し、メッセージ履歴リストを更新してレンダリングします。
  2. APIをリクエストし、ページごとに一括でメッセージ履歴を取得します。

  一般的なユースケースは次のとおりです：

  1. インターフェースが新しいセッションに入ると、まず一定量のメッセージ履歴を一括でリクエストし、メッセージ履歴リストの表示に用います。
  2. 長時間接続を監視し、新しいメッセージをリアルタイムに受信してメッセージ履歴リストに追加します。

  #### メッセージ履歴リストの一括リクエスト

  ページごとに取得するメッセージ数が多すぎると取得速度に影響しますので、多すぎてはなりません。20通前後に設定することをお勧めします。

  次のリクエストの際に使用できるよう、現在のページ数を動的に記録しなければなりません。

  サンプルコードは次のとおりです：

  ```c#
  // シングルチャットメッセージ履歴の取得
  // 初めて取得する場合は、msg_getmsglist_param_last_msgをnullに設定します
  // 再度取得する場合は、msg_getmsglist_param_last_msgは、返されたメッセージリストの最後のメッセージを使用できます
  var get_message_list_param = new MsgGetMsgListParam
      {
        msg_getmsglist_param_last_msg = LastMessage
      };
  TIMResult res = TencentIMSDK.MsgGetMsgList(conv_id, TIMConvType.kTIMConv_C2C, get_message_list_param, (int code, string desc, string user_data) => {
    // コールバックロジックを処理します
  });
  ```

  ```c#
  // シングルチャットメッセージ履歴を取得します
  // 初めて取得する場合は、msg_getmsglist_param_last_msgをnullに設定します
  // 再度取得する場合は、msg_getmsglist_param_last_msgは、返されたメッセージリストの最後のメッセージを使用できます
  var get_message_list_param = new MsgGetMsgListParam
      {
        msg_getmsglist_param_last_msg = LastMessage
      };
  TIMResult res = TencentIMSDK.MsgGetMsgList(conv_id, TIMConvType.kTIMConv_Group, get_message_list_param, (int code, string desc, string user_data) => {
    // コールバックロジックを処理します
  });
  ```

  #### 長時間接続の監視による新メッセージのリアルタイム取得

  メッセージ履歴リストを初期化すると、新メッセージは`TencentIMSDK.AddRecvNewMsgCallback`長時間接続から送信されます。

  `AddRecvNewMsgCallback`コールバックがトリガーされると、必要に応じて、メッセージ履歴リストに新しいメッセージを追加できます。

  モニターをバインドするサンプルコードは次のとおりです

  ```c#
  TencentIMSDK.AddRecvNewMsgCallback((List<Message> message, string user_data) => {
    // 新メッセージを処理します
  });
  ```

  この時点で、IMモジュールの開発は基本的に完了し、メッセージの送受信や様々なセッションに入ることが可能になりました。

  続いて、[グループ](https://intl.cloud.tencent.com/document/product/1047/48169)、[ユーザー個人情報](https://intl.cloud.tencent.com/document/product/1047/48859)、[リレーションシップチェーン](https://intl.cloud.tencent.com/document/product/1047/49563)、[ローカル検索](https://intl.cloud.tencent.com/document/product/1047/50066)などの関連機能の開発を完了することができます。

  詳細については、[SDKドキュメントのUI統合の自己実装](https://www.tencentcloud.com/document/product/1047/34299)をご確認ください。

  [](id:part5)

  ## その5：#Unity for WebGLの[](id:web)へのサポート

  Tencent Cloud IM SDK (Unityバージョン)は、バージョン`1.8.1`からWebGLの構築をサポートします。

  AndroidとiOS端末と比べると、いくつかの追加手順が必要です。次のとおりです：

  ### JSの導入インポート

  GitHubから次の3つのJSファイルをダウンロードし、プロジェクトビルドWebGL製品のフォルダーに配置します。

  - [tim-js](https://github.com/TencentCloud/TIMSDK/blob/master/Web/IMSDK/tim-js.js)
  - [tim-js-friendship.js](https://github.com/TencentCloud/TIMSDK/blob/master/Web/IMSDK/tim-js-friendship.js)
  - [このファイルの名前をtim-upload-plugin.jsに変更](https://github.com/TencentCloud/TIMSDK/blob/master/Web/IMSDK/tim-upload-plugin/index.js)
  `index.html`を開き、この3つのJSファイルを導入します。次のとおりです：

  ```html
  <script src="./tim-js.js"></script>
  <script src="./tim-js-friendship.js"></script>
  <script src="./tim-upload-plugin.js"></script>
  ```

  ## よくあるご質問

  #### サポートされているプラットフォームはどれですか？

  現時点ではiOS、Android、Windows MacおよびWebGLをサポートしています。

  #### AndroidでBuild And Runをクリックすると、使用できるデバイスが見つからないというエラーが発生します。

  デバイスが他のリソースに使用されないことを保証するか、またはBuildをクリックしてapkパッケージを生成してから、エミュレーター内にドラッグして実行します。

  #### iOSで初回実行時にエラーが発生します。

  上のDemoで設定を実行した後もエラーが発生する場合、**Product**>**Clean**をクリックし、プロダクトを削除してから改めてBuildするか、またはXcodeをオフにして改めて開いて再度Buildします。

  #### 2019.04バージョンのUnity、iOSプラットフォームでエラーが発生します。

  Library/PackageCache/com.unity.collab-proxy@1.3.9/Editor/UserInterface/Bootstrap.cs(23,20): error CS0117: 'Collab' does not contain a definition for 'ShowChangesWindow'
  Editorツールバーで**Window**>**Package Manager**をクリックし、Unity Collaborateを1.2.16にダウングレードします。

  #### 2019.04バージョンのUnity、iOSプラットフォームでエラーが発生します。

  Library/PackageCache/com.unity.textmeshpro@3.0.1/Scripts/Editor/TMP_PackageUtilities.cs(453,84): error CS0103: The name 'VersionControlSettings' does not exist in the current context
  ソースコードを開き、`|| VersionControlSettings.mode != "Visible Meta Files"`の部分のコードを削除すれば完了です。

  #### エラーコードのクエリー方法

  - IM SDKのAPIレベルのエラーコードについては、[このドキュメント](https://intl.cloud.tencent.com/document/product/1047/34348)をご確認ください。
