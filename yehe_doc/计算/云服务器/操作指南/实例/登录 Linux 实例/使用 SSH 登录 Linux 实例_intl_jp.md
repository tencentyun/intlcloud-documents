## 概要

このドキュメントでは、Linux、Mac OSまたはWindowsシステムのローカルPCでSSHキーを利用してLinuxインスタンスにログインする方法について説明します。

## サポートされるシステム

Linux、Mac OSまたはWindows（Windows 10およびWindows Server 2019）

## 認証方式

**パスワード**または**キー**です。

## 前提条件
- インスタンスにログインするための管理者アカウント及びパスワード(またはキー)を取得しました。
 - システムのデフォルトパスワードを利用して、インスタンスにログインする場合は、[サイト内メール](https://console.cloud.tencent.com/message) にアクセスしてパスワードを取得してください。
 - [キーを使用してログインする](#LoginWithKey) 場合、キーを作成してこのCVMにバインドする必要があります。詳細の操作については、[SSHキー](https://intl.cloud.tencent.com/document/product/213/16691)をご参照ください。
 - パスワードを忘れた場合、[インスタンスパスワードのリセット](https://intl.cloud.tencent.com/document/product/213/16566)を行ってください。
- ご利用のCVMインスタンスはすでにパブリックIPを購入されており、このインスタンスは22ポート（クイック設定で購入したCVMインスタンスの場合、デフォルトでポートを開放）を開放しました。

## 操作手順

### パスワードでログインする

1. 次のコマンドを実行して、Linux CVMに接続します。
> ローカルPCがMac OSの場合、最初にシステム付属の端末（Terminal）を起動して、次のコマンドを実行する必要があります。
> ローカルPCがLinuxシステムの場合、次のコマンドを直接実行できます。
> ローカルPCがWindows 10またはWindows Server 2019の場合、コマンドプロンプト（CMD）を起動して、次のコマンドを実行する必要があります。
>
```
ssh <username>@<hostname or IP address>
```
 - `username` は、前提条件で取得されたデフォルトアカウントです。
 - `hostname or IP address` はLinuxインスタンスのパブリックIPアドレス或いはカスタムドメイン名です。
2. すでに取得しているパスワードを入力し、**Enter**キーを押してログインします。

<span id="LoginWithKey"></span>
### キーでログインする

1. 次のコマンドを実行して、プライベートキーファイルに本人のみ読み取り権限を付与します。
 > ローカルPCがMac OSの場合、最初にシステム付属の端末（Terminal）を起動して、次のコマンドを実行する必要があります。
 > ローカルPCがLinuxシステムの場合、次のコマンドを直接実行できます。
```
chmod 400 <The absolute path of the private key downloaded to be associated with the CVM>
```
 > ローカルPCがWindows 10の場合、コマンドプロンプト（CMD）を起動して、次のコマンドを順次実行する必要があります。
```
icacls <The absolute path of the private key downloaded to be associated with the CVM> /grant <ユーザー名>:F
```
```
icacls <The absolute path of the private key downloaded to be associated with the CVM> /inheritancelevel:r
```
2. 次のコマンドを実行して、リモートログインします。
```
ssh -i <The absolute path of the private key downloaded to be associated with the CVM> <username>@<hostname or IP address>
```
 - `username` は、前提条件で取得したデフォルトアカウントです。
 - `hostname or IP address` はLinuxインスタンスのパブリックIPアドレス或いはカスタムドメイン名です。

 例えば、 `ssh -i "Mac/Downloads/shawn_qcloud_stable" ubuntu@192.168.11.123` コマンドを実行して、Linux CVMにリモートログインします。

## 後続の操作

CVMにログインした後、個人のWebサイトまたはフォーラムを構築したり、その他の操作を実行したりできます。関連操作については、下記をご参照ください：　　
- [WordPress Webサイトを構築する](https://intl.cloud.tencent.com/document/product/213/8044)


