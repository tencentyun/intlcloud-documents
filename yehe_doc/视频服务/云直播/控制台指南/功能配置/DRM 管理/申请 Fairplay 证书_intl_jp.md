AppleのFairPlay Streaming(FPS)DRMを使用する場合、コンテンツサービスプロバイダはAppleにFPSデプロイパッケージの取得を申請し、以下のファイルをSDMCライセンスサーバーにアップロードする必要があります。
- FPS証明書ファイル（`.der`または`.cer`）
- 秘密鍵ファイル（`.pem`）
- 秘密鍵パスワードファイル（`.txt`）
- アプリケーションキー（ASK）ファイル（`.txt`）

## 操作手順
 [](id:step1)
### ステップ1：Apple開発者アカウントを登録し、デプロイパッケージをリクエストします
1. [Appleアカウント登録サイト](https://developer.apple.com/support/enrollment/)にアクセスし、アカウント登録を行います。
2. [FairPlay Streaming](https://developer.apple.com/streaming/fps/)サイトの下部にある[Request FPS Deployment Package](https://developer.apple.com/contact/fps/)をクリックし、お客様のApple開発者アカウントを使用して登録を行います。
3. 入力フォームに基づいてデプロイパッケージを申請した場合、Appleが確認後、FPS証明書作成ガイドドキュメントを含むパッケージが届きます。

>! 申請にあたっては、キーサーバーモジュール(KSM)の実装とテストが完了しているかどうか質問されますので、それにお答えください。
```
I am using a 3rd party DRM company and the company has already built and tested KSM
```

 [](id:step2)
### ステップ2：秘密鍵および証明書署名リクエスト(CSR)
開発キットのガイダンスドキュメントに従って、秘密鍵（`privatekey.pem`）ファイルと証明書署名リクエスト（`certreq.csr`）ファイルを作成します。本ガイドの証明書署名リクエスト部分のOpenSSLメソッドについて、以下にご説明します。
>! この手順を実行するPCやサーバー環境には、OpenSSLがインストールされている必要があります。

1. **秘密鍵ファイル（privatekey.pem）の作成**：
	1. 以下のコマンドを実行し、秘密鍵を発行します。[](id:step1_1)
```
openssl genrsa -aes256 -out privatekey.pem 1024
```
	2. 秘密鍵のパスワードを入力し、メモしておき後ほど使用します（パスワードは32文字以内）。
2. **証明書署名リクエストファイルの作成**：
	1. 以下のコマンドを実行し、`-subj`パラメータの内容をお客様の組織に合わせて変更します。
```
openssl req -new -sha1 -key privatekey.pem -out certreq.csr -subj "/CN=SubjectName/OU=OrganizationalUnit/O=Organization/C=US"
```
	2. [前へ戻る](#step1_1)で入力した秘密鍵のパスワードを入力します。

[](id:step3)
### ステップ3：Apple Developer PortalでFPS証明書を作成します
1. [Apple Developer Portal](https://developer.apple.com/)にログインし、[Certificates, IDs, & Profiles](https://developer.apple.com/account/ios/certificate/)に進みます。
![](https://qcloudimg.tencent-cloud.cn/raw/3c2963e1317986b25f05014042f120de.png)
2. メニューの**+**ボタンをクリックし、Create a New Certificateページにジャンプします。
![](https://qcloudimg.tencent-cloud.cn/raw/79a02a3d039ae6bfe40144e2d90b0d44.png)
3. **FairPlay Streaming Certificate**を選択し、**Continue**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/fef15cd65ddf3c21752c3b71c37b9b04.png)
4. **Choose File**をクリックし、上記の手順で作成した`certreq.csr`ファイルを選択し、**Continue**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/d179f0554b61453a51e2a6efa83338e9.png)
5. Application Secret Key(ASK)の文字列をコピーし、別のファイルに別途保存します。次に下の空欄にコピーして、**Continue**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/3a69ea9e79824df5d39213373830c8a2.png)
6. この時、ポップアップウィンドウが表示されますので、ASK文字列がファイルに別途保存されたかどうか確認します。保存されたことを確認したら、**Generate**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/1a9471e089b5224e393b8efecd5a77c7.png)
7. 上記の手順が完了すると、FairPlay Streaming typeを使用して作成された証明書がCertificateリストに表示されます。
![](https://qcloudimg.tencent-cloud.cn/raw/0a0a4fa58cb43e811b21f34bfa91823e.png)
8. **Download**をクリックし、FPS証明書ファイル（`fairplay.cer`）を保存します。
![](https://qcloudimg.tencent-cloud.cn/raw/dcc1be70e6c01658348920c8856ec6c2.png)

[](id:step4)
### ステップ4：華曦達(SDMC)コンソールからFPS証明書ファイルをアップロードします
1. [SDMC DRMコンソール](https://www.xmediacloud.com/contact-us/)にログインし、DRM設定メニューに進みます。
![](https://qcloudimg.tencent-cloud.cn/raw/3147f0f1b675351dfdde217fc5449ceb.png)
2. **DRM設定** > **設定メニュー**からFPS証明書登録に進み、更新ボタンをクリックして証明書をアップロードします。
![](https://qcloudimg.tencent-cloud.cn/raw/b6e7c92bab1dc0c7efa7b8bbfc179303.png)
3. FPS証明書ファイル、秘密鍵ファイル、秘密鍵パスワードファイルおよびASKファイルをアップロードし、**OK**をクリックしてアップロードします。
![](https://qcloudimg.tencent-cloud.cn/raw/c318449d607d21ed74d2aaaa89119f9e.png)


>? DRMまたは華曦達への接続プロセスで発生したいかなる問題についても、[お問い合わせ](https://console.cloud.tencent.com/workorder/category)からチケットを提出することができます。すべての工程でお客様の問題解決をサポートします。
