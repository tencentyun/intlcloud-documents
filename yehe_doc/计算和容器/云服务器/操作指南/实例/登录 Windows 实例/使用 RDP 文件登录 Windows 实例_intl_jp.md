## 操作シナリオ

RDPはRemote Desktop Protocolの略称であり。お客様のローカルコンピュータがリモートコンピュータに接続できるようにするためにMicrosoftが開発したマルチチャネルプロトコルです。 Tencent Cloudは、Windows CVMへのログインにRDP方式を推奨しています。このドキュメントは、RDPファイルを使用してWindowsインスタンスにログインする方法について説明します。

## ローカルOSに適用する
Windows、Linuxと Mac OSは全てRDPを使用してCVMにログインすることができます。

## 前提条件

- Windowsインスタンスにリモートログインするには、インスタンスの管理者アカウント番号と対応するパスワードを獲得する必要があります。
 - システムのデフォルトパスワードを使用してインスタンスにログインする場合は、[サイト内メール](https://console.cloud.tencent.com/message)にアクセスして取得してください。
 - パスワードを忘れた場合、[インスタンスのパスワードをリセット](https://intl.cloud.tencent.com/document/product/213/16566)してください。
- CVMインスタンスはパブリックネットワークIPを購入済みであり、このインスタンスはCVMインスタンスの3389ポート（クイック設定で購入したCVMインスタンスの場合、デフォルトでアクティブになっています）をアクティブしました。

## 操作手順
<dx-tabs>
::: Windows\sシステムでは\sRDP\sを使用してログインします[](id:windowsRDP)
1. [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインします。
2. インスタンスの管理画面で、下図に示すように、ログインしようとするWindows CVMを選択し、【ログイン】をクリックします。
![](https://main.qcloudimg.com/raw/e7b1192332a116edca67425a301236be.png)
3. ポップアップの【Windowsインスタンスのログイン】ウィンドウで、【RDPファイルを使用してログイン】を選択し、【RDPファイルをダウンロード】をクリックし、RDPファイルをローカルにダウンロードします。
>?リモートログインポートを変更した場合は、RDPファイルを変更し、IPアドレスの後ろに`：port`を追加する必要があります。
>
![](https://main.qcloudimg.com/raw/0b0076390b95da3885c8967093683975.png)
4. ローカルにダウンロードしたRDPファイルをダブルクリックし、パスワードを入力して【OK】をクリックすると、リモートでWindows CVMに接続できます。
 - システムのデフォルトパスワードを使用してインスタンスにログインする場合は、[サイト内メッセージ](https://console.cloud.tencent.com/message) に進んで取得してください。
 - パスワードを忘れた場合は、[インスタンスのパスワードをリセット](https://intl.cloud.tencent.com/document/product/213/16566)してください。
:::
::: Linux\sシステムでは\sRDP\sを使用してログインします[](id:LinuxRDP)
>?対応するリモートデスクトップ接続プログラムをインストールする必要がある場合は、rdesktopを使用して接続することをお勧めします。詳細は [rdesktop 公式説明](http://www.rdesktop.org/)をご参照ください。
>
1. 以下のコマンドを実行し、システムの中にrdesktopをインストールしたかどうかを確認します。
```
rdesktop
```
 - rdesktopをインストールしている場合、[ステップ4](#step04)を実行してください。
 - command not foundが表示される場合、rdesktopがまだインストールされていないことを示しています。[ステップ2](#step02)を実行してください。
2. [](id:step02)端末で以下のコマンドを実行し、rdesktopのインストールパッケージをダウンロードします。この手順ではrdesktop 1.8.3バージョンを例示します。
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
4. [](id:step04)以下のコマンドを実行し、Windowsのインスタンスにリモートで接続します。</span>
>? 例中のパラメータを自身のパラメータに変更してください。
>
```
rdesktop -u Administrator -p <your-password> <hostname or IP address>
```
 - `Administrator` は前提条件で取得した管理者アカウントです。
 - `&lt;your-password&gt;` はお客様が設定したログインパスワードです。
   システムのデフォルトのパスワードを使用してインスタンスにログインする場合は、[サイト内メッセージ]（https://console.cloud.tencent.com/message）にアクセスして取得してください。 パスワードを忘れた場合は、[インスタンスのパスワードをリセット](https://intl.cloud.tencent.com/document/product/213/16566)してください。
 - `&lt;hostname or IP address&gt;`とは、WindowsインスタンスのパブリックIPまたはカスタムドメイン名です。 インスタンスのパブリックIPアドレスの取得方法については、[パブリックIPアドレスの取得](https://intl.cloud.tencent.com/document/product/213/17940)をご参照ください。
:::
::: MacOS\sシステムでは\sRDP\sを使用してログインします[](id:MacRDP)
>?
>- 以下の操作は Microsoft Remote Desktop for Mac の例です。マイクロソフトは2017年に Remote Desktop クライアントのダウンロードリンクの提供を正式に停止し、現在は、子会社の HockeyApp が Beta 版を配布しています。 [Microsoft Remote Desktop Beta](https://install.appcenter.ms/orgs/rdmacios-k2vy/apps/microsoft-remote-desktop-for-mac/distribution_groups/all-users-of-microsoft-remote-desktop-for-mac)で Beta 版をダウンロードすることができます。
>- 以下の操作は Windows Server 2012 R2 OSに接続されるCVMを例に説明します。
>
1. Microsoft Remote Desktop for Macをダウンロードして、ローカルにインストールします。
2. MRDを起動し、以下に示すように【Add Desktop】をクリックします。
![](https://main.qcloudimg.com/raw/e69528d10e9a17dfa26119a090766c49.png)
3. 表示された「Add Desktop」ウィンドウで、以下の手順に従って、接続を作成します。下図に示すように：
![](https://main.qcloudimg.com/raw/d8e20278dd7c8aed487be2c43986f5e4.png)
    1.「PC name」にCVMのパブリックネットワークIPを入力します。取得方法については、[パブリックIPアドレスの取得](https://intl.cloud.tencent.com/document/product/213/17940)をご参照ください。
    2. 【Add】をクリックして、接続の作成を確認します。
    3. 他のオプションはデフォルト設定のままで、接続が作成されます。
    ウィンドウで作成された接続を確認できます。下図に示すように：
![](https://main.qcloudimg.com/raw/1c0eff28aa68a7f02e8f295917bb603b.png)
4.新しく作成した接続をダブルクリックして開き、ポップアップウィンドウでプロンプトに従って、CVMのアカウントとパスワードを入力し、【Continue】をクリックしてください。
 - システムのデフォルトパスワードでインスタンスにログインする際は、[サイト内メッセージ](https://console.cloud.tencent.com/message)に進んで取得してください。
 - パスワードを忘れた場合、[インスタンスパスワードのリセット](https://intl.cloud.tencent.com/document/product/213/16566)してください。
5. ポップアップウインドウで【Continue】をクリックし、接続を確認します。下図に示すように：
![](https://main.qcloudimg.com/raw/61b3d9566365183fcc1d92c2f6bc2e7b.png)
接続に成功すると、下図に示すとおり、Windows CVMのインターフェースが開きます：
![](https://main.qcloudimg.com/raw/5a524210acd13624af7263b6de3aea54.png)
:::
</dx-tabs>
