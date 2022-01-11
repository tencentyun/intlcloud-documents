## 操作シナリオ
このドキュメントでは、SSHキーペアのインスタンスへのログインにおける一般的な関連操作について紹介します。例えばSSHキーの作成、バインド、バインド解除、修正、削除などの操作です。
>!キーのバインドまたはバインド解除を行うには、CVMがシャットダウンされている必要があります。[インスタンスのシャットダウン](https://intl.cloud.tencent.com/document/product/213/4929) を参照してCVMのシャットダウン操作を行ってください。
>

## 操作手順

<span id="creatSSH"></span>
### SSHキーの作成
 1. [CVMコンソール](https://console.cloud.tencent.com/cvm/)にログインします。
 2. 左側ナビゲーションバーの**[SSHキー](https://console.cloud.tencent.com/cvm/sshkey)**をクリックします。
 3. SSHキー管理画面で**キーの作成**をクリックします。
>! **OK**をクリックすると、秘密鍵が自動的にダウンロードされます。Tencent Cloudは秘密鍵の情報を保管しませんので、秘密鍵は必ずご自身で適切に保管してください。
 > 
![](https://main.qcloudimg.com/raw/a6675ade459e6bf236ff7301995a35f2.png)
  - 作成方式で「新しいキーペアを作成」を選択した場合は、キーの名称を入力してください。
  - 作成方式で「既存の公開鍵をインポート」を選択した場合は、キーの名称と既存の公開鍵情報を入力してください。


<span id="bindingSSH"></span>
### キーによるインスタンスのバインド
 1. [CVMコンソール](https://console.cloud.tencent.com/cvm/)にログインします。
 2. 左側ナビゲーションバーの**[SSHキー](https://console.cloud.tencent.com/cvm/sshkey)**をクリックします。
 3. SSHキー管理画面で、バインドしたいCVMのSSHキーにチェックを入れ、下図のように**インスタンスのバインド**をクリックします。
![](https://main.qcloudimg.com/raw/7419df720863aa9463e0dcf478580bbd.png)
 4. ポップアップしたインスタンスバインドウィンドウで、リージョンを選択し、バインドしたいCVMにチェックを入れ、**OK**をクリックします。


### キーによるインスタンスのバインド解除
 1. [CVMコンソール](https://console.cloud.tencent.com/cvm/)にログインします。
 2. 左側ナビゲーションバーの**[SSHキー](https://console.cloud.tencent.com/cvm/sshkey)**をクリックします。
 3. SSHキー管理画面で、バインドを解除したいCVMのSSHキーにチェックを入れ、下図のように**インスタンスのバインド解除**をクリックします。
![](https://main.qcloudimg.com/raw/263f344c4bea3cdff4e422996821cb5d.png)
 4. ポップアップしたインスタンスバインド解除ウィンドウで、リージョンを選択し、バインドを解除したいCVMにチェックを入れ、**OK**をクリックします。


### SSHキーの名称/説明の修正
 1. [CVMコンソール](https://console.cloud.tencent.com/cvm/)にログインします。
 2. 左側ナビゲーションバーの**[SSHキー](https://console.cloud.tencent.com/cvm/sshkey)**をクリックします。
 3. SSHキー管理画面で、下図のようにキー名称の右側の<img  style="margin:-3px 0px" src="https://main.qcloudimg.com/raw/9db81482f9242417d94a04f314b42b19.png"/>を選択します。
![](https://main.qcloudimg.com/raw/e4c46354bafa78daa7efa24064eafea9.png)
 4. ポップアップしたキー修正ウィンドウで、新しいキーの名称とキーの説明を入力し**OK**をクリックします。

### SSHキーの削除
>!  SSHキーがCVMまたはカスタムイメージに関連付けられている場合、そのキーは削除できません。
>
1. [CVMコンソール](https://console.cloud.tencent.com/cvm/)にログインします。
2. 左側ナビゲーションバーの、**[SSHキー](https://console.cloud.tencent.com/cvm/sshkey)**をクリックします。必要に応じてキーの単独削除または一括削除を行うことができます。
 - **キーの単独削除**
    1. SSHキー管理画面で、下図のように、削除したいSSHキーのある行の右側の**削除**を選択します。
![](https://main.qcloudimg.com/raw/96d57d5beb3d73c0978cc1464bc73c7e.png)
    2. ポップアップしたキー削除ウィンドウで、 **OK**をクリックします。
 - **キーの一括削除**
    1. SSHキー管理画面で、削除したいキーにチェックを入れて画面上方の**削除**をクリックし、キーの一括削除操作を実行します。
    2. ポップアップしたキー削除ウィンドウで、 下図のように**OK**をクリックします。
    選択したキーペアの中に削除できないキーペアが含まれる場合、この操作は削除可能なキーペアに対してのみ行われます。
		![](https://main.qcloudimg.com/raw/bfcdfb401f8906834b02372d3e50dbe0.png)


### SSHキーを使用したLinux CVMへのログイン

1. [SSHキーの作成](#creatSSH)
2. [SSHキーをCVMにバインド](#bindingSSH)
3. [SSHを使用してLinuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32501)
