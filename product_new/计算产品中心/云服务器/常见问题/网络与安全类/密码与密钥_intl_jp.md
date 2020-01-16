### SSHキーログインとパスワードログインに何か違いがありますか。
SSHキーは、Linuxサーバーにリモートログインする方法であり、その原理はキージェネレーターにより、キーペア（パブリックキーとプライベートキー）を作成します。パブリックキーをサーバーに追加して、クライアントでプライベートキーを利用して認証とログインを完成させます。この方式はデータの安全性を重視します。また従来のパスワードログイン方式の手動入力に比べて、更なる利便性を提供します。
現在、Linuxインスタンスはパスワード及びSSHキーの二つのログイン方式が利用できます。Windowsインスタンスはパスワードログイン方式のみ利用できます。関連ドキュメント：
- [Linuxインスタンスをログインする](https://intl.cloud.tencent.com/document/product/213/5436)
- [Windowsインスタンスをログインする](https://intl.cloud.tencent.com/document/product/213/32498)

### SSHキーでログインする同時にパスワードログインが利用できますか。
ユーザーが [SSHキーでLinuxインスタンスをログインする](https://intl.cloud.tencent.com/document/product/213/32501) 場合は、パスワードログインがデフォルトで利用不可であることにより、安全性を向上させます。従って、SSHキーログインした後にユーザーはパスワードログインを利用できません。

### パスワードを忘れた場合どうすればよいですか。
パスワードをリセットすることができます。詳細な操作については、[インスタンスパスワードのリセット](https://intl.cloud.tencent.com/document/product/213/16566) をご参照ください。

### どのようにSSHキーを作成するか、キーを紛失した場合どうすればよいですか。
キーの作成については、[SSHキーの作成](https://intl.cloud.tencent.com/document/product/213/16691) を参照して作成します。
キーの紛失の問題を解決するために、二つの解決策を提供します：
 - CVMの [SSHキーのコンソール](https://console.cloud.tencent.com/cvm/sshkey) を利用して新しいキーを作成して、既存のインスタンスにバインディングします。
  1. [SSHキーの作成](https://intl.cloud.tencent.com/document/product/213/16691)。
  2. キーの作成が完了したら、[CVMインスタンスのコンソール](https://console.cloud.tencent.com/cvm) にアクセスしてください。
  3. キーをバインドしたい元のインスタンスを選択して、【詳細】>【パスワード/キー】>【キーのロード】にクリックすると、新しいキーを利用してインスタンスをログインすることができます。
 - CVMコンソールでパスワードをリセットして、新しいパスワードでインスタンスをログインします。詳細な操作については [インスタンスパスワードのリセット](https://intl.cloud.tencent.com/document/product/213/16566) をご参照ください。

### どのようにSSHキーをサーバーにバインド/バインド解除しますか。

[SSHキー操作ガイド](https://intl.cloud.tencent.com/document/product/213/16691)の**キーとサーバーをバインド/バインド解除**する部分をご参照ください。

### どのようにSSHキーの名前/説明を修正しますか。

[SSHキー操作ガイド](https://intl.cloud.tencent.com/document/product/213/16691)の**SSHキーの名前/説明を修正する**部分をご参照ください。

### どのようにSSHキーを削除しますか。

[SSHキー操作ガイド](https://intl.cloud.tencent.com/document/product/213/16691)の**SSHキーを削除する**部分をご参照ください。

### SSHキーはどのような使用制限がありますか。

[SSHキー概要](https://intl.cloud.tencent.com/document/product/213/6092)の**使用制限**部分をご参照ください。

### SSHキーを利用してLinuxインスタンスをログイン不能場合は、どのようにトラブルシューティングしますか。

[SSH方式でLinuxインスタンスをログイン不能](https://cloud.tencent.com/document/product/213/37925) をご参照ください。
