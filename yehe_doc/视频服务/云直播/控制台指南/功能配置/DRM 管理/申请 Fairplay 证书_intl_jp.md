Apple社のFairPlay Streaming (FPS)DRMを使用するには、コンテンツサプライヤーはアップル社からFPSデプロイパッケージを入手し、以下のファイルをSDMC認証サーバにアップロードしてください。
- FPS証明書ファイル（`.der` または `.cer`）
- プライベートキー(`.pem`)
- プライベートキーファイル(`.txt`)
- アプリケーションキー(ASK)ファイル(`.txt`)

## 操作手順
 [](id:step1)
### ステップ1：Apple開発者アカウントの登録とデプロイパッケージの申請
1. [Appleアカウント登録サイト](https://developer.apple.com/support/enrollment/)にアクセスしてアカウントを登録します。
2. [FairPlay Streaming](https://developer.apple.com/streaming/fps/)サイトの一番下の[Request FPS Deployment Package](https://developer.apple.com/contact/fps/)をクリックし、Apple開発者アカウントでログインします。
3. 入力フォームでデプロイパッケージを申請した場合、Appleに承認されると、FPS 認証情報作成ガイドを含んだパッケージを受信します。

>! 申請中に、キーサーバモジュール(KSM)の実装とテストが完了しているかが聞かれます。以下のように回答してください：
```
I am using a 3rd party DRM company and the company has already built and tested KSM
```

 [](id:step2)
### ステップ2：プライベートキーと証明書署名リクエスト(CSR)の作成
デプロイパッケージ中のガイドに従って、プライベートキー(`privatekey.pem`)ファイルと証明書署名リクエスト(`certreq.csr`)ファイルを作成します。以下にガイドに載っている証明書署名リクエスト部分のOpenSSL方法を説明します。
>! このステップを実施するPCまたはサーバにOpenSSLをインストールしなければなりません。

1. **プライベートキーファイル(privatekey.pem)の作成**
	1. 以下のコマンドを実行して、プライベートキーを作成します：[](id:step1_1)
```
openssl genrsa -aes256 -out privatekey.pem 1024
```
	2. プライベートキーのパスワードを入力して、今後に備え覚えてください（パスワードは32文字より少なくしてください）。
2. **証明書署名リクエストファイルの作成**：
	1. 以下のコマンドを実行し、組織と一致するように `-subj` パラメーターを設定します。
```
openssl req -new -sha1 -key privatekey.pem -out certreq.csr -subj "/CN=SubjectName/OU=OrganizationalUnit/O=Organization/C=US"
```
	2. [前のステップ](#step1_1)でのプライベートキーパスワードを入力します。

[](id:step3)
### ステップ3：Apple Developer PortalでのFPS証明書の作成
1. [Apple Developer Portal](https://developer.apple.com/)にログインし、[Certificates, IDs, & Profiles](https://developer.apple.com/account/ios/certificate/)に進みます。
![](https://qcloudimg.tencent-cloud.cn/raw/3c2963e1317986b25f05014042f120de.png)
2. メニューで**+**ボタンをクリックすると、Create a New Certificate画面にジャンプします。
![](https://qcloudimg.tencent-cloud.cn/raw/79a02a3d039ae6bfe40144e2d90b0d44.png)
3. **FairPlay Streaming Certificate**を選択して、**Continue**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/fef15cd65ddf3c21752c3b71c37b9b04.png)
4. **Choose File**をクリックし、前述したステップで作成した`certreq.csr`ファイルを作成して、**Continue**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/d179f0554b61453a51e2a6efa83338e9.png)
5. Application Secret Key (ASK)文字列をコピーして、独立したファイルに保存します。その後、下側のスペースのところにコピーして、**Continue**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/3a69ea9e79824df5d39213373830c8a2.png)
6. ASK文字列を独立したファイルに保存しているかを問い合わせるダイアログが表示されます。保存されている場合、**Generate**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/1a9471e089b5224e393b8efecd5a77c7.png)
7. 上記のステップを完了すると、FairPlay Streaming typeで作成した証明書はCertificateリストに表示されます。
![](https://qcloudimg.tencent-cloud.cn/raw/0a0a4fa58cb43e811b21f34bfa91823e.png)
8. **Download**をクリックして、FPS証明書ファイル(`fairplay.cer`)を保存します。
![](https://qcloudimg.tencent-cloud.cn/raw/dcc1be70e6c01658348920c8856ec6c2.png)

[](id:step4)
### ステップ4：SDMCコンソールによるFPS証明書ファイルのアップロード
1. [SDMC DRMコンソール](https://www.xmediacloud.com/contact-us/)にログインし、DRM設定メニューに進みます。
![](https://qcloudimg.tencent-cloud.cn/raw/3147f0f1b675351dfdde217fc5449ceb.png)
2. **DRM設定** > **設定メニュー**をクリックし、FPS証明書登録に進み、更新ボタンをクリックして証明書をアップロードします。
![](https://qcloudimg.tencent-cloud.cn/raw/b6e7c92bab1dc0c7efa7b8bbfc179303.png)
3. FPS証明書ファイル、プライベートキーファイル、プライベートキーパスワードファイル とASKファイルをアップロードし、**OK**をクリックしてアップロードします。
![](https://qcloudimg.tencent-cloud.cn/raw/c318449d607d21ed74d2aaaa89119f9e.png)
