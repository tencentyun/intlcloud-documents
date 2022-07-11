## 概要
このドキュメントではCentOS 8.2オペレーティングシステムにおけるTencent CloudのCloud Virtual Machine（CVM）を例として、SCPを使用してLinux CVMにファイルをアップロードまたはダウンロードします。


##  前提条件
Linux CVMを購入済みであること。

## 操作手順
### パブリックIPの取得
[CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインし、ファイルをアップロードするCVMのパブリックIPを、インスタンスリストページに記述します。下図に示すとおりです。
![](https://main.qcloudimg.com/raw/4ffafbd2f6ab65d55e56fe59b669363a.png)


### ファイルのアップロード
1. 次のコマンドを実行して、Linux CVMにファイルをアップロードします。
```
scpローカルファイルアドレス CVMアカウント@CVMインスタンスのパブリックIP/ドメイン名:CVMファイルアドレス
```
例えば、ローカルファイル`/home/lnmp0.4.tar.gz`をIPアドレスが`129.20.0.2`のCVMの対応ディレクトリにアップロードする必要がある場合、実行するコマンドは以下のようになります。
```
scp /home/Inmp0.4.tar.gz root@129.20.0.2:/home/Inmp0.4.tar.gz
```
<dx-alert infotype="explain" title="">
`-r` パラメータを追加することでフォルダをアップロードすることができます。より多くのscpコマンドの機能をお知りになりたい場合は、`man scp`を実行して情報を取得することができます。
</dx-alert>

2. **yes**を入力してから**Enter**を押してアップロードを確認し、ログインパスワードを入力すると、アップロードが完了します。
 - システムのデフォルトパスワードを使用してインスタンスにログインする場合は、[サイト内メール](https://console.cloud.tencent.com/message)にアクセスしてパスワードを取得してください。
 - パスワードを忘れた場合は、[インスタンスのパスワードをリセット](https://intl.cloud.tencent.com/document/product/213/16566)してください。

### ファイルのダウンロード
1. 次のコマンドを実行して、Linux CVM上のファイルをローカルにダウンロードします。
```
scp CVMアカウント@CVMインスタンスのパブリックIP/ドメイン名:CVMファイルアドレス ローカルファイルアドレス 
```
例えば、IPアドレスが`129.20.0.2`であるCVMのファイル`/home/lnmp0.4.tar.gz`をローカルの対応ディレクトリにダウンロードする必要がある場合、実行するコマンドは以下のようになります。
```
scp root@129.20.0.2:/home/Inmp0.4.tar.gz /home/Inmp0.4.tar.gz
```

