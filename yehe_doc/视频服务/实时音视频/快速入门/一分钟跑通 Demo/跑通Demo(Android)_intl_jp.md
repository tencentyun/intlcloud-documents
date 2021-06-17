ここでは、主にTencent CloudのTRTC Demo (Android)を速く操作する方法を紹介します。

## 環境要件
- 最低でもAndroid 4.1 (SDK API Level 16)と互換性を有していますが、Android 5.0 (SDK API Level 21)以上のバージョンを使用されることを推奨します
- Android Studio 3.5以上のバージョン 
- AppではAndroid Studio 4.1以上のデバイスが必要です

## 前提条件
[Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)、及び [実名認証](https://intl.cloud.tencent.com/document/product/378/3629)を完了済みです。

## 操作手順
<span id="step1"></span>
### 手順1：アプリケーションの新規作成
1．Tencent Real-Time Communicationコンソールにログインし、【開発支援】>【[Demoのクイック実行](https://console.cloud.tencent.com/trtc/quickstart)】を選択します。
2．【今すぐ開始】をクリックし、例えば、`TestTRTC`などアプリケーション名を入力して、【アプリケーションの作成】をクリックします。

<span id="step2"></span>
### 手順2：SDKおよびDemoのソースコードをダウンロード
１．マウスを該当するカードまで移動し、【[Github](https://github.com/tencentyun/TRTCSDK/tree/master/Android)】をクリックしてGithub（または【[ZIP](http://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Android_latest.zip?_ga=1.195966252.185644906.1567570704)】をクリック）にジャンプし、関連するSDK および付属のDemoのソースコードをダウンロードします。
 ![](https://main.qcloudimg.com/raw/b0f6f1bd5e0bc083bafddcc7c04a1593.png)
2. ダウンロード完了後、Tencent Real-Time Communicationコンソールに戻り、【ダウンロードしました。次のステップ】をクリックすれば、SDKAppIDおよびキー情報をクエリできます。


<span id="step3"></span>
### 手順3：Demoプロジェクトファイルの設定
1．[手順2]（#step2）でダウンロードしたソースコードパッケージを解凍します。
2.`LiteAVSDK_TRTC_Android_バージョン番号/TRTCScenesDemo/debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java`ファイルを探して開きます。
3．`GenerateTestUserSig.java`ファイルの関連するパラメータを設定します。
  <ul><li>SDKAPPID：デフォルトは PLACEHOLDER、実際のSDKAppIDを設定してください。</li>
  <li>SECRETKEY：デフォルトはPLACEHOLDER、実際のキー情報を設定してください。</li></ul> 
	<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">
4．Tencent Real-Time Communicationコンソールに戻り、【貼り付け完了。次のステップ】をクリックします。
5.【ガイドを閉じてコンソールへ進む】をクリックします。

≻本書で言及した新規UserSigの作成法は、クライアントコードでSECRETKEYを設定し、この手法のうちSECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになり、そのため**のこの手法はローカルDemo実行および機能デバッグにのみ適合します**。
≻ UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。 UserSigが必要なときは、Appから業務サーバーにリクエストを発出し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

### 手順4：コンパイル動作
Android Studio（バージョン3.5以上）を使用してソースコードプロジェクトの`TRTCScenesDemo`を開き、【実行】をクリックします。

## よくあるご質問
### 1. キーをクエリするとき、パブリックキーとプライベートキーの情報しか取得できませんが、キーはどうしたら取得できますか？
TRTC SDK 6.6バージョン（2019年08月）では新しい署名アルゴリズムのHMAC-SHA256の使用を始めています。その前に作成済のアプリケーションは、署名アルゴリズムをアップグレードしないと暗号化したキーを取得できません。アップグレードしなくても、[旧バージョンアルゴリズム ECDSA-SHA256]（https://intl.cloud.tencent.com/document/product/647/35166)は引き続き使用できます。アップグレード済みなら、必要に応じて新旧アルゴリズムに切り替えます。

アップグレード/切替の操作：
 1. [Tencent Real-Time Communicationコンソール](https://console.cloud.tencent.com/trtc)にログインします。
 2. 左側ナビゲーションバーで【アプリケーション管理】を選択し、目的とするアプリケーションのある行の【アプリケーション情報】をクリックします。
 3．【すぐに作業を開始】タブを選択して【ステップ2 UserSigを発行するためのキーを取得】エリアの【このアップグレードをクリック】、【非対称暗号化】または【HMAC-SHA256】をクリックします。
  - アップグレード：

  - 旧バージョンアルゴリズムのECDSA-SHA256に戻るよう切り替えます。
   ![](https://main.qcloudimg.com/raw/a8737123c1e3cc0f7eb34901ed2629f7.png)
  - 新バージョンアルゴリズムのHMAC-SHA256に切り替えます。
   ![](https://main.qcloudimg.com/raw/701fcde1a562bf9fbbb0d426948e311e.png)

### 2. 2台の携帯電話で同時にDemoを実行しているのに、お互いの画面が表示されないのはなぜですか？
2台の携帯電話でDemoを操作するとき、UserIDが異なるものを使用してください。TRTCでは、同一のUserID（SDKAppIDが異なる場合を除く）が2つの端末で同時に使用することをサポートしていません。


### 3. ファイアウォールにどのような制限がありますか？
SDK が UDP プロトコルを使用してオーディオビデオ伝送を行っていることから、 UDPに対してブロックがあるパブリックネットワークでは使用することができません。類似の問題があれば、 [企業ファイアウォール制限の対応](https://intl.cloud.tencent.com/document/product/647/35164)をご参照の上、問題原因を調べ解決してください。

