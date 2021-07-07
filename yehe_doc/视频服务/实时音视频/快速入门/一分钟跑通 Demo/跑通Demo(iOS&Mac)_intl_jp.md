ここでは、主にTencent Cloud TRTC Demo (iOS&Mac)を素早く実行する方法をご紹介します。

## 環境要件
- Xcode 11.0およびそれ以降のバージョン。
- プロジェクトが有効な開発者による署名を設定済みであることを確認してください。
- Qt Creator 4.13.3（Mac）以上のバージョン。

## 前提条件
[Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)および[実名認証](https://intl.cloud.tencent.com/document/product/378/3629)を完了していること。実名認証を行っていないユーザーは、中国国内のTRTCサービスを購入できません。

## 操作手順
[](id:step1)
### 手順1：アプリケーションの新規作成
1．Tencent Real-Time Communicationコンソールにログインし、【開発支援】>【[Demoのクイックスタート](https://console.cloud.tencent.com/trtc/quickstart)】を選択します。
2. アプリケーション名（例：`TestTRTC`）を入力し、【作成】をクリックします。

[](id:step2)
### 手順2：SDKおよびDemoのソースコードをダウンロード
1. 実際の業務のニーズにもとづき、SDKおよびセットのDemoソースコードをダウンロードします。
2. ダウンロード完了後、【ダウンロードしました。次のステップ】をクリックします。

[](id:step3)
### 手順3：Demoプロジェクトファイルの設定
1. 設定変更画面に入り、ダウンロードしたソースコードパッケージに基づき、対応する開発環境を選択します。
2. `GenerateTestUserSig.h`ファイルを見つけて開きます。
 <table><tr>
      <th nowrap="nowrap">適用可能なプラットフォーム</th>
      <th nowrap="nowrap">ファイル相対パス</th>
  </tr>
<tr>
      <td>iOS</td>
<td>iOS/TRTCScenesDemo/TXLiteAVDemo/Debug/GenerateTestUserSig.h</td>
  </tr>
<tr>
    <td>Mac</td>
    <td>Mac/OCDemo/TRTCDemo/TRTC/GenerateTestUserSig.h</td>
  </tr></table>
3. `GenerateTestUserSig.h`のファイルの関連するパラメータを設定します。
  <ul><li>SDKAPPID：デフォルトは0、実際のSDKAppIDを設定してください。</li>
  <li>SECRETKEY：デフォルトは空文字列。実際のキー情報を設定してください。</li></ul> 
4. 貼り付け完了後、【貼り付けました。次のステップ】をクリックすれは作成が完了します。
5. コンパイル完了後、【コンソール概要に戻る】をクリックすればOKです。

>!
>-ここで言及した新規UserSigの作成法は、クライアントコードでSECRETKEYを設定し、この手法のうちSECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになり、そのため**のこの手法はローカルDemo実行および機能デバッグにのみ適合します**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。 UserSigが必要なときは、Appから業務サーバーにリクエストを発出しダイナミックUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

### 手順4：コンパイル動作
1. 端末のウィンドウから、ソースコードの TRTCScenesDemo > Podfileファイルがあるディレクトリに入ります。
2. `pod install` コマンドを実行して、TRTC SDKをインストールするか、または`pod update`コマンドを実行して、ローカルライブラリのバージョンをアップデートします。
3. XCode（バージョン11.0以上）を使用してソースコードディレクトリのTXLiteAVDemo.xcworkspace工程を開き、Demo工程をコンパイル、動作すればOKです。
>? Qt Creator（バージョン4.13.3以上）を使用している場合は、ソースコードディレクトリの `QTDemo.pro` 工程を直接開いて Demo 工程をコンパイル、動作すればOKです。

## よくあるご質問
### 1. キーをクエリーするとき、パブリックキーおよびプライベートキーの情報しか取得できませんが、キーはどうしたら取得できますか。
TRTC SDK 6.6バージョン（2019年08月）では新しい署名アルゴリズムのHMAC-SHA256の使用を始めています。その前に作成済のアプリケーションは、署名アルゴリズムをアップグレードしないと暗号化したキーを取得できません。アップグレードしなくても、[旧バージョンアルゴリズム ECDSA-SHA256]（https://intl.cloud.tencent.com/document/product/647/35166)は引き続き使用できます。アップグレード済みなら、必要に応じて新旧アルゴリズムに切り替えます。

アップグレード/切替の操作：
 1. [Tencent Real-Time Communicationコンソール](https://console.cloud.tencent.com/trtc)にログインします。
 2. 左側ナビゲーションバーで【アプリケーション管理】を選択し、目的とするアプリケーションのある行の【アプリケーション情報】をクリックします。
 3．【クイックマスター】タブを選択して【ステップ2 UserSigを発行するためのキーを取得】エリアの【ここをクリックしてアップグレード】、【非対称暗号化】または【HMAC-SHA256】をクリックします。
  - アップグレード：
  - 旧バージョンアルゴリズムのECDSA-SHA256に切り替えます。
      ![](https://main.qcloudimg.com/raw/bc5cc756b93bd3e688f9f31a9c1efdfe/%E8%B7%91%E9%80%9ADemo(iOS&Mac)5-%E8%BF%94%E8%BF%98.png)
  - 新バージョンアルゴリズムのHMAC-SHA256に切り替えます。
      ![](https://main.qcloudimg.com/raw/2f55ac47bbff3257bfadc7e670e0ff1c/%E8%B7%91%E9%80%9ADemo(iOS&Mac)6-%E8%BF%94%E8%BF%98.png)

### 2. 2台の携帯電話で同時にDemoを実行しているのに、お互いの画面が表示されないのはなぜですか。
2台の携帯電話でDemoを操作するとき、UserIDが異なるものを使用してください。TRTCでは、同一のUserID（SDKAppIDが異なる場合を除く）が2つの端末で同時に使用することをサポートしていません。

### 3. ファイアウォールにはどのような制限がありますか。
SDKがUDP プロトコルを使用してオーディオビデオ伝送を行っていることから、 UDPに対してブロックがあるパブリックネットワークでは使用することができません。類似の問題があれば、 [企業ファイアウォール制限の対応](https://intl.cloud.tencent.com/document/product/647/35164)をご参照ください。
