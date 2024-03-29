## 操作シナリオ
CAM（Cloud Access Management）のロールは一組の権限を持つ仮想ロールで、Tencent Cloud中のサービスをダウンロードし、操作およびリソースのアクセス権限をロールに付与するために使用します。CAMのロールはCVMインスタンスに関連付けられ、インスタンス内でTencent Cloudセキュリティ証明書サービスSTSの一時キーに基づき他のクラウド製品のAPIにアクセスすることができます（一時キーは周期的に更新されます）。この方法を使用すると、直接SecretKeyを使用して権限制御を実行するのと比べ、アカウント下のSecretKeyセキュリティの安全性が強化され、CAMの機能を活用して制限と権限付与をより緻密に管理することができます。

ここでは、インスタンスロールのバインド、変更および削除などの、インスタンスロールの管理方法について説明します。

## 機能のメリット
インスタンスのためにCAMのロールをバインドすると、以下の機能およびメリットが加わります。
- STS一時キーを使用すると、Tencent Cloudの他のクラウドサービスにアクセスできます。
- 異なるインスタンスに異なる権限付与ポリシーが含まれるロールを付与すると、インスタンスは異なるクラウドリソースに対する異なるアクセス権限を持つことができ、より緻密な権限制御が実現します。
- 自分でインスタンス中にSecretKeyを保存する必要はありません。修正ロールの権限付与によって権限を変更することができ、インスタンスが備えているアクセス権限を迅速にメンテナンスすることができます。




## 利用説明
- インスタンスは`cvm.qcloud.com`のロールを含むロールのバインドのみをサポートしています。詳細については、[ロールの基本概念](https://intl.cloud.tencent.com/document/product/598/19421)をご参照ください。
- インスタンスのネットワークタイプは専用ネットワークVPCである必要があります。
- 1つのインスタンスは一度に1つのCAMロールの権限付与のみをサポートしています。
- インスタンスロールをバインド、変更および削除しても、別料金は発生しません。


## 操作手順

### インスタンスロールのバインド/変更
<dx-tabs>
::: 単一インスタンスロールのバインド/変更
1. [CVMコンソール](https://console.cloud.tencent.com/cvm)にログインし、左側のナビゲーションバーで**インスタンス**を選択します。
2. インスタンスの管理画面で、実際に使用されているビューモードに従って操作します。
    -**リストビュー**：ロールをバインドまたは変更する必要があるCVMの行の右側にある**その他**>**インスタンス設定**>**ロールのバインド/変更**を選択します。下図のとおりです。
  ![](https://main.qcloudimg.com/raw/34d5a9866aa28fdb8a3363884918e3bb.png)
    -**タブビュー**：CVM画面で、画面の右上隅にある**その他**>**インスタンス設定**>**ロールのバインド/変更**を選択します。
3. ポップアップした「ロールのバインド/変更」ウィンドウで、バインドするロールを選択して、**OK**をクリックすれば完了です。

:::
::: 複数インスタンスロールのバインド/変更

1. 「インスタンス」リスト画面で、ロールをバインドまたは変更する必要があるCVMにチェックを入れ、トップにある**その他の操作**>**インスタンス設定**>**ロールのバインド/変更**をクリックします。下図のとおりです。
![](https://main.qcloudimg.com/raw/4093443ee4f5b484860f8c8eae3b3b3e.png)
2. ポップアップした「ロールのバインド/変更」ウィンドウで、バインドするロールを選択して、**OK**をクリックすれば完了です。
<dx-alert infotype="explain" title="">
この方法で変更された複数のインスタンスでは、ロールが同じになります。
</dx-alert>


:::
</dx-tabs>


### インスタンスロールの削除
<dx-tabs>
::: 単一インスタンスロールの削除
1. [CVMコンソール](https://console.cloud.tencent.com/cvm)にログインし、左側のナビゲーションバーで**インスタンス**を選択します。
2. インスタンスの管理画面で、実際に使用されているビューモードに従って操作します。
   -**リストビュー**：ロールを削除する必要があるCVMの行の右側にある**その他**>**インスタンス設定**>**ロールの削除**を選択します。下図のとおりです。
   ![](https://main.qcloudimg.com/raw/8b44772763ab60fa69c404360db1ebbf.png)
   -**タブビュー**：CVM画面で、画面の右上隅にある**その他の操作**>**インスタンス設定**>**ロールの削除**を選択します。
2. ポップアップした「ロールの削除」ウィンドウで、**OK**をクリックすれば完了です。

:::
::: 複数インスタンスロールの削除
1. 「インスタンス」リスト画面で、ロールを削除する必要があるCVMにチェックを入れ、トップにある**その他の操作**>**インスタンス設定** > **ロールの削除**をクリックします。下図のとおりです。
![](https://main.qcloudimg.com/raw/72669a0d3bbdde1491c24b5acc0eadbf.png)
3. ポップアップした「ロールの削除」ウィンドウで、**OK**をクリックすれば完了です。
:::
</dx-tabs>

