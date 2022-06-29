通常、Linuxシステムの問題の多くは、VNC方式およびレスキューモードによりトラブルシューティング・修復ができます。このドキュメントでは、上記の2つの方法を使用して、LinuxインスタンスがSSHにログインできない問題、システムが失敗する問題をトラブルシューティングする方法について説明します。このドキュメントで問題が発生した場合のトラブルシューティングと修正について理解できます。


## トラブルシューティングツール
- VNCログインは、Webブラウザを介してCVMにリモート接続する方法であり、通常はインスタンスにいつものようにSSHリモートログインできない場合に使用されます。VNCログインを使用すると、CVMの状態を直接観察したり、システム内の設定ファイルを変更したりすることができます。
- レスキューモードは通常、Linuxシステムが正常に起動しない場合、またはVNCからログインできない場合に使用されます。一般的なユースケースとしては、fstab設定の異常、システムクリティカルファイルの欠落、libダイナミックライブラリファイルの破損/欠落などがあります。

## 問題の特定および対処

<dx-accordion>
：：： VNCによるSSHログイン不能の問題のトラブルシューティング[](id：cantSSHlogin)
####　故障について
SSHを使用してLinuxインスタンスにログインすると、次の図に示すように、「ssh_exchange_identification: Connection closed by remote host」エラー情報が表示されます：
![](https://qcloudimg.tencent-cloud.cn/raw/4cfe14beb79b3b7b1b617fce540a53a0.png)



#### 考えられる原因
kex_exchange_identificationフェーズのconnection resetにエラーが発生すると、通常、ssh関連プロセスが開始されたことを意味しますが、sshd設定ファイルの権限が変更された場合など、設定に異常が発生した可能性があります。


#### ソリューション
[処理手順](#ProcessingSteps1)を参照して、sshdプロセスを確認し、問題を特定して解決します。


#### 処理手順[](id:ProcessingSteps1)
1. [](id：ProcessingSteps1Step1)次の手順を参照して、VNCを使用してLinuxインスタンスにログインします：
   1. [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインし、ログインするLinuxCVMを探し、右側の[**ログイン**]をクリックします。下図の通りです：
   ![](https://qcloudimg.tencent-cloud.cn/raw/93c135917fbe34913151bbefc5b48832.png)
 2. 開いた「標準ログイン | Linuxインスタンス」ウィンドウで、**VNCログイン**をクリックします。
 3. 「login」後にユーザー名を入力し、**Enter**を押し、「Password」後にパスワードを入力し、**Enter**を押します。次の図に示すように、ログインが成功しました：
 ![](https://qcloudimg.tencent-cloud.cn/raw/0db1a72ceca22fbf56f8872f60baff4f.png)
2. 次のコマンドを実行して、sshdプロセスが正常に動作しているかどうかを確認します。
```shellsession
ps -ef | grep sshd
```
次の図のような結果が返されると、sshdプロセスは正常です。
![](https://qcloudimg.tencent-cloud.cn/raw/c1024ca17237af64df91503164854983.png)
3. 次のコマンドを実行し、エラーの原因を確認します。
```shellsession
sshd -t
```
次の図のような「/var/empty/sshd must be owned by root and not group or world-writable.
」が返された場合、`/var/empty/sshd/`権限の問題がエラーの原因であると特定できます。
![](https://qcloudimg.tencent-cloud.cn/raw/19912fbd3406488556cf2e2937a6c2de.png)
また、`/var/log/secure`のログにあるエラー情報を確認することで、トラブルシューティングを支援することもできます。下図の通りです：
![](https://qcloudimg.tencent-cloud.cn/raw/a696b1ce175631aebcfb92037680b506.png)
4. 次のコマンドを実行して、`/var/empty/sshd`ディレクトリの権限を表示します。
```shellsession
ll -d /var/empty/sshd/
```
次の図に示すよう結果が返されると、権限が777に変更されたことがわかります。
![](https://qcloudimg.tencent-cloud.cn/raw/952ac209bb81e882474f413b31bedfc1.png)
5. 次のコマンドを実行し、`/var/empty/sshd/`のファイル権限を修正します。
```shellsession
chmod 711 /var/empty/sshd/
```
[SSHキーを使用してLinuxインスタンスにログインする](https://intl.cloud.tencent.com/document/product/213/32501)を参照してテストすると、正常にインスタンスにリモートログインできます。


:::
：：： VNCによるLinuxシステムの起動失敗のトラブルシューティング[](id：OSStartupFailed)

#### 故障について[](id:symptom)
CVMへのログインに失敗し、VNCでログインした後、「Welcome to emergency mode」というメッセージが表示され、システムの起動に失敗したことを確認します。下図の通りです：
![](https://qcloudimg.tencent-cloud.cn/raw/dea541a48d2a01503c1dbbc85b0d396f.png)


#### 考えられる原因
`/etc/fstab`が適切に設定されていない恐れがあります。
例えば、`/etc/fstab`でデバイス名を使用してディスクを自動的にマウントするように設定したが、CVMの再起動時にデバイス名が変更されたため、システムが正常に起動できなくなります。


#### ソリューション
[処理手順](#ProcessingSteps2)を参照して`/etc/fstab`設定ファイルを修正し、サーバを再起動してから検証してください。


#### 処理手順[](id:ProcessingSteps2)
1. [処理ステップ1]（#ProcessingSteps1Step1）を参照し、VNCを用いてLinuxインスタンスにログインします。
2. VNC画面に入り、[故障について](#symptom)に表示されている画面が表示されたら、rootアカウントのパスワードを入力し、**Enter**キーを押してCVMにログインします。入力したパスワードは、次の図に示すように、デフォルトで非表示となっています：
![](https://qcloudimg.tencent-cloud.cn/raw/7b9a8cdc6fe38ca6cb1e571790a54894.png)
3. システムに入り、次のコマンドを実行して、fstabファイルのドライブ文字情報が正しいかどうかを確認します。
```shellsession
lsblk
```
次の図に示すような結果が返されると、ファイルのドライブ文字情報にエラーがあります：
![](https://qcloudimg.tencent-cloud.cn/raw/be6158d53fcb6e261be719f523cacb93.png)
4. 次のコマンドを実行して、fstabファイルをバックアップします。
```shellsession
cp /etc/fstab /home
```
5. 以下のコマンドを実行して、VIエディタを利用して`/etc/fstab` ファイルを開きます。
```shellsession
vi /etc/fstab
```
6. **i**キーを押して編集モードに入り、カーソルを誤った設定の行の先頭に移動し、`#`と入力して行の設定をコメントします。下図の通りです：
![](https://qcloudimg.tencent-cloud.cn/raw/a2d9e675d6586341e6b5e3a221ee7906.png)
7. **Esc**を押して、**:wq**を入力し、**Enter**を押してください。設定を保存して、エディターを終了します。
8. コンソールでインスタンスを再起動します。詳細については、 [インスタンスの再起動](https://intl.cloud.tencent.com/document/product/213/4928)をご参照ください。
9. 起動後に正常に起動してログインできるか確認します


:::
：：：レスキューモードによるLinuxシステム起動失敗のトラブルシューティング[](id：rescueModeStartupFailed)
####　故障について

Linuxシステムが再起動後に正常に起動せず、FAILED起動失敗項目が多数表示されます。下図の通りです：
![](https://qcloudimg.tencent-cloud.cn/raw/ac026f0cbea1eab4761a8557d5078cde.png)



#### 考えられる原因
binファイルやlibファイルが見つからないなど、重要なシステムファイルの欠落によって起動に失敗することがあります。


#### ソリューション
[処理手順](#ProcessingSteps3)を参照して、コンソールからケースレスキューモードに移行し、問題のトラブルシューティングと修復を行います。


#### 処理手順[](id:ProcessingSteps3)

1. レスキューモード開始前に、誤操作などによる影響を防止するため、インスタンスをバックアップすることを強くお勧めします。CBSでは[スナップショットの作成](https://intl.cloud.tencent.com/document/product/362/5755)を介してバックアップでき、ローカルシステムディスクでは[カスタムイメージの作成](https://intl.cloud.tencent.com/document/product/213/4942) を介してイメージをバックアップできます。
2. [CVMコンソール](https://console.cloud.tencent.com/cvm/instance/index?rid=1)にログインし、[インスタンス]ページで、インスタンスが存在する行の右側にある**その他**>**運用保守と検査**>**レスキューモードに入る**を選択します。下図の通りです：
![](https://qcloudimg.tencent-cloud.cn/raw/e695226792081b7cebe90507586a1d0f.png)
3. [](id:step3)下図に示すように、ポップアップした「レスキューモードの開始」ウィンドウで、レスキューモード中にインスタンスにログインするためのパスワードを設定します。
![](https://qcloudimg.tencent-cloud.cn/raw/fdceacda011b0b0678c76c6c1f2a3c56.png)
4. 「**レスキューモードに入る**をクリックします。この場合、インスタンスの状態が「レスキューモードに入る」に変わります。このプロセスは通常、次の図に示すように数分で完了します：
![](https://qcloudimg.tencent-cloud.cn/raw/d6ed01e61aeb960da1209040c9383cc7.png)
通常のレスキューモードに入ると、インスタンスの状態は赤い感嘆符の「レスキューモード」に変わります。下図の通りです：
![](https://qcloudimg.tencent-cloud.cn/raw/ca7c6bacd0f11471c23eb4980718f906.png)
5. `root`アカウントおよび [手順3](#step3) で設定したパスワードを使用し、次の方式でインスタンスにログインします。
 - インスタンスにパブリックIPがある場合は、[SSHを使用したLinuxインスタンスへのログイン](https://intl.cloud.tencent.com/document/product/213/32501)をご参照ください。
 - インスタンスにパブリックIPがない場合は、[VNCを使用したLinuxインスタンスへのログイン](https://intl.cloud.tencent.com/document/product/213/32494)をご参照ください。
2. このドキュメントではVNCによるログインを例としています。ログインに成功した後、以下のコマンドを順次実行してシステムディスクルートパーティションをマウントします。
<dx-alert infotype="explain" title="">
レスキューモードでのインスタンスのシステムディスクデバイス名は`vda`、ルートパーテーションは`vda1`で、デフォルトではマウントされていません。
</dx-alert>
```shellsession
mkdir -p /mnt/vm1
```
```shellsession
mount /dev/vda1 /mnt/vm1
```
実行が完了した後、実行結果は下図のように示されます：
<img src="https://qcloudimg.tencent-cloud.cn/raw/c48cd3e7b83abfc17cff3aedbf6dbfa2.png"/>
7. 正常にマウントされると、元のシステムのルートパーティションのデータを操作できます。
また`mount -o bind`コマンドを使用して元のファイルシステムのサブディレクトリの一部をマウントし、かつ`chroot`コマンドを使用して指定のルートディレクトリでコマンドを実行することもできます。具体的な操作コマンドは次のとおりです：
```shellsession
mount -o bind /dev /mnt/vm1/dev
mount -o bind /dev/pts /mnt/vm1/dev/pts
mount -o bind /proc /mnt/vm1/proc
mount -o bind /run /mnt/vm1/run
mount -o bind /sys /mnt/vm1/sys
chroot /mnt/vm1 /bin/bash
```
`chroot`コマンドを実行する時：
 - エラーが報告されない場合は、`cd/`コマンドを引き続き実行できます。
 - 次の図のようなエラーメッセージが表示された場合は、ルートディレクトリの切り替えが正常に行われないため、`cd/mnt/vm1`を実行してルートパーティションのデータを表示できます。
![](https://qcloudimg.tencent-cloud.cn/raw/12e2bccf5c19edb4d248ac26d257c31e.png)
8. コマンドを使用すると、元のシステムのルートパーティションにある`/usr/bin`ディレクトリのすべてのファイルが削除されたことを確認できます。下図の通りです：
![](https://qcloudimg.tencent-cloud.cn/raw/0f2820f10b457378d26c9a6efaf14966.png)
9. この場合、同じオペレーティングシステムの正常なマシンを作成し、次のコマンドを実行して、正常なシステムの`/usr/bin`ディレクトリにあるファイルを圧縮して、リモートで異常なマシンにコピーします。
 - 通常のマシン：次のコマンドを順番に実行します
```shellsession
cd /usr/bin/ && tar -zcvf bin.tar.gz *
```
```shellsession
scp bin.tar.gz root@異常インスタンスip：/mnt/vm1/usr/bin/
```
<dx-alert infotype="explain" title="">
パブリックIPがあればパブリックネットワーク経由でコピーしますが、パブリックIPがなければプライベートネットワーク経由でコピーします。
</dx-alert>
```実行結果は、下図のように示されます：
<img src="https://qcloudimg.tencent-cloud.cn/raw/937f1d97edda8a2b2786b856750dfb5e.png"/>
  - 異常なマシン：レスキューモードで次のコマンドを順次実行します
```shellsession
cd /mnt/vm1/usr/bin/
```
```shellsession
tar -zxvf bin.tar.gz
```
```shellsession
chroot /mnt/vm1 /bin/bash
```
```実行結果は、下図のように示されます：
![](https://qcloudimg.tencent-cloud.cn/raw/90e4c3d4c06806f07401ec01863dcdfa.png)
10. インスタンス修復が完了した後、下図に示すように、インスタンスが配置される行右側の**その他** > **運用保守と検査** > **レスキューモードの終了**を選択します。
![](https://qcloudimg.tencent-cloud.cn/raw/d9f8f26b745a654cb145bbfc4bb1cd2a.png)
11. レスキューモードを終了した後、インスタンスはシャットダウン状態になり、電源が入った後にシステムの検証が行われます。次の図に示すように、システムは回復しました。
![](https://qcloudimg.tencent-cloud.cn/raw/705c27323e74f424b775f88567d7252c.png)






:::
</dx-accordion>



