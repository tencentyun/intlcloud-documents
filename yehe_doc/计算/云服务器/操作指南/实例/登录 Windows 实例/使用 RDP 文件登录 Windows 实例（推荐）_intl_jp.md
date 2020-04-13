## ユースケース

RDPはRemote Desktop Protocolの略称であり。お客様のローカルコンピュータがリモートコンピュータに接続できるようにするためにMicrosoftが開発したマルチチャネルプロトコルです。 Tencent Cloudは、Windows CVMへのログインにRDP方式を推奨しています。このドキュメントは、RDPファイルを使用してWindowsインスタンスにログインする方法について説明します。

## ローカルOSに適用する
Windows、Linuxと Mac OSは全てRDPを使用してCVMにログインすることができます。

## 前提条件

- Windowsインスタンスにリモートログインするには、インスタンスの管理者アカウント番号と対応するパスワードを獲得する必要があります。
 - システムのデフォルトパスワードを使用してインスタンスにログインする場合は、[サイト内メール](https://console.cloud.tencent.com/message)にアクセスして取得してください。
 - パスワードを忘れた場合、[インスタンスのパスワードをリセット](https://intl.cloud.tencent.com/document/product/213/16566)してください。
- CVMインスタンスはパブリックネットワークIPを購入済みであり、このインスタンスはCVMインスタンスの3389ポート（クイック設定で購入したCVMインスタンスの場合、デフォルトでアクティブになっています）をアクティブしました。

## 操作手順

### WindowsシステムはRDPを使用してログインする
1.[CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインします。
2. インスタンスの管理画面で、ログインするWindows CVMを選択し、【ログイン】をクリックします。<!--下図に示すように：
![](https://main.qcloudimg.com/raw/e7b1192332a116edca67425a301236be.png)-->
3.ポップアップの【Windowsインスタンスにログインする】ウィンドウで、【RDPファイルでログイン】を選択し、【RDPファイルをダウンロードします】をクリックし、RDPファイルをローカルにダウンロードします。
<!--![](https://main.qcloudimg.com/raw/9bcfe6774b483261d61f648968efe5ee.png)-->
4. ローカルにダウンロードしたRDPファイルをダブルクリックすると、リモートでWindows CVMに接続できます。
 - システムのデフォルトパスワードを使用してインスタンスにログインする場合は、[サイト内メール](https://console.cloud.tencent.com/message)にアクセスしてパスワードを取得してください。
 - パスワードを忘れた場合、[インスタンスのパスワードをリセット](https://intl.cloud.tencent.com/document/product/213/16566)してください。

### LinuxシステムはRDPを使用してログインする

>対応するリモートデスクトップ接続プログラムをインストールする必要があり、rrdesktopを使用して接続することをお勧めします。詳細については、 [rdesktop 公式説明](http://www.rdesktop.org/)をご参照ください。
>
1. 以下のコマンドを実行し、システムにrdesktopをインストールされているかどうかを確認します。
```
rdesktop
```
 - rdesktopをインストールしている場合、[ステップ4](#step04)を実行してください。
 - command not foundというプロンプトが表示された場合、rdesktopをインストールされていないことを示し、[ステップ2](#step02)を実行してください。
2. <span id="step02"></span>の端末で以下のコマンドを実行し、rdesktop のインストールパッケージをダウンロードします。この手順はrdesktop 1.8.3バージョンを例として説明します。
```
wget https://github.com/rdesktop/rdesktop/releases/download/v1.8.3/rdesktop-1.8.3.tar.gz
```
最新のインストールパッケージが必要な場合、[GitHub rdesktop画面](https://github.com/rdesktop/rdesktop/releases)にアクセスし、最新のインストールパッケージを検索して、またコマンドラインで最新のインストールパスに置き換えることができます。
3. rdesktopをインストールするディレクトリで、以下のコマンドを実行し、rdesktopを解凍してインストールします。
```
tar xvzf rdesktop-<x.x.x>.tar.gz ##x.x.xをダウンロードしたバージョン番号に置き換えます 
cd rdesktop-1.8.3
./configure 
make 
make install
```
4. <span id="step04">　以下のコマンドを実行し、Windowsインスタンスにリモートデスクトップ接続します。</span>
> 例の中のパラメータを自分のパラメータに変更してください。
>
```
rdesktop -u Administrator -p <your-password> <hostname or IP address>
```
 - `Administrator` は前提条件で入手した管理者アカウントです。
 - `<your-password>` は設定されたログインパスワードです。
   システムのデフォルトパスワードを使用してインスタンスにログインする場合、[サイト内メール](https://console.cloud.tencent.com/message)から取得してください。パスワードを忘れた場合、[インスタンスのパスワードをリセット](https://intl.cloud.tencent.com/document/product/213/16566)してください。
 - `<hostname or IP address>` は WindowsインスタンスのパブリックネットワークIP或いはカスタムドメイン名です。
 
###  MacOS システムはRDPを使用してログインする

>
>- 以下の操作は Microsoft Remote Desktop for Mac を例として説明します。Microsoftは2017年に Remote Desktop クライアントのダウンロードリンクの提供を正式に停止し、子会社HockeyApp により Beta バージョンをリリースしました。
>- 以下の操作は Windows Server 2012 R2  OSに接続されているCloud Virtual Machine を例として説明します。
>
1. [Microsoft Remote Desktop for Mac](https://www.techspot.com/downloads/4698-microsoft-remote-desktop-for-mac.html)をダウンロードして、ローカルにインストールします。
2. MRDを起動して、【Add Desktop】をクリックします。下図に示すように：
![](https://main.qcloudimg.com/raw/e69528d10e9a17dfa26119a090766c49.png)
3. 表示された「Add Desktop」ウィンドウで、以下の手順に従って、接続を作成します。下図に示すように：
![](https://main.qcloudimg.com/raw/d8e20278dd7c8aed487be2c43986f5e4.png)
    1. 「PC name」に CVM のパブリックネットワークIPを入力します。
    2. 【Add】をクリックして、接続の作成を確認します。
    3. 他のオプションはデフォルト設定のままで、接続が作成されます。
    ウィンドウで作成された接続を確認できます。下図に示すように：
![](https://main.qcloudimg.com/raw/1c0eff28aa68a7f02e8f295917bb603b.png)
4.新しく作成した接続をダブルクリックして開き、ポップアップウィンドウでプロンプトに従って、CVMのアカウントとパスワードを入力し、【Continue】をクリックしてください。
 - システムのデフォルトパスワードを使用してインスタンスにログインする場合は、[サイト内メール](https://console.cloud.tencent.com/message)にアクセスして取得してください。
 - パスワードを忘れた場合、[インスタンスのパスワードをリセット](https://intl.cloud.tencent.com/document/product/213/16566)してください。
5. ポップアップウインドウで【Continue】をクリックし、接続を確認します。下図に示すように：
![](https://main.qcloudimg.com/raw/61b3d9566365183fcc1d92c2f6bc2e7b.png)
接続に成功すると、Windows CVMのインターフェース を開きます。<!--下図に示すように：
![](https://main.qcloudimg.com/raw/5a524210acd13624af7263b6de3aea54.png)-->
