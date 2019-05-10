[Tencent Cloud GME SDK](https://cloud.tencent.com/product/tmg?idx=1)へようこそ。開発者がTencent Cloud GME製品を容易に導入するために、ここではGME SDKに適した導入ガイドを紹介します。

GMEを使用するには、以下の5つのステップに従います。
1. [Tencent CloudコンソールでGMEサービスを新規作成する](#.E6.96.B0.E5.BB.BA.E6.9C.8D.E5.8A.A1)。
2. [対応するバージョンのクライアントSDKをダウンロードする](#.E4.B8.8B.E8.BD.BD-sdk)。
3. [API導入ドキュメントを参照し、SDKをプロジェクトに移し換える](#.E7.9B.B8.E5.85.B3-sdk-.E6.8A.80.E6.9C.AF.E6.96.87.E6.A1.A3)。
4. [日常運営のバックグラウンド統計を確認する](#.E6.8E.A7.E5.88.B6.E5.8F.B0.E7.94.A8.E9.87.8F.E7.BB.9F.E8.AE.A1)。
5. [導入プロセスにおける特別な問題の自己解決とフィードバック](#.E7.89.B9.E6.AE.8A.E9.97.AE.E9.A2.98.E5.A4.84.E7.90.86)。


## サービスの新規作成
### 1. アプリケーションの新規作成
![](https://main.qcloudimg.com/raw/a4b3dbd8aefd9dd032f8c3ce4154b227.png)

### 2. 該当する情報
このページに必要な情報を入力し、必要に応じて必要なサービスを選択してください。 
- 音質によって課金方式も異なります。課金の詳細は[製品の価格](https://cloud.tencent.com/document/product/607/17808)を参照し、関連するTencent Cloud営業担当にお問い合わせください。設定が完了後にも変更することができます。
- ゲームアプリケーションの場合は、対応するプラットフォームエンジンを選択する必要があります。
- ボイスメッセージ及びテキスト変換サービスの設定が完了後にも変更することができます。

![](https://main.qcloudimg.com/raw/bafdd3250004a5d69322beab1d6c25c7.png)


### 3. アプリケーションの表示
リストのAppIDは、SDKを導入し開発を行う間にパラメータとして使用します。
![](https://main.qcloudimg.com/raw/9e78b27c75b9bfcd2ce02ae1d02b7046.png)


### 4. アプリケーション設定
![](https://main.qcloudimg.com/raw/ac27c53e9a07fa819344f668978fe019.png)
アプリケーション情報モジュールで【変更】をクリックすると、該当する情報を変更することができます。

### 5. 認証情報
![](https://main.qcloudimg.com/raw/76b5038763d2aded0be39b0d1bc27efa.png)
- このモジュールにおける権限暗号鍵は、パラメータとしてSDK導入プロセスに使用されます。 
- ページで暗号鍵を変更した後、15分間～1時間以内に有効となります。頻繁な変更はお勧めしません。
- ゲームを作成したアカウント、メインアカウント、グローバル協力者のみが【暗号鍵のリセット】を操作することができます。
- 認証の詳細な使用については、[GME暗号鍵の説明ドキュメント](https://cloud.tencent.com/document/product/607/12218)を参照してください。
 ![](https://main.qcloudimg.com/raw/df3f92e2eb50aea9d8dde32f252045f6.png)


### 6. サービスの有効化/無効化
ここでは、ビジネスおよびサービスを有効化・無効化することができます。
![](https://main.qcloudimg.com/raw/a5711820b59c6d4047565562094d1595.png)
![](https://main.qcloudimg.com/raw/ec0f00f1afc229b6db5676772c53edad.png)


## SDKのダウンロード 
### 1. ダウンロードURL
[SDKダウンロードガイド](https://cloud.tencent.com/document/product/607/18521)で関連DemoおよびSDKをダウンロードしてください。

### 2. 導入準備
SDKを導入するには、Tencent Cloudが提供するappidおよび関連権限暗号鍵を使用する必要があります。つまり、アプリケーション管理リスト中のAppIDおよびアプリケーション設定中の認証情報モジュールです。

プラットフォーム関連構成の詳細については、各プラットフォームプロジェクトの構成ドキュメントを参照してください。

### 3. 公式Demoの使用上の注意
Demoには機能体験可能なTencent Cloudテストアカウントがあります。個人または企業のテストアカウントに変更する必要がある場合、Demoの該当するインタフェースでTencent CloudテストアカウントAppIDを開発者がコンソールで取得したAppIDに変更し、且つAVChatViewController-GetAuthBuffer関数においてリアルタイムボイスの権限暗号鍵を変更する必要があります。


## 関連APIドキュメント
使用しているプラットフォームまたはエンジンに応じて、以下のドキュメントを参考して、導入できます。

Unity関連ドキュメント：
[プロジェクト構成ドキュメント](https://cloud.tencent.com/document/product/607/10783)
[APIドキュメント](https://cloud.tencent.com/document/product/607/15228)

Unreal Engine関連ドキュメント：
[プロジェクト構成ドキュメント](https://cloud.tencent.com/document/product/607/17025)
[APIドキュメント](https://cloud.tencent.com/document/product/607/15231)

Cocos2D関連ドキュメント：
[プロジェクト構成ドキュメント](https://cloud.tencent.com/document/product/607/15216)
[APIドキュメント](https://cloud.tencent.com/document/product/607/15218)

Windows関連ドキュメント：
[プロジェクト構成ドキュメント](https://cloud.tencent.com/document/product/607/19068)
[APIドキュメント](https://cloud.tencent.com/document/product/607/15232)

iOS関連ドキュメント：
[プロジェクト構成ドキュメント](https://cloud.tencent.com/document/product/607/15219)
[APIドキュメント](https://cloud.tencent.com/document/product/607/15221)

Android関連ドキュメント：
[プロジェクト構成ドキュメント](https://cloud.tencent.com/document/product/607/15203)
[APIドキュメント](https://cloud.tencent.com/document/product/607/15210)

Mac関連ドキュメント：
[プロジェクト構成ドキュメント](https://cloud.tencent.com/document/product/607/18617)
[APIドキュメント](https://cloud.tencent.com/document/product/607/18739)

H5関連ドキュメント：
[プロジェクト構成ドキュメント](https://cloud.tencent.com/document/product/607/32156)
[APIドキュメント](https://cloud.tencent.com/document/product/607/32157)



## コンソール使用量統計
[運営ガイドドキュメント](https://cloud.tencent.com/document/product/607/17448)


## 特別な問題の処理
[よくある問題ドキュメント](https://cloud.tencent.com/document/product/607/17359)     [エラーコードドキュメント](https://cloud.tencent.com/document/product/607/15173)

