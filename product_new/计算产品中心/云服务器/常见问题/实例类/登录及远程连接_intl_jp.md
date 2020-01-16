### 初期パスワードを設定するには、どうすればいいですか。

CVMを購入する時に、選択された設定方法により、初期パスワードの設定が異なっています。
- 【[**クイック設定**](https://buy.cloud.tencent.com/cvm?tab=lite)】の方法でCVMを購入する場合は、CVMの初期パスワードはメールとコンソールの [内部メッセージ](https://console.cloud.tencent.com/message)にて送信させていただきます。
- 【[**カスタム設定**](https://buy.cloud.tencent.com/cvm?tab=custom)】の方法でCVMを購入する場合は、ログイン方法により、初期パスワードの設定方法は下記の通りです。
<table>
	<tr><th>ログイン方法</th><th>説明</th></tr>
	<tr><td>自動的にパスワードを生成する</td><td>初期パスワードはメールとコンソールの <a href="https://console.cloud.tencent.com/message">内部メッセージ</a> にて送信させていただきます。</td></tr>
	<tr><td>キーをすぐに関連付ける</td><td><b>デフォルトでオフする</b>ユーザー名とパスワードによるログインしますが、初期パスワードはメールとコンソールの<a href="https://console.cloud.tencent.com/message">内部メッセージ</a> にて送信させていただきます。</td></tr>
	<tr><td>パスワード設定</td><td>カスタムパスワードは初期パスワードです。</td></tr>
</table>

詳細については [ログインパスワードの管理](https://intl.cloud.tencent.com/document/product/213/17008)をご参照ください。

### パスワードをリセットするには、どうすればいいですか。

パスワードのリセットについては [インスタンスパスワードのリセット](https://intl.cloud.tencent.com/document/product/213/16566)をご参照ください。

### パスワードリセットに失敗した場合は、どうすればいいですか。

パスワードをリセットしようとするインスタンスがシャットダウンされているかを確認してください。
- シャットダウンされていない場合は、 [インスタンスをシャットダウン](https://intl.cloud.tencent.com/document/product/213/4929)してから、[インスタンスパスワードをリセット](https://intl.cloud.tencent.com/document/product/213/16566)してください。
- インスタンスがシャットダウンされている場合は、 [作業依頼書を提出](https://console.cloud.tencent.com/workorder/category)してください。それにより、エンジニアは問題解決に協力を提供します。

### LinuxインスタンスがSSHキーに関連をつけた後に、なぜユーザー名とパスワードでログインできなくなったでしょうか。

CVMがSSHキーを関連付けた後、ユーザー名とパスワードによるログインが**デフォルトでオフ**になっていますので、 [SSH キーでCVMにログイン](https://intl.cloud.tencent.com/document/product/213/32501)してください。 

### VNCでCVMにログインするには、どうすればいいですか。

VNCログインはTencent Cloudがユーザーのために提供している、WebブラウザーのリモートコネクティングによりCVMに接続する方法です。リモートログインクライアントをインストールしていない場合、あるいはクライアントのリモートログインが利用できない場合は、ユーザーはVNCログインによりCVMに接続し、CVMの状態を確認する上、CVMアカウントで基本的なCVM管理操作を行うことが可能です。具体的な操作手順は下記のドキュメントをご参照ください。
- [VNCによるLinuxインスタンスのログイン](https://intl.cloud.tencent.com/document/product/213/32494)
- [VNCによるWindowsインスタンスのログイン](https://intl.cloud.tencent.com/document/product/213/32496)

### Windowsサーバーでは、どのようにマルチユーザーのリモートログインを設定したらいいでしょうか。

Windowsサーバーは複数ユーザーの同時リモートログインに対応しています。具体的な設定方法は、 [マルチユーザーのリモートログイン可能なWindows CVMの設定](https://intl.cloud.tencent.com/document/product/213/32497)をご参照ください。
設定が有効になっていない場合は、再起動してからログインを再度試してください。

### Ubuntuシステムでは、どのようにrootユーザーでインスタンスにログインしますか。

Ubuntuシステムはデフォルトのユーザー名がubuntuであり、インストールプロセスではデフォルトでrootアカウントとパスワードを設定しません。必要な場合は、設定でrootユーザーログインを有効することが可能です。具体的な操作手順は下記の通りです。
1. ubuntuアカウントでCVMにログインします。
2. 下記のコマンドを実行し、rootのパスワードを設定します。
```
sudo passwd root
```
3. rootのパスワードを入力し、**Enter**を押します。
4. rootのパスワードを再度入力し、**Enter**を押します。
下記のような情報が返された場合は、 rootパスワードの設定に成功したことを示しています。
```
passwd: password updated successfully
```
5. 下記のコマンドを実行し、 `sshd_config` 設定ファイルを開きます。
```
sudo vi /etc/ssh/sshd_config 
```
6.  下図に示すように、**i** を押して編集モードに切り替え、 `#Authentication`を見つけてから、`PermitRootLogin` パラメータを `yes`に変更します。
>  `PermitRootLogin` パラメータが注釈された場合、最初の行の注釈符号（`#`）を取り除いてください。
> 
![](https://main.qcloudimg.com/raw/359242f7e5df666d43459fe74abce72a.png)
7.  **Esc**を押し、 **:wq**を入力し、ファイルを保存してから戻ります。
8. 下記のコマンドを実行し、sshサービスをリスタートします。
```
sudo service ssh restart
```
9.  rootアカウントとパスワードでUbuntu CVMにログインします。

### 稼働中のLinuxインスタンスのパスワードを一括的にリセットするには、どうすればいいですか。

サーバーをシャットダウンしない状態で、 Linuxインスタンスのパスワードを一括リセットするには、 [ここをクリックしてダウンロード](http://batchchpasswd-10016717.file.myqcloud.com/batch-chpasswd.tgz?_ga=1.165307193.726382295.1500898081) からスクリプトを一括リセットし、当該スクリプトを実行します。一括リセットスクリプトの使用方法は下記の通りです。
> 
> - パブリックネットワークにおけるマシンで当該スクリプトを実行する場合は、 hosts.txtファイルに入力するIPはインスタンスのパブリックIPである必要があります。
> - プライベートネットワークにおけるマシンで当該スクリプトを実行するには、インスタンスのプライベートIPを入力してもよいです。
> 
1. 操作しようとするインスタンスIP、SSHポート、アカウント、古いパスワードと新しいパスワードを hosts.txtファイルに記入します。各行は一つのホストを示しています。例えば：
```
10.0.0.1 22 root old_passwd new_passwd 
10.0.0.2 22 root old_passwd new_passwd
```
2. 下記のコードを実行します。
```
./batch-chpasswd.py
```
返信例：
```
change password for root@10.0.0.1
spawn ssh root@10.0.0.1 -p 22

root's password: 
Authentication successful.
Last login: Tue Nov 17 20:22:25 2017 from 10.181.225.39
[root@VM_18_18_centos ~]# echo root:root | chpasswd
[root@VM_18_18_centos ~]# exit
logout
```
```
change password for root@10.0.0.2
spawn ssh root@10.0.0.2 -p 22
root's password: 
Authentication successful.
Last login: Mon Nov  9 15:19:22 2017 from 10.181.225.39
[root@VM_19_150_centos ~]# echo root:root | chpasswd
[root@VM_19_150_centos ~]# exit
logout
```
