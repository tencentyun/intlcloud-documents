 このドキュメントでは、ローカルサーバーからFTP経由でCVMにファイルをアップロードする方法について説明します。

## 1. CVMでFTPサービスを構築する

1) root権限で以下のコマンドを実行して、Vsftpをインストールします（CentOSシステムを例に）：

```
yum install vsftpd
```


2) vsftpdサービスを起動する前に、CVMにログインして設定ファイルを変更し、匿名ログインを禁止します。

設定ファイルを開きます。コマンドは下記の通り：

```
vim /etc/vsftpd/vsftpd.conf
```

設定ファイルの11行目の 
```
anonymous_enable=YES
```
を下記のように変更すれば、

```
anonymous_enable=NO
```
匿名ログインを禁止できます。

3) 有効な設定を読み込みます。

```
cat /etc/vsftpd/vsftpd.conf |grep ^[^#] 
```
返される結果は下記の通り：

```
local_enable=YES
write_enable=YES
local_umask=022
anon_upload_enable=YES
anon_mkdir_write_enable=YES
anon_umask=022
dirmessage_enable=YES
xferlog_enable=YES
connect_from_port_20=YES
xferlog_std_format=YES
listen=YES
pam_service_name=vsftpd
userlist_enable=YES
tcp_wrappers=YES
```

4) vsftpdサービスを起動します。

```
service vsftpd start
```

5) FTPユーザーアカウントを設定します。
以下のコマンドで、FTPユーザーのアカウントを設定します：

```
useradd
```
例えば、アカウントが「ftpuser1」、ディレクトリが/home/ftpuser1で、sshによるログインを許可しないように設定します。

```
useradd -m -d /home/ftpuser1 -s /sbin/nologin ftpuser1
```

以下のコマンドでアカウントのパスワードを設定します：

```
passwd
```
例えば、上記アカウントのパスワードを「ftpuser1」に設定します：

```
passwd ftpuser1
```

設定が成功した後、上記のアカウントでFTPサーバーにログインできます。

6) vsftpdのpam設定を変更して、ユーザーが自分で設定したFTPユーザーアカウントとパスワードでCVMに接続できるようにします。

以下のコマンドを利用してpamを変更します：

```
 vim /etc/pam.d/vsftpd
```

内容を下記のように変更します：

```
#%PAM-1.0 
auth required /lib64/security/pam_listfile.so item=user sense=deny file=/etc/ftpusers onerr=succeed 
auth required /lib64/security/pam_unix.so shadow nullok 
auth required /lib64/security/pam_shells.so 
account required /lib64/security/pam_unix.so 
session required /lib64/security/pam_unix.so 
```

以下のコマンドで、変更したファイルが正しいかどうかを確認します。

```
cat /etc/pam.d/vsftpd
```

返される結果は下記の通り：

```
auth required /lib64/security/pam_listfile.so item=user sense=deny file=/etc/ftpusers onerr=succeed 
auth required /lib64/security/pam_unix.so shadow nullok 
auth required /lib64/security/pam_shells.so 
account required /lib64/security/pam_unix.so 
session required /lib64/security/pam_unix.so 
```

以下のコマンドでvsftpdサービスを再起動して、変更を有効にします。

```
service vsftpd restart
```

返される結果は下記の通り：

```
Shutting down vsftpd: [ OK ]
Starting vsftpd for vsftpd: [ OK ]
```

## 2. Linux CVMにファイルをアップロードする
1) オープンソースソフトウェアFileZillaをダウンロードしてインストールします
FileZilla Ver.3.5.1または3.5.2を利用してください。（　FileZilla Ver.3.5.3を使用してFTP経由でファイルをアップロードすると、アップロードが失敗する場合があります。）　　
FileZillaの公式サイトでは、最新のVer.3.5.3のダウンロードのみを提供しているため、Ver.3.5.1または3.5.2のダウンロードURLをユーザーは自分で検索することをお勧めします。推奨のVer.3.5.1のダウンロードURL：http://www.oldapps.com/filezilla.php?old_filezilla=6350

2) FTPに接続します
FileZillaを実行して、下図に示すように設定します。設定した後、「クイック接続」をクリックします。
![](//mccdn.qcloud.com/img56b0593f99e17.png)

>設定情報の説明：
- ホスト：CVMのパブリックIPアドレスです。（[CVMコンソール](https://console.cloud.tencent.com/cvm）にログインして、該当CVMのパブリックIPアドレスを確認することができます）。
- ユーザー名：前の手順で設定したFTPユーザーのアカウントです。ここでは「ftpuser1」を例にします。
- パスワード：前の手順で設定したFTPユーザーアカウントのパスワードです。ここでは「ftpuser1」を例にします。
- ポート：FTPリスナーポート、デフォルトは「21」です。

3) Linux CVMにファイルをアップロードします。

ファイルをアップロードするときに、マウスでローカルファイルを選択し、リモートサイトにドラッグしてLinux CVMにアップロードします。

>注：CVM FTPチャネルは、アップロードしたtarアーカイブを自動解凍または削除する機能をサポートしていません。

ファイルアップロード操作は下図の通り：

![](//mccdn.qcloud.com/img56b05a11b4b80.png)