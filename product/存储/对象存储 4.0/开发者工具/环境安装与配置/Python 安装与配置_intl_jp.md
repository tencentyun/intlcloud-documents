本ドキュメントは、Python 2.7バージョンを例として、WindowsとLinuxシステムのPythonのインストールと環境構成を詳しく説明します。

## Windows
### 1. ダウンロード
[Python公式サイト](https://www.python.org/downloads/)に入り、適切なバージョンを選択してダウンロードします。本例では、[Python 2.7.13](https://www.python.org/ftp/python/2.7.13/python-2.7.13.amd64.msi)バージョンをダウンロードします。
### 2. インストール
Pythonのインストールパッケージをダウンロードした後にPythonのインストールパッケージをダブルクリックします。デフォルトの案内に従ってインストールします。
### 3. 環境変数の構成
インストール完了後、【コンピュータ】を右クリックし、【属性】>【システム詳細設定】>【環境変数】>【システム変数(S)】をクリックし、「Path」（なければ新規作成）を見つけ、「変数値」の末尾にPythonのインストールパス：`;C:\Python27`（要望のインストールパスに変更してください）を追加し、【OK】をクリックして保存します。
![161709](//mc.qcloudimg.com/static/img/b5784ed03d0f2fd07195c9c3ae1e5075/image.png)
### 4. 構成が成功であるかどうかをテストする
【開始】（またはショートカットキー：Win+R）>【実行】（`cmd`を入力する）>【OK】（またはEnterキーを押す）をクリックし、ポップアップされたウィンドウにPythonコマンドを入力しEnterキーを押します。以下の情報が表示されると、Python 2.7のインストールと構成が完了したことを示します。
![152355](//mc.qcloudimg.com/static/img/026d7738b234171b285a98f0e751038a/image.png)
## Linux
### 1. Pythonバージョンの表示
LinuxのyumにPythonが付属されます。まずは、デフォルトのPythonバージョンを確認します。
```
python -V
```
Python 2.7以降のバージョンであれば、次の手順を無視してください。さもなければ（ここで現在バージョンがPython 2.6.6と仮定する）、以下のコマンドを入力します。
```
yum groupinstall "Development tools"
```
### 2. Pythonコンパイル用コンポーネントをインストールする
```
yum install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel
```
### 3. Python 2.7をダウンロードし、解凍する
```
wget https://www.python.org/ftp/python/2.7.12/Python-2.7.12.tar.xz
tar xf Python-2.7.12.tar.xz
```
### 4. Pythonのコンパイルとインストール
```
cd Python-2.7.12 //ディレクトリに入る
./configure -prefix=/usr/local
make && make install //インストール
make clean
make distclean
```
### 5. システムPythonコマンドをPython 2.7に指定する
```
mv /usr/bin/python /usr/bin/python2.6.6
ln -s /usr/local/bin/python2.7 /usr/bin/python
```
### 6. 構成が成功であるかどうかをテストする
```
python
```
以下の情報が表示されると、Python 2.7のインストールと構成が完了したことを示します。
![112046](//mc.qcloudimg.com/static/img/0eb560566c1f67e302e75b1dcb515d98/image.png)

> <font color="#0000cc">**注意：** </font>
権限の問題があれば、コマンドの前にsudoを追加して解決してみてください。
