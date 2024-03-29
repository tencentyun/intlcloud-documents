## 概要

COSコンソールからバケットのグローバルアクセラレーション機能を有効化することによって、世界各地のユーザーがバケットにスピーディーにアクセスしやすくなり、ビジネスのアクセス成功率とビジネスの安定性を引き上げることができます。グローバルアクセラレーション機能は、アップロードとダウンロードを高速化することができます。詳細については、[グローバルアクセラレーションの概要](https://intl.cloud.tencent.com/document/product/436/33409)をご参照ください。

## 操作手順

1. [COSコンソール](https://console.cloud.tencent.com/cos5)にログインし、左側メニューバーの【バケットリスト】をクリックし、グローバルアクセラレーション機能を設定する必要があるバケットを選択してクリックし、バケットの詳細インターフェースに進みます。
2. 左側の【ドメイン名と伝送管理】>【グローバルアクセラレーション】をクリックし、【グローバルアクセラレーション】の管理項目を見つけ、【編集】をクリックして現在のステータスをオンにします。
![](https://main.qcloudimg.com/raw/e26fe8fd79c9bbc0d0ad1f9fe9088169.png)
3. 間違いのないことを確認してから「保存」をクリックすると、バケットのグローバルアクセラレーション機能を有効化できます。
![](https://main.qcloudimg.com/raw/1c6a7197c77a1555a91ad83fd29c8264.png)
4. グローバルアクセラレーション機能を有効化すると、グローバルアクセラレーションのドメイン名でバケットにアクセスするだけで、データにすばやくアクセスできるようになります。グローバルアクセラレーションドメイン名の形式としては、`<BucketName-APPID>.cos.accelerate.myqcloud.com`などがあります。
>?グローバルアクセラレーション機能を有効化しても、元のバケットのデフォルトドメイン名に影響を与えることなく、通常どおり使用することができます。
