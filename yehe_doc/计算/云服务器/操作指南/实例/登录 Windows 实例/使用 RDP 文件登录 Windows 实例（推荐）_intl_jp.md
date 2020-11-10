## 操作シナリオ

リモートデスクトッププロトコル（RDP）は、Microsoftが開発したマルチチャネルプロトコルです。お客様のローカルコンピュータをリモートコンピュータに接続することに役立ちます。RDPを使用してWindows CVMにログインすることをお勧めします。このドキュメントは、RDPファイルを使用してWindowsインスタンスにログインする方法について説明します。

## ローカルOSに適用する
Windows、Linuxと Mac OSは全てRDP方式でCVMにログインすることができます。

## 前提条件

- Windowsインスタンスにリモートでログインするには、インスタンスの管理者アカウントと対応するパスワードを取得する必要があります。
 - システムのデフォルトパスワードを利用して、インスタンスにログインする場合は、[サイト内メール](https://console.cloud.tencent.com/message)にアクセスしてパスワードを取得してください。
 - パスワードを忘れた場合、[インスタンスパスワードのリセット](https://intl.cloud.tencent.com/document/product/213/16566)を実行してください。
- CVMインスタンスがパブリックIPを購入済みで、ポート3389が開いています。

## 操作手順

### WindowsシステムはRDPでCVMにログインする
1. [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインします。
2. インスタンスの管理画面で、ログインしたいWindows CVMを選択し、下図に示すように、【ログイン】をクリックします。
![](https://main.qcloudimg.com/raw/e7b1192332a116edca67425a301236be.png)
3. ポップアップの【Windowsインスタンスにログインする】ウィンドウで、【RDPファイルを使用してログイン】を選択し、【RDPファイルをダウンロード】をクリックし、RDPファイルをローカルにダウンロードします。
>?リモートログインポートを変更した場合は、RDPファイルを変更し、IPアドレスの後に`:ポート`を追加する必要があります。
![](https://main.qcloudimg.com/raw/0b0076390b95da3885c8967093683975.png)
4. ローカルにダウンロードしたRDPファイルをダブルクリックし、パスワードを入力して【OK】をクリックすると、リモートでWindows CVMに接続できます。
 - システムのデフォルトパスワードを利用して、インスタンスにログインする場合は、[サイト内メール](https://console.cloud.tencent.com/message)にアクセスしてパスワードを取得してください。
 - パスワードを忘れた場合、[インスタンスパスワードのリセット](https://intl.cloud.tencent.com/document/product/213/16566)を実行してください。

### LinuxシステムはRDPでCVMにログインする

> 対応するリモートデスクトップ接続プログラムをインストールする必要があり、rdesktopを使用して接続することをお勧めします。詳細については、 [rdesktop 公式説明](http://www.rdesktop.org/)をご参照ください。
>
1. 次のコマンドを実行して、rdesktopがインストールされているかどうかを確認します。
```
rdesktop
```
 - rdesktopがインストール済みの場合、[ステップ4](#step04)を実行してください。
 - 「command not found」というプロンプトが表示される場合、rdesktopがまだインストールされていないことを示しています。この場合、[ステップ2](#step02)を実行してください。
2. <span id="step02"></span>ターミナルウィンドウを開き、次のコマンドを実行してrdesktopをダウンロードします。この手順はrdesktop 1.8.3バージョンを例とします。
```
wget https://github.com/rdesktop/rdesktop/releases/download/v1.8.3/rdesktop-1.8.3.tar.gz
```
最新バージョンをインストールする場合は、[GitHub rdesktop画面](https://github.com/rdesktop/rdesktop/releases)にアクセスし、最新のインストールパッケージを検索して、またコマンドのパスを最新バージョンのパスに置き換えます。
3. rdesktopをインストールするディレクトリで、次のコマンドを実行して、rdesktopを解凍してインストールします。
```
tar xvzf rdesktop-<x.x.x>.tar.gz ##x.x.xをダウンロードしたバージョン番号に置き換えます 
cd rdesktop-1.8.3
./configure 
make 
make install
```
4. <span id="step04">　次のコマンドを実行して、Windowsインスタンスにリモート接続します。</span>
> 例の中のパラメータを自分のパラメータに置き換えます。
>
```
rdesktop -u Administrator -p <your-password> <hostname or IP address>
```
 - `Administrator` は前提条件で入手した管理者アカウントです。
 - `<your-password>` はお客様が設定したログインパスワードです。
   システムのデフォルトパスワードを使用してインスタンスにログインする場合、[サイト内メール](https://console.cloud.tencent.com/message)にアクセスしてパスワードを取得してください。パスワードを忘れた場合、[インスタンスパスワードのリセット](https://intl.cloud.tencent.com/document/product/213/16566)を実行してください。
 - `<hostname or IP address>` はWindowsインスタンスのパブリックIPアドレスまたはカスタムドメイン名を指します。
 
###  MacOS システムはRDPでCVMにログインする

>
> - 次の操作は、Microsoft Remote Desktop for Macを例に使用しています。マイクロソフト社は、公式には2017年にRemote Desktopクライアントへのダウンロードリンクの提供を停止し、ベータ版のリリースは、その子会社である HockeyApp によって提供されます。
>- 以下の操作は Windows Server 2012 R2  OSに接続されているCVMを例に説明します。
>
1. Microsoft Remote Desktop for Macをダウンロードして、ローカルにインストールします。
2. MRDを起動して、下図に示すように【Add Desktop】をクリックします。
![](https://main.qcloudimg.com/raw/e69528d10e9a17dfa26119a090766c49.png)
3. 下図に示すように、ポップアップされた「Add Desktop」ウィンドウで、以下の手順に従って、Windows CVMへの接続を確立します。
![](https://main.qcloudimg.com/raw/d8e20278dd7c8aed487be2c43986f5e4.png)
    1. 「PC name」テキストフィールドに、CVMのパブリックIPアドレスを入力します。
    2. 【Add】をクリックします。
    3. 他のオプションはデフォルト設定のままで、接続を確立します。
    下図に示すように、ウィンドウで作成された接続を確認できます。
![](https://main.qcloudimg.com/raw/1c0eff28aa68a7f02e8f295917bb603b.png)
4. 新しく作成した接続をダブルクリックして開き、ポップアップウィンドウでプロンプトに従って、CVMのアカウントとパスワードを入力し、【Continue】をクリックしてください。
 - システムのデフォルトパスワードを利用して、インスタンスにログインする場合は、[サイト内メール](https://console.cloud.tencent.com/message)にアクセスしてパスワードを取得してください。
 - パスワードを忘れた場合、[インスタンスパスワードのリセット](https://intl.cloud.tencent.com/document/product/213/16566)を実行してください。
5. 下図に示すように、ポップアップウインドウで【Continue】をクリックし、接続を確立します。
![](https://main.qcloudimg.com/raw/61b3d9566365183fcc1d92c2f6bc2e7b.png)
接続に成功すると、以下の画面が表示されます。
![](https://main.qcloudimg.com/raw/20db4a1d63384bc0575ded68a8fe912d.png)
