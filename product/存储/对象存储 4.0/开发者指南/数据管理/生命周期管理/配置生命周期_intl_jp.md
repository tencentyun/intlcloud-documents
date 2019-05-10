## 適用シナリオ

ライフサイクルの設定により、ルールに適合するオブジェクトが指定条件で一部の操作を自動的に実行できるようになります。例えば：

- ストレージタイプの変換：作成したオブジェクトを指定時間後に低頻度ストレージタイプSTANDARD_IAまたはCASタイプARCHIVEに変換します。
- 期限切れ時の削除：オブジェクトが期限切れになると自動的に削除されるように、オブジェクトの有効期限を設定します。

ライフサイクル機能の[基本的説明ドキュメント](/document/product/436/17028)を参照してください。設定の際に、[構成要素](/document/product/436/17029)を指定する必要があります。

## 使用方法
### COSコンソールの使用
COSコンソールによるライフサイクルの設定に関して、[ライフサイクルの管理](https://cloud.tencent.com/document/product/436/14605) コンソールガイドのドキュメントを参照してください。

### REST APIの使用

REST APIを直接使用し、バケットにおけるObjectのライフサイクルを構成し、管理できます。下記APIドキュメントを参照してください：

- [PUT Bucket lifecycle](https://cloud.tencent.com/document/product/436/8280)
- [GET Buket lifecycle](https://cloud.tencent.com/document/product/436/8278)
- [DELETE Bucket lifecycle](https://cloud.tencent.com/document/product/436/8284)

### C++ SDKの使用

COSのC++ SDKにおいてこの方法を提供しています。C++ SDK APIキュメント[ PUT Bucket lifecycleの部分](https://cloud.tencent.com/document/product/436/12302#put-bucket-lifecycle)を参照してください。

手順の説明：

1. クライアントcosClientを初期化します。
2. putBucketLifecycleとGetBucketLifecycleを実行し、バケットのライフサイクルと検索ライフサイクルをそれぞれ設定します。

#### ライフサイクルの設定

コード例：

```
cloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-12345";

// PutBucketLifecycleReqの構造関数にbucket_nameを入力する必要があります
qcloud_cos::PutBucketLifecycleReq req(bucket_name);
qcloud_cos::PutBucketLifecycleResp resp;

// ルールの設定
{
    qcloud_cos::LifecycleRule rule;
    rule.SetIsEnable(true);
    rule.SetId("lifecycle_rule00");

    // Filterを設定します。タグキーdatalevelと値backupのタグ付きのオブジェクトに対して発効します
    qcloud_cos::LifecycleFilter filter;
    Lifecycle tag;
    tag.key = "datalevel";
    tag.value = "backup";
    filter.AddTag(tag);
    rule.SetFilter(filter);

    // オブジェクト作成の30日後にSTANDARD_IAに変換します
    qcloud_cos::LifecycleTransition transition1;
    transition1.SetDays(30);
    transition1.SetStorageClass("STANDARD_IA");
    rule.AddTransition(transition1);

    // オブジェクト作成の365日後にARCHIVEストレージタイプに変換します
    qcloud_cos::LifecycleTransition transition2;
    transition2.SetDays(365);
    transition2.SetStorageClass("ARCHIVE");
    rule.AddTransition(transition2);

    req.AddRule(rule);
}

qcloud_cos::CosResult result = cos.PutBucketLifecycle(req, &resp);
//呼び出しに成功した場合、respのメンバー関数を呼び出してレスポンス内容を取得します
if (result.IsSucc()) {
    // ...
} else {
    // ライフサイクルの設定に失敗した場合、CosResultのメンバー関数を呼び出してrequestID等のエラーメッセージを出力できます
}
```

#### ライフサイクルの検索
コード例：

```
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-12345";

//GetBucketLifecycleReqの構造関数にbucket_nameを渡す必要があります
qcloud_cos::GetBucketLifecycleReq req(bucket_name);
qcloud_cos::GetBucketLifecycleResp resp;
qcloud_cos::CosResult result = cos.GetBucketLifecycle(req, &resp);

//呼び出しに成功した場合、respのメンバー関数を呼び出してレスポンス内容を取得します
if (result.IsSucc()) {
    // ...
} else {
    // ライフサイクル構成の取得に失敗した場合、CosResultのメンバー関数を呼び出してrequestID等のエラーメッセージを出力できます
}
```

### Python SDKの使用
COSのPython SDKにおいてこの方法を提供しています。Python SDK APIドキュメント[バケットライフサイクル構成の部分](https://cloud.tencent.com/document/product/436/12270#.E8.AE.BE.E7.BD.AE-bucket-.E7.94.9F.E5.91.BD.E5.91.A8.E6.9C.9F.E9.85.8D.E7.BD.AE)を参照してください。
#### ライフサイクルの設定
手順の説明：

1. CosConfig類で構成し、クライアントCosS3Clientを初期化します。
2. put_bucket_lifecycle()方法を実行してバケットにおけるライフサイクル構成を設定します。

ライフサイクルを設定するためのコード例を下記に示します：

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client

secret_id = 'xxxxxxxx'      # ユーザーのsecretIdに置き換え
secret_key = 'xxxxxxx'      # ユーザーのsecretKeyに置き換え
region = 'ap-beijing-1'     # ユーザーのRegionに置き換える
token = ''                 # 一時暗号鍵を使用する場合、Tokenに渡す必要があります。デフォルトはブランクですから、入力しなくてもいいです。

config = CosConfig(Access_id=secret_id, Access_key=secret_key, Region=region, Token=token)
client = CosS3Client(config)

bucket = 'testbucket-123456789'
lifecycle_config = {
    'Rule': [
        {
            'Status': 'Enabled',
            'Filter': {
                # タグキーdatalevelと値backupのタグ付きのオブジェクトに対して発効します
                'Tag': [
                    {
                        'Key': 'datalevel',
                        'Value': 'backup'
                    }
                ]
            },
            'Transition': [
                {
                    # 30日後にStandard_IAに変換します
                    'Days': 30,
                    'StorageClass': 'Standard_IA'
                },
                {
                    # 365日後にArchiveに変換
                    'Days': 365,
                    'StorageClass': 'Archive'
                }
            ],
            'Expiration': {
                # 3650日後に期限切れになって削除されます
                'Days': 3650
            }
        }
    ]
}

response = client.put_bucket_lifecycle(
    Bucket=bucket,
    LifecycleConfiguration=lifecycle_config
)
```

#### ライフサイクルの取得
手順の説明：

1. CosConfigクラスにより構成され、クライアントCosS3Clientを初期化します。
2. get_bucket_lifecycle()方法を実行してバケットにおけるライフサイクル構成を取得します

ライフサイクル構成を取得するためのコードを下記に示します：

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client

secret_id = 'xxxxxxxx'     # ユーザーのsecretIdに置き換える
secret_key = 'xxxxxxx'     # ユーザーのsecretKeyに置き換えます
region = 'ap-beijing-1'    # ユーザーのRegionに置き換える
token = ''                 # 一時暗号鍵を使用する場合、Tokenに渡す必要があります。デフォルトはブランクですから、入力しなくてもいいです。

config = CosConfig(Access_id=secret_id, Access_key=secret_key, Region=region, Token=token)
client = CosS3Client(config)

bucket = 'testbucket-123456789'
response = client.get_bucket_lifecycle(
    Bucket=bucket    
)
```

### PHP SDKの使用
COSのPHP SDKにおいてこの方法を提供しています。PHP SDK APIドキュメント[PUT Bucket lifecycle](https://cloud.tencent.com/document/product/436/12267#putbucketlifecycle)を参照してください。

#### ライフサイクルの設定
手順の説明：

1. クライアントcosClientを初期化します。
2. putBucketLifecycle()を実行してバケットのライフサイクルを設定します。

下記コードはバケットのライフサイクルを設定する手順を示しています：

```php
## putBucketLifecycle(bucketライフサイクルの設定)
$cosClient = new Qcloud\Cos\Client(array('region' => getenv('COS_REGION'),
    'credentials'=> array(
        'secretId'    => getenv('COS_KEY'),
        'secretKey' => getenv('COS_SECRET'))));

//バケットの命名規則は{name}-{appid}です。ここで入力するバケット名はこのフォーマットでなければなりません。
$bucket = 'lewzylu02-1252448703';

try {
    $result = $cosClient->putBucketLifecycle(array(
        'Bucket' => $bucket,
        'Rules' => array(
            array(
                'Status' => 'Enabled',
                'Filter' => array(
                    'Tag' => array(
                        'Key' => 'datalevel',
                        'Value' => 'backup'
                    )
                ),
                'Transitions' => array(
                   array(
                    # 30日後にStandard_IAに変換します
                    'Days' => 30,
                    'StorageClass' => 'Standard_IA'),
                array(
                    # 365日後にArchiveに変換
                    'Days' => 365,
                    'StorageClass' => 'Archive')
                ),
                'Expiration' => array(
                # 3650日後に期限切れになって削除されます
                'Days' => 3650,
                )
            )
        )
    ));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```

#### ライフサイクルの取得
手順の説明：

1. クライアントcosClientを初期化します。
2. getBucketLifecycleを実行してバケットのライフサイクル情報を取得します。

下記コードはバケットのライフサイクルを取得する手順を示しています：

```php
## getBucketLifecycle(bucketのライフサイクルの取得)
$cosClient = new Qcloud\Cos\Client(array('region' => getenv('COS_REGION'),
    'credentials'=> array(
        'secretId'    => getenv('COS_KEY'),
        'secretKey' => getenv('COS_SECRET'))));

//バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名はこのフォーマットでなければなりません
$bucket = 'lewzylu02-1252448703';

try {
    $result = $cosClient->getBucketLifecycle(array(
        'Bucket' =>$bucket,
    ));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```

#### ライフサイクルの削除
手順の説明：

1. クライアントcosClientを初期化します。
2. deleteBucketLifecycleを実行してバケットのライフサイクルを削除します。

下記コードはバケットのライフサイクルを削除する手順を示しています：

```php
## deleteBucketLifecycle(bucketのライフサイクルの削除)
$cosClient = new Qcloud\Cos\Client(array('region' => getenv('COS_REGION'),
    'credentials'=> array(
        'secretId'    => getenv('COS_KEY'),
        'secretKey' => getenv('COS_SECRET'))));

//バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名はこのフォーマットでなければなりません
$bucket = 'lewzylu02-1252448703';

try {
    $result = $cosClient->deleteBucketLifecycle(array(
        'Bucket' =>$bucket,
    ));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```
