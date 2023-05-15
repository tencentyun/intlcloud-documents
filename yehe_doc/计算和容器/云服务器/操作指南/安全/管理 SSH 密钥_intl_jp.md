## 概要
このドキュメントでは、SSHキーの作成、バインド、バインド解除、変更、削除など、SSHキーを使用したインスタンスへのログインに関連する一般的な操作について説明します。

<dx-alert infotype="notice" title="">
CVMインスタンスがシャットダウンされた後にのみ、キーをバインドまたはバインド解除できます。CVMインスタンスをシャットダウンする方法については、[インスタンスのシャットダウン](https://intl.cloud.tencent.com/document/product/213/4929)をご参照ください。
</dx-alert>



## 操作手順

### SSHキーの作成[](id:creatSSH)
1. CVMコンソールにログインし、左側のナビゲーションバーで **[SSHキー](https://console.cloud.tencent.com/cvm/image)** を選択します。
2. SSHキー管理画面で**作成**をクリックします。
3. 「SSHキーを作成」画面が表示されます。「SSHキーを作成」画面でキーを設定します。下図に示すように：
![](https://main.qcloudimg.com/raw/a6675ade459e6bf236ff7301995a35f2.png)
 - **作成方法**：
    - 「新しいキーペアを作成します」を選択した場合は、キー名を入力してください。
    - 「既存の公開鍵を使用します」を選択した場合は、キー名と既存の公開鍵情報を入力してください。
    <dx-alert infotype="notice" title="">
    パスワードが必要ない公開鍵を使用する必要があります。そうしないと、コンソールでインスタンスにログインできません。
    </dx-alert>
 - **キー名**: 名前をカスタマイズします。
 - **タグ（オプション）**：必要に応じてキーのタグを追加できます。タグは、リソースの分類、検索、および集約に使用できます。 詳細については [タグ](https://intl.cloud.tencent.com/document/product/651/13334)をご参照ください。
4. **OK**をクリックすると、作成が完了します。
<dx-alert infotype="notice" title="">
**OK**をクリックすると秘密鍵が自動的にダウンロードされます。Tencent Cloudは秘密鍵の情報を保管しませんので、ご自身で大切に保管してください。
</dx-alert>


### インスタンスへのキーのバインド[](id:bindingSSH)
1. CVMコンソールにログインし、左側のナビゲーションバーで **[SSHキー](https://console.cloud.tencent.com/cvm/image)** を選択します。
2. 下図に示すように、「SSHキー」ページで、ターゲットキーの右側にある**インスタンスをバインドする**をクリックします。
![](https://main.qcloudimg.com/raw/7419df720863aa9463e0dcf478580bbd.png)
3. ポップアップウィンドウで、リージョンとターゲットCVMインスタンスを選択し、**バインド**をクリックします。

### インスタンスからキーのバインドを解除
1. CVMコンソールにログインし、左側のナビゲーションバーで **[SSHキー](https://console.cloud.tencent.com/cvm/image)** を選択します。
2. 下図に示すように、ターゲットキーの右側にある**インスタンスのバインドを解除する**をクリックします。
![](https://main.qcloudimg.com/raw/263f344c4bea3cdff4e422996821cb5d.png)
3. ポップアップウィンドウで、リージョンとターゲットCVMインスタンスを選択し、**バインド解除**をクリックします。


### SSHキーの名前または説明の変更
1. CVMコンソールにログインし、左側のナビゲーションバーで **[SSHキー](https://console.cloud.tencent.com/cvm/image)** を選択します。
2. 「SSHキー」ページで、キー名の右側にある<img  style="margin:-3px 0px" src="https://main.qcloudimg.com/raw/9db81482f9242417d94a04f314b42b19.png"/>を選択します。下図に示すように：
![](https://main.qcloudimg.com/raw/e4c46354bafa78daa7efa24064eafea9.png)
3. ポップアップウィンドウで、新しいキーの名前と説明を入力し、**OK**をクリックします。


### SSHキーの削除

<dx-alert infotype="notice" title="">
CVMインスタンスまたはカスタムイメージにバインドされているSSHキーは削除できません。
</dx-alert>


1. CVMコンソールにログインし、左側のナビゲーションバーで **[SSHキー](https://console.cloud.tencent.com/cvm/image)** を選択します。
2. 「SSHキー」ページで、必要に応じてキーを個別または一括で削除することができます。
   <dx-tabs>
   ::: キーの個別削除
    1. 下図に示すように、削除したいSSHキーの右側にある**削除**をクリックします。
   ![](https://main.qcloudimg.com/raw/96d57d5beb3d73c0978cc1464bc73c7e.png)
    2. 「削除」画面が表示されます。「削除」画面で**OK**をクリックします。
   

:::
::: キーの一括削除
    1. 削除したいキーをすべて選択し、ページ上方にある**削除**をクリックし、キーの一括削除を行います。
        2. 「削除」画面が表示されます。「削除」画面でOKをクリックします。 下図のように：
        選択したキーペアに削除できないキーペアが含まれている場合、この操作は削除可能なキーペアに対してのみ行われます。
		![](https://main.qcloudimg.com/raw/bfcdfb401f8906834b02372d3e50dbe0.png)
		

:::
</dx-tabs>



## 関連操作


### SSHキーを使用したLinux CVMへのログイン

1. [SSHキーの作成](#creatSSH)
2. [インスタンスへのキーのバインド](#bindingSSH)
3. [SSHキーを使用したLinuxインスタンスへのログイン](https://intl.cloud.tencent.com/document/product/213/32501)


### キータグの編集

SSHキーのタグを追加、変更、および削除する方法については、次の手順を参照してください。タグの詳細については、 [タグ](https://intl.cloud.tencent.com/document/product/651/13334)をご参照ください。

1. 「SSHキー」ページでキーの右側にある**タグ編集**をクリックします。
2. 「タグ編集」画面が表示されます。「タグ編集」画面で必要に応じて設定してください。
3. **OK**をクリックします。
