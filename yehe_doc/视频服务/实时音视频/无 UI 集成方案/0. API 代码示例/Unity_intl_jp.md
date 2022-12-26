このサンプルプロジェクトはUnity内でTRTC SDKのクイックインテグレーションを行い、ゲーム中のオーディオビデオ通話を実現する方法を示しています。

このサンプルプロジェクトには以下の機能が含まれています。
- 通話の参加および通話からの退出。
- ビデオレンダリングのカスタマイズ。
- デバイス管理、音楽の特殊効果および声の特殊効果。

>?
>- 具体的なAPI機能パラメータの説明については、[Unity API概要](https://intl.cloud.tencent.com/document/product/647/40139)をご参照ください。
>- Unityの推奨バージョン： 2020.2.1f1c1。
>- 現在、Android、iOS、Windows、Mac（Macはベータ版テスト中です）プラットフォームをサポートしています。
>- `Android Build Support`、`iOS Build Support`、`Winodows Build Support`および`MacOs Build Support`モジュールが含まれている必要があります。
>- そのうち、iOS端末の開発には以下が必要です。
   - Xcode 11.0およびそれ以降のバージョン。
   - プロジェクトが有効な開発者による署名を設定済みであることを確認してください。

## 操作手順

### ステップ1：アプリケーションの新規作成

1. TRTCコンソールにログインし、【[アプリケーション管理](https://console.tencentcloud.com/trtc/app)】を選択します。
2. 【アプリケーションの作成】をクリックし、`APIExample`などのアプリケーション名を入力します。すでにアプリケーションを作成している場合は、【既存のアプリケーションを選択】にチェックを入れ、【次のステップ】をクリックします。
   ![](https://qcloudimg.tencent-cloud.cn/raw/6704c9f7eb9e18e422c513cb9a2a3926.png)

### ステップ2：サンプルコードのダウンロード

1. UIなしの統合を選択後、ご自身の業務プラットフォームに合わせて、【[Github](https://github.com/LiteAVSDK/TRTC_Unity/tree/main/TRTC-Simple-Demo)】で、関連するSDKと付属のDemoソースコードをダウンロードします。
2. ダウンロード完了後、【次のステップ】をクリックします。
   ![](https://qcloudimg.tencent-cloud.cn/raw/d28964ad85dddd85833a28310a62d514.png)

### ステップ3：プロジェクトの設定

1. サンプルプロジェクトのクイックスタート段階で【デバッグ段階】を選択します。その後、ご自身のSDKAppID、Secret keyを記録しておきます。
   ![](https://qcloudimg.tencent-cloud.cn/raw/82a45972f2d12763a6dc80eee6c952c0.png)
2. ダウンロードしたサンプルコードを開き、`TRTC-Simple-Demo/Assets/TRTCSDK/Demo/Tools/GenerateTestUserSig.cs`ファイルを見つけて開き、`GenerateTestUserSig.cs`ファイル内の関連パラメータを設定します。
  - SDKAPPID：デフォルトはPLACEHOLDERです。実際のSDKAppIDを設定してください。
  - SECRETKEY：デフォルトはPLACEHOLDERです。実際のSecret keyを設定してください。
3. プロジェクトの設定はこれで完了です。【次のステップ】をクリックしてください。

>?
>- ここで言及したUserSigの発行方法は、クライアントコードにSECRETKEYを設定しますが、この手法のSECRETKEYは逆コンパイルによって逆クラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになります。そのため**この手法は、ローカルのTRTC-Simple-Demoクイックスタートおよび機能デバッグにのみ適しています**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供する方法となります。 UserSigが必要なときは、Appから業務サーバーにリクエストを送信し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://www.tencentcloud.com/document/product/647/35166)をご参照ください。

### ステップ4：コンパイル実行

#### Androidプラットフォーム

1. Unity Editorを設定して、【File】>【Build Setting】をクリックし、Androidに切り替えます。
![](https://main.qcloudimg.com/raw/4464eb891829e3505a59c8ec00cc2414.png)
2. Androidの実機に接続して、【Build And Run】をクリックすると、Demoを実行できます。
3. インターフェーステストでは、まずenterRoomの呼び出しをクリックしてから他の関連テストを実行します。データ表示ウィンドウには呼び出しのクリックが成功したことが表示され、もう1つのウィンドウには呼び出した情報が表示されます。

#### iOSプラットフォーム

1. `TRTC構築設定ツール`（Unityエディタ上部のナビゲーションバーにあります）を開きます
2. `iOSの構築&設定`をクリックし、プロジェクトの生成が完了するのを待ちます
   ![](https://qcloudimg.tencent-cloud.cn/raw/d7aa3153469c10b2dfe35db31bebbbf2.png)
3. 生成したUnity-iPhone.xcodeprojプロジェクトをxcodeで開きます
4. [TRTC基盤sdk](https://comm.qq.com/trtc/TRTC_9.7.0.11440_iOS.zip)をダウンロードし、Generalをクリックし、Frameworks,Libraries,and Embedded Contentを選択し、一番下の「+」のアイコンをクリックして必要な動的ライブラリFFmpeg.xcframework、SoundTouch.xcframeworkを順に追加し、Embed & Signを選択します。
   ![](https://imgcache.qq.com/operation/dianshi/other/unity.ca7b6e717bf7b34e4f08a7e688ff59bf49d92217.png)
5. iOSの実機に接続してデバッグを行います

#### Windowsプラットフォーム

1. Unity Editorを設定して、【File】>【Build Setting】をクリックし、`PC, Mac & Linux Standalone`に切り替え、Target PlatformにWindowsを選択します。
   ![](https://main.qcloudimg.com/raw/580764f661c06cf71c4952727c409c5e.png)
2. 【Build And Run】をクリックすると、Demoを実行できます。

#### macOSプラットフォーム

1. Unity Editorを設定して、【File】>【Build Setting】をクリックし、`PC, Mac & Linux Standalone`に切り替え、Target PlatformにmacOSを選択します。
   ![](https://main.qcloudimg.com/raw/6f3f9c21aa9eeadd7a4e3be377b2a6b3.png)
2. 【Build And Run】をクリックすると、Demoを実行できます。
3. Unity Editorエミュレーターランタイムを使用して、最初に`Device Simulator Package`をインストールします。
4. 【Window】>【General】>【Device Simulator】をクリックします
   ![](https://main.qcloudimg.com/raw/79f707b89553528956a888f48b4d4d6d.png)

[](id:demo)
## Demoサンプル
Demo内にはアップロード済みのAPIの大部分が含まれており、テストおよび参考のために呼び出すことができます。APIドキュメントについては[SDK API（Unity）](https://intl.cloud.tencent.com/zh/document/product/647/40139)をご参照ください。
>? UIは部分的に調整され更新される可能性があります。最新バージョンを基準としてください。

## ディレクトリ構造
```
├─Assets
├── Editor                        // Unityエディタスクリプト
│   ├── BuildScript.cs            // Unityエディタbuildメニュー
│   ├── IosPostProcess.cs         // Unityエディタビルドiosアプリケーションスクリプト
├── Plugins
│   ├── Android                   
│   │   ├── AndroidManifest.xml   //Androidアプリケーションプロファイル
├── StreamingAssets               // Unity Demoオーディオ・ビデオストリーミングファイル
├── TRTCSDK
    ├── Demo                      // UnityサンプルDemo
    ├── SDK                       // TRTC Unity SDK
        ├── Implement             // TRTC Unity SDK実装
        ├── Include               // TRTC Unity SDKヘッダーファイル
        └── Plugins               // TRTC Unity SDKの異なるプラットフォーム基盤を実現
            
```