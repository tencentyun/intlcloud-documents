### COSにはプライベートネットワークドメイン名はありますか。

Cloud Object Storage (COS)のデフォルトのオリジンサーバードメイン名の形式は、&lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.comです。デフォルトでパブリックネットワークアクセスおよび同一リージョン内のプライベートネットワークアクセスをサポートしています。プライベートネットワーク環境でこのドメイン名を使用してCOSにアクセスするとき、COSはインテリジェントにプライベートIPに解決します。その際に発生するトラフィックはすべてプライベートネットワークトラフィックであり、トラフィック料金はかかりません。
例えば、examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com。ドメイン名の詳細については、[リージョンとアクセスドメイン名](https://intl.cloud.tencent.com/document/product/436/6224)をご参照ください。



