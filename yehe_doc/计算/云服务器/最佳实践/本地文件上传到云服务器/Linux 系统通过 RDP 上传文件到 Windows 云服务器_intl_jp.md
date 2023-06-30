## 操作シナリオ
Rdesktopは、リモートデスクトッププロトコル(RDP)のオープンソースクライアントであり、Windows CVMへの接続などの操作に用いられます。ここでは、ローカルLinuxマシンからファイルを、rdesktopを介してWindows Server 2012 R2 OSのTencent CloudCloud Virtual Machine(CVM)にすばやくアップロードする方法についてご説明します。
>? 
>- ローカルLinuxマシンはビジュアルインターフェースを構築する必要があり、構築しないとrdesktopが使えません。
>- ここではLinuxマシンのOSに、CentOS 7.6を使用した場合を例として取り上げます。OSのバージョンによって手順が異なる場合がありますので、実際の業務状況に応じてドキュメントを参照して操作を行ってください。  
>

## 前提条件
Windows CVMを購入済みであること。

## 操作手順
### パブリックIPの取得
[CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインし、ファイルをアップロードするCVMのパブリックIPを、インスタンスリストページに記述します。下図に示すとおりです。
![](https://main.qcloudimg.com/raw/59ce52615c467ad80bc4220425bf2b80.png)

### rdesktopのインストール
1. 端末で以下のコマンドを実行し、rdesktopのインストールパッケージをダウンロードします。この手順はrdesktop 1.8.3バージョンを例とします。
```
wget https://github.com/rdesktop/rdesktop/releases/download/v1.8.3/rdesktop-1.8.3.tar.gz
```
最新のインストールパッケージが必要な場合は、[GitHub rdesktopページ](https://github.com/rdesktop/rdesktop/releases)にアクセスし、最新のインストールパッケージを検索して、コマンドラインで最新のインストールパスに置き換えることができます。
2. 次のコマンドを順番に実行して、インストールパッケージを解凍し、インストールディレクトリに入ります。
```
tar xvzf rdesktop-1.8.3.tar.gz
```
```
cd rdesktop-1.8.3
```
3.次のコマンドを順番に実行して、rdesktopをコンパイルしてインストールします。
```
./configure 
```
```
make
```
```
make install
```
4. インストールが完了したら、次のコマンドを実行して、インストールが成功したかどうか確認します。
```
rdesktop
```

### ファイルのアップロード
1. 次のコマンドを実行して、CVMと共有するフォルダを指定します。
```
rdesktopCVMパブリックIP  -u CVMアカウント -pCVMログインパスワード -r disk:指定された共有フォルダ名=ローカルフォルダパス
```
>?
>- CVMのアカウントはデフォルトで`Administrator`となります。
>- システムのデフォルトパスワードを使用してインスタンスにログインする場合は、[サイト内メッセージ](https://console.cloud.tencent.com/message)に進んで取得してください。
>- パスワードを忘れた場合は、[インスタンスのパスワードをリセット](https://intl.cloud.tencent.com/document/product/213/16566)してください。
>
例えば、次のコマンドを実行して、ローカルコンピュータの`/home`フォルダを指定したCVMと共有し、共有フォルダ名を`share`に変更します。
```
rdesktop 118.xx.248.xxx  -u Administrator -p 12345678 -r disk:share=/home
```
共有が成功すると、Windows CVMのインターフェースが開きます。
左下隅にある<img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-3px 0px"> > 【このコンピュータ】を選択し、CVMシステムインターフェースで共有フォルダを表示することができます。
2. ダブルクリックして共有フォルダを開き、Windows CVMの他のハードディスクにアップロードする必要があるローカルファイルをレプリケートすると、ファイルのアップロード操作は完了です。
例えば、`share`フォルダ内のAファイルをWindows CVMのCドライブにレプリケートします。

### ファイルのダウンロード
Windows CVMからローカルコンピュータにファイルをダウンロードする必要がある場合は、ファイルのアップロード操作を参照して、必要なファイルをWindows CVMから共有フォルダにレプリケートすると、ファイルのダウンロード操作は完了です。
