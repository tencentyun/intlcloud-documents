ここでは、さまざまなオペレーティングシステムにPython開発環境をインストールする方法を簡単にご紹介します。

## インストールパッケージによるインストール

### 1. ダウンロード
[Python公式サイト](https://www.python.org/downloads/)にアクセスし、使用しているOSに応じて適切なインストールパッケージを選択し、ダウンロードします。

>! Pythonは、2020年1月1日をもってPython2のメンテナンスを終了しており、Python3のインストールが推奨されています。

### 2. インストール
インストールパッケージをダウンロードしたら、インストールパッケージの指示に従って、Python開発環境のインストールを完了します。

>? Windowsシステムユーザーは、インストール時にオプションの「Add Python to environment variables」にチェックを入れるようご注意ください。
> ![](https://main.qcloudimg.com/raw/bd52e448e3ba0e8171b5a37b31caadb8.png)

### 3. 検証
端末で以下のコマンドを実行し、Pythonのバージョンを確認します。
```shell
python -V
```
端末からPythonのバージョン番号が出力されれば、インストールは成功です。

>? Windowsシステムユーザーはインストール完了後、コンピュータの再起動が必要になる場合があります。

### 4. 環境変数の設定
Windowsシステムで上記のコマンドを実行した際、端末に「内部コマンドでも外部コマンドでもありません」と表示された場合は、【コンピュータ】>【プロパティ】>【高度なシステム設定】>【環境変数】>【システム変数(S)】で「Path」を編集し、Pythonのインストールパスを追加してください。

## パッケージマネージャーによるインストール

### Mac OS
Mac OSをお使いのユーザーは、あらかじめ[HomeBrew](https://brew.sh/index_zh-cn)をインストールした上で、HomeBrew経由でPythonをインストールすることができます。
```shell
brew install python
```

### Ubuntu
Ubuntuをお使いのユーザーは、Ubuntuに付属しているapt(Advanced Packaging Tool)パッケージマネージャーを使用すると、Pythonをインストールすることができます。
```shell
sudo apt-get install python
```

### CentOS
CentOSをお使いのユーザーは、CentOSに付属しているyum(Yellow dog Updater, Modified)パッケージマネージャーを使用すると、Pythonをインストールすることができます。
```shell
sudo yum install -y python
```
