## ユースケース

WebShellはTencent Cloudに推薦されたログイン方式です。お客様のロカールOSはWindows、Linux、またはMac OSのどちらでも、インスタンスがパブリックIPを購入している限り、WebShellによりログインすることができます。このドキュメントは、標準ログイン方式（WebShell）を利用してLinux インスタンスにログインする方法について説明します。
WebShellの利点は下記の通り：
- コピー＆ペーストのショートカットキーをサポートします。
- マウスのスクロールをサポートします。
- 中国語入力をサポートします。
- セキュリティが高い、ログインするたびにパスワードまたはキーを入力する必要があります。

## ローカルOSに適する

Window、Linux、またはMac OS

## 認証方式

**パスワード**または**キー**

## 前提条件

- インスタンスにログインするための管理者アカウント及びパスワード(またはキー)は取得しました。
 - システムのデフォルトパスワードを利用して、インスタンスにログインする際は、[内部メッセージ](https://console.cloud.tencent.com/message)にアクセスして取得してください。
 - パスワードを忘れた場合、[インスタンスパスワードをリセット](https://intl.cloud.tencent.com/document/product/213/16566)してください。
- お客様のCVMインスタンスはパブリックIPを購入し、このインスタンスはCVMインスタンスの22ポート（クイック設定により購入したCVMインスタンスの場合、デフォルトで開通になっています）を開通しました。

## 操作手順

1. [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインします。
2. インスタンスの管理画面で、ログインするLinux CVMを選択して、【ログイン】をクリックします。
![](https://main.qcloudimg.com/raw/cc5786b9f8b57ff4057b666503729bc0.png)
3.【Linuxインスタンスのログイン】ポップアップウインドウで、【標準ログイン方式】を選択して、【今すぐログイン】をクリックします。
![](https://main.qcloudimg.com/raw/cc5786b9f8b57ff4057b666503729bc0.png)
4. 開いたWebShellのログイン画面で、実際のニーズにより、【パスワードログイン】または【キーログイン】を選択してログインします。
![](https://main.qcloudimg.com/raw/87ba7e511f8d0ffe48f220cecaa7b057.png)
ログインが成功すると、WebShellインターフェースにSocket connection establishedのような通知が表示されます。
![](https://main.qcloudimg.com/raw/6bcd152ff947909f52da67430aa7eda6.png)
## 後続の操作

CVMにログインした後、Tencent Cloud CVMでパーソナルサーバーやフォーラムを構築できると同時に、他の操作も利用できます。関連操作については、下記をご参照ください：
- [WordPress パーソナルサーバーを構築する](https://intl.cloud.tencent.com/document/product/213/8044)

