このサンプルプロジェクトはUnity内でTRTC SDKのクイックインテグレーションを行い、ゲーム中のオーディオビデオ通話を実現する方法を示しています。

このサンプルプロジェクトには以下の機能が含まれています。
- 通話の参加および通話からの退出。
- ビデオレンダリングのカスタマイズ。
- デバイス管理、音楽の特殊効果および声の特殊効果。

>?
>
>- 具体的なAPI機能パラメータの説明については、[Unity API概要](https://intl.cloud.tencent.com/zh/document/product/647/40139)をご参照ください。
- Unityの推奨バージョン： 2020.2.1f1c1。
- 現在、Android、iOS、Windows、Mac（Macはベータ版テスト中です）プラットフォームをサポートしています。
- `Android Build Support`、`iOS Build Support`、`Winodows Build Support`および`MacOs Build Support`モジュールが含まれている必要があります。
- その内、iOS端末の開発には以下が必要です。
  - Xcode 11.0およびそれ以降のバージョン。
  - プロジェクトが有効な開発者による署名を設定済みであることを確認してください。

## サンプル実行の順序
[](id:step1)
### 手順1：アプリケーションの新規作成
1．TRTCコンソールにログインし、【開発支援】>【[Demoクイックスタート](https://console.cloud.tencent.com/trtc/quickstart)】を選択します。
2．【今すぐ開始】をクリックし、`TestTRTC`などのアプリケーション名を入力して、【アプリケーションの作成】をクリックします。
![](https://main.qcloudimg.com/raw/7178fb5203b8c1ad9eb4a3b7a3c008d7.png)

[](id:step2)
### 手順2： SDKとソースコードのダウンロード
1. 自分の実際の業務ニーズに応じて、SDKおよび付属する[Demoソースコード](https://tccweb-1258344699.cos.ap-nanjing.myqcloud.com/sdk/trtc/unity/TRTCUnitySDK.zip)をダウンロードします。
2. ダウンロード完了後、【ダウンロードしました。次のステップ】をクリックします。（直接Unityを使用してこのプロジェクトを開くことができます。直接SDKファイルを使用する場合は、SDKパッケージ内の`TRTCUnitySDK/Assets/TRTCSDK/SDK`フォルダを自分のプロジェクトAssetsディレクトリ下にコピーすることができます）

3. `Assets/TRTCSDK/Demo/Tools/GenerateTestUserSig.cs`ファイルを見つけて開きます。
4. `GenerateTestUserSig.cs`ファイルの関連パラメータを設定します。
  <ul><li>SDKAPPID：デフォルトは0。実際のSDKAppIDを設定してください。</li>
  <li>SECRETKEY：デフォルトは空文字列。実際のキー情報を設定してください。</li></ul> 
	<img src="https://main.qcloudimg.com/raw/4dad4541a4a0d400441e9cd75c07ba1e.png"/>

[](id:step3)
### 手順3：コンパイル実行
<dx-tabs>
::: Android\sプラットフォーム
1. Unity Editorを設定して、【File】>【Build Setting】をクリックし、Androidに切り替えます。
![](https://main.qcloudimg.com/raw/4464eb891829e3505a59c8ec00cc2414.png)
2. Androidの実機に接続して、【Build And Run】をクリックすると、Demoを実行できます。
3. インターフェーステストでは、まずenterRoomの呼び出しをクリックしてから他の関連テストを実行します。データ表示ウィンドウには呼び出しのクリックが成功したことが表示され、もう1つのウィンドウには呼び出した情報が表示されます。
:::
::: iOS\sプラットフォーム
1. Unity Editorを設定して、【File】>【Build Setting】をクリックし、iOSに切り替えます。
![](https://main.qcloudimg.com/raw/3a0ef43000fe53e8e7ff58b6cc243785.png)
2. iPhoneの実機に接続して、【Build And Run】をクリックします。1つの新しいディレクトリを選択して、コンパイルされたiOSプロジェクトに保存する必要があります。コンパイルが終了すると、新しいウィンドウにXcodeプロジェクトが表示されます。
:::
::: Windows\sプラットフォーム
1. Unity Editorを設定して、【File】>【Build Setting】をクリックし、`PC, Mac & Linux Standalone`に切り替え、Target PlatformにWindowsを選択します。
![](https://main.qcloudimg.com/raw/580764f661c06cf71c4952727c409c5e.png)
2. 【Build And Run】をクリックすると、Demoを実行できます。
:::
::: macOS\sプラットフォーム
1. Unity Editorを設定して、【File】>【Build Setting】をクリックし、`PC, Mac & Linux Standalone`に切り替え、Target PlatformにmacOSを選択します。
![](https://main.qcloudimg.com/raw/6f3f9c21aa9eeadd7a4e3be377b2a6b3.png)
2. 【Build And Run】をクリックすると、Demoを実行できます。
3. Unity Editorエミュレーターランタイムを使用して、最初に`Device Simulator Package`をインストールします。
4. 【Window】>【General】>【Device Simulator】をクリックします
![](https://main.qcloudimg.com/raw/79f707b89553528956a888f48b4d4d6d.png)
:::
</dx-tabs>


[](id:demo)
## Demoサンプル
Demo内にはアップロード済みのAPIの大部分が含まれており、テストおよび参考のために呼び出すことができます。APIドキュメントについては[SDK API（Unity）](https://intl.cloud.tencent.com/zh/document/product/647/40139)をご参照ください。
>? UIは部分的に調整され更新される可能性があります。最新バージョンを基準としてください。

![](https://main.qcloudimg.com/raw/2ce3ab51c6fdc843c1e8b086b55840c0.png)

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
