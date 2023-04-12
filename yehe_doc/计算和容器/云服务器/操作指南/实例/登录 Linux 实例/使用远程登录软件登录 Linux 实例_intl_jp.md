## 概要

このドキュメントでは、PuTTYソフトウェアを例として、リモートログインソフトウェアを使用してWindowsからLinuxインスタンスにログインする方法について説明します。


## 対応OS

Windows

## 認証方式

**パスワード**または**キー**です。

## 前提条件
- インスタンスにログインするための管理者アカウント及びパスワード(またはキー)を取得しました。
 - システムのデフォルトパスワードを使用してインスタンスにログインする場合は、[サイト内メール](https://console.cloud.tencent.com/message)にアクセスしてパスワードを取得してください。
 - パスワードを忘れた場合は、[インスタンスのパスワードをリセット](https://intl.cloud.tencent.com/document/product/213/16566)してください。
- CVMインスタンスはすでにパブリックIPを購入されており、このインスタンスは22番ポート（クイック設定で購入したCVMインスタンスの場合、デフォルトで開放している）を開放しました。


## 操作手順
<dx-tabs>
::: パスワードでログインする[](id:passwordLogin)
1. リモートログオンクライアントソフト「PuTTY」をダウンロードします。
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://the.earth.li/~sgtatham/putty/latest/w64/putty.exe" target="_blank" style="color: white; font-size:16px;">ダウンロードPuTTYをダウンロード</a></div>
2. **putty.exe**をダブルクリックして、PuTTYクライアントを開きます。
3.  PuTTY Configuration ウィンドウで、次の内容を入力します。次の図に示すように：
![](https://main.qcloudimg.com/raw/7ac87da9721ef7d64fe8cac81a3dab33.png)
パラメータは次のとおりです：
 - **Host Name（or IP address）**：CVMのパブリックIPアドレスです。（[CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインし、インスタンスリストと詳細画面でパブリックIPを取得できます）。
 - **Port**：CVMのポート。「22」である必要があります。
 - **Connect type**：「SSH」を選択します。
 - **Saved Sessions**：testなどのセッション名を入力します。
 「Host Name」を設定した後、「Saved Sessions」を設定して保存します。「Saved Sessions」の下に保存されているセッション名をダブルクリックしてCVMにログインできます。
4. **Open**をクリックして「PuTTY」インターフェースに入り、「login as:」というコマンドプロンプトが表示されます。
5.「login as」の後にユーザー名を入力し、**Enter**キーを押します。
6.「Password」の後にパスワードを入力し、**Enter**キーを押します。
入力されたパスワードはデフォルトでは表示されません。次の図に示すように：
![](https://main.qcloudimg.com/raw/9e7ddc631de2a27bfd35f9225de85506.png)
ログインが完了すると、コマンドプロンプトの左側に現在ログインしているCVMに関する情報が表示されます。
:::
::: キーでログインする[](id:keyLogin)
1. リモートログオンクライアントソフト「PuTTY」をダウンロードします。putty.exeとputtygen.exeの両方をそれぞれダウンロードして​ください。
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;margin:5px;"><a href="https://the.earth.li/~sgtatham/putty/latest/w64/putty.exe" target="_blank" style="color: white; font-size:16px;">PuTTY</a></div><div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;margin:5px;"><a href="https://the.earth.li/~sgtatham/putty/latest/w64/puttygen.exe" target="_blank" style="color: white; font-size:16px;">PuTTYgen</a></div>
2. **puttygen.exe**をダブルクリックして、PuTTy Keyクライアントを開きます。
3. **Load**をクリックし、ダウンロードした秘密鍵が保存されているパスを選択して開きます。キーペアを作成した後、秘密鍵をダウンロードして保持する必要があります。詳細については、[SSHキーの管理](https://intl.cloud.tencent.com/document/product/213/16691)をご参照ください。
例えば、davidという名前の秘密鍵ファイルを選択して開きます。
![](https://main.qcloudimg.com/raw/0110ba722331fb2892a8e6822ec3f709.png)
4. <span id="Step4"></span>PuTTY Key Generatorウィンドウにキー名を入力し、PuTTY が秘密鍵の暗号化に使用するパスワードを設定します（オプション）。設定が完了したら、【Save private key】をクリックします。次の図に示すように：
![](https://main.qcloudimg.com/raw/58a250d3f3d1b78eff3edaab64cd01c0.png)
5. ポップアップウィンドウで、キーを保存するパスを選択します。ファイル名フィールドに「Key Name.ppk」と入力して、Saveをクリックします。 例えば、david秘密鍵ファイルをdavid.ppkキーファイルとして保存します。次の図に示すように：
![](https://main.qcloudimg.com/raw/fad925e85923ac1d41afacde4a9c690c.png)
6. **putty.exe**をダブルクリックして、PuTTYクライアントを開きます。
7. 左側のナビゲーションバーで、**Connection**>**SSH**>**Auth**を選択して、Auth設定インターフェースに入ります。
8. **Browse**をクリックし、キーが保存されているパスを選択して開きます。次の図に示すように：
![](https://main.qcloudimg.com/raw/61993f3977ff681b8b2d78beac55f2ca.png)
9. Session設定インターフェースに切り替えて、CVM IP、ポート、および接続タイプを設定します。次の図に示すように：
![](https://main.qcloudimg.com/raw/ddfd58429288ce0e195e86a6cb1c9cd6.png)
 - **Host Name (IP address)**：CVMのパブリックIPアドレスです。 [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインし、インスタンスリストと詳細画面でパブリックIPを取得できます。
 - **Port**：CVMのポート。「22」である必要があります。
 - **Connect type**：「SSH」を選択します。
 - **Saved Sessions**：testなどのセッション名を入力します。
 「Host Name」を設定した後、「Saved Sessions」を設定して保存します。「Saved Sessions」の下に保存されたセッション名をダブルクリックしてCVMにログインできます。
10. **Open**をクリックして「PuTTY」インターフェースに入り、「login as:」というコマンドプロンプトが表示されます。
11.「login as」の後にユーザー名を入力し、**Enter**キーを押します。
12.[ステップ4](#Step4) に従って暗号化された秘密鍵のパスワードを設定する場合は、「Passphrase for key "imported-openssh-key":」の後にパスワードを入力し、Enterを押してください。　
入力されたパスワードはデフォルトでは表示されません。次の図に示すように：
![](https://main.qcloudimg.com/raw/89b2ef5f04a6402f0b1832301fa811cb.png)
ログインが完了すると、コマンドプロンプトの左側に現在ログインしているCVMに関する情報が表示されます。
:::
</dx-tabs>

## その後の操作

CVMにログインした後、個人用Webサイトまたはフォーラムを構築したり、その他の操作を実行したりできます。詳細については、下記のドキュメントをご参照ください：　　　　
- [WordPress 個人用サイトを構築する](https://intl.cloud.tencent.com/document/product/213/33469)
- [Discuz!フォーラムを手動で構築する](https://intl.cloud.tencent.com/document/product/213/34278)

