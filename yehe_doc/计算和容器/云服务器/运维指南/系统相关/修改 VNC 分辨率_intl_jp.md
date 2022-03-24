## 概要
ここでは、CVMコンソールでインスタンスのVNCログイン時の表示解像度を調整する方法についてご紹介いたします。

Windowsシステムイメージの場合、VNCの解像度が低すぎると、一部のプロジェクトの正常な表示に影響が生じたり、一部のアプリケーションが開けなくなったりすることがあります。解像度を変更することで、これらの問題を回避することができます。
一部のLinuxシステムイメージではVNCのデフォルト解像度が低く、例えばCentOS 6のVNCのデフォルト解像度は720 \* 400しかありません。grubパラメータを変更することで、LinuxシステムイメージのVNC解像度を1024 \* 768に設定できます。
<dx-alert infotype="explain" title="">
Linuxシステムイメージには様々なタイプがあり、CentOS 7、CentOS 8、Ubuntu、Debian 9.0などの比較的新しいシステムイメージでは、VNCのデフォルト解像度は1024 \* 768となっており、解像度を変更する必要はありません。
</dx-alert>












##  前提条件
すでにVNCを使用してインスタンスにログインしていること。ログインしていない場合は、次のドキュメントを参照して操作することができます。
 - [VNCによるWindowsインスタンスのログイン](https://intl.cloud.tencent.com/document/product/213/32496)
 - [VNCによるLinuxインスタンスにログインする](https://intl.cloud.tencent.com/document/product/213/32494)。


## 操作手順

<dx-tabs>
::: Windowsインスタンス
<dx-alert infotype="explain" title="">
ここでは、Windows Server 2012中国語版のシステムイメージを例として、WindowsインスタンスのVNC解像度を変更する方法をご説明いたします。
</dx-alert>



1. 下図に示すように、OSインターフェース上で右クリックし、**ディスプレイの解像度**を選択します。
![](https://main.qcloudimg.com/raw/b8ec8e8ec22002532a4a517150079d2d.png)
2. 下図に示すように、表示されたディスプレイの解像度ウィンドウで、**解像度**の大きさを設定し、**適用**をクリックします。
![](https://main.qcloudimg.com/raw/b90a33fa0600846888a15154f1e656dc.png)
3. ポップアップしたダイアログボックスで、**変更を維持する**をクリックします。
4. **OK**をクリックし、ディスプレイの解像度ウィンドウを閉じます。


:::
::: Linuxインスタンス

ここでは、CentOS 6およびDebian 7.8を例として、VNC解像度を変更する方法をご説明いたします。


#### CentOS 6

CentOS 6システムイメージでは、VNCのデフォルト解像度は720 \* 400です。grub起動パラメータを変更することで、VNC解像度を1024 \* 768に設定できます。設定の方法は次のとおりです。
1. OSインターフェース上で次のコマンドを実行し、`grub.conf`ファイルを開きます。
```
vim /etc/grub.conf
```
2. 下図に示すように、**i**キーを押して編集モードに切り替え、`grub`パラメータ値に`vga=792`を追加します。
![](https://main.qcloudimg.com/raw/3c2193fa370c48a7af149c63720da077.png)
3. **Esc**を押し、**:wq**を入力して、ファイルを保存して戻ります。
4. 次のコマンドを実行し、CVMを再起動します。
```
reboot
```



#### Debian 7.8

Debian 7.8およびDebian 8.2システムイメージのVNCのデフォルト解像度は720 \* 400です。grub起動パラメータを変更することで、VNC解像度を1024 \* 768に設定できます。設定の方法は次のとおりです。
1. OSインターフェース上で次のコマンドを実行し、grubファイルを開きます。
```
vim /etc/default/grub
```
2. 下図に示すように、**i**キーを押して編集モードに切り替え、`GRUB_CMDLINE_LINUX_DEFAULT`パラメータ値の後に`vga=792`を追加します。
![](https://main.qcloudimg.com/raw/f8e275c35b65b7b2d26cfbd7a8ae4dd6.png)
3. **Esc**を押し、**:wq**を入力して、ファイルを保存して戻ります。
4. 次のコマンドを実行し、`grub.cfg`ファイルを更新します。
```
grub-mkconfig -o /boot/grub/grub.cfg
```
5. 次のコマンドを実行し、CVMを再起動します。
```
reboot
```

:::
</dx-tabs>



## 付録

Linuxインスタンスの解像度とVGAのパラメータ対照表は次のとおりです。
<table>
	<tr><th>解像度</th><td>640 * 480</td><td>800 * 600</td><td>1024 * 768</td></tr>
	<tr><th>VGA</th><td>786</td><td>789</td><td>792</td></tr>
</table>
