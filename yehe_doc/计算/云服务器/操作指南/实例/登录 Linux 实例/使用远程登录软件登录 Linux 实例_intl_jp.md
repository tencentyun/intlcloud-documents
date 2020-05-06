## ユースケース

このドキュメントでは、PuTTYソフトウェアを例として、WindowsのローカルPCでリモートログインソフトウェアを使用して、Linuxインスタンスにログインする方法について説明します。


## 対応OS

Windows

## 認証方式

**パスワード**または**キー**です。

## 前提条件
- インスタンスにログインするための管理者アカウント及びパスワード(またはキー)は取得しました。
 - システムのデフォルトパスワードを利用して、インスタンスにログインする場合は、[サイト内メール](https://console.cloud.tencent.com/message) にアクセスしてパスワードを取得してください。
 - パスワードを忘れた場合、[インスタンスパスワードをリセット](http://intl.cloud.tencent.com/document/product/213/16566)してください。
- CVMインスタンスのパブリックIPを購入して取得し、且つポート22（クイック設定で購入したCVMインスタンスの場合、デフォルトで開放している）を開放しました。


## 操作手順

### パスワードでログインする

1. WindowsリモートログインソフトウェアPuTTYをダウンロードします。
PuTTYをダウンロードするには：[ここをクリック](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)してください。
2. 【putty.exe】をダブルクリックして、PuTTYクライアントを開きます。
3.  PuTTY Configuration ウィンドウで、次の内容を入力します。 下記画像に示すように：
![](https://main.qcloudimg.com/raw/7ac87da9721ef7d64fe8cac81a3dab33.png)
パラメータは次のとおりです：
 - Host Name（or IP address）：CVMのパブリックIPアドレスです。（[CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインし、インスタンスリストと詳細画面でパブリックIPを取得できます）。
 - Port：CVMのポート。これは22に設定する必要があります。
 - Connect type：「SSH」を選択します。
 - Saved Sessions：testなどのセッション名を入力します。
 「Host Name」を設定した後、「Saved Sessions」を設定して保存したら、「Saved Sessions」の下に保存されたセッション名をダブルクリックしてCVMにログインできます。
3. 【Open】をクリックして「PuTTY」インターフェースに入り、「login as:」が提示されます。
4.「login as」の後にユーザー名を入力し、** Enter**キーを押します。
5.「Password」の後にパスワードを入力し、** Enter**キーを押します。
ログインが完了すると、コマンドプロンプトの左側にCVMへの現在のログイン情報が表示されます。下記画像に示すように：
![](https://main.qcloudimg.com/raw/9e7ddc631de2a27bfd35f9225de85506.png)

### キーでログインする

1. WindowsリモートログインソフトウェアPuTTyをダウンロードします。
putty.exeおよびputtygen.exeソフトウェアをダウンロードしてください。PuTTyをダウンロードするには：[ここをクリック](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)してください。。
2. 【puttygen.exe】をダブルクリックして、PuTTy Keyクライアントを開きます。
3. 【Load】をクリックし、ダウンロードしたプライベートキーストレージパスを選択して開きます。下記画像に示すように：
例えば、davidという名前のプライベートキーファイルを選択して開きます。
![](https://main.qcloudimg.com/raw/0110ba722331fb2892a8e6822ec3f709.png)
4. PuTTY Key Generator ウィンドウで、キー名と暗号化されたプライベートキーのパスワードを入力し、【Save private key】をクリックします。 下記画像に示すように：
![](https://main.qcloudimg.com/raw/58a250d3f3d1b78eff3edaab64cd01c0.png)
5. ポップアップウィンドウで、キーを保存するパスを選択します。ファイル名フィールドに「キー名.ppk」と入力して、【保存】をクリックします。 例えば、davidプライベートキーファイルをdavid.ppkキーファイルとして保存します。 下記画像に示すように：
![](https://main.qcloudimg.com/raw/44df54ca77069356a26c51e2a4db7643.png)
6. 【putty.exe】をダブルクリックして、PuTTYクライアントを開きます。
7. 左側のナビゲーションバーで、【Connection】>【SSH】>【Auth】を選択して、Auth設定インターフェースを開きます。
8. 【Browse】をクリックし、キーのストレージパスを選択して開きます。 下記画像に示すように：
![](https://main.qcloudimg.com/raw/61993f3977ff681b8b2d78beac55f2ca.png)
8. Session設定インターフェースに切り替えて、 CVM IP、ポート、および接続タイプを設定します。 下記画像に示すように：
![](https://main.qcloudimg.com/raw/ddfd58429288ce0e195e86a6cb1c9cd6.png)
 - Host Name (IP address)：CVMのパブリックIPアドレスです。 [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインし、インスタンスリストと詳細画面でパブリックIPを取得できます。
 - Port：CVMのポート。22を記入する必要があります。
 - Connect type：「SSH」を選択します。
 - Saved Sessions：testなどのセッション名を入力します。
 「Host Name」を設定した後、「Saved Sessions」を設定して保存したら、「Saved Sessions」の下に保存されたセッション名をダブルクリックしてCVMにログインできます。
9. 【Open】をクリックして、ログインリクエストを発行します。


