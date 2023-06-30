## 概要
仮想ネットワークコンソール (VNC) はAT&T ケンブリッジ研究所によって開発されたリモートコントロールソフトウェアです。UNIX および Linux OSをベースとしたオープンソースソフトウェアであるVNC は、リモートコントロール機能が高く、効率的かつ実用的で、その機能はWindowsおよびMACのどのリモートコントロールソフトウェアより優れています。このドキュメントでは、Ubuntu OSを搭載した CVMインスタンスでビジュアルインターフェースを構築する方法を説明します。

## 前提条件
Ubuntu OSを搭載した Linux インスタンスを購入しました。

## 操作手順


### インスタンスセキュリティグループの設定

VNCサービスは、デフォルトで TCPプロトコルとポート5901 を使用します。インスタンスに関連付けられているセキュリティグループでポート5901を開く必要があり、即ち、「インバウンドルール」にプロトコルポートTCP:5901を開くためのルールを追加する必要があります。具体的な操作については、[セキュリティグループルールの追加](https://intl.cloud.tencent.com/document/product/213/34272)をご参照ください。


### ソフトウェアパッケージのインストール

<dx-tabs>
::: Ubuntu 18.04
1. [標準ログイン方式を使用してLinuxインスタンスにログインする（推奨）](https://intl.cloud.tencent.com/document/product/213/5436)。
2. 次のコマンドを実行してキャッシュをクリアし、ソフトウェアパッケージリストを更新します。
```shellsession
sudo apt clean all && sudo apt update
```
3. 次のコマンドを実行して、デスクトップ環境に必要なソフトウェアパッケージをインストールします。これにはシステムパネル、ウィンドウマネージャー、ファイルブラウザ、端末などのデスクトップアプリケーションプログラムが含まれます。
```shellsession
sudo apt install gnome-panel gnome-settings-daemon metacity nautilus gnome-terminal ubuntu-desktop
```
4. 次のコマンドを実行して VNC をインストールします。
```shellsession
apt-get install vnc4server
```
:::
::: Ubuntu 20.04
1. [標準ログイン方式を使用してLinuxインスタンスにログインする（推奨）](https://intl.cloud.tencent.com/document/product/213/5436)。
2. 次のコマンドを実行してキャッシュをクリアし、ソフトウェアパッケージリストを更新します。
```shellsession
sudo apt clean all && sudo apt update
```
3. 次のコマンドを実行して、デスクトップ環境に必要なソフトウェアパッケージをインストールします。これにはシステムパネル、ウィンドウマネージャー、ファイルブラウザ、端末などのデスクトップアプリケーションプログラムが含まれます。
```shellsession
sudo apt install gnome-panel gnome-settings-daemon metacity nautilus gnome-terminal ubuntu-desktop
```
4. 次のコマンドを実行して VNC をインストールします。
```shellsession
apt-get install tightvncserver
```
:::
::: Ubuntu 22.04
1. [標準ログイン方式を使用してLinuxインスタンスにログインする（推奨）](https://intl.cloud.tencent.com/document/product/213/5436)。
2. キャッシュをクリアし、ソフトウェアパッケージリストを更新します。
```shellsession
sudo apt clean all && sudo apt update
```
3. デスクトップ環境をインストールします。
```shellsession
sudo apt install xfce4 xfce4-goodies
```
4. 次のコマンドを実行して VNC をインストールします。
```shellsession
sudo apt install tightvncserver
```
:::
</dx-tabs>

### VNCの構成
<dx-tabs>
::: Ubuntu 18.04
1. [](id:step02)次のコマンドを実行してVNCサービスを起動し、パスワードを設定します。
```shellsession
vncserver
```
次のような結果が返された場合は、VNCが正常に起動されたことを示します。
![](https://main.qcloudimg.com/raw/adad6ffbb0b1b722d1e429133060134b.png)
2. 次のコマンドを実行して、VNC 構成ファイルを開きます。
```shellsession
vi ~/.vnc/xstartup
```
3.  **i** を押して編集モードに切り替え、構成ファイルを以下の内容に変更します。
```shellsession
#!/bin/sh
export XKL_XMODMAP_DISABLE=1
export XDG_CURRENT_DESKTOP="GNOME-Flashback:GNOME"
export XDG_MENU_PREFIX="gnome-flashback-"
gnome-session --session=gnome-flashback-metacity --disable-acceleration-check &
```
4.  **Esc**を押し、**:wq**を入力して、ファイルを保存して戻ります。
5. 次のコマンドを実行して、デスクトッププロセスを再起動します。
```shellsession
vncserver -kill :1 #元のデスクトッププロセスを終了し、コマンドを入力します (ここで:1はデスクトップ番号です)  
```
```shellsession
vncserver -geometry 1920x1080 :1 #新しいセッションを生成します
```
6. [ここをクリックして](https://www.realvnc.com/en/connect/download/viewer/) VNC Viewer公式サイトに進み、ローカルコンピューターのオペレーティングシステムタイプに合わせて、対応するバージョンをダウンロードおよびインストールします。
7.  VNC Viewerソフトウェア内で、`CVMのIPアドレス:1`を入力し、 **Enter **を押します。
![](https://main.qcloudimg.com/raw/df25e2085e9d27d53b1827ccf98a3618.png)
8. ポップアップしたダイアログボックスで **Continue **をクリックします。
9.  [手順2](#step02) で設定したVNCのパスワードを入力し、**OK**をクリックすれば、インスタンスにログインしてグラフィック化インターフェースを使用することができます。

:::


::: Ubuntu 20.04
1. [](id:step03)次のコマンドを実行してVNCサービスを起動し、パスワードを設定します。
```shellsession
vncserver
```
次のような結果が返された場合は、VNCが正常に起動されたことを示します。
![](https://main.qcloudimg.com/raw/adad6ffbb0b1b722d1e429133060134b.png)
2.  次のコマンドを実行して、VNC 構成ファイルを開きます。
```shellsession
vi ~/.vnc/xstartup
```
3.  **i** を押して編集モードに切り替え、構成ファイルを以下の内容に変更します。
```shellsession
#!/bin/sh
export XKL_XMODMAP_DISABLE=1
export XDG_CURRENT_DESKTOP="GNOME-Flashback:GNOME"
export XDG_MENU_PREFIX="gnome-flashback-"
gnome-session --session=gnome-flashback-metacity --disable-acceleration-check &
```
4. **Esc**を押し、**:wq**を入力して、ファイルを保存して戻ります。
5. 次のコマンドを実行して、デスクトッププロセスを再起動します。
```shellsession
vncserver -kill :1 #元のデスクトッププロセスを終了し、コマンドを入力します (ここで:1はデスクトップ番号です)  
```
```shellsession
vncserver -geometry 1920x1080 :1 #新しいセッションを生成します
```
6.  [ここをクリックして](https://www.realvnc.com/en/connect/download/viewer/) VNC Viewer公式サイトに進み、ローカルコンピューターのオペレーティングシステムタイプに合わせて、対応するバージョンをダウンロードおよびインストールします。
7.  VNC Viewerソフトウェア内で、`CVMのIPアドレス:1`を入力し、 **Enter **を押します。
![](https://main.qcloudimg.com/raw/df25e2085e9d27d53b1827ccf98a3618.png)
8. ポップアップしたダイアログボックスで **Continue **をクリックします。
9. [手順2](#step02) で設定したVNCのパスワードを入力し、**OK**をクリックすれば、インスタンスにログインしてグラフィック化インターフェースを使用することができます。

:::

::: Ubuntu 22.04
[](id:g1)
1. 次のコマンドを実行してVNCサービスを起動し、パスワードを設定します。
```shellsession
vncserver
```
次のような結果が返された場合は、VNCが正常に起動されたことを示します。
![](https://qcloudimg.tencent-cloud.cn/raw/5fb63d9cc28d3a0cebd5def424051e7a.png)
2.  [VNC Viewer](https://www.realvnc.com/en/connect/download/viewer/) 公式サイトに進み、ローカルコンピューターのオペレーティングシステムタイプに合わせて、対応するバージョンをダウンロードおよびインストールします。
3. VNC Viewerソフトウェア内で、 `CVMのIPアドレス:1 `を入力し、**Enter**を押します。
![](https://qcloudimg.tencent-cloud.cn/raw/3e7d432ce674a8587066df25f42595bf.png)
4. ポップアップしたダイアログボックスで **Continue **をクリックします。
5. 前の手順で作成したパスワードを入力し、**OK** をクリックします。
 <dx-alert infotype="notice" title="">
パスワードを忘れた場合は、インスタンスにログインし、 `vncpasswd` コマンドを実行して VNCログインパスワードをリセットします。
 </dx-alert>
付録：
Chrome をインストールする：
 - インスタンスにログインし、次のコマンドを実行して **.deb** パッケージ ファイルをダウンロードします。
```shellsession
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
```
 - **.deb** ファイルをインストールする
```shellsession
sudo apt install ./google-chrome-stable_current_amd64.deb
```
:::
</dx-tabs>