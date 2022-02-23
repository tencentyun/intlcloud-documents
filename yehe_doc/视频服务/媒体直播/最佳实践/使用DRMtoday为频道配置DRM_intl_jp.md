### ステップ1：アカウントの申請

1. DRMtodayの申請

   a. [DRMtoday製品ページ](https://castlabs.com/drmtoday/)に進み、DRMtodayのアクティブ化を申請します。
   ![img](https://main.qcloudimg.com/raw/b1fa760d75f68f27c4470bf52f81b800.png)

   b. 申請が完了するとDRMtodayアカウント、パスワードおよびDashboard URLを取得できます。

2. Fairplay証明書の申請

   a. [Apple Fairplay公式サイト](https://developer.apple.com/streaming/fps/)に進みます。

   b. [Request FPS Deployment Package](https://idmsa.apple.com/IDMSWebAuth/signin.html?path=%2Fcontact%2Ffps%2F&appIdKey=891bd3417a7776362562d2197f89480a8547b108fd934911bcbea0110d07f757)をクリックし、関連の情報を入力して送信します。
   ![img](https://main.qcloudimg.com/raw/9592e1021494896689ad0d7135f26560.png)

   c. FPS_Deployment_Package.zipファイルを取得します。

   d. FPS_Deployment_Package.zipの解凍後のドキュメントを参照し、パスワードで保護された秘密鍵、およびCSR（証明書署名要求）をローカルで作成します。

   e. FPS_Deployment_Package.zipの解凍後のドキュメントを参照し、CSRをAppleにアップロードします。ページから返されるASKは適切に保存してください。

   f. 公式に作成されたFairPlay Certificate（証明書）をローカルにダウンロードします。


## ステップ2：Fairplay証明書をDRMtodayにアップロード

DRMtoday Dashboard URLに進み、Configuration-DRMsettingsを選択します。
![img](https://main.qcloudimg.com/raw/352f6e951f0ca3252c5bf346ad19464b.png)
パラメータ：

- **Default IV**：空で問題ありません。

**Update certificate and keys**にチェックを入れた後、次のパラメータを設定します。

   - **Application secret key(ASK)**：Fairplay証明書申請のステップ5で取得したASKを、hexエンコード形式で入力します。
    
   - Provider certificate：Fairplay証明書申請のステップ6でダウンロードしたFairPlay Certificate（証明書）は、アップロードする証明書のタイプがPEM形式でなければならず、linuxのopensslツールを使用して変換することができます。例：証明書名がfairplay.cerの場合、変換コマンドは次のとおりです。

  ```
  openssl x509 -inform der -in fairplay.cer -out fairplay.pem
  ```

- Provider private key

  ：ユーザーはキーで保護された秘密鍵を作成します。アップロードするキーのタイプはPKCS #8 PEM形式でなければならず、linuxのopensslツールを使用して変換することができます。例：秘密鍵のファイル名がprivatekey.pemの場合、変換コマンドは次のとおりです。

  ```
  openssl rsa -in privatekey.pem -outform PEM -out out.pem
  ```



## ステップ3：DRMtoday APIによってWidevineまたはFairplayキーを設定

次の操作はいずれもDRMtoday公式サイトで提供されている操作ドキュメントを参照しています。元のドキュメントは[DRMtoday Key Ingestion](https://fe.staging.drmtoday.com/frontend/documentation/integration/key_ingestion.html)をご参照ください。

1. CAS認証
   DRMtodayはCAS（Central Authentication Service）を使用して、承認されていないアクセスからAPIを保護します。元のドキュメントは[DRMtoday CAS Authentication](https://fe.staging.drmtoday.com/frontend/documentation/integration/cas_authentication.html)をご参照ください。

   a. CAS Login：LoginアドレスにHTTP POSTリクエストを送信します。

   事例：

   ```
   curl -v 'https://auth.staging.drmtoday.com/cas/v1/tickets' -H 'Content-Type: application/x-www-form-urlencoded' -XPOST -d 'username=${username}&amp;password=${password}'
   ```

   パラメータ：

   - **username、password**：DRMtodayのアカウントパスワードを使用することも、DRMtodayで作成したAPIアカウントとそのパスワードを使用することもできます。[DRMtodayでのAPIアカウント作成ドキュメント](https://fe.staging.drmtoday.com/frontend/documentation/integration/dashboard.html? dummy#adding-accounts)をご参照ください。

   b. CAS Ticket Retrieval：CAS Loginリクエスト後に返されるheaderの中のLocationアドレスにHTTP POSTリクエストを送信します。

   事例：

   ```
   curl -v 'https://auth.staging.drmtoday.com/cas/v1/tickets/xxx' -H 'Content-Type: application/x-www-formurlencoded'-XPOST -d 'service=https://fe.staging.drmtoday.com/frontend/api/keys/v2/ingest/${merchantApiName}'
   ```

   パラメータ：

   - **service**：Dashboard-APIページのIngest keyに対応するEndpointは下図のとおりです。
     ![img](https://main.qcloudimg.com/raw/299f6fdcdfd5016a48c4b41f530e277a.png)

2. キーの設定
   認証完了後、Ingest key APIによってWidevineまたはFairplayキーを設定します。インターフェース使用のドキュメントは[DRMtoday Key Ingestion](https://fe.staging.drmtoday.com/frontend/documentation/integration/key_ingestion.html)をご覧ください。
   事例：

   ```
   curl -v 'https://fe.staging.drmtoday.com/frontend/api/keys/v2/ingest/${merchant}?ticket=${ticket}' -H 'Content-Type: application/json' -H 'Accept: application/json' -XPOST -d '{"assets":[{"type":"CENC","assetId":"assettest","variantId":"varianttest","ingestKeys":[{"streamType":"VIDEO_AUDIO","algorithm":"AES","keyId":"MDAwMDAwMDAwMDAwMDAwMA==","key":"MDAwMDAwMDAwMDAwMDAwMA==","iv":"MDAwMDAwMDAwMDAwMDAwMA=="}]}]}'
   ```

   パラメータ：

   - **merchant**：Dashboardの中のIngest keyに対応するEndpoint。
   - **ticket**：CAS Ticket Retrievalから返されるBody内容。
   - **type**：CENCに設定するとWidevineとFairplayをサポートできます。Widevineの暗号化にはkeyIdとkeyの設定が、Fairplayの暗号化にはkeyとivの設定がそれぞれ必要です。
   - **keyId、key、iv**：base64エンコード形式で設定します。「MDAwMDAwMDAwMDAwMDAwMA==」に対応するhexエンコードは30303030303030303030303030303030です。



## ステップ4：StreamLive上でのDRMキーの設定

StreamLiveコンソール操作ガイドの出力グループ設定（*ここの「出力グループ設定」を「StreamLiveチャネル管理」 3、出力グループ設定画面にリダイレクトリンクさせる）を参照し、StreamLiveDRMキーの設定を次のように行います。

- **DRM**：有効
- **Scheme**:Custom DRM Keys

Fairplayキー：
![img](https://main.qcloudimg.com/raw/d1fd0abc8a2c4b1aa970f74160641731.png)

- **ContentId**：ステップ3-2のキー設定で設定したassetIdです。hexエンコードで入力します。
- **Key**：ステップ3-2のキー設定で設定したKeyです。hexエンコードで入力します。
- **Iv**：ステップ3-2のキー設定で設定したivです。hexエンコードで入力します。

Widevineキー：
![img](https://main.qcloudimg.com/raw/d65d6a93e13b12d8014558a601a21692.png)

- **ContentId**：ステップ3-2のキー設定で設定したassetIdです。hexエンコードで入力します。
- **KeyId**：ステップ3-2のキー設定で設定したKeyIdです。hexエンコードで入力します。
- **Key**：ステップ3-2のキー設定で設定したKeyです。hexエンコードで入力します。


## ステップ5：再生テスト

StreamLive使用マニュアルに従って再生アドレスを設定した後（例えば、[ライブストリーミングをStreamPackageのChannelに出力](https://intl.cloud.tencent.com/document/product/1048/41760#6.-output-content-to-streampackage-through-streamlive)し、StreamPackageの[Endpointノードの再生アドレス取得]([コンソールガイド | Tencent Cloud (tencent.com)](https://intl.cloud.tencent.com/document/product/1063/41787))、[DRMtoday再生ページ](https://players.castlabs.com/presto/6.1.2/#/player/config)を使用してテストを行うことができます。
![img](https://main.qcloudimg.com/raw/5b8b559d838497dd5b75cf9c7cedf363.png)
![img](https://main.qcloudimg.com/raw/77249ddf9131bc9578bdb28fc3c37fb4.png)
パラメータ：

- **Content URL**：再生コンテンツのURL。
- **DRM Environment**：実際の状況に応じて選択します。
- **Merchant**：ユーザーのDRMtodayでの名前であり、通常はmerchantApiNameと同一です。
- **User ID、Session ID**：[設定ドキュメント](https://fe.staging.drmtoday.com/frontend/documentation/integration/dashboard.html#uisetting-Test_dummy)を参照可能です（License Delivery AuthorizationタイプがTest_dummyの場合）。
- **Asset ID**：ステップ3-2のキー設定で設定したassetIdです。
- **Variant ID**：ステップ3-2のキー設定で設定したvariantIdです。
