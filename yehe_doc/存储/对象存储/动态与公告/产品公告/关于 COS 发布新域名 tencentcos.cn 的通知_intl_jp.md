2022年3月15日、Cloud Object Storage（COS）は新ドメイン名tencentcos.cnを正式にリリースします。旧ドメイン名のmyqcloud.comも引き続きご利用いただけますが、今後COSに追加される特性および機能はサポートされません。新しいドメイン名では安全性と安定性が向上していますので、新ドメイン名tencentcos.cnを優先的に使用することをお勧めします。


>! 旧ドメイン名myqcloud.comは引き続き使用でき、旧ドメイン名の既存の特性（プライベートネットワークとパブリックネットワークのインテリジェント解決など）は影響を受けませんが、今後追加される新たな特性はサポートされません。
>

新ドメイン名tencentcos.cnの主な変更点は次のとおりです。

**1. 拡張子tencentcos.cnの統一使用**

デフォルトのバケットドメイン名を例にとると、次のようになります。

- 旧ドメイン名の形式：&lt;BucketName-APPID&gt;.cos.&lt;Region&gt;.myqcloud.com
- 新ドメイン名の形式：&lt;BucketName-APPID&gt;.cos.&lt;Region&gt;.tencentcos.cn

**2. プライベートネットワークドメイン名とパブリックネットワークドメイン名の区別**

旧ドメイン名ではプライベートネットワークドメイン名とパブリックネットワークドメイン名を区別していませんでした。デフォルトのバケットドメイン名を例にとると、ドメイン名の形式は、&lt;BucketName-APPID&gt;.cos.&lt;Region&gt;.myqcloud.comを統一使用していました。

新ドメイン名ではプライベートネットワークドメイン名とパブリックネットワークドメイン名を区別します。デフォルトのバケットドメイン名を例にとると、ドメイン名の形式は次のようになります。

- 新ドメイン名のパブリックネットワークドメイン名：&lt;BucketName-APPID&gt;.cos.&lt;Region&gt;.tencentcos.cn
- 新ドメイン名のプライベートネットワークドメイン名：&lt;BucketName-APPID&gt;.cos-internal.&lt;Region&gt;.tencentcos.cn


新旧ドメイン名の比較は次のとおりです。

| ドメイン名タイプ   | 旧ドメイン名                    | 新ドメイン名                |
| -------------- | ---------------------------------- | ---------------- |
| デフォルトバケットドメイン名 | &lt;BucketName-APPID&gt;.cos.&lt;Region&gt;.myqcloud.com。プライベートネットワークドメイン名とパブリックネットワークドメイン名の区別はありません。 | <ul  style="margin: 0;"><li>パブリックネットワークドメイン名：&lt;BucketName-APPID&gt;.cos.&lt;Region&gt;.tencentcos.cn </li><li>プライベートネットワークドメイン名：&lt;BucketName-APPID&gt;.cos-internal.&lt;Region&gt;.tencentcos.cn  </li></ul>     |   
| グローバルアクセラレーションドメイン名 | &lt;BucketName-APPID&gt;.cos.accelerate.myqcloud.com。プライベートネットワークドメイン名とパブリックネットワークドメイン名の区別はありません。   |  <ul  style="margin: 0;"><li>パブリックネットワークドメイン名：&lt;BucketName-APPID&gt;.cos.accelerate.tencentcos.cn </li><li>プライベートネットワークドメイン名：&lt;BucketName-APPID&gt;.cos-internal.accelerate.tencentcos.cn </li></ul>              |   
| 静的ウェブサイトドメイン名 |&lt;BucketName-APPID&gt;.cos-website.&lt;Region&gt;.myqcloud.com。プライベートネットワークドメイン名とパブリックネットワークドメイン名の区別はありません。 | <ul  style="margin: 0;"><li>パブリックネットワークドメイン名：&lt;BucketName-APPID&gt;.cos-website.&lt;Region&gt;.tencentcos.cn </li><li>プライベートネットワークドメイン名：&lt;BucketName-APPID&gt;.cos-website-internal.&lt;Region&gt;.tencentcos.cn</li></ul> |       


