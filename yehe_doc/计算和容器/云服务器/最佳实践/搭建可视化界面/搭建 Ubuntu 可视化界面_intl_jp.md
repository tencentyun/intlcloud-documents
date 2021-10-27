## 概要
VNC（Virtual Network Console）はバーチャルネットワークコンソールの省略形です。これは優れたリモートコントロールツールソフトウェアで、有名なAT&Tのヨーロッパ研究所で開発されました。VNCはUNIXおよびLinuxオペレーティングシステムのオープンソースソフトウェアであり、リモートコントロール機能が高く、効率的かつ実用的で、その機能はWindowsおよびMACのどのリモートコントロールソフトウェアより優れています。ここではUbuntuオペレーティングシステムのCloud Virtual Machineでビジュアルインターフェースを構築する方法を説明します。

## 前提条件
OSがUbuntuのLinux CVMを購入していること。CVMを購入していない場合は、[Linux CVMのクイック設定](https://intl.cloud.tencent.com/zh/document/product/213/10517)をご参照ください。


## 操作手順


### インスタンスセキュリティグループの設定

VNCサービスにはTCPプロトコルを使用し、デフォルトでは5901ポートを使用します。従って、インスタンスにバインディングしたセキュリティグループの中で5901ポートを開放する必要があり、即ち、「インバウンドルール」にプロトコルポートTCP:5901を開放するルールを追加する必要があります。具体的な操作については、[セキュリティグループルールの追加](https://intl.cloud.tencent.com/document/product/213/34272)をご参照ください。


### ソフトウェアパッケージのインストール
1. [標準のログイン方法を使用してLinuxインスタンスにログインする（推奨）](https://intl.cloud.tencent.com/document/product/213/5436)。
2. 以下のコマンドを実行して、現在のユーザーをrootユーザーに切り替えます。
```
sudo -i
```
3. 以下のコマンドを実行し、最新のソフトウェアに更新してバージョン情報を取得します。
```
apt-get update
```
4. 次のコマンドを実行して、デスクトップ環境に必要なソフトウェアパッケージをインストールします。これにはシステムパネル、ウィンドウマネージャー、ファイルブラウザ、端末などのデスクトップアプリケーションプログラムが含まれます。
```bash
apt install gnome-panel gnome-settings-daemon metacity nautilus gnome-terminal ubuntu-desktop
```



### VNCの設定

1. 実際の状況に基づき、以下のコマンドを選択して実行し、VNCをインストールします。
<dx-tabs>
::: Ubuntu 18.04
```
apt-get install vnc4server
```
:::
::: Ubuntu 20.04
```
apt-get install tightvncserver
```
:::
</dx-tabs>
2. [](id:step02)次のコマンドを実行して、VNCサービスを起動し、VNCのパスワードを設定します。
```
vncserver
```
以下のような結果が返されると、VNCの起動が成功したことを示します。
![](https://main.qcloudimg.com/raw/adad6ffbb0b1b722d1e429133060134b.png)
3. 以下のコマンドを実行して、VNC設定ファイルを開きます。
```
vi ~/.vnc/xstartup
```
4. **i**を押して編集モードに切り替え、設定ファイルを以下の内容に変更します。
```
#!/bin/sh
export XKL_XMODMAP_DISABLE=1
export XDG_CURRENT_DESKTOP="GNOME-Flashback:GNOME"
export XDG_MENU_PREFIX="gnome-flashback-"
gnome-session --session=gnome-flashback-metacity --disable-acceleration-check &
```
5. **Esc**を押し、**:wq**を入力して、ファイルを保存して戻ります。
6. 以下のコマンドを実行して、デスクトッププロセスを再起動します。
```
vncserver -kill :1 #元のデスクトッププロセスを閉じ、コマンドを入力します（ここで:1はデスクトップ番号です）
```
```
vncserver -geometry 1920x1080 :1 #新しいセッションを生成
```
7. [ここをクリック](https://www.realvnc.com/en/connect/download/viewer/)してVNC Viewer公式サイトに進み、ローカルコンピューターのオペレーティングシステムタイプに合わせて、対応するバージョンをダウンロードおよびインストールします。
8. VNC Viewerソフトウェア内で、「CVMのIPアドレス:1」を入力し、**Enter**を押します。
![](https://main.qcloudimg.com/raw/df25e2085e9d27d53b1827ccf98a3618.png)
9. ポップアップしたダイアログボックスの中の**Continue**をクリックします。
10. [手順2](#step02)で設定したVNCのパスワードを入力し、**OK**をクリックすれば、インスタンスにログインしてグラフィック化インターフェースを使用することができます。



