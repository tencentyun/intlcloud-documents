## ユースケース
このドキュメントでは、SSHキーを使用して、ローカル Linux、Mac OS、または Windowsサーバーから Linux インスタンスにログインする方法について説明します。

## サポートされているOS
Linux、Mac OS または Windows (Windows 10 および Windows Server 2019 を含む)

## 認証方式
**パスワード**または**キー**です。

## 前提条件
- インスタンスにログインするための管理者アカウントとパスワード (またはキー)を取得しました。
 - Linux インスタンスの管理者アカウントは通常、デフォルトでは `root`にし、Ubuntu システムは `ubuntu`です。 実際の状況に応じて変更できます。
 - システムのデフォルトパスワードを利用してインスタンスにログインする場合は、 [サイト内メール](https://console.cloud.tencent.com/message) に移動してパスワードを取得してください。
 - [キーを使用してログイン](#LoginWithKey) する場合は、キーを作成してこのCVMインスタンスに関連付ける必要があります。さらに詳細な操作については、 [SSHキー](https://intl.cloud.tencent.com/document/product/213/16691)をご参照ください。
 - パスワードを忘れた場合は、 [インスタンスのパスワードをリセット](https://intl.cloud.tencent.com/document/product/213/16566)してください。
- CVMインスタンスはすでにパブリックIPを購入されており、このインスタンスは22番ポート(クイック設定で購入したCVMインスタンスの場合、デフォルトで開放している）を開放しました。

## 操作手順
<dx-tabs>
::: パスワードでログインする[](id:passwordLogin)
1. 次のコマンドを実行して、Linux CVMに接続します。
<dx-alert infotype="explain" title="">
- ローカルコンピューターが Mac OSを実行している場合は、次のコマンドを実行する前に、システム付属のターミナルを開く必要があります。
- ローカルコンピューターが Linuxを実行している場合は、次のコマンドを直接実行できます。
- ローカルコンピューターがWindows 10またはWindows Server 2019を実行している場合は、次のコマンドを実行する前に、コマンドプロンプト（CMD）を開く必要があります。
</dx-alert>
```
ssh <username>@<hostname or IP address>
```
 - `username` は、前提条件で取得されたデフォルトのアカウントです。
 - `hostname or IP address` は Linux インスタンスのパブリックIPアドレス或いはカスタムドメイン名です。
2. 取得したパスワードを入力し、**Enter**キーを押してログインを完了します。

:::
::: キーでログインする[](id:LoginWithKey)
1. 次のコマンドを実行して、プライベートキーファイルに本人だけ読み取り権限を付与します。
 - ローカルコンピューターが Mac OSを実行している場合は、次のコマンドを実行する前に、システム付属のターミナルを開く必要があります。
 - ローカルコンピューターが Linuxを実行している場合は、次のコマンドを直接実行できます。
```
chmod 400 <ダウンロードしたCVMに関連するプライベートキーの絶対パス>
```
 - ローカルコンピューターがWindows 10を実行している場合は、次のコマンドを実行する前に、コマンドプロンプト（CMD）を開く必要があります。
```
icacls <ダウンロードしたCVMに関連するプライベートキーの絶対パス> /grant <システムのユーザーアカウント>:F
```
```
icacls <ダウンロードしたCVMに関連するプライベートキーの絶対パス> /inheritancelevel:r
```
2. 次のコマンドを実行してリモートログインします。
```
ssh -i <ダウンロードしたCVMに関連するプライベートキーの絶対パス> <username>@<hostname or IP address>
```
 - `username` は、前提条件で取得したデフォルトのアカウントです。
 - `hostname or IP address` は Linux インスタンスのパブリックIPアドレス或いはカスタムドメイン名です。

例えば、 `ssh -i "Mac/Downloads/shawn_qcloud_stable.pem" ubuntu@192.168.11.123` コマンドを実行して、Linux CVMにリモートログインします。
:::
</dx-tabs>

## その後の操作

CVMにログインした後、個人用Webサイトまたはフォーラムを構築したり、その他の操作を実行したりできます。詳細については、下記のドキュメントをご参照ください：　　
- [WordPress 個人用サイトを構築する](https://www.tencentcloud.com/document/product/213/33469)
- [Discuz!フォーラムを手動で構築する](https://www.tencentcloud.com/document/product/213/34278)