## ユースケース

Linux ユーザーは、パスワード管理、sshdの破損など、特別な操作を実行するためにシングルユーザーモードに入る必要がある場合があります。本ドキュメントは主流Linux OSのシングルユーザーモードに入る操作手順について説明します。

## 操作手順

### OSの種類は判断する

CVMのOS種類に応じて、最適な操作手順を選んでください。
 - CentOS 6 OS、[CentOS 6 の手順](#configCentOS6)を実行しください。
 - CentOS 7 OS、[CentOS 7 の手順](#configCentOS7)を実行しください。
 - Ubuntu OS、[Ubuntu の手順](#configUbuntu)を実行してください。

<span id="configCentOS6"></span>
### CentOS 6

>? Centos 6は GRUB ブートローダーを利用しています。以下の操作手順は CentOS 6.9 を例に説明します。OSのバージョンによって詳細の操作手順は若干異なります。
> 
1. リモートで CVM インスタンスにログインします。
2. 以下のコマンドを実行して、 `/etc/grub.conf` ファイルを開きます。
```
vi /etc/grub.conf
```
3. **I** を押して、編集モードに入ります。
4. 「GRUB_TIMEOUT」（デフォルトエントリが起動されるまでの待機時間を設定するパラメータ）を検索し、実際のニーズに応じて、時間の範囲を変更します。
「GRUB_TIMEOUT」のデフォルト値は5秒です。待機時間が短すぎでスタートアップ インターフェースが見えない問題を回避するには、60秒以上に変更するのをお勧めします。
>! この項目はシステムの起動時間に影響します。設定が完了したら、デフォルト値に戻す必要があります。
5. **Esc** を押して編集モードを終了し、**:wq** を入力し、**Enter** を押してください。
設定を保存して、VI エディターを終了します。
6. 以下のコマンドを実行して、サーバーを再起動します。
```
reboot
```
7. 約1分を待ってから、[VNCでCVM インスタンスにログインします。](https://intl.cloud.tencent.com/document/product/213/5436#.E4.BD.BF.E7.94.A8-vnc-.E7.99.BB.E5.BD.95.E5.AE.9E.E4.BE.8B)ログイン インターフェースは下図に示すように：
![](https://main.qcloudimg.com/raw/82a82601e1545274c4f61c8f34f5c100.png)
8. 任意のキーを押して、メニューに入ります。下図に示すように：
![](https://main.qcloudimg.com/raw/6336b8fd579799108a5765b5b58e2a21.png)
9. **e** を押してカーネル編集インターフェースに入り、**single** を入力します。下図に示すように：
![](https://main.qcloudimg.com/raw/14168276d81a398702e80f9c83186869.png)
10. **Enter**を押します。下図に示すように：
![](https://main.qcloudimg.com/raw/149eeb5776329a5db1ea42ae20cd316d.png)
11. 以下に示すインターフェースで、**b** を押して、シングルユーザーモードに入ります。
![](https://main.qcloudimg.com/raw/2d6d53de84cd78b3e88319b8538cec8e.png)
12. 以下のコマンドを実行して、シングルユーザーモードを終了します。
```
exec /sbin/init
```

<span id="configCentOS7"></span>
### CentOS 7

>? CentOS 6と違って、CentOS 7 以降のバージョンは GRUB 2を利用しています。以下の操作手順は CentOS 7.5 を例に説明します。OSのバージョンによって詳細の操作手順は若干異なります。
> 
1. リモートで CVM インスタンスにログインします。
2. 以下のコマンドを実行して、 `/etc/default/grub` ファイルを開きます。
```
vi /etc/default/grub
```
3. **I** を押して、編集モードに入ります。
4. 「GRUB_TIMEOUT」（デフォルトエントリが起動されるまでの待機時間を設定するパラメータ）を検索し、実際のニーズに応じて、時間の範囲を変更します。下図に示すように：
「GRUB_TIMEOUT」のデフォルト値は5秒です。待機時間が短すぎでスタートアップ インターフェースが見えない問題を回避するには、60秒以上に変更するのをお勧めします。
>! この項目はシステムの起動時間に影響します。設定が完了したら、デフォルト値に戻す必要があります。
>
![](https://main.qcloudimg.com/raw/5ee3b8d8a4609ca846e3c1e929608b34.png)
5. **Esc** を押して編集モードを終了し、**:wq** を入力し、**Enter** を押してください。
設定を保存して、VI エディターを終了します。
6. 以下のコマンドを実行して、grub.cfgファイルを再コンパイルして生成します。
```
grub2-mkconfig -o /boot/grub2/grub.cfg
```
実行結果は下図に示すように：
![](https://main.qcloudimg.com/raw/62da54e985f2f78efce045bb2da1e5e5.png)
7. 以下のコマンドを実行して、サーバーを再起動します。
```
reboot
```
8. 約1分を待ってから、[VNCでCVM インスタンスにログインします。](https://intl.cloud.tencent.com/document/product/213/5436#.E4.BD.BF.E7.94.A8-vnc-.E7.99.BB.E5.BD.95.E5.AE.9E.E4.BE.8B)ログイン インターフェースは下図に示すように：
![](https://main.qcloudimg.com/raw/95dba957dea2da680ffca516dc2b62b3.png)
9. **e** を押してカーネル編集インターフェースに入り、 **init=/bin/sh** を赤い枠のところに追加します。下図に示すように：
![](https://main.qcloudimg.com/raw/81173f4c723809f1b733a51a2eb002d5.png)
10. **Ctrl+X** を押して、シングルユーザーモードに入ります。下図に示すように：
![](https://main.qcloudimg.com/raw/b9004e2a1d58a9a09316cf2a8a907399.png)
11. 以下のコマンドを実行して、シングルユーザーモードを終了します。
```
exec /sbin/init
```

<span id="configUbuntu"></span>
### Ubuntu 

>? 以下の操作手順は Ubuntu 16.04 を例に説明します。OSのバージョンによって詳細の操作手順は若干異なります。
>
1. リモートで CVM インスタンスにログインします。
2. 以下のコマンドを実行して、 `/etc/default/grub` ファイルを開きます。
```
sudo vi /etc/default/grub
```
3. **I** を押して、編集モードに入ります。
4. 「GRUB_TIMEOUT」（デフォルトエントリが起動されるまでの待機時間を設定するパラメータ）を検索し、実際のニーズに応じて、時間の範囲を変更します。下図に示すように：
「GRUB_TIMEOUT」のデフォルト値は5秒です。待機時間が短すぎでスタートアップ インターフェースが見えない問題を回避するには、60秒以上に変更するのをお勧めします。
>! 
> - この項目はシステムの起動時間に影響します。設定が完了したら、デフォルト値に戻す必要があります。
> - Ubuntu のデフォルトアカウントは root ではないので、sudoコマンドの利用をご注意ください。
> 
```
sudo vi /etc/default/grub
```
![](https://main.qcloudimg.com/raw/65553c2d5a01113e33b93caa93485dae.png)
3. 以下のコマンドを実行して、grub.cfgファイルを再コンパイルして生成します。
```
sudo update-grub
```
実行結果は下図に示すように：
![](https://main.qcloudimg.com/raw/9e685185ef67e7129ce34b11b5a16061.png)
4. 以下のコマンドを実行して、サーバーを再起動します。
```
sudo reboot
```
5. 約1分を待ってから、[VNCでCVM インスタンスにログインします。](https://intl.cloud.tencent.com/document/product/213/5436#.E4.BD.BF.E7.94.A8-vnc-.E7.99.BB.E5.BD.95.E5.AE.9E.E4.BE.8B)ログイン インターフェースは下図に示すように：
![](https://main.qcloudimg.com/raw/4893e2a2ed32bbe4241b33b468bdb8cf.png)
6. **e** を押してカーネル編集インターフェースに入り、 **rw single init=/bin/bash** を赤い枠のところに追加します。下図に示すように：
![](https://main.qcloudimg.com/raw/0879dd0c8c7a720542352a0722f9b9a7.png)
7. **Ctrl+X** を押して、シングルユーザーモードに入ります。下図に示すように：
![](https://main.qcloudimg.com/raw/ffc6c3cf07a9254fdcb4f6326c3daf75.png)

