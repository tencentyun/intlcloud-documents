##  操作シナリオ

このドキュメントでは、LinuxシステムのローカルPC上でFTPサービスを使用して、ファイルをローカルからCVMにアップロードする方法について説明します。

## 前提条件

Cloud Virtual Machine(CVM)にFTPサービスを構築済み。
- FTPを使用してファイルをLinux CVMにアップロードするには、[Linux CVMでFTPサービスの構築](https://intl.cloud.tencent.com/document/product/213/10912)をご参照ください。
- FTPを使用してファイルをWindows CVMにアップロードするには、[Windows CVMでFTPサービスの構築](https://intl.cloud.tencent.com/document/product/213/10414)をご参照ください。

## 操作手順

### CVMへの接続
1. 次のコマンドを実行し、FTPサービスをインストールします。
> LinuxシステムのローカルPCにFTPサービスがインストールされている場合は、このステップをスキップして次に進んでください。
>
```
yum -y install ftp
```
2. 次のコマンドを実行し、ローカルPCでCVMに接続します。画面の指示に従って、FTPサービスのアカウントとパスワードを入力します。
```
ftp CVMのIPアドレス
```
次の画面に進むと、接続は正常に確立されています。
![](https://main.qcloudimg.com/raw/9d93f45167addf70e023a21543af59f8.png)

### ファイルのアップロード
次のコマンドを実行して、ローカルファイルをCVMにアップロードします。
```
put local-file [remote-file]
```
たとえば、ローカルファイル `/home/1.txt`をCVMにアップロードします。
```
put /home/1.txt 1.txt
```

### ファイルのダウンロード
次のコマンドを実行して、CVM上のファイルをローカルディレクトリにダウンロードします。
```
get [remote-file] [local-file]
```
たとえば、CVM上の`A.txt`ファイルをローカルの`/ home`ディレクトリにダウンロードします。
```
get A.txt /home/A.txt
```

