## 操作ケース

このドキュメントでは、PuTTYソフトウェアを例として、WindowsOSのローカルPCでリモートログインソフトウェアを使用して、Linuxインスタンスにログインする方法について説明します。


## 対応OS

Windows

## 認証方式

**パスワード**または**キー**

## 前提条件
- インスタンスにログインするための管理者アカウント及びパスワード(またはキー)を取得しました。
 - システムのデフォルトパスワードを利用して、インスタンスにログインする際は、[内部メッセージ](https://console.cloud.tencent.com/message)にアクセスして取得してください。
 - パスワードを忘れた場合、[インスタンスパスワードを再設定](https://intl.cloud.tencent.com/document/product/213/16566)してください。
- CVMインスタンスのパブリックIPを購入して取得し、且つこのインスタンスはCVMインスタンスのポート22（クイック設定で購入したCVMインスタンスの場合、デフォルトで開放している）を開放しました。


## 操作手順

### パスワードでログインする

1. WindowsリモートログインソフトウェアPuTTYをダウンロードします。
PuTTYをダウンロードするには：[ここをクリック](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)してください。
2. 【putty.exe】をダブルクリックして、PuTTYクライアントを開きます。
3.  PuTTY Configuration ウィンドウで、次の内容を入力します。 以下の通りです：
![](https://main.qcloudimg.com/raw/7ac87da9721ef7d64fe8cac81a3dab33.png)
パラメータは次のとおりです：
 - Host Name（or IP address）：CVMのパブリックIPアドレスです。（[CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインし、インスタンスリストと詳細画面でパブリックIPを取得できます）。
 - Port：CVMのポート。これは22に設定する必要があります。
 - Connect type：「SSH」を選択します。
 - Saved Sessions：testなどのセッション名を入力します。
 「Host Name」を設定した後、「Saved Sessions」を設定して保存したら、「Saved Sessions」の下に保存されたセッション名をダブルクリックしてCVMにログインできます。
4. 【Open】をクリックして「PuTTY」インターフェースに入り、「login as:」が提示されます。
5.「login as」の後にユーザー名を入力し、** Enter**キーを押します。
6.「Password」の後にパスワードを入力し、** Enter**キーを押します。
次の図に示すように、入力したパスワードはデフォルトでは表示されません。
![](https://main.qcloudimg.com/raw/9e7ddc631de2a27bfd35f9225de85506.png)
ログインが完了すると、コマンドプロンプトの左側にCVMへの現在のログイン情報が表示されます。

### キーでログインする

1. WindowsリモートログインソフトウェアPuTTyをダウンロードします。
putty.exeおよびputtygen.exeソフトウェアをダウンロードしてください。PuTTyをダウンロードするには：[ここをクリック](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)してください。。
2. 【puttygen.exe】をダブルクリックして、PuTTy Keyクライアントを開きます。
3. 【Load】をクリックし、ダウンロードしたプライベートキーストレージパスを選択して開きます。以下の通りです：
例えば、ファイル名davidのプライベートキーファイルを選択して開きます。
![](https://main.qcloudimg.com/raw/0110ba722331fb2892a8e6822ec3f709.png)
4. <span id="Step4"></span>PuTTY Key Generatorウィンドウで、キー名を入力し、PuTTYのプライベートキーの暗号化に使用するパスワードを設定します（オプション）。設定が完了したら、【Save private key】をクリックします。以下の通りです。
![](https://main.qcloudimg.com/raw/58a250d3f3d1b78eff3edaab64cd01c0.png)
5. ポップアップウィンドウで、キーを保存するパスを選択します。ファイル名フィールドに「キー名.ppk」を入力して、【保存】をクリックします。 例えば、davidプライベートキーファイルをdavid.ppkキーファイルとして名前を付けて保存します。 以下の通りです：
![](https://main.qcloudimg.com/raw/44df54ca77069356a26c51e2a4db7643.png)
6. 【putty.exe】をダブルクリックして、PuTTYクライアントを開きます。
7. 左側のナビゲーションバーで、【Connection】>【SSH】>【Auth】を選択して、Auth設定インターフェースを開きます。
8. 【Browse】をクリックし、キーのストレージパスを選択して開きます。 以下の通りです：
![](https://main.qcloudimg.com/raw/61993f3977ff681b8b2d78beac55f2ca.png)
8. Session設定インターフェースに切り替えて、 CVM IP、ポート、および接続タイプを設定します。 以下の通りです：
![](https://main.qcloudimg.com/raw/ddfd58429288ce0e195e86a6cb1c9cd6.png)
 - Host Name (IP address)：CVMのパブリックIPアドレスです。 [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインし、インスタンスリストと詳細画面でパブリックIPを取得できます。
 - Port：CVMのポート。22を記入する必要があります。
 - Connect type：「SSH」を選択します。
 - Saved Sessions：testなどのセッション名を入力します。
 「Host Name」を設定した後、「Saved Sessions」を設定して保存したら、「Saved Sessions」の下に保存されたセッション名をダブルクリックしてCVMにログインできます。
9. 【Open】をクリックして「PuTTY」インターフェースに入り、「login as:」が提示されます。
10.「login as」の後にユーザー名を入力し、** Enter**キーを押します。
11. [ステップ4](#Step4)に従ってプライベートキー暗号化用のパスワードを設定した場合は、「Passphrase for key "imported-openssh-key":」にパスワードを入力した後、**Enter**を押してください。
次の図に示すように、入力したパスワードはデフォルトでは表示されません。
![](https://main.qcloudimg.com/raw/89b2ef5f04a6402f0b1832301fa811cb.png)
ログインが完了すると、コマンドプロンプトの左側にCVMへの現在のログイン情報が表示されます。



## 後続の操作

CVMにログインした後、パーソナルサーバーまたはフォーラムを構築したり、その他の操作を実行したりできます。関連操作については、下記をご参照ください：　　
- [WordPress パーソナルサーバーを構築する](https://intl.cloud.tencent.com/document/product/213/8044)
- [Discuz! フォーラムを構築する](https://intl.cloud.tencent.com/document/product/213/8043)

