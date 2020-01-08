## ユースケース
パスワードは各CVMインスタンスの専用のログイン資格情報です。インスタンスの安全性と信頼性を保証するために、Tencent Cloudは以下2種類の暗号化ログイン方式を提供します。
- [パスワードログイン](https://intl.cloud.tencent.com/document/product/213/6093)
- SSH キーペア・ログイン

本ドキュメントは、SSH キーペアでのインスタンス・ログインに関する一般的な操作について説明します。

## 操作手順

<span id="creatSSH"></span>
### SSH キーの作成
 1.  [CVMコンソール](https://console.cloud.tencent.com/cvm/)にログインします。
 2. 左側ナビゲーションバーで、【[SSH キー](https://console.cloud.tencent.com/cvm/sshkey)】をクリックします。
 3. SSH キー管理画面で、【キーの作成】をクリックします。
 4. ポップアップの【SSH キーの作成】ウィンドウで、キーの作成方式を選択し、関連情報を入力して、【OK】をクリックします。
  - 作成方式は「新しいキーペアの作成」を選択した場合、キーの名前を入力してください。
  - 作成方式は「既存のパブリックキーを利用する」を選択した場合、キーの名前と元のパブリックキーの情報を入力してください。
 4. ポップアップのプロンプトボックスで、【ダウンロード】をクリックして、プライベートキーをダウンロードできます。
 > Tencent Cloudはプライベートキーの情報を保管しません、10分以内にプライベートキーをダウンロードして取得してください。
 > 

<span id="bindingSSH"></span>
### キーをCVMにバインド/バインド解除する
 1.  [CVMコンソール](https://console.cloud.tencent.com/cvm/)にログインします。
 2. 左側ナビゲーションバーで、【[SSH キー](https://console.cloud.tencent.com/cvm/sshkey)】をクリックします。
 3. SSHキー管理画面で、バインド/バインド解除するCVMのSSH キーを選択して、【インスタンスのバインド/バインド解除】をクリックします。
 4. ポップアップの「インスタンスのバインド/バインド解除」ウィンドウで、リージョン、バインド/バインド解除のCVMを選択して、【OK】をクリックします。


### SSH キーの名前/説明の修正
 1.  [CVMコンソール](https://console.cloud.tencent.com/cvm/)にログインします。
 2. 左側ナビゲーションバーで、【[SSH キー](https://console.cloud.tencent.com/cvm/sshkey)】をクリックします。
 3. SSH キー管理画面で、修正するキーを選択して、【修正】をクリックします。
 4. ポップアップの「キーの修正」ウィンドウで、新しいキーの名前と説明を入力して、【OK】をクリックします。

### SSH キーの削除
> SSH キーがCVMまたはカスタマイズイメージと関連つけられた場合は、キーは削除できません。
>
 1.  [CVMコンソール](https://console.cloud.tencent.com/cvm/)にログインします。
 2. 左側ナビゲーションバーで、【[SSH キー](https://console.cloud.tencent.com/cvm/sshkey)】をクリックします。
 3. SSH キー管理画面で、削除するSSHキーを選択して、【削除】をクリックします。
 4. ポップアップの「キーの削除」ウィンドウで、【OK】をクリックします。

### SSHキーを利用してLinux CVMにログインする

1. [SSH キーを作成する](#creatSSH)。
2. [SSH キーをCVMにバインドする](#bindingSSH)。
3. [SSH キーを利用して、Linux インスタンスにログインする](https://cloud.tencent.com/document/product/213/35700)。
