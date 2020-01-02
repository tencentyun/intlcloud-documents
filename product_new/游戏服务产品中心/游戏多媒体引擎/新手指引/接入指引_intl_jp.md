[Tencent Cloud Gaming Multimedia Engine SDK](https://cloud.tencent.com/product/tmg?idx=1)を利用頂き、有難うございました。開発者のTencent Cloud Gaming Multimedia Engine製品へのアクセスを容易にするために、ここで、Gaming Multimedia Engine SDK のアクセスガイドをさせて頂きます。

GME の利用は以下5つのステップがあります。
1. [Tencent Cloudコンソールにおける GME サービスの新規作成](#.E6.96.B0.E5.BB.BA.E6.9C.8D.E5.8A.A1)；
2. [対応バージョンのクライアント SDK のダウンロード](#.E4.B8.8B.E8.BD.BD-sdk)；
3. [APIドキュメンテーションを参照し、SDK をプロジェクトに移植する](#.E7.9B.B8.E5.85.B3-api-.E6.96.87.E6.A1.A3)；
4. [日常運営統計の確認](#.E6.8E.A7.E5.88.B6.E5.8F.B0.E7.94.A8.E9.87.8F.E7.BB.9F.E8.AE.A1)；
5. [アクセス中の特殊問題の自主的な排除とフィードバック](#.E7.89.B9.E6.AE.8A.E9.97.AE.E9.A2.98.E5.A4.84.E7.90.86)；


## サービスの新規作成
### 1. アプリケーションの新規作成
![](https://main.qcloudimg.com/raw/7b682f5aaf2f9995a6eef37a3296b7ac.png)

### 2. 関連情報
該当画面の必要情報を記入し、必要に応じてサービスを選びます。 
- 音質によって課金モードが違います。課金については [製品価格](https://cloud.tencent.com/document/product/607/17808) をご参照いただくか、Tencent Cloudの営業担当者までお問い合わせください。設定した後も修正できます。
- ゲームアプリケーションの場合、対応のプラットフォームエンジンを選択する必要があります。
- 音声メッセージとボイスツーテキスト変換は設定した後も修正できます。

<!--![](https://main.qcloudimg.com/raw/8bed789287a2b1a0dfe4861fd052d70c.png)-->


### 3. アプリケーションの確認
リスト内の AppID は SDK にアクセスして開発をしている間、パラメータとして使用します。
![](https://main.qcloudimg.com/raw/efbdf4105eb37cfa40e96223e2b7a840.png)


### 4. アプリケーション設定
![](https://main.qcloudimg.com/raw/c3cef70b9fe48c050cfec1ce81b23979.png)

アプリケーション情報のモジュールです。【修正】をクリックした後、対応情報の修正ができます。

### 5.認証情報
![](https://main.qcloudimg.com/raw/fa2ca0b76d1ac0f03aa769a4d5972308.png)
- 該当モジュール内の権限キーはパラメータとして SDK アクセスに使用します。 
- 画面でキーを修正した後、発効所要時間が15分 - 1時間になるため、頻繁な修正はお控えください。
- ゲームのアカウント、ルートアカウント、グロバール協力者を作成する際に限って【キーのリセット】を操作できます。
- 認証については、「認証キー」(https://intl.cloud.tencent.com/document/product/607/12218)をご参照ください。
 ![](https://main.qcloudimg.com/raw/e65e03a506eda099d3cedca85ea9685c.png)


### 6. 業務のオンとオフ
ここで業務とサービスのオンとオフができます
![](https://main.qcloudimg.com/raw/1e3d12f084942645714158eb68767acf.png)
![](https://main.qcloudimg.com/raw/ec0f00f1afc229b6db5676772c53edad.png)


## SDK のダウンロード 
### 1. ダウンロードURL
[SDK ダウンロードガイド](https://intl.cloud.tencent.com/document/product/607/18521)から関連 Demo と SDK をダウンロードしてください。

### 2. アクセス準備
SDK にアクセスするにはTencent Cloudが提供する appid と関連権限キー、即ちアプリケーション管理リスト内の AppID とアプリケーション設定の認証情報モジュールを使用する必要があります。

プラットフォーム関連構成の詳細については各プラットフォームの技術構成ドキュメントをご参照ください。

### 3. 公式 Demo 利用の注意事項
Demo にはTencent Cloudのテスト用アカウントがあるため、機能を体験できます。個人と会社のテスト用アカウントを変更したい場合、 Demo の対応インターフェースでTencent Cloudのテスト用アカウントの AppID を開発者がコンソールで獲得した AppID に変更した上、 AVChatViewController-GetAuthBuffer 関数でリアルタイム音声の権限キーを修正する必要があります。


## 関連APIドキュメンテーション
ご利用のプラットフォームまたはエンジンによって以下のドキュメントを参照しながらアクセスしてください。

Unityの関連ドキュメント：
 [技術構成ドキュメント](https://intl.cloud.tencent.com/document/product/607/10783)
 [インターフェースドキュメント](https://intl.intl.cloud.tencent.com/document/product/607/15210)

Unreal Engineの関連ドキュメント：
 [技術構成ドキュメント](https://intl.cloud.tencent.com/document/product/607/10783)
 [インターフェースドキュメント](https://intl.intl.cloud.tencent.com/document/product/607/15210)

Cocos2Dの関連ドキュメント：
 [技術構成ドキュメント](https://intl.cloud.tencent.com/document/product/607/10783)
 [インターフェースドキュメント](https://intl.intl.cloud.tencent.com/document/product/607/15210)

Windowsの関連ドキュメント：
 [技術構成ドキュメント](https://intl.cloud.tencent.com/document/product/607/10783)
 [インターフェースドキュメント](https://intl.intl.cloud.tencent.com/document/product/607/15210)

iOSの関連ドキュメント：
 [技術構成ドキュメント](https://intl.cloud.tencent.com/document/product/607/10783)
 [インターフェースドキュメント](https://intl.intl.cloud.tencent.com/document/product/607/15210)

Androidの関連ドキュメント：
 [技術構成ドキュメント](https://intl.cloud.tencent.com/document/product/607/10783)
 [インターフェースドキュメント](https://intl.cloud.tencent.com/document/product/607/15210)

Macの関連ドキュメント：
 [技術構成ドキュメント](https://intl.cloud.tencent.com/document/product/607/10783)
 [インターフェースドキュメント](https://intl.cloud.tencent.com/document/product/607/15210)

H5の関連ドキュメント：
 [技術構成ドキュメント](https://intl.cloud.tencent.com/document/product/607/10783)
 [インターフェースドキュメント](https://intl.cloud.tencent.com/document/product/607/15210)



## コンソール使用量統計
ご不明な点がございましたら、[運営ガイド](https://intl.cloud.tencent.com/document/product/607/17448)をご参照ください。


## 特殊問題の対処
ご不明な点がございましたら、[一般的な問題](https://intl.cloud.tencent.com/document/product/607/30254)をご参照ください。
ご不明な点がございましたら、[エラーコード](https://intl.cloud.tencent.com/document/product/607/15173)をご参照ください。



