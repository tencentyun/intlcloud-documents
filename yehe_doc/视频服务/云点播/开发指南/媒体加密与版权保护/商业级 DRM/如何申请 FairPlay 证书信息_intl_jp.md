AppleのFairPlay DRM(FPS)を使用する場合、まずAppleにFPSデプロイパッケージを申請する必要があります。ここでは、FPSデプロイパッケージの取得方法と、以下の重要な情報について詳しくご説明します。

- FPS証明書ファイル(.cer)
- 秘密鍵ファイル(.pem)
- 秘密鍵パスワード
- ASK(Application Secret Key)

## ステップ1：FairPlay Streaming Deployment Packageの取得

1. [Apple FairPlayページ](https://developer.apple.com/streaming/fps/)にアクセスし、画面下部の`Request FPS Deployment Package`というリンクをクリックすると、フォーム画面が表示されます。

>! Apple開発者アカウントを取得し、ログインに成功するとフォームが表示されます。

![image-20220426181021189](https://qcloudimg.tencent-cloud.cn/raw/c8533ed9e4cf2b7961058eb9e5cd502a.png)

2. 画面の申請フォームに必要事項を入力し、提出してAppleの承認を待ちます。

![image-20220426181021190](https://qcloudimg.tencent-cloud.cn/raw/5f905c0a865990ba4f1705fabdcdd652.png)

3. Appleが申請を承認すると、`FPS_Deployment_Package.zip`という圧縮パッケージを取得できます。

  >? 申請にあたっては、キーサーバーモジュール(KSM)の実装とテストが完了しているかどうか質問されますので、それにお答えください。 
   > ```
   > I am using a 3rd party DRM company and the company has already built and tested KSM
   > ```

## ステップ2：秘密鍵と証明書署名リクエストの作成(CSR、Certificate Signing Request)

`FPS_Deployment_Package.zip`を解凍し、解凍した説明ドキュメント(.pdf)をもとに、パスワードで保護された秘密鍵と証明書署名リクエスト(CSR)を作成します。

>! 以下の手順を実行するPCやサーバー環境には、OpenSSLがインストールされている必要があります。 

1. 秘密鍵ファイル(privatekey.pem)を作成し、以下のコマンドを実行します。

   ```shell
openssl genrsa -aes256 -out privatekey.pem 2048
   ```
   作成中、秘密鍵パスワードを指定する必要があります。秘密鍵パスワードは、その後の手順で使用するため、必ず記録しておいてください。また、秘密鍵パスワードは32文字以下にするようお勧めします。
   
   ![image-20220421115813168](https://staticintl.cloudcachetci.com/yehe/backend-news/ksBs652_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16723902163742.png)
   
2. 証明書署名リクエスト(`certreq.csr`)を作成し、以下のコマンドを実行します。

   ```shell
   openssl req -new -sha1 -key privatekey.pem -out certreq.csr -subj "/CN=SubjectName/OU=OrganizationalUnit/O=Organization/C=US"
   ```
   作成中、秘密鍵ファイルの作成時に指定した秘密鍵のパスワードを入力する必要があります。
   
   ![image-20220421115929084](https://qcloudimg.tencent-cloud.cn/raw/25c7097a4633a2429b0f7173c0f255b6.png)
   

## ステップ3：FPS証明書の生成(FairPlay Streaming Certificate)

[Apple開発者ページ](https://developer.apple.com/account)にアクセスして、FPS証明書とASKを取得します。

1. [Apple開発者ページ](https://developer.apple.com/account)にアクセスして、左側ナビゲーションバーの`Certificates, Identifiers & Profiles`をクリックします

   ![image-20220419113745847](https://qcloudimg.tencent-cloud.cn/raw/29e8bb1b63a60c877f17dd0c39d9e8d5.png)

2. 画面上の`+`ボタンをクリックします。

   ![image-20220419113637808](https://qcloudimg.tencent-cloud.cn/raw/4b88b93e4450b7171f09a3b75e2cb2bc.png)

3. 画面上の`FairPlay Streaming Certificate`オプションを選択し、`Continue`ボタンをクリックします。

   ![image-20220419114215512](https://qcloudimg.tencent-cloud.cn/raw/00fa1494b1256c9b4e1d769356450721.png)

4. 画面上の`Choose File`ボタンをクリックし、前のステップで作成した`certreq`ファイルを選択し、`Continue`ボタンをクリックします。

   ![image-20220419114506263](https://qcloudimg.tencent-cloud.cn/raw/52c2834bf36f4074e7f9f731aefc8948.png)

5. 画面上の`Application Secret Key(ASK)`をコピーしてバックアップし、続けて下の入力フィールドに`ASK`を再入力して、`Continue`ボタンをクリックします。

   ![image-20220419114920781](https://qcloudimg.tencent-cloud.cn/raw/8e55fb6e817a2279f6b2cea3418506f7.png)

6. 前の手順が完了したら、`ASK`をバックアップしたことを再確認するポップアップボックスが表示されますので、バックアップしたことを確認した後、`Generate`ボタンをクリックします。

   >! この手順が完了すると、ASKを再度照会することができなくなりますので、必ずASKのバックアップが行われているか確認してください。

   ![image-20220419115103618](https://qcloudimg.tencent-cloud.cn/raw/808347b36d824de46b6cbb84654d20c8.png)

7. 以上の手順が完了すると、証明書リスト画面に先ほど作成したFPS証明書が表示され、証明書タイプは`FairPlay Streaming`となります。

   ![image-20220419115340087](https://qcloudimg.tencent-cloud.cn/raw/ee831cfc5c26f37bdc09c9a50bab5ef5.png)

8. **Download**ボタンをクリックし、FPS証明書(`fairplay.cer`)をダウンロードします。

   ![image-20220419115536031](https://qcloudimg.tencent-cloud.cn/raw/d7e7ad03c0168b61db084cfee762f6cc.png)

## まとめ

この時点で、`FairPlay`証明書情報の申請が完了しました。
