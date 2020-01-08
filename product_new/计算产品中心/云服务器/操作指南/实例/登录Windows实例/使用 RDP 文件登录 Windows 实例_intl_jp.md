## ユースケース

RDPはRemote Desktop Protocolの略称であり、Microsoftが開発したマルチチャネルのプロトコルです。お客様のローカルコンピュータがリモートコンピュータに接続することに役立ちます。RDPがWindows CVMにログインする方式としてTencent Cloudに推薦されました。このドキュメントは、RDPファイルを使用してWindowsインスタンスにログインする方法について説明します。

## ローカルOSに適用する
Windows、Linuxと Mac OSは全てRDP方式でCVMにログインすることができます。

## 前提条件

- Windows インスタンスをリモートログインするために必要なインスタンスの管理者アカウントと該当するパスワードを獲得しました。
 - システムのデフォルトパスワードでインスタンスにログインする場合、[内部メッセージ](https://console.cloud.tencent.com/message)から取得してください。
 - パスワードを忘れた場合、 [インスタンスのパスワードをリセット](https://intl.intl.intl.intl.cloud.tencent.com/document/product/213/16566)してください。
- CVMインスタンスはパブリックネットワークIPを購入済みであり、このインスタンスはCVMインスタンスの3389ポート（クイック構成で購入したCVMインスタンスの場合、デフォルトでアクティブになっています）をアクティブしました。

## 操作手順

### WindowsシステムはRDPでログインする
1.[CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインします。
2. インスタンスの管理画面で、ログインしたいWindows CVMを選択し、【ログイン】をクリックします。
3.ポップアップの【Windowsインスタンスのログイン】ウィンドウで、【RDPファイルによりログイン】を選択し、【RDPファイルをダウンロードする】をクリックし、RDPファイルをローカルにダウンロードします。
4. ローカルにダウンロードしたRDPファイルをダブルクリックすると、リモートでWindows CVMに接続できます。
 - システムのデフォルトパスワードでインスタンスにログインする場合、[内部メッセージ](https://console.cloud.tencent.com/message)から取得してください。
 - パスワードを忘れた場合、 [インスタンスのパスワードをリセット](https://intl.intl.intl.intl.cloud.tencent.com/document/product/213/16566)してください。

### LinuxシステムはRDPでログインする

>対応するリモートデスクトップ接続プログラムをインストールする必要があり、rrdesktopを使用して接続することをお勧めします。詳細については、 [rdesktop 公式説明](http://www.rdesktop.org/)をご参照ください。
>
1. 以下のコマンドを実行し、システムの中にrdesktopをインストールしたかどうかを確認します。
```
rdesktop
```
 - rdesktopをインストールした場合、[ステップ4](#step04)を実行してください。
 - command not foundが表示される場合、rdesktopはまだインストールしていないことを示し、[ステップ2](#step02)を実行してください。
2. <span id="step02"></span>の端末で以下のコマンドを実行し、rdesktop のインストールパッケージをダウンロードします。この手順はrdesktop 1.8.3バージョンを例とします。
```
wget https://github.com/rdesktop/rdesktop/releases/download/v1.8.3/rdesktop-1.8.3.tar.gz
```
最新のインストールパッケージが必要であれば、[GitHub rdesktop画面](https://github.com/rdesktop/rdesktop/releases)にアクセスし、最新のインストールパッケージを検索して、またコマンドラインで最新のインストールパスに置き換えることができます。
3. rdesktopをインストールするディレクトリで、以下のコマンドを実行し、rdesktopを解凍とインストールします。
```
tar xvzf rdesktop-<x.x.x>.tar.gz ##x.x.xをダウンロードのバージョン番号に置き換える 
cd rdesktop-1.8.3
./configure 
make 
make install
```
4. <span id="step04">　以下のコマンドを実行し、Windowsのインスタンスにリモートで接続します。</span>
> 例の中のパラメータを自分のパラメータに変更してください。
>
```
rdesktop -u Administrator -p <your-password> <hostname or IP address>
```
 - `Administrator` は前提条件で入手した管理者アカウントです。
 - `<your-password>` は設置されたログインパスワードです。
   システムのデフォルトパスワードでインスタンスにログインする場合、[内部メッセージ](https://console.cloud.tencent.com/message)から取得してください。パスワードを忘れた場合、[インスタンスパスワードをリセット](https://intl.intl.intl.intl.cloud.tencent.com/document/product/213/16566)してください。
 - `<hostname or IP address>` は WindowsインスタンスのパブリックネットワークIP或いはカスタマイズのドメイン名です。

###  MacOS システムはRDPでログインする

> 以下の操作は Microsoft Remote Desktop for Mac を例として説明します。このクライアントはテスト用のクライアントであり、Microsoft公式にメンテナンスされています、このバージョンのクライアントを優先的に使用することを推薦します。Microsoft公式サイトは2017年にRemote Desktopクライアントのダウンロードリンクの提供を停止し、子会社のHockeyAppによりBetaバージョンをリリースしました。
>
1. [Microsoft Remote Desktop for Mac](https://rink.hockeyapp.net/apps/5e0c144289a51fca2d3bfa39ce7f2b06/)をダウンロードします。
2. クライアントツールを開き、【Add Deskop】をクリックします。下図に示すように：
![](https://main.qcloudimg.com/raw/d310a22009134182def49929625e6f1d.png)
3. 表示されるダイアログボックで、WindowsインスタンスのパブリックネットワークIPを入力し、【Add】をクリックし、リモートデスクトップに追加します。下図に示すように：
![](https://main.qcloudimg.com/raw/57d7f343e8d52d9365fcd4f4ada5d090.png)
4. 新しく追加されたリモートデスクトップをダブルクリックし、インスタンスの管理者アカウントと該当するパスワードを入力し、 リモートでWindows CVMに接続します。
 - システムのデフォルトパスワードでインスタンスにログインする場合、[内部メッセージ](https://console.cloud.tencent.com/message)から取得してください。
 - パスワードを忘れた場合、[インスタンスのパスワードをリセット](https://intl.intl.intl.intl.cloud.tencent.com/document/product/213/16566)してください。
