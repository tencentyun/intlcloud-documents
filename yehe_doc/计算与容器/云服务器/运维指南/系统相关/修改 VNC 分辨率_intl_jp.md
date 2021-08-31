## 操作シナオリ

一部のLinuxシステムイメージのVNCのデフォルトの表示解像度が低くなっています。例えば、CentOS 6のVNCのデフォルトの解像度は720 \* 400です。パラメーターgrubを変更することで、LinuxシステムイメージのVNC解像度を1024 \* 768に設定できます。
Windowsシステムイメージの場合、VNCの解像度が低すぎると、一部の項目は正常に表示されないことがあり、または一部のアプリケーションを開けないことがあります。これらの問題を回避するには、Windowsシステムイメージの解像度を変更する必要があります。

このドキュメントでは、CVMのVNC表示解像度を調整する方法について説明します。

## 操作手順

### WindowsインスタンスのVNC解像度を変更する

> 以下は、WindowsインスタンスのVNC解像度を変更するためのガイドとして、Windows Server 2012中国語バージョンのシステムイメージを例として使用しています。
>

1. [VNCを利用してWindowsインスタンスにログインする](https://intl.cloud.tencent.com/document/product/213/32496)。
2. デスクトップ画面上で右クリックし、表示されるメニューから［画面の解像度］を選択します。
![](https://main.qcloudimg.com/raw/b8ec8e8ec22002532a4a517150079d2d.png)
3. 「画面の解像度」画面が表示されます、「解像度」の設定値をクリックして、表示されるスライダーで解像度を設定します。
![](https://main.qcloudimg.com/raw/b90a33fa0600846888a15154f1e656dc.png)
4. 「ディスプレイ設定」画面が表示された場合は、［変更を維持する］をクリックしてください。
5. ［OK］をクリックして画面解像度ウィンドウを閉じます。

### LinuxインスタンスのVNC解像度を変更する

Linuxシステムイメージには、CentOS 7、CentOS 8、Ubuntu、Debian 9.0などの新しいシステムイメージを含む、多くの種類があります。VNCのデフォルト解像度は1024 \* 768であり、VNC解像度を変更する必要はありません。以下では、例としてCentOS 6とDebian 7.8を使用して、VNC解像度を変更する方法について説明します。

#### CentOS 6

CentOS 6システムイメージの場合、VNCのデフォルト解像度は720 \* 400です。grub起動パラメータを変更することにより、VNC解像度を1024 \* 768に設定できます。設定方法は次の通りです。
1. [標準のログイン方法を利用してLinuxインスタンスにログインする（推奨）](https://intl.cloud.tencent.com/document/product/213/5436)。実際の操作方法に応じて、他のログイン方法を選択することもできます。
 - [リモートログインソフトウェアを利用してLinuxインスタンスにログインする](https://intl.cloud.tencent.com/document/product/213/32502)
 - [SSHを利用してLinuxインスタンスにログインする](https://intl.cloud.tencent.com/document/product/213/32501)
 - [VNCを利用してLinuxインスタンスにログインする](https://intl.cloud.tencent.com/document/product/213/32494)
2. OS画面で次のコマンドを実行し、`grub.conf` ファイルを開きます。
```
vim /etc/grub.conf
```
3. 次に示すように、「**i**」キーを押して編集モードに切り替えて、`grub`パラメータ値に`vga=792`を追加します。
![](https://main.qcloudimg.com/raw/3c2193fa370c48a7af149c63720da077.png)
4. 「**Esc**」キーを押し、「**:wq**」を入力し、ファイルを保存して閉じます。
5. 次のコマンドを実行して、CVMを再起動します。
```
reboot
```

#### Debian 7.8

Debian 7.8とDebian 8.2システムイメージのVNC解像度は、デフォルトで720 \* 400です。grub起動パラメーターを変更することにより、VNC解像度を1024 \* 768に設定できます。設定方法は次の通りです。
1.[標準のログイン方法を利用してLinuxインスタンスにログインする（推奨）](https://intl.cloud.tencent.com/document/product/213/5436)。実際の操作方法に応じて、他のログイン方法を選択することもできます。
 - [リモートログインソフトウェアを利用してLinuxインスタンスにログインする](https://intl.cloud.tencent.com/document/product/213/32502)
 - [SSHを利用してLinuxインスタンスにログインする](https://intl.cloud.tencent.com/document/product/213/32501)
 - [VNCを利用してLinuxインスタンスにログインする](https://intl.cloud.tencent.com/document/product/213/32494)
2. OS画面で次のコマンドを実行し、grubファイルを開きます。
```
vim /etc/default/grub
```
3. 次に示すように、「**i**」キーを押して、編集モードに切り替えて、`GRUB_CMDLINE_LINUX_DEFAULT`パラメータ値の後ろに`vga=792`を追加します。
![](https://main.qcloudimg.com/raw/f8e275c35b65b7b2d26cfbd7a8ae4dd6.png)
4. 「**Esc**」キーを押し、「**:wq**」を入力し、ファイルを保存して閉じます。
5. 次のコマンドを実行して、`grub.cfg`ファイルを更新します。
```
grub-mkconfig -o /boot/grub/grub.cfg
```
6. 次のコマンドを実行して、CVMを再起動します。
```
reboot
```


## 付録

解像度とVGAのパラメータ照合表は次の通りです。
<table>
	<tr><th>解像度</th><td>640 * 480</td><td>800 * 600</td><td>1024 * 768</td></tr>
	<tr><th>VGA</th><td>786</td><td>789</td><td>792</td></tr>
</table>
