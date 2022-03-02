Tencent Cloud Instant Messaging(IM)は、Web IM SDKに基づきHBuilderXでAndroid、iOSにコンパイルしたアプリケーションを正式にリリースし、一連のコードマルチターミナルパッケージ化を実現しました。

## オンラインカスタマーサービスシーン
例示のカスタマーサービスグループ、フレンドといった基本的なテンプレートを提供します。オンラインカスタマーサービスシーンのFeature Packは次のとおりです。
- テキストメッセージ、画像メッセージ、音声メッセージ、ビデオメッセージなどの一般的なメッセージの送信をサポート。
- 常用語、注文、サービスレビューなどカスタムメッセージをサポート。
- グループチャットセッションの作成、グループメンバーの管理などをサポート。


## 操作手順
### 手順1：uni-appアカウントの作成と登録
1. app開発環境を構築し、[HBuilderXエディタ](https://www.dcloud.io/hbuilderx.html)をダウンロードしてください。
>!プロジェクトで現在使用されているのはHBuilderXの最新バージョンです。以前にHBuilderXをダウンロードしている場合は、開発環境の一致を保証するために最新バージョンに更新してください。
2. [DCloud開発者センター](https://dev.dcloud.net.cn/)に登録した後、HBuilderXエディタにログインします。

### 手順2：アプリケーションの作成
1. [IMコンソール](https://console.cloud.tencent.com/im)にログインします。
>?
>- アプリケーションをすでに保有している場合は、そのSDKAppIDを記録してから[キー情報の取得](#step2)を実行してください。
>- 同じTencent Cloudのアカウントで、最大300個のIMアプリケーションを作成することができます。すでにアプリケーションが300個ある場合は、使用する必要のないアプリケーションを[使用停止して削除](https://intl.cloud.tencent.com/document/product/1047/34540)すると、新しいアプリケーションを作成することができます。**アプリケーションを削除した後、そのSDKAppIDに対応するすべてのデータとサービスは失われます。慎重に操作を行ってください。**
>
2. **新しいアプリケーションの作成**をクリックし、**アプリケーションの作成**のダイアログボックスにアプリケーション名を入力し、**OK**をクリックします。
![](https://main.qcloudimg.com/raw/15e61a874a0640d517eeb67e922a14bc.png)
3. SDKAppID情報を保存してください。コンソールの概要ページで、作成したアプリケーションのステータス、サービスバージョン、SDKAppID、作成時間、有効期限を確認できます。
    ![](https://main.qcloudimg.com/raw/7954cc2882d050f68cd5d1df2ee776a6.png)
4. 作成後のアプリケーションをクリックし、左側のナビゲーションバーで**支援ツール**>**UserSig発行&チェック**をクリックすると、UserIDおよびそれに対応するUserSigが作成されます。署名情報をコピーし、後でログインして使用します。
![](https://main.qcloudimg.com/raw/2286644d987d24caf565142ae30c4392.png)
>!キー情報を適切に保管して、漏えいしないようにしてください。

### 手順3：uni-appソースコードのダウンロードと設定
1. 実際のサービス要求に基づいて、SDKと付属の[Demoソースコード](https://intl.cloud.tencent.com/document/product/1047/33996)をダウンロードします。
```javascript
# コマンドラインの実行
git clone https://github.com/tencentyun/TIMSDK.git

# uni-app TUIKitプロジェクトに移動
cd TIMSDK/uni-app/TUIKit
```
2. uni-app中のTUIKitプロジェクトファイルを自身のHBuilderXプロジェクト（バージョン3.2.11.20211021-alpha）にインポートします。公式の[uni-app開発](https://uniapp.dcloud.io/quickstart-hx)をご参照ください。
3. GenerateTestUserSigファイルの関連パラメータを設定します。
- `debug/GenerateTestUserSig.js`ファイルを見つけて開きます。
- `GenerateTestUserSig.js`ファイルの関連パラメータを設定します。
  <ul><li>SDKAPPID：デフォルトは0。実際のSDKAppIDを設定してください。</li>
  <li>SECRETKEY：デフォルトは空文字列。実際のキー情報を設定してください。</li></ul> 
  

>! 
>- ここで言及する`UserSig`の発行方法は、クライアントコードの中での`SECRETKEY`設定となりますが、この手法の`SECRETKEY`は逆コンパイルによって逆クラッキングされやすく、キーがいったん漏洩すると、攻撃者がお客様のTencent Cloudトラフィックを盗用できるようになります。そのため**この手法は、ローカルのuni-appクイックスタートおよび機能デバッグにのみ適しています**。
>- `UserSig`の正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。 UserSigが必要なときは、Appから業務サーバーにリクエストを送信し動的に`UserSig`を取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

###  手順4：コンパイル実行
公式の[uni-app実行](https://uniapp.dcloud.io/quickstart-hx?id=%e8%bf%90%e8%a1%8cuni-app)をご参照ください。

###  手順5：パッケージ化リリース

 公式の[uni-appパッケージ化](https://uniapp.dcloud.io/quickstart-hx?id=%e5%8f%91%e5%b8%83uni-app)をご参照ください。
- ネイティブApp-クラウドパッケージ化：**HBuilderXエディタ**>**発行**>**ネイティブApp**-**クラウドパッケージ化**（appアイコン、起動ページなどの詳細な設定はmanifest.jsonで設定できます）。
- ネイティブApp-オフラインパッケージ化：**HBuilderXエディタ**>**発行**>ローカルパッケージ化Appリソース（詳細なパッケージ化方法については、iOS、Androidローカルパッケージ化ガイドをご参照ください）。

## よくあるご質問
[](id:Q1)
### 1. uni-appが同時にサポートするAndroid、iOS、IM SDKの選択方法。
`tim-wx-sdk`、npmインストールまたは静的インポートを選択してください。
```javascript
    // v2.11.2以降のSDKはWebSocketをサポートしていますので、アクセスをお勧めします。v2.10.2以前のバージョンにはHTTPを使用することをお勧めします
	npm install tim-wx-sdk@2.15.0 --save
	import TIM from 'tim-wx-sdk';
	// SDKインスタンスの作成では、`TIM.create()`方法は同じ`SDKAppID`に同じインスタンスのみを返します。
	uni.$TUIKit = TIM.create({
		SDKAppID: 0 // アクセスするときは、0をお客様のIMアプリケーションのSDKAppIDに置き換える必要があります
	});
	
	// SDKログの出力レベルの設定では、レベル別の詳細はsetLogLevelインターフェースの説明をご参照ください
	uni.$TUIKit.setLogLevel(0); // 通常のレベル。ログ量はやや多く、アクセス時に使用することをお勧めします
	// uni.$TUIKit.setLogLevel(1); // releaseレベル別。SDK出力キーワード情報は、本番環境時での使用をお勧めします
```
プロジェクトにリレーションシップチェーン機能が必要な場合は、`tim-wx-friendship.js`をご使用ください。
```javascript
	import TIM from 'tim-wx-sdk/tim-wx-friendship.js';
```
>?
>- **uni-appのより適切なアクセスにtimを使用し、問題を素早く特定して解決するために、uni.$TUIKitネームを変更しないでください。timにアクセス済みである場合は、uni.timをuni.$TUIKitに変更してください。**
>- IM SDKを[2.15.0](https://intl.cloud.tencent.com/document/product/1047/34281)にアップグレードしてください。このバージョンはiOS音声再生をサポートしています。
>- 依存の同期に問題が発生した場合は、npmソースを切り替えて再試行してください。
```javascript
	cnpmソースの切り替え
	>npm config set registry http://r.cnpmjs.org/
	>
	>
```

[](id:Q2)
### 2. 画像、ビデオ、音声メッセージなどのリッチメディアメッセージのアップロード方法。
`cos-wx-sdk-v5`をご使用ください。
```javascript
    // 画像、音声、ビデオなどのメッセージを送信するにはcos-wx-sdk-v5アップロードプラグインが必要です
	npm install cos-wx-sdk-v5@0.7.11 --save
	import COS from "cos-wx-sdk-v5";
	// COS SDKプラグインの登録
	uni.$TUIKit.registerPlugin({
		'cos-wx-sdk': COS
	});
```

[](id:Q3)
### 3. uni-appパッケージ化iOS音声メッセージが再生できない。
  IM SDKを[2.15.0](https://intl.cloud.tencent.com/document/product/1047/34281)にアップグレードしてください。このバージョンはiOS音声メッセージの再生をサポートしています。

[](id:Q4)
### 4. uni-appパッケージ化app音声メッセージの送信時間が誤って表示される。
   uni-appパッケージ化appは、`recorderManager.onStop`コールバックに`duration`と`fileSize`がありません。ユーザー自身がdurationとfileSizeを追加する必要があります。
- **ローカルタイマーを使用して時間を記録し、durationを計算します。**
- **ファイルのサイズをローカルで計算します。fileSize＝(オーディオビットレート)x時間(単位:秒) / 8、概算。**
詳細なコードについては、[uni-app TUIKit](https://github.com/tencentyun/TIMSDK/tree/master/uni-app)をご参照ください。
>!
>
>- 音声メッセージオブジェクトに`duration`と`fileSize`を含める必要があります。`fileSize`がない場合は、音声メッセージ時間が誤った数字の列になります

[](id:Q5)
###5. videoビデオメッセージレイヤーが高すぎてスワイプできない。
 プロジェクトでは、ビデオ画像が代わりに使用され、`video`は直接レンダリングされません。再生中のレンダリング方式によってレイヤーが高すぎる問題を回避しました。
 詳細なコードについては、[uni-app TUIKit](https://github.com/tencentyun/TIMSDK/tree/master/uni-app)をご参照ください。
>!公式の[ネイティブコンポーネントに関する説明](https://uniapp.dcloud.io/component/native-component)をご参照ください。

[](id:Q6)

### 6. 実機のプレビュー、システムエラーの報告、ボリュームが大きすぎる。
実行時にコード圧縮にチェックを入れ、ミニプログラムエミュレーター>実行時にコードを圧縮するかどうかを実行してください。

[](id:Q7)



## 技術的なお問い合わせ
詳細については[お問い合わせ](https://intl.cloud.tencent.com/zh/contact-us)をご参照ください。

## 参照ドキュメント

- [SDK APIマニュアル](https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html)
- [SDK更新ログ](https://intl.cloud.tencent.com/document/product/1047/34281)
- [uni-app TUIKitソースコード](https://github.com/tencentyun/TIMSDK/tree/master/uni-app)
- [クイックインテグレーションuni-app TUIKitソースコード](https://intl.cloud.tencent.com/document/product/1047/43893)

