## ユースケース

リモートデスクトッププロトコル（RDP）は、Microsoft社が開発したマルチチャネルのプロトコルです。お客様のローカルコンピュータからリモートコンピュータに接続するのに役立ちます。Tencent Cloudでは、RDPを使用してWindows CVMにログインすることをお勧めします。このドキュメントでは、RDPファイルを使用してWindowsインスタンスにログインする方法について説明します。

## ローカルOSに適用する
Windows、LinuxとMac OSは、いずれもRDP方式でCVMにログインすることができます。

## 前提条件

- Windows インスタンスにリモートログインするために必要なインスタンスの管理者アカウントと対応するパスワードを取得しました。
 - システムのデフォルトパスワードを利用して、インスタンスにログインする場合は、[サイト内メッセージ](https://console.cloud.tencent.com/message)に進んでパスワードを取得してください。
 - パスワードを忘れた場合、[インスタンスパスワードのリセット](https://intl.cloud.tencent.com/document/product/213/16566)をご参照ください。
- ご利用のCVMインスタンスはパブリックネットワークIPを購入済みであり、このインスタンスはCVMインスタンスの3389ポート（クイック構成で購入したCVMインスタンスの場合、このポートはデフォルトで開いている）が開いています。

## 操作手順

### WindowsシステムはRDPでログインする
1.[CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインします。
2. インスタンスの管理画面で、下図に示すように、ログインするWindows CVMを選択し、【ログイン】をクリックします。
![](https://main.qcloudimg.com/raw/e7b1192332a116edca67425a301236be.png)
3.ポップアップされた【Windowsインスタンスにログインする】画面で、【RDPファイルでログイン】を選択し、【RDPファイルをダウンロードします】をクリックし、RDPファイルをローカルにダウンロードします。
![](https://main.qcloudimg.com/raw/0b0076390b95da3885c8967093683975.png)
4. ローカルにダウンロードしたRDPファイルをダブルクリックすると、リモートでWindows CVMに接続できます。
 - システムのデフォルトパスワードを使用してインスタンスにログインする場合は、[サイト内メッセージ](https://console.cloud.tencent.com/message)に進んでパスワードを取得してください。
 - パスワードを忘れた場合、[インスタンスパスワードをリセット](https://intl.cloud.tencent.com/document/product/213/16566)してください。

### LinuxシステムはRDPでログインする

>リモートデスクトップクライアントとしてrdesktopを使用することをお勧めします。詳細については、 [rdesktop 公式説明](http://www.rdesktop.org/)をご参照ください。
>
1. 以下のコマンドを実行し、システムにrdesktopがインストールされているかを確認します。
```
rdesktop
```
 - rdesktopがインストール済みの場合、[ステップ4](#step04)を実行してください。
 - command not foundがというプロンプトが表示される場合、rdesktopはインストールしていないことを示し、[ステップ2](#step02)を実行してください。
2. <span id="step02"></span>ターミナルウィンドウで以下のコマンドを実行し、rdesktop のインストールパッケージをダウンロードします。この手順はrdesktop 1.8.3バージョンを例として説明します。
```
wget https://github.com/rdesktop/rdesktop/releases/download/v1.8.3/rdesktop-1.8.3.tar.gz
```
rdesktopの最新バージョンをインストールするには、[GitHub rdesktopページ](https://github.com/rdesktop/rdesktop/releases)に進んで、最新のインストールパッケージを検索して、コマンドのインストールパスを新しいパスに置き換えます。
3. rdesktopをインストールするディレクトリで、以下のコマンドを実行し、rdesktopを解凍してインストールします。
```
tar xvzf rdesktop-<x.x.x>.tar.gz ##のx.x.xをダウンロードしたバージョン番号に置き換える 
cd rdesktop-1.8.3
./configure 
make 
make install
```
4. <span id="step04">以下のコマンドを実行し、Windowsインスタンスにリモートで接続します。</span>
> 例の中のパラメータをお客様のパラメータに変更してください。
>
```
rdesktop -u Administrator -p <your-password> <hostname or IP address>
```
 - `Administrator` は前提条件で入手した管理者アカウントです。
 - `<your-password>` は設定されたログインパスワードです。
   システムのデフォルトパスワードを使用してインスタンスにログインする場合、[サイト内メッセージ](https://console.cloud.tencent.com/message)から取得してください。パスワードを忘れた場合、[インスタンスパスワードのリセット](https://intl.intl.intl.intl.cloud.tencent.com/document/product/213/16566)をご参照ください。
 - `<hostname or IP address>` は WindowsインスタンスのパブリックネットワークIPまたはカスタマイズのドメイン名です。
 
###  MacOS システムはRDPでログインする

>
>- 次の操作は、Microsoft Remote Desktop for Macを例として説明します。マイクロソフト社は、2017年にRemote Desktopクライアントへのダウンロードリンクの提供を停止し、ベータ版のリリースは、その子会社である[HockeyApp]（https://appcenter.ms/apps）によって提供されます。
>- 次の操作は、Windows Server 2012 R2 OSに接続するCVMを例として説明します。
>
1. Microsoft Remote Desktop for Macをダウンロードして、ローカルにインストールします。
2. MRDを起動し、以下に示すように、【Add Desktop】をクリックします。
![](https://main.qcloudimg.com/raw/e69528d10e9a17dfa26119a090766c49.png)
3.ポップアップされた「Add Desktop」画面で、 次に示すように、以下の手順に従ってWindows CVMへの接続を確立します。
![](https://main.qcloudimg.com/raw/d8e20278dd7c8aed487be2c43986f5e4.png)
    1.「PC name」テキストボックスに、CVMのパブリックIPアドレスを入力します。
    2.【Add】をクリックして、作成を確認します。
    3. 他のオプション項目をデフォルト設定のままにして、接続の確立が完了します。
    以下に示すように、正常に作成された接続が画面に表示されます。
![](https://main.qcloudimg.com/raw/1c0eff28aa68a7f02e8f295917bb603b.png)
4. 新しく作成した接続をダブルクリックして開き、ポップアップされた画面の指示従って、CVMのアカウントとパスワードを入力し、【Continue】をクリックします。
 - システムのデフォルトパスワードでインスタンスにログインする場合は、[サイト内メッセージ](https://console.cloud.tencent.com/message)に進んで取得してください。
 - パスワードを忘れた場合、[インスタンスパスワードのリセット](https://intl.cloud.tencent.com/document/product/213/16566)をご参照ください。
5.ポップアップされた画面で、以下に示すように、【Continue】をクリックして、接続を確立します。
![](https://main.qcloudimg.com/raw/61b3d9566365183fcc1d92c2f6bc2e7b.png)
接続が成功すると、以下に示すように、Windows CVM画面が表示されます。
![](https://main.qcloudimg.com/raw/20db4a1d63384bc0575ded68a8fe912d.png)
