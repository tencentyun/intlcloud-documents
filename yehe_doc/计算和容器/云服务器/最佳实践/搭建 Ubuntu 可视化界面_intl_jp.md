## 操作シナリオ
VNC（Virtual Network Console）はバーチャルネットワークコンソールの省略形です。これは優れたリモートコントロールツールソフトウェアで、有名なAT&Tのヨーロッパ研究所で開発されました。VNCはUNIXおよびLinuxオペレーティングシステムのオープンソースソフトウェアであり、リモートコントロール機能が高く、効率的かつ実用的で、その機能はWindowsおよびMACのどのリモートコントロールソフトウェアより優れています。ここではUbuntuオペレーティングシステムのCloud Virtual Machineでビジュアルインターフェースを構築する方法を説明します。

## 前提条件
オペレーティングシステムがUbuntuであるLinux Cloud Virtual Machineを購入済みであること。Cloud Virtual Machineを購入していない場合は、[Linux CVMのカスタム設定](https://intl.cloud.tencent.com/document/product/213/10517)をご参照ください。


## 操作手順

- [VNCを使用してLinuxインスタンスにログインする](https://intl.cloud.tencent.com/document/product/213/5436)。
2. 以下のコマンドを実行して、現在のユーザーをrootユーザーに切り替えます。
```
sudo su root
```
3. 以下のコマンドを実行し、最新のソフトウェアに更新してバージョン情報を取得します。
```
apt-get update
```
4. 実際の状況に基づき、以下のコマンドを選択して実行し、VNCをインストールします。
<dx-tabs>
::: Ubuntu\s16.04/18.04
```
apt-get install vnc4server
```
:::
::: Ubuntu\s20.04
```
apt-get install tightvncserver
```
:::
</dx-tabs>
5. <span id="step05"></span>以下のコマンドを実行して、VNCサービスを起動し、VNCのパスワードを設定します。
```
vncserver
```
以下のような結果が返されると、VNCの起動が成功したことを示します。
![](https://main.qcloudimg.com/raw/adad6ffbb0b1b722d1e429133060134b.png)
6. 以下のコマンドを実行して、X-windowsの基本構成をインストールします。
```
sudo apt-get install x-window-system-core
```
7. 実際の状況に基づき、以下のコマンドを選択して実行し、ログインマネージャーをインストールします。
<dx-tabs>
::: Ubuntu\s16.04/18.04
```
sudo apt-get install
```
:::
::: Ubuntu\s20.04
```
sudo apt-get install
```
:::
</dx-tabs>
8. 以下のコマンドを実行して、Ubuntuのデスクトップをインストールします。
```
sudo apt-get install ubuntu-desktop
```
インストール中、`Default display manager:`で“gdm3”を選択します。
9. 以下のコマンドを実行して、Gnome関連のサポートソフトウェアをインストールします。
```
sudo apt-get install gnome-panel gnome-settings-daemon metacity nautilus gnome-terminal
```
10. 以下のコマンドを実行して、VNC設定ファイルを開きます。
```
vi ~/.vnc/xstartup
```
11. **i**を押して編集モードに切り替え、設定ファイルを以下の内容に変更します。
```
#!/bin/sh
# Uncomment the following two lines for normal desktop:
export XKL_XMODMAP_DISABLE=1
 unset SESSION_MANAGER
# exec /etc/X11/xinit/xinitrc
unset DBUS_SESSION_BUS_ADDRESS
gnome-panel &
gnome-settings-daemon &
metacity &
nautilus &
gnome-terminal &
```
12. **Esc**を押して、**:wq**と入力し、ファイルを保存して戻ります。
13. 以下のコマンドを実行して、デスクトッププロセスを再起動します。
```
ncserver -kill :1 #元のデスクトッププロセスを閉じ、コマンドを入力します（ここで:1はデスクトップ番号です）
```
```
vncserver :1 #新しいセッションを作成します
```
14. [ここをクリック](https://www.realvnc.com/en/connect/download/viewer/)してVNC Viewer公式サイトに進み、ローカルコンピューターのオペレーティングシステムタイプに合わせて、対応するバージョンをダウンロードおよびインストールします。
15. VNC Viewerソフトウェア内で、「CVMのIPアドレス:1」を入力し、**Enter**を押します。
![](https://main.qcloudimg.com/raw/df25e2085e9d27d53b1827ccf98a3618.png)
16. ポップアップしたダイアログボックスで、【Continue】をクリックします。
17. [手順5](#step05)で設定したVNCのパスワードを入力して、【OK】をクリックします。
>?接続時間超過エラー情報が表示される場合は、ネットワークが接続されているか、セキュリティグループが開放されているかを確認してください。この内、セキュリティグループはVNC Serverが監視する5901ポートを開放する必要があり、「インバウンドルール」内にプロトコルポート`TCP:5901`を開放するルールを追加する必要があります。具体的な操作については、[セキュリティグループルールの追加](https://intl.cloud.tencent.com/document/product/213/34272)をご参照ください。









