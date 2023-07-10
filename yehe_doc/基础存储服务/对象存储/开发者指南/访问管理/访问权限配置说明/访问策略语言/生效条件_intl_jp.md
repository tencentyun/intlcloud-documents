## 概要

発効条件とはアクセスポリシー言語の一部であり、完全な発効条件には次の要素が含まれます。
- 条件キー：発効条件の具体的な種類を表します。例えば、ユーザーのアクセス元のIP、権限承認時間などです。
- 条件オペレーター：発効条件の判断方法を表します。
- 条件値：条件キーの値です。

詳細については[CAM発効条件](https://www.tencentcloud.com/document/product/598/10608)をご参照ください。

>? 
>- 条件キーを使用してポリシーを作成する際は、必ず最小権限の原則を遵守し、適用可能なリクエスト（action）にのみ該当する条件キーを追加してください。アクション（action）を指定する際にワイルドカード「\*」を使用すると、リクエストが失敗しますので避けてください。
>- Cloud Access Management（CAM）コンソールを使用してポリシーを作成する際は、構文形式にご注意ください。version、principal、statement、effect、action、resource、conditionの構文要素はアルファベットの先頭の文字を大文字にするか、またはすべて小文字にする必要があります。


## 発効条件の例

次のバケットポリシーの例における発効条件（condition）は、ユーザーが10.217.182.3/24または111.21.33.72/24ネットワークセグメントに属している場合にのみ、`cos:PutObject`アクションの権限付与が完了することを表します。このうち、
- **条件キー**は`qcs:ip`であり、発効条件の種類がIPであることを表します。
- **条件オペレーター**は`ip_equal`であり、発効条件の判断方法がIPアドレスの同一性であることを表します。
- **条件値は**配列`["10.217.182.3/24","111.21.33.72/24"]`であり、発効条件判断の規定値を表します。ユーザーが配列の中の任意のIPがあるネットワークセグメントに属している場合、条件判断はすべてtrueとなります。

```
{
    "version":"2.0",
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/1250000000:uin/1250000001"
                ]
            },
            "effect":"allow",
            "action":[
                "name/cos:PutObject"
            ],
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ],
            "condition":{
                "ip_equal":{
                    "qcs:ip":[
                        "10.217.182.3/24",
                        "111.21.33.72/24"
                    ]
                }
            }
        }
    ]
}
```

## COSのサポートする条件キー


>? 条件キー`tls-version`は現在北京リージョンでのみサポートしています。その他のリージョンでも順次サポート予定です。
>


Cloud Object Storage（COS）のサポートする条件キーには2種類あり、1つはIP、VPC、HTTPSを含むすべてのリクエストに適用可能なもので、もう1つはリクエストヘッダーおよびリクエストパラメータによる条件キーであり、一般的にこのリクエストヘッダーまたはリクエストパラメータを持つリクエストにのみ適用できます。これらの条件キーに関する説明および実際の使用例については、[条件キーの説明およびユースケース](https://intl.cloud.tencent.com/document/product/436/46206)のドキュメントをご参照ください。

>? 発効条件、条件キーなどの概念はすべてユーザーリクエストを対象としてCAMが実行するものです。ライフサイクル、バケットコピールールが有効になっている場合の削除、コピーなどの動作はCOSが行うものであり、ユーザーによるリクエストではないため、条件キーがライフサイクル、バケットコピールールに対して起こす動作は無効となります。
>

### すべてのリクエストに適用可能な条件キー

1種類目はすべてのリクエストに適用可能な条件キーです。`qcs:ip`、`qcs:vpc`および`cos:secure-transport`が含まれ、それぞれ、リクエスト元のIPネットワークセグメント、VPC ID、HTTPSプロトコルを使用しているかどうかを表します。すべてのリクエストが使用できます。

| 条件キー |適用リクエスト |意味 |タイプ|
|:----------|:----------|:----------|:----------|
|[cos:secure-transport](https://intl.cloud.tencent.com/document/product/436/46206#secure-transport) |すべてのリクエスト |リクエストにHTTPSプロトコルが適用されているかどうか確認 |  Boolean  |
|[qcs:ip](https://intl.cloud.tencent.com/document/product/436/46206#RestrictUserAccessIP) |すべてのリクエスト |リクエスト元のIPネットワークセグメント|  IP|
|[qcs:vpc](https://intl.cloud.tencent.com/document/product/436/46206#requester_vpc) |すべてのリクエスト |リクエスト元のVPC ID  | String  |
|[cos:tls-version](https://intl.cloud.tencent.com/document/product/436/46206#tls-version) |すべてのhttpsリクエスト|httpsリクエストに使用しているTLSバージョン |Numeric|


### リクエストヘッダーおよびリクエストパラメータによる条件キー

2種類目は、リクエストヘッダー（Header）およびリクエストパラメータ（Param）による条件キーです。リクエストごとにリクエストヘッダーおよびリクエストパラメータが異なるため、これらの条件キーは一般的にこの種類のヘッダーまたはリクエストパラメータが含まれるリクエストにのみ適します。

例えば、条件キー`cos:content-type`は、リクエストヘッダー`Content-Type`を使用する必要があるアップロードクラスのリクエスト（PutObjectなど）に適用できます。条件キー`cos:response-content-type`はGetObjectオブジェクトにのみ適用できます。このリクエストのみがリクエストパラメータ`response-content-type`をサポートしているためです。

COSが現在サポートしている、リクエストヘッダーおよびリクエストパラメータによる条件キーと、それらの条件キーが適用可能なリクエストは下表のとおりです。


|条件キー   |適用リクエスト | リクエストヘッダー/リクエストパラメータの確認 |タイプ|
|:----------|:----------|:----------|:----------|
|[cos:x-cos-storage-class](https://intl.cloud.tencent.com/document/product/436/46206#x-cos-storage-class) |PutObject<br>PostObject<br>InitiateMultipartUpload<br>AppendObject |リクエストヘッダー：x-cos-storage-class |String|
|[cos:versionid](https://intl.cloud.tencent.com/document/product/436/46206#versionid) |GetObject<br>DeleteObject<br>PostObjectRestore<br>PutObjectTagging<br>GetObjectTagging<br>DeleteObjectTagging<br>HeadObject |リクエストパラメータ：versionid |String|
|[cos:prefix](https://intl.cloud.tencent.com/document/product/436/46206#prefix) |GetBucket（List Objects）<br>GET Bucket Object versions<br>List Multipart Uploads<br>ListLiveChannels |リクエストパラメータ：prefix |String|
|[cos:x-cos-acl](https://intl.cloud.tencent.com/document/product/436/46206#x-cos-acl) |PutObject<br>PostObject<br>PutObjectACL<br>PutBucket<br>PutBucketACL<br>AppendObject<br>Initiate Multipart Upload |リクエストヘッダー：x-cos-acl |String|
|[cos:content-length](https://intl.cloud.tencent.com/document/product/436/46206#content-length) |このリクエストは適用範囲が広いため、リクエストボディ付きのリクエストなどの代表的なリクエストに注目 |リクエストヘッダー：Content-Length |Numeric|
|[cos:content-type](https://intl.cloud.tencent.com/document/product/436/46206#content-type) |このリクエストは適用範囲が広いため、リクエストボディ付きのリクエストなどの代表的なリクエストに注目 |リクエストヘッダー：Content-Type |String|
|[cos:response-content-type](https://intl.cloud.tencent.com/document/product/436/46206#response-content-type) |GetObject |リクエストパラメータ：response-content-type |String|
|[qcs:request_tag](https://intl.cloud.tencent.com/document/product/436/46206#request_tag) |PutBucket<br>PutBucketTagging |リクエストヘッダー：x-cos-tagging<br>リクエストパラメータ：tagging|String|



## 条件オペレーター

COSの条件キーは次の条件オペレーターをサポートしており、文字列（String）、数値型（Numeric）、ブール型（Boolean）およびIPなどの様々なタイプの条件キーに適用できます。

|条件オペレーター |意味 |タイプ |
|:----------|:----------|:----------|
|string_equal |文字列一致（大文字と小文字を区別） |String |
|string_not_equal |文字列不一致（大文字と小文字を区別） |String |
|string_like |文字列が類似（大文字と小文字を区別）。現在は文字列の前後へのワイルドカード`*`の追加をサポートしています（例：`image/*`） |String |
|ip_equal |IP一致 |IP |
|ip_not_equal |IP不一致 |IP |
|numeric_equal |数値一致 |Numeric |
|numeric_not_equal |数値不一致 |Numeric |
|numeric_greater_than |数値が大きい |Numeric |
|numeric_greater_than_equal |数値が同じか大きい |Numeric |
|numeric_less_than |数値が小さい |Numeric |
|numeric_less_than_equal |数値が同じか小さい |Numeric |

### _if_existの意味

上記のすべての条件オペレーターは、その後に`_if_exist`を追加することで単一条件オペレーターとすることができます。例えば、`string_equal_if_exist`などです。条件オペレーターに`_if_exist`が含まれるかどうかで異なる点は、リクエストに、条件キーに対応するリクエストヘッダーまたはリクエストパラメータが含まれない場合にどのように処理されるかの違いです。

- 条件オペレーターに`_if_exist`が含まれない場合、例えば`string_equal`の場合は、リクエストに対応するリクエストヘッダー/リクエストパラメータが含まれないとき、デフォルトで条件にヒットし、`False`となります。
- 条件オペレーターに`_if_exist`が含まれる場合、例えば`string_equal_if_exist`の場合は、リクエストに対応するリクエストヘッダー/リクエストパラメータが含まれないとき、デフォルトで条件にヒットし、`True`となります。

## 事例


### 事例1：指定されたオブジェクトバージョンのダウンロードを許可

例えば、次のバケットポリシーについて、エフェクトがallowの場合は、リクエストパラメータversionidによる“MTg0NDUxNTc1NjIzMTQ1MDAwODg”のGetObjectリクエストの承認が許可されることを表します。条件にヒットした場合（True）、allowの権限付与ポリシーに基づいてリクエストは承認されます。条件にヒットしなかった場合（False）、allowの権限付与ポリシーに基づいて、リクエストは権限を得られず、リクエストは失敗します。

```
{
    "version":"2.0",
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/1250000000:uin/1250000001"
                ]
            },
            "effect":"allow",
            "action":[
                "name/cos:GetObject"
            ],
            "condition":{
                "string_equal":{
                    "cos:versionid":"MTg0NDUxNTc1NjIzMTQ1MDAwODg"
                }
            },
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ]
        }
    ]
}
```

条件オペレーターが`string_equal`または`string_equal_if_exist`の場合、conditionのヒット状況およびリクエストが承認されるかどうかは下表のとおりとなります。

|条件オペレーター  |リクエスト |conditionにヒットするか |リクエストが承認されるか |
|:----------|:----------|:----------|:----------|
|string_equal |versionidなし |FALSE |不承認 |
|string_equal_if_exist |versionidなし |TRUE |承認 |
|string_equal |versionid付き、指定のもの |TRUE |承認 |
|string_equal_if_exist |versionid付き、指定のもの |TRUE |承認 |
|string_equal |versionid付き、指定のもの以外 |FALSE |不承認 |
|string_equal_if_exist |versionid付き、指定のもの以外 |FALSE |不承認 |

### 事例2：指定されたオブジェクトバージョンのダウンロードを拒否

次のバケットポリシーの例では、エフェクトがdenyであり、リクエストパラメータversionidによる「MTg0NDUxNTc1NjIzMTQ1MDAwODg」のGetObjectリクエストが拒否されることを表します。条件にヒットした場合（True）、denyの権限付与ポリシーに基づいてリクエストは失敗します。条件にヒットしなかった場合（False）、denyの権限付与ポリシーに基づいて、リクエストは拒否されません。

```
{
    "version":"2.0",
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/1250000000:uin/1250000001"
                ]
            },
            "effect":"deny",
            "action":[
                "name/cos:GetObject"
            ],
            "condition":{
                "string_equal":{
                    "cos:versionid":"MTg0NDUxNTc1NjIzMTQ1MDAwODg"
                }
            },
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ]
        }
    ]
}
```

条件オペレーターが`string_equal`または`string_equal_if_exist`の場合、conditionのヒット状況およびリクエストが拒否されるかどうかは下表のとおりとなります。

| 条件オペレーター |リクエスト |conditionにヒットするか |リクエストが拒否される/拒否されない |
|:----------|:----------|:----------|:----------|
|string_equal |versionidなし |FALSE |拒否されない |
|string_equal_if_exist |versionidなし |TRUE |拒否される |
|string_equal |versionid付き、指定のもの |TRUE |拒否される |
|string_equal_if_exist |versionid付き、指定のもの |TRUE |拒否される |
|string_equal |versionid付き、指定のもの以外 |FALSE |拒否されない |
|string_equal_if_exist |versionid付き、指定のもの以外 |FALSE |拒否されない |


## 関連説明

### 特殊文字はurlencodeでの処理が必要

リクエストパラメータ内の特殊文字はurlencodeでの処理が必要です。このため、バケットポリシーの中で、リクエストパラメータによる条件キーを使用する場合は、先にurlencode処理をしておく必要があります。例えば、`cos:response-content-type`条件キーを使用する際、条件値が"image/jpeg"であれば、必ずurlencodeで"image%2Fjpeg"に変換してからバケットポリシーに入力する必要があります。

### 最小権限の原則に従い、\*の使用を避ける

条件キーを使用する際は最小権限の原則に従い、権限の設定が必要なactionのみを追加し、ワイルドカード「\*」の使用は避けてください。ワイルドカード「\*」を乱用すると、一部のリクエストが失敗する場合があります。例えば次の例のように、GetObject以外の他のリクエストはいずれもリクエストパラメータresponse-content-typeの使用をサポートしていません。

deny + string_equal_if_exist条件オペレーターはリクエスト内にこの条件キーがない場合、デフォルトでtrueとして処理します。このため、PutObject、PutBucketなどのリクエストを発行した際に、このdeny statementにヒットし、リクエストが拒否されます。

allow + string_equalはリクエストにこの条件キーがない場合、デフォルトでfalseとして処理します。このため、PutObject、PutBucketなどのリクエストを発行した際に、このallow statementにヒットすることができず、リクエストが許可されません。

```
{
    "version":"2.0",
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/1250000000:uin/1250000001"
                ]
            },
            "effect":"allow",
            "action":[
                "*"
            ],
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ],
            "condition":{
                "string_equal":{
                    "cos:response-content-type":"image%2Fjpeg"
                }
            }
        },
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/1250000000:uin/1250000001"
                ]
            },
            "effect":"deny",
            "action":[
                "*"
            ],
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ],
            "condition":{
                "string_not_equal_if_exist":{
                    "cos:response-content-type":"image%2Fjpeg"
                }
            }
        }
    ]
}
```

別の方法として、allow+string_equal_if_existおよびdeny + string_not_equalを使用すると、response-content-typeリクエストパラメータを含まないリクエストが許可されます。

deny + string_equal条件オペレーターはリクエスト内にこの条件キーがない場合、デフォルトでfalseとして処理します。このため、PutObject、PutBucketなどのリクエストを発行した際に、このdeny statementにヒットせず、リクエストは拒否されません。

allow + string_equal_if_existはリクエスト内にこの条件キーがない場合、デフォルトでtrueとして処理します。このため、PutObject、PutBucketなどのリクエストを発行した際に、allow statementにヒットすることができ、リクエストは権限を取得します。

ただし、このように条件オペレーターを使用すると、GetObjectにresponse-content-typeを含めるかどうかの制限が行えなくなります。GetObjectにresponse-content-typeリクエストパラメータが含まれない場合は、他のリクエストと同様にデフォルトで許可されます。GetObjectにresponse-content-typeリクエストパラメータが含まれる場合のみ、ご自身で定めた条件に従って、リクエストパラメータの内容が意図するものと一致しているかを確認することができ、それによって条件付きの権限付与を実現できます。

```
{
    "version":"2.0",
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/1250000000:uin/1250000001"
                ]
            },
            "effect":"allow",
            "action":[
                "*"
            ],
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ],
            "condition":{
                "string_equal_if_exist":{
                    "cos:response-content-type":"image%2Fjpeg"
                }
            }
        },
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/1250000000:uin/1250000001"
                ]
            },
            "effect":"deny",
            "action":[
                "*"
            ],
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ],
            "condition":{
                "string_not_equal":{
                    "cos:response-content-type":"image%2Fjpeg"
                }
            }
        }
    ]
}
```


このため、より安全な方法は、最小権限の原則に従い、ワイルドカード「\*」を使用せず、actionをGetObjectに限定することとなります。

次の例では、ポリシーの発効条件は、「GetObjectリクエストに必ずresponse-content-typeが含まれ、かつリクエストパラメータの値が必ずimage%2Fjpeg"である場合にのみ権限を得られる」と厳格に限定されています。

その他のリクエストは次の例におけるポリシーの影響を受けないため、最小権限の原則に従って、追加で単独の権限を付与することができます。

```
{
    "version":"2.0",
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/1250000000:uin/1250000001"
                ]
            },
            "effect":"allow",
            "action":[
                "name/cos:GetObject"
            ],
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ],
            "condition":{
                "string_equal":{
                    "cos:response-content-type":"image%2Fjpeg"
                }
            }
        },
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/1250000000:uin/1250000001"
                ]
            },
            "effect":"deny",
            "action":[
                "name/cos:GetObject"
            ],
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ],
            "condition":{
                "string_not_equal_if_exist":{
                    "cos:response-content-type":"image%2Fjpeg"
                }
            }
        }
    ]
}
```


