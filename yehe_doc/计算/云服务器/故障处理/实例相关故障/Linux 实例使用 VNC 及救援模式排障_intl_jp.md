通常、Linuxシステムの問題のほとんどは、VNC方式とレスキューモードを使用したトラブルシューティングで解決することができます。ここでは、この2つの方法を用いて、SSHログインができない、システムの障害発生などに対しトラブルシューティングを行う方法についてご説明します。インスタンスのトラブルシューティングと修復の方法について学ぶことができます。


## トラブルシューティングツール
- VNCログインは、Webブラウザを使ってCVMにリモート接続する方法であり、通常は、正常なSSHリモートログインができない場合に使用します。VNCログイン方式を使用すると、CVMのステータスの直接観察やシステム内の設定ファイルの変更といった操作が可能です。
- レスキューモードは、通常、Linuxシステムが正常に起動しない場合やVNCでログインできない場合に使用します。一般的なユースケースとしては、fstab設定の異常、重要なシステムファイルの欠落、lib動的ライブラリファイルの破損/欠落などがあります。

## 問題の特定および処理

<dx-accordion>
::: VNC方式によるSSHログインのトラブルシューティング方法[](id:cantSSHlogin)
#### 現象の説明
SSHを使用してLinuxインスタンスにログインすると、下図のように、「ssh_exchange_identification: Connection closed by remote host」というエラー情報が表示されます。
![](https://qcloudimg.tencent-cloud.cn/raw/4cfe14beb79b3b7b1b617fce540a53a0.png)



#### 考えられる原因
kex_exchange_identificationフェーズでのconnection resetエラーは、通常、ssh関連のプロセスが開始されたことを意味しますが、sshd設定ファイルの権限が変更されているなど、設定に異常がある可能性があります。


#### 解決方法
[処理手順](#ProcessingSteps1)を参照し、sshdのプロセスをチェックして、問題を特定して解決します。


#### 処理手順[](id:ProcessingSteps1)
1. [](id:ProcessingSteps1Step1)以下の手順を参照し、VNCを使用してLinuxインスタンスにログインします。
   1. 下図に示すように、[CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインし、ログインしたいLinux CVMを見つけて、右側の**ログイン**をクリックします。
   ![](https://qcloudimg.tencent-cloud.cn/raw/93c135917fbe34913151bbefc5b48832.png)
 2. 開いた「標準ログイン | Linuxインスタンス」ウィンドウで、**VNCログイン**をクリックします。
 3. 「login」の後にユーザー名を入力し、**Enter**を押します。「Password」の後にパスワードを入力し、**Enter**を押します。下図のようになれば、ログインに成功しています。
 ![](https://qcloudimg.tencent-cloud.cn/raw/0db1a72ceca22fbf56f8872f60baff4f.png)
2. 以下のコマンドを実行し、sshdプロセスが正常に動作しているか確認します。
```shellsession
ps -ef | grep sshd
```
下図のような結果が返されれば、sshdプロセスは正常です。
![](https://qcloudimg.tencent-cloud.cn/raw/c1024ca17237af64df91503164854983.png)
3. 次のコマンドを実行し、エラーの原因を確認します。
```shellsession
sshd -t
```
下図のような情報、"/var/empty/sshd must be owned by root and not group or world-writable.
"が返された場合、エラーの原因は、`/var/empty/sshd/`の権限の問題である可能性があります。
![](https://qcloudimg.tencent-cloud.cn/raw/19912fbd3406488556cf2e2937a6c2de.png)
また、下図に示すように、`/var/log/secure`ログにあるエラー情報を確認することで、トラブルシューティングを支援することができます。
![](https://qcloudimg.tencent-cloud.cn/raw/a696b1ce175631aebcfb92037680b506.png)
4. 次のコマンドを実行して、`/var/empty/sshd`ディレクトリの権限を確認します。
```shellsession
ll -d /var/empty/sshd/
```
下図のような結果が返されます。権限が777に変更されたことがわかります。
![](https://qcloudimg.tencent-cloud.cn/raw/952ac209bb81e882474f413b31bedfc1.png)
5. 次のコマンドを実行し、`/var/empty/sshd/`ファイル権限を変更します。
```shellsession
chmod 711 /var/empty/sshd/
```
[SSHを使用してLinuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32501)を参照してテストを行うと、正常にインスタンスにリモートログインできるようになります。


:::
::: VNC方式によるLinuxシステムの起動失敗のトラブルシューティング[](id:OSStartupFailed)

#### 現象の説明[](id:symptom)
SSHでLinux CVMへの正常なリモートログインができず、VNC方式でログインすると、システムの起動失敗が確認され、下図のように「Welcome to emergency mode」というメッセージが表示されます。
![](https://qcloudimg.tencent-cloud.cn/raw/dea541a48d2a01503c1dbbc85b0d396f.png)


#### 考えられる原因
`/etc/fstab`の設定が不適切であることが原因という可能性があります。
例えば、`/etc/fstab`においてディスクがデバイス名で自動的にマウントされるように設定されている場合も、CVMを再起動するとデバイス名が変わってしまい、システムが正常に起動しなくなることがあります。


#### 解決方法
[処理手順](#ProcessingSteps2)を参照して`/etc/fstab`設定ファイルを修復し、サーバーを再起動してから検証します。


#### 処理手順[](id:ProcessingSteps2)
1. [処理手順1](#ProcessingSteps1Step1)を参照し、VNCを使用してLinuxインスタンスにログインします。
2. 下図に示すように、VNCインターフェースに進み、[現象の説明](#symptom)のようなインターフェースが表示されたら、rootアカウントのパスワードを入力し、**Enter**を押してサーバーにログインしてください。入力されたパスワードは、デフォルトでは表示されません。
![](https://qcloudimg.tencent-cloud.cn/raw/7b9a8cdc6fe38ca6cb1e571790a54894.png)
3. システムに入った後、以下のコマンドを実行し、fstabファイル内のボリュームラベル情報が正しいかどうかを確認します。
```shellsession
lsblk
```
下図のような結果が返されます。ファイル内ボリュームラベル情報に誤りがあります。
![](https://qcloudimg.tencent-cloud.cn/raw/be6158d53fcb6e261be719f523cacb93.png)
4. 以下のコマンドを実行し、fstabファイルのバックアップを取ります。
```shellsession
cp /etc/fstab /home
```
5. 以下のコマンドを実行し、VIエディタを使用して`/etc/fstab`ファイルを開きます。
```shellsession
vi /etc/fstab
```
6. 下図に示すように、**i**を押して編集モードに入り、カーソルを設定エラーの行の先頭に移動させ、`#`を入力して行の設定についてコメントアウトします。
![](https://qcloudimg.tencent-cloud.cn/raw/a2d9e675d6586341e6b5e3a221ee7906.png)
7. **Esc**を押して**:wq**と入力した後、**Enter**を押して設定を保存し、エディタを終了します。
8. コンソールからインスタンスを再起動します。詳細については、[インスタンスの再起動](https://intl.cloud.tencent.com/document/product/213/4928)をご参照ください。
9. 正常に起動、ログインできるかどうかを検証します。


:::
::: レスキューモードによるLinuxシステムの起動失敗のトラブルシューティング[](id:rescueModeStartupFailed)
#### 現象の説明

下図に示すように、Linuxシステムが再起動後に起動せず、多数のFAILED起動失敗の項目が情報に表示されています。
![](https://qcloudimg.tencent-cloud.cn/raw/ac026f0cbea1eab4761a8557d5078cde.png)



#### 考えられる原因
binファイルやlibファイルなど、重要なシステムファイルの欠落が原因で起動に失敗することがあります。


#### 解決方法
[処理手順](#ProcessingSteps3)を参照し、コンソールからインスタンスレスキューモードに入り、トラブルシューティングと修復を行います。


#### 処理手順[](id:ProcessingSteps3)

1. レスキューモード開始前に、誤操作などによる影響を防止するため、インスタンスをバックアップすることを強くお勧めします。CBSでは[スナップショットの作成](https://intl.cloud.tencent.com/document/product/362/5755)を介してバックアップでき、ローカルシステムディスクでは[カスタムイメージの作成](https://intl.cloud.tencent.com/document/product/213/4942)を介してイメージをバックアップできます。
2. 下図に示すように、[CVMコンソール](https://console.cloud.tencent.com/cvm/instance/index?rid=1)にログインし、「インスタンス」ページで、インスタンスが配置されている行の右側の**その他** > **運用保守と検査** > **レスキューモードの開始**を選択します。
![](https://qcloudimg.tencent-cloud.cn/raw/e695226792081b7cebe90507586a1d0f.png)
3. [](id:step3)下図に示すように、ポップアップした「レスキューモードの開始」ウィンドウで、レスキューモード中にインスタンスにログインするためのパスワードを設定します。
![](https://qcloudimg.tencent-cloud.cn/raw/fdceacda011b0b0678c76c6c1f2a3c56.png)
4. **レスキューモードの開始**をクリックすると、インスタンスのステータスが「レスキューモードの開始」に変わります。下図のように、通常、この処理は数分以内に完了します。
![](https://qcloudimg.tencent-cloud.cn/raw/d6ed01e61aeb960da1209040c9383cc7.png)
レスキューモードが正常に開始された後、下図に示すように、インスタンスのステータスが赤いエクスクラメーションマーク付きの「レスキューモード」に変更します。
![](https://qcloudimg.tencent-cloud.cn/raw/ca7c6bacd0f11471c23eb4980718f906.png)
5. `root`アカウントおよび[ステップ3](#step3)で設定したパスワードを使用し、次の方式でインスタンスにログインします。
 - インスタンスにパブリックIPが有る場合は、[SSHを使用してLinuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32501)をご参照ください。
 - インスタンスにパブリックIPがない場合は、[VNCを使用してLinuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32494)をご参照ください。
2. ここでは、VNC方式によるログインを例に取ります。ログインに成功したら、下記のコマンドを実行し、システムディスクのルートパーティションをマウントします。
<dx-alert infotype="explain" title="">
レスキューモードでのインスタンスのシステムディスクデバイス名はvda、ルートパーティションはvda1で、デフォルトではマウントされていません。
</dx-alert>
```shellsession
mkdir -p /mnt/vm1
```
```shellsession
mount /dev/vda1 /mnt/vm1
```
実行が完了すると、下図のような結果が返されます。
<img src="https://qcloudimg.tencent-cloud.cn/raw/c48cd3e7b83abfc17cff3aedbf6dbfa2.png"/>
7. マウントに成功したら、元のシステムルートパーティション内のデータを操作できるようになります。
`mount -o bind`コマンドを使用して元のファイルシステムのサブディレクトリの一部をマウントし、かつ`chroot`コマンドを使用して指定のルートディレクトリでコマンドを実行することもできます。具体的な操作コマンドは次のとおりです。
```shellsession
mount -o bind /dev /mnt/vm1/dev
mount -o bind /dev/pts /mnt/vm1/dev/pts
mount -o bind /proc /mnt/vm1/proc
mount -o bind /run /mnt/vm1/run
mount -o bind /sys /mnt/vm1/sys
chroot /mnt/vm1 /bin/bash
```
`chroot`コマンドを実行する場合。
 - エラー情報がなければ、`cd /`コマンドで続行できます。
 - 下図のようなエラー情報が表示された場合は、ルートディレクトリが正常に切り替えられていないので、`cd /mnt/vm1`を実行してルートパーティションのデータを確認します。
![](https://qcloudimg.tencent-cloud.cn/raw/12e2bccf5c19edb4d248ac26d257c31e.png)
8. 下図に示すように、このコマンドは、元のシステムルートパーティションの`/usr/bin`ディレクトリにある、削除されたすべてのファイルを表示することができます。
![](https://qcloudimg.tencent-cloud.cn/raw/0f2820f10b457378d26c9a6efaf14966.png)
9. この時点で、同じOSの正常なマシンを作成して以下のコマンドを実行し、正常なシステムの`/usr/bin`ディレクトリにあるファイルを圧縮して異常なマシンへリモートでコピーすることができます。
 - 正常なマシン：以下のコマンドを順次実行します。
```shellsession
cd /usr/bin/ && tar -zcvf bin.tar.gz *
```
```shellsession
scp bin.tar.gz root@異常インスタンスip：/mnt/vm1/usr/bin/
```
<dx-alert infotype="explain" title="">
パブリックIPをお持ちの方はパブリックネットワーク経由でコピーできますが、パブリックIPをお持ちでない方は、プライベートネットワーク経由でコピーする必要があります。
</dx-alert>
```実行結果は、下図のように示されます。
<img src="https://qcloudimg.tencent-cloud.cn/raw/937f1d97edda8a2b2786b856750dfb5e.png"/>
  - 異常なマシン：レスキューモードでは、以下のコマンドが順次実行されます。
```shellsession
cd /mnt/vm1/usr/bin/
```
```shellsession
tar -zxvf bin.tar.gz
```
```shellsession
chroot /mnt/vm1 /bin/bash
```
```実行結果は、下図のように示されます。
![](https://qcloudimg.tencent-cloud.cn/raw/90e4c3d4c06806f07401ec01863dcdfa.png)
10. 下図に示すように、インスタンスの修復が完了したら、インスタンスが配置されている行右側の**その他** > **運用保守と検査** > **レスキューモードの終了**を選択します。
![](https://qcloudimg.tencent-cloud.cn/raw/d9f8f26b745a654cb145bbfc4bb1cd2a.png)
11. レスキューモード終了後、インスタンスはシャットダウン状態になり、起動後にシステム検証が行われます。下図のようになった場合、システムはすでに復元されています。
![](https://qcloudimg.tencent-cloud.cn/raw/705c27323e74f424b775f88567d7252c.png)






:::
</dx-accordion>



