## ご使用にあたっての注意事項

### 内容紹介

本ドキュメントでは、DRM機能を使用するときにApple Inc.にFairPlay証明書を申請し、次の証明書情報をTencent Cloud VODに送信する方法について説明します：

- FPS証明書ファイル(.cer)
- プライベートキーファイル(.pem)
- プライベートキーパスワード
- ASK (Application Secret Key)

## 手順1：FairPlay Streaming Deployment Packageの取得

1. [Apple FairPlayページ](https://developer.apple.com/streaming/fps/)にアクセスして、ページ下部のリンク`Request FPS Deployment Package`をクリックすると、フォームページが表示されます。

>! Apple開発者のアカウントが必要です。ログインに成功した後にのみフォームが表示されます。

![image-20220426181021189](https://qcloudimg.tencent-cloud.cn/raw/c8533ed9e4cf2b7961058eb9e5cd502a.png)

2. ページの申請フォームに記入して送信し、提出後にApple Inc.の承認を待ちます。

![image-20220426181021190](https://qcloudimg.tencent-cloud.cn/raw/5f905c0a865990ba4f1705fabdcdd652.png)

3. Apple Inc.により申請が承認された後、`FPS_Deployment_Package.zip`圧縮パッケージを取得します。

## 手順2：プライベートキーと証明書署名要求の作成(CSR、Certificate Signing Request)

`FPS_Deployment_Package.zip`を解凍し、解凍後のドキュメント(.pdf)に従って、パスワードで保護されたプライベートキーと証明書署名要求(CSR)を作成します。

1. 次のコマンドを実行して、プライベートキーファイル(`privatekey.pem`)を作成します。

   ```shell
openssl genrsa -aes256 -out privatekey.pem 1024
   ```
   作成中、プライベートキーパスワードを指定してください。後続の手順で使用されるため、プライベートキーパスワードを必ず記録してください。また、プライベートキーのパスワードは32文字を超えないようにしてください。
   
   ![image-20220421115813168](https://qcloudimg.tencent-cloud.cn/raw/ce0f6e159601c772694e79c69648e343.png)
   
2. 次のコマンドを実行して、証明書署名要求(`certreq.csr`)を作成します。

   ```shell
   openssl req -new -sha1 -key privatekey.pem -out certreq.csr -subj "/CN=SubjectName/OU=OrganizationalUnit/O=Organization/C=US"
   ```
   作成中、プライベートキーファイルの作成時に指定したプライベートキーパスワードを入力してください。
   
   ![image-20220421115929084](https://qcloudimg.tencent-cloud.cn/raw/25c7097a4633a2429b0f7173c0f255b6.png)


## 手順3：FPS証明書（FairPlay Streaming Certificate）の生成

[Apple開発者ページ](https://developer.apple.com/account)にアクセスして、FPS証明書とASKを取得します。

1. [Apple開発者ページ](https://developer.apple.com/account)にアクセスして、左側ナビゲーションバーの`Certificates, Identifiers & Profiles`をクリックします

   ![image-20220419113745847](https://qcloudimg.tencent-cloud.cn/raw/29e8bb1b63a60c877f17dd0c39d9e8d5.png)

2. 画面上の`+`ボタンをクリックします。

   ![image-20220419113637808](https://qcloudimg.tencent-cloud.cn/raw/4b88b93e4450b7171f09a3b75e2cb2bc.png)

3. 画面上の` FairPlay Streaming Certificate `オプションを選択して、` Continue `ボタンをクリックします。

   ![image-20220419114215512](https://qcloudimg.tencent-cloud.cn/raw/00fa1494b1256c9b4e1d769356450721.png)

4. 画面上の` Choose File `ボタンをクリックし、前の手順で作成した`certreq`ファイルを選択して、` Continue `ボタンをクリックします。

   ![image-20220419114506263](https://qcloudimg.tencent-cloud.cn/raw/52c2834bf36f4074e7f9f731aefc8948.png)

5. 画面上の`Application Secret Key (ASK)`をコピーしてバックアップし、次に下部の入力フィールドに`ASK`を再入力して、` Continue `ボタンをクリックします。

   ![image-20220419114920781](https://qcloudimg.tencent-cloud.cn/raw/8e55fb6e817a2279f6b2cea3418506f7.png)

6. 前の手順が完了すると、`ASK`がバックアップされたかどうかを再確認させるために、ポップアップボックスが表示されます。バックアップされたことを確認したら、` Generate `ボタンをクリックします。

   >! ASKがバックアップされたことを必ず確認してください。この手順を完了すると、ASKを再度確認することはできません。

   ![image-20220419115103618](https://qcloudimg.tencent-cloud.cn/raw/808347b36d824de46b6cbb84654d20c8.png)

7. 上記の手順を完了すると、先ほど作成した` FairPlay Streaming `タイプのFPS証明書が証明書リストページに表示されます。

   ![image-20220419115340087](https://qcloudimg.tencent-cloud.cn/raw/ee831cfc5c26f37bdc09c9a50bab5ef5.png)

8. `Download`ボタンをクリックして、FPS証明書(`fairplay.cer`)をダウンロードします

   ![image-20220419115536031](https://qcloudimg.tencent-cloud.cn/raw/d7e7ad03c0168b61db084cfee762f6cc.png)


## 手順4：コンソールからのFPS証明書情報の送信

1. Tencent Cloud VODコンソールにログインします。
2. 左側にあるナビゲーションバーの`ビデオ処理設定`をクリックして展開し、` DRM暗号化設定`をクリックします。その後、右側にある`編集`をクリックします。
   ![image-20220425210931543](https://qcloudimg.tencent-cloud.cn/raw/041b560536deebd1bd5bc986d95ed289.png)
3. 証明書ファイル(`fairplay.cer`)、プライベートキーファイル(`privatekey.pem`)、プライベートキーパスワード、およびASKなどのFPS証明書情報を設定し、`保存`をクリックします。

   ![image-20220425211140740](https://qcloudimg.tencent-cloud.cn/raw/effefe51d8ca82e46d292112eab9a3b4.png)

4. 保存すると、`FairPlay`証明書情報が表示されます。そのうち、`Certificate URL`はDRM暗号化ビデオの再生に使用できます。

   ![image-20220426191830269](https://qcloudimg.tencent-cloud.cn/raw/8d64c3dbb65ac6f54a81f08314ca1473.png)

## まとめ

これで、`FairPlay`証明書情報の設定が完了しました。
