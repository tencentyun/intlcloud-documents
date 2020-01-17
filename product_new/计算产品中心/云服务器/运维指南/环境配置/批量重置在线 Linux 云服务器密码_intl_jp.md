## 操作シナリオ

このドキュメントは非シャットダウン状態の場合、複数の Linux CVMがパスワードリセットのバッチ処理する方法について説明します。

## スクリプトのダンロード
Tencent Cloudは既にリセット操作のスクリプトを作成しました、このスクリプトをダンロードして解凍・圧縮してCVMに転送することにより、簡単にオンラインでリセットのバッチ処理を実行することができます。
パスを取得する：`http://batchchpasswd-10016717.file.myqcloud.com/batch-chpasswd.tgz`

## 操作手順

### CentOS / SUSE OSの操作方法

1.以下コマンドを実行し、`hosts.txt`ファイルを開きます。
```
vi /etc/hosts
```
2. **i** または **Insert** を押し、編集モデルを切り替えて、【CVM IP + SSH ポート号 + アカウント + 旧パスワード + 新パスワード】形式に基づいて、 修正する必要があるCVM情報を`hosts.txt` ファイルに追加します。下図に示すように：
```
10.0.0.1 22 root old_passwd new_passwd 
10.0.0.2 22 root old_passwd new_passwd
```
> 情報の一行は一つCVMを表します。パプリックネットワークでこのスクリプトを実行する場合、CVM IPに **パプリックIP**を記入します。プライベートネットワークでこのスクリプトを実行する場合、CVM IPに **プライベートIP**を記入します。
>
3. **Esc**を押し、**:wq**を入力して、ファイルを保存して戻ります。
4. 以下コマンドを実行し、スクリプトファイルを実行します。
```
./batch-chpasswd.py
```
以下のような結果が返された場合、リセットが成功したを示しています。
```
change password for root@10.0.0.1
spawn ssh root@10.0.0.1 -p 22
root password: 
Authentication successful.
Last login: Tue Nov 17 20:22:25 2015 from 10.181.XXX.XXX
[root@VM_18_18_centos ~]# echo root:root | chpasswd
[root@VM_18_18_centos ~]# exit
logout
change password for root@10.0.0.2
spawn ssh root@10.0.0.2 -p 22
root password: 
Authentication successful.
Last login: Mon Nov  9 15:19:22 2015 from 10.181.XXX.XXX
[root@VM_19_150_centos ~]# echo root:root | chpasswd
[root@VM_19_150_centos ~]# exit
logout
```

### Ubuntu OSの操作方法

1.以下コマンドを実行し、`hosts.txt`ファイルを開きます。
> ここでシステムのデフォルトエディターを呼び出し、他のテキストエディターを利用して編集することも可能です。
>
```
sudo gedit /etc/hosts
```
2. **i** または **Insert** を押し、編集モデルを切り替えて、【CVM IP + SSH ポート号 + アカウント + 旧パスワード + 新パスワード】形式に基づいて、 修正する必要があるCVM情報を`hosts.txt` ファイルに追加します。下図に示すように：
```
10.0.0.1 22 root old_passwd new_passwd 
10.0.0.2 22 root old_passwd new_passwd
```
> 情報の一行は一つCVMを表します。パプリックネットワークでこのスクリプトを実行する場合、CVM IPに **パプリックIP**を記入します。プライベートネットワークでこのスクリプトを実行する場合、CVM IPに **プライベートIP**を記入します。
>
3．以下コマンドを実行し、ネットワークを再起動します。
```
sudo rcnscd restart
```
4. 以下コマンドを実行し、スクリプトファイルを実行します。
```
python batch-chpasswd.py
```
