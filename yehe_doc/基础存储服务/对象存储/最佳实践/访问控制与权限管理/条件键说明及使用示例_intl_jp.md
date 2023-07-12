アクセスポリシーを使用して権限承認を行う場合、ポリシーの[発効条件](https://intl.cloud.tencent.com/document/product/436/18023)を指定することができます。例えば、ユーザーのアクセス元、アップロードファイルのストレージタイプなどの制限があります。

ここでは、バケットポリシーにおけるCloud Object Storage（COS）条件キー使用の一般的な例について記載します。[発効条件](https://intl.cloud.tencent.com/document/product/436/46205)のドキュメント内で、COSがサポートするすべての条件キーおよび適用可能なリクエストを確認することができます。

>? 
>- 条件キーを使用してポリシーを作成する際は、必ず最小権限の原則を遵守し、適用可能なリクエスト（action）のみに該当する条件キーを追加してください。アクション（action）を指定する際にワイルドカード「\*」を使用すると、リクエストが失敗しますので避けてください。条件キーに関する説明は、[発効条件](https://intl.cloud.tencent.com/document/product/436/46205)のドキュメントをご参照ください。
>- Cloud Access Management（CAM）コンソールを使用してポリシーを作成する際は、構文形式にご注意ください。version、principal、statement、effect、action、resource、conditionの構文要素はアルファベットの先頭の文字を大文字にするか、またはすべて小文字にする必要があります。


## 条件キーの使用例

<span id="RestrictUserAccessIP"></span>
### ユーザーアクセスIPの制限（qcs:ip）

#### 条件キー qcs:ip

条件キー`qcs:ip`を使用してユーザーアクセスIPを制限します。すべてのリクエストに適用可能です。

#### 例：指定IPからのユーザーアクセスのみを許可

次のポリシーの記述例は、ルートアカウントID 100000000001（APPIDは1250000000）下のサブアカウントID 100000000002に対し、北京リージョンのバケットのexamplebucket-bjおよび広州リージョンのバケットのexamplebucket-gz下のオブジェクトexampleobjectについて、アクセスIPが`192.168.1.0/24`ネットワークセグメントにある場合およびIPが`101.226.100.185`または`101.226.100.186`である場合に、オブジェクトのアップロードおよびオブジェクトのダウンロード権限を許可するものです。

```
{
    "version": "2.0",
    "principal":{
        "qcs": [
            "qcs::cam::uin/100000000001:uin/100000000002"
        ]
    },
    "statement":[
        {
            "effect": "allow",
            "action":[
                "name/cos:PutObject",
                "name/cos:GetObject"
            ],
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-gz-1250000000/exampleobject"
            ],
            "condition":{
                "ip_equal":{
                    "qcs:ip":[
                        "192.168.1.0/24",
                        "101.226.100.185",
                        "101.226.100.186"
                    ]
                }
            }
        }
    ]
}
```

<span id="requester_vpc"></span>
### vpcidの制限（vpc:requester_vpc）

#### 条件キー vpc:requester_vpc

条件キー`vpc:requester_vpc`を使用してユーザーアクセスのvpcidを制限します。vpcidに関するその他の説明については、Tencent Cloud製品[VPC](https://www.tencentcloud.com/document/product/215)をご参照ください。

#### 例：vpcidをaqp5jrc1に制限

次のポリシーの記述例は、ルートアカウントID 100000000001（APPIDは1250000000）下のサブアカウントID 100000000002によるバケットexamplebucket-1250000000へのアクセスについて、vpcidがaqp5jrc1の場合にリクエストが権限を得ることを許可するものです。

```
{
  "statement":[
    {
      "action":[
        "name/cos:*"
      ],
      "condition":{
        "string_equal":{
          "vpc:requester_vpc": [
            "vpc-aqp5jrc1"
          ]
        }
      },
      "effect": "allow",
      "principal":{
        "qcs": [
          "qcs::cam::uin/100000000001:uin/100000000002"
        ]
      },
      "resource":[
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/*"
      ]
    }
  ],
  "version": "2.0"
}
```

<span id="versionid"></span>
### オブジェクトの最新バージョンまたは指定されたバージョンへのアクセスのみを許可（cos:versionid）

#### リクエストパラメータ versionid

リクエストパラメータ`versionid`はオブジェクトのバージョン番号を表します。バージョン管理に関する内容は、[バージョン管理の概要](https://intl.cloud.tencent.com/document/product/436/19883)をご参照ください。オブジェクトのダウンロード（GetObject）、オブジェクトの削除（DeleteObject）の際に、リクエストパラメータ`versionid`を使用して、アクションを行いたいオブジェクトのバージョンを指定することができます。

- `versionid`が含まれないリクエストパラメータの場合、リクエストはデフォルトでオブジェクトの最新バージョンに作用します。
- `versionid`リクエストパラメータを空の文字列にすると、`versionid`が含まれないリクエストパラメータの場合と同じになります。
- `versionid`リクエストパラメータが文字列`"null"`の場合、あるバケットにバージョン管理を有効にする前にオブジェクトをアップロードし、その後バージョン管理を有効にすると、それらのオブジェクトのバージョン番号はすべて文字列`"null"`となります。


#### 条件キー cos:versionid 

条件キー`cos:versionid`はリクエストパラメータ`versionid`の制限に用いられます。


#### 事例1：指定されたバージョン番号のオブジェクトの取得のみをユーザーに許可する

ルートアカウント（uin:100000000001）がバケットexamplebucket-1250000000を所有し、そのサブユーザー（uin:100000000002）に対し権限承認を行い、指定されたバージョン番号のオブジェクトの取得のみをサブユーザーに許可する必要があるとします。

次のバケットポリシーを採用した後、サブユーザー（uin:100000000002）がオブジェクトダウンロードリクエストを送信した場合、versionidパラメータが含まれ、なおかつversionidの値がバージョン番号「MTg0NDUxNTc1NjIzMTQ1MDAwODg」である場合にのみ、リクエストが成功します。

```
{
    "version":"2.0",
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
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

#### 明示的な拒否の追加

上記のポリシーを使用してサブユーザーへの権限承認を行う場合、サブユーザーが他の手段によって何の条件もない同一の権限を取得しているために、より広範囲の権限が発効する可能性があります。例えば、サブユーザーがあるユーザーグループに所属しており、ルートアカウントがユーザーグループにGetObject権限を与え、それに何の条件も付け加えなかった場合、上記のポリシーはバージョン番号に対する制限の役割を発揮しません。

このような状況に対応するため、上記のポリシーをベースにした上で、明示的な拒否のポリシー（deny）を追加することで、より厳格な権限制限を行うことができます。下記におけるこのdenyポリシーは、サブユーザーがオブジェクトダウンロードリクエストを送信する際に、 versionidパラメータを含めなかった場合、またはversionidのバージョン番号が「MTg0NDUxNTc1NjIzMTQ1MDAwODg」ではなかった場合に、そのリクエストは拒否されることを意味します。denyの優先順位は他のポリシーより高いため、明示的な拒否の追加によって、権限の脆弱性を最も高いレベルで回避することができます。

```
{
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
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
        },
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"deny",
            "action":[
                "name/cos:GetObject"
            ],
            "condition":{
                "string_not_equal_if_exist":{
                    "cos:versionid":"MTg0NDUxNTc1NjIzMTQ1MDAwODg"
                }
            },
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ]
        }
    ],
    "version":"2.0"
}
```

#### 事例2：最新バージョンのオブジェクトの取得のみをユーザーに許可する

ルートアカウント（uin:100000000001）がバケットexamplebucket-1250000000を所有し、そのサブユーザー（uin:100000000002）が最新バージョンのオブジェクトのみを取得できるように制限する必要があるとします。

リクエストパラメータ`versionid`が含まれない場合、または`versionid`が空の文字列の場合、GetObjectはデフォルトで最新バージョンのオブジェクトを取得します。このため、条件の中でstring_equal_if_exsitを使用することができます。
1. versionidが含まれない場合は、デフォルトでtrueとして処理し、allow条件にヒットすれば、リクエストはallowされます。
2. リクエストパラメータversionidが空、すなわち`“”`の場合も同様にallowポリシーにヒットし、最新バージョンのオブジェクト取得に対するリクエストのみ権限が承認されます。
```
	"condition":{
		"string_equal_if_exist":{
			"cos:versionid": ""
		}
	}
```
明示的な拒否を追加した、完全なバケットポリシーは次のようになります。
```
{
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"allow",
            "action":[
                "name/cos:GetObject"
            ],
            "condition":{
                "string_equal_if_exist":{
                    "cos:versionid":""
                }
            },
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ]
        },
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"deny",
            "action":[
                "name/cos:GetObject"
            ],
            "condition":{
                "string_not_equal":{
                    "cos:versionid":""
                }
            },
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ]
        }
    ],
    "version":"2.0"
}
```

#### 事例3：バージョン管理の有効化前にアップロードしたオブジェクトの削除をユーザーに許可しない

バージョン管理を有効化する前に、一部のオブジェクトがバケットにアップロードされている可能性があり、それらのオブジェクトのバージョン番号は“null”となります。これらのオブジェクトに対しては、場合によっては追加の保護を有効化する必要があります。例えば、ユーザーに対しこれらのオブジェクトの完全削除操作を禁止する、すなわちバージョン番号があるものの削除操作を拒否するなどです。

次に挙げるこのバケットポリシーの例には、2つのポリシーが含まれます。
1. DeleteObjectリクエストを使用してバケット内のオブジェクトを削除する権限をサブユーザーに承認します。
2. DeleteObjectリクエストの発効条件を制限しています。DeleteObjectリクエストにリクエストパラメータversionidが含まれ、なおかつversionidが「null」の場合は、このDeleteObjectリクエストを拒否します。

このため、バケットexamplebucket-1250000000に先にオブジェクトAをアップロードし、その後バケットのバージョン管理を有効化した場合、オブジェクトAのバージョン番号は文字列の「null」となります。

このバケットポリシーを追加すると、オブジェクトAは保護されます。サブユーザーがオブジェクトAに対しDeleteObjectリクエストを送信し、リクエストにバージョン番号が含まれていない場合、バージョン管理を有効化しているため、オブジェクトA自体は完全削除されず、削除マーカーだけが付与されます。リクエストにAのバージョン番号「null」が含まれていた場合、このリクエストは拒否され、オブジェクトAは完全削除されることなく保護されます。

```
{
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"allow",
            "action":[
                "name/cos:DeleteObject"
            ],
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ]
        },
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"deny",
            "action":[
                "name/cos:DeleteObject"
            ],
            "condition":{
                "string_equal":{
                    "cos:versionid":"null"
                }
            },
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ]
        }
    ],
    "version":"2.0"
}
```

<span id="content-length"></span>
### アップロードファイルサイズの制限（cos:content-length）

#### リクエストヘッダーContent-Length
RFC 2616で定義されたHTTPリクエストのコンテンツの長さ（バイト）です。PUTおよびPOSTリクエストで頻繁に使用されます。詳細については、[リクエストヘッダーリスト](https://intl.cloud.tencent.com/document/product/436/7728)をご参照ください

#### 条件キーcos:content-length

オブジェクトをアップロードする際、条件キー`cos:content-length`によってリクエストヘッダー`Content-Length`を制限することができます。それによりアップロードするオブジェクトのファイルサイズを制限することで、ストレージスペースをより柔軟に管理し、大きすぎるファイルや小さすぎるファイルのアップロードによる、ストレージスペースやネットワーク帯域幅の浪費防止に役立ちます。

下記の2つの例では、ルートアカウント（uin:100000000001）がバケットexamplebucket-1250000000を所有している場合、`cos:content-length`条件キーによってサブユーザー（uin:100000000002）のアップロードリクエストのContent-Lengthヘッダーのサイズを制限することができます。

#### 事例1: リクエストヘッダーContent-Lengthの最大値を制限する

PutObjectおよびPostObjectのアップロードリクエストには必ずContent-Lengthヘッダーが含まれなければならず、かつこのヘッダーの値を10バイト以下とするよう制限します。

```
{
    "version":"2.0",
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"allow",
            "action":[
                "name/cos:PutObject",
                "name/cos:PostObject"
            ],
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ],
            "condition":{
                "numeric_less_than_equal":{
                    "cos:content-length":10
                }
            }
        },
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"deny",
            "action":[
                "name/cos:PutObject",
                "name/cos:PostObject"
            ],
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ],
            "condition":{
                "numeric_greater_than_if_exist":{
                    "cos:content-length":10
                }
            }
        }
    ]
}
```

#### 事例2: リクエストヘッダーContent-Lengthの最小値を制限する

PutObjectおよびPostObjectのアップロードリクエストには必ずContent-Lengthヘッダーが含まれなければならず、かつContent-Lengthの値を2バイト以上とするよう制限します。

```
{
    "version":"2.0",
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"allow",
            "action":[
                "name/cos:PutObject",
                "name/cos:PostObject"
            ],
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ],
            "condition":{
                "numeric_greater_than_equal":{
                    "cos:content-length":2
                }
            }
        },
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"deny",
            "action":[
                "name/cos:PutObject",
                "name/cos:PostObject"
            ],
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ],
            "condition":{
                "numeric_less_than_if_exist":{
                    "cos:content-length":2
                }
            }
        }
    ]
}
```

<span id="content-type"></span>
### アップロードファイルタイプの制限（cos:content-type）

#### リクエストヘッダーContent-Type 

RFC 2616で定義されたHTTPリクエストのコンテンツタイプ（MIME）であり、例えば`application/xml`や`image/jpeg`などです。詳細については、[リクエストヘッダーリスト](https://intl.cloud.tencent.com/document/product/436/7728)をご参照ください。

#### 条件キーcos:content-type

条件キー`cos:content-type`を使用すると、リクエストの`Content-Type`ヘッダーを制限することができます。


#### 事例1: オブジェクトのアップロード（PutObject）のContent-Typeを必ず「image/jpeg」とするよう限定する

ルートアカウント（uin:100000000001）がバケットexamplebucket-1250000000を所有している場合、`cos:content-type`条件キーによってサブユーザー（uin:100000000002）のアップロードリクエストのContent-Typeヘッダーの具体的な内容を制限することができます。

以下のこのバケットポリシーの意味は、PutObjectを使用してオブジェクトをアップロードする場合に、必ずContent-Typeヘッダーを含め、かつContent-Typeの値を「image/jpeg」とするよう制限するものです。

注意すべきは、string_equalはリクエストに必ずContent-Typeヘッダーを含め、なおかつContent-Typeの値が規定値と完全に一致することを要求するという点です。実際のリクエストでは、**リクエストのContent-Typeヘッダーを明確に指定する**必要があります。それを行わず、リクエストにContent-Typegヘッダーが含まれない場合、リクエストは失敗します。また、何らかのツールを使用してリクエストを送信し、Content-Typeを明確に指定しなかった場合、ツールが想定と異なるContent-Typeヘッダーを自動的に追加する可能性があり、この場合もリクエストの失敗につながる可能性があります。

```
{
    "version":"2.0",
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
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
                "string_equal":{
                    "cos:content-type":"image/jpeg"
                }
            }
        },
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"deny",
            "action":[
                "name/cos:PutObject"
            ],
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ],
            "condition":{
                "string_not_equal_if_exist":{
                    "cos:content-type":"image/jpeg"
                }
            }
        }
    ]
}
```

<span id="response-content-type"></span>
### ダウンロードリクエストに返されるファイルタイプの制限（cos:response-content-type）

#### リクエストパラメータresponse-content-type

GetObjectインターフェースは、リクエストパラメータ`response-content-type`を追加し、レスポンスのContent-Typeヘッダーの値を設定するために用いることができます。

#### 条件キーcos:response-content-type

条件キー`cos:response-content-type`を使用すると、リクエストにリクエストパラメータ`response-content-type`のパラメータ値を必ず含めるかどうかを制限することができます。

#### 事例1: Get Objectのリクエストパラメータresponse-content-typeを必ず「image/jpeg」とするよう限定する

ルートアカウント（uin:100000000001）がバケットexamplebucket-1250000000を所有している場合、以下のバケットポリシーの意味は、サブユーザー（uin:100000000002）のGet Objectリクエストに必ずリクエストパラメータresponse-content-typeを含め、かつリクエストパラメータの値を必ず「image/jpeg」とするよう制限するものです。`response-content-type`はリクエストパラメータであるため、リクエストの送信時にurlencodeを経る必要があり、`response-content-type=image%2Fjpeg`となります。そのため、Policyを設定する際は、「image/jpeg」にもurlencodeを行って「image%2Fjpeg」と入力する必要があります。

```
{
    "version":"2.0",
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
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
                    "qcs::cam::uin/100000000001:uin/100000000002"
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

<span id="secure-transport"></span>
### HTTPSプロトコルを使用したリクエストのみ承認する（cos:secure-transport）

#### 条件キーcos:secure-transport

条件キー`cos:secure-transport`を使用して、リクエストが必ずHTTPSプロトコルを使用するよう制限することができます。

#### 事例1：ダウンロードリクエストにHTTPSプロトコルの使用を必須とする

ルートアカウント（uin:100000000001）がバケットexamplebucket-1250000000を所有している場合、以下のバケットポリシーの意味は、サブユーザー（uin:100000000002）からのHTTPSプロトコルを使用したGetObjectリクエストに対してのみ権限承認を行うことを表します。

```
{
    "version":"2.0",
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
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
                "bool_equal":{
                    "cos:secure-transport":"true"
                }
            }
        }
    ]
}
```

#### 事例2：HTTPSプロトコルを使用していないあらゆるリクエストを拒否する

ルートアカウント（uin:100000000001）がバケットexamplebucket-1250000000を所有している場合、以下のバケットポリシーの意味は、サブユーザー（uin:100000000002）からの、HTTPSプロトコルを使用していないあらゆるリクエストを拒否することを表します。

```
{
    "version":"2.0",
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
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
                "bool_equal":{
                    "cos:secure-transport":"false"
                }
            }
        }
    ]
}
```

<span id="x-cos-storage-class"></span>
### 指定されたストレージタイプの設定のみを許可（cos:x-cos-storage-class）

#### リクエストヘッダーx-cos-storage-class

ユーザーはリクエストヘッダー`x-cos-storage-class`によって、オブジェクトをアップロードする際にストレージタイプを指定したり、オブジェクトのストレージタイプを変更したりすることができます。

#### 条件キーcos:x-cos-storage-class

条件キー`cos:x-cos-storage-class`によって、リクエストヘッダー`x-cos-storage-class`を制限し、それによりストレージタイプを変更する可能性のあるリクエストを制限することができます。

COSのストレージタイプフィールドには、`STANDARD`、`MAZ_STANDARD`, `STANDARD_IA`、`MAZ_STANDARD_IA`、`INTELLIGENT_TIERING`、`MAZ_INTELLIGENT_TIERING`、`ARCHIVE`、`DEEP_ARCHIVE`があります。

#### 事例1：PutObjectの際にストレージタイプを必ず標準タイプに設定するよう要求する

ルートアカウント（uin:100000000001）がバケットexamplebucket-1250000000を所有している場合、バケットポリシーによって、サブユーザー（uin:100000000002）からのPutObjectリクエストには必ずx-cos-storage-classヘッダーを含めなければならず、かつヘッダー値は`STANDARD`とするよう制限します。

```
{
    "version":"2.0",
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
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
                "string_equal":{
                    "cos:x-cos-storage-class":"STANDARD"
                }
            }
        },
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"deny",
            "action":[
                "name/cos:PutObject"
            ],
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ],
            "condition":{
                "string_not_equal_if_exist":{
                    "cos:x-cos-storage-class":"STANDARD"
                }
            }
        }
    ]
}
```

<span id="x-cos-acl"></span>
### 指定されたバケット/オブジェクトACLの設定のみを許可（cos:x-cos-acl）

#### リクエストヘッダーx-cos-acl

リクエストヘッダー`x-cos-acl`を使用すると、オブジェクトのアップロード、バケットの作成時にアクセス制御リスト（ACL）を指定するか、またはオブジェクト、バケットACLを変更することができます。ACLに関する説明については、[ACLの概要](https://intl.cloud.tencent.com/document/product/436/30583)をご参照ください。

- バケットのプリセットACL：`private`、`public-read`、`public-read-write`、`authenticated-read`。
- オブジェクトのプリセットACL：`default`、`private`、`public-read`、`authenticated-read`、`bucket-owner-read`、`bucket-owner-full-control`。

#### 条件キーcos:x-cos-acl

条件キー`cos:x-cos-acl`によって、リクエストヘッダー`x-cos-acl`を制限し、それによりオブジェクトまたはバケットACLを変更する可能性のあるリクエストを制限することができます。

#### 事例1：PutObjectの際に必ず同時にオブジェクトのACLをプライベートに設定する

ルートアカウント（uin:100000000001）がバケットexamplebucket-1250000000を所有し、サブユーザー（uin:100000000002）にプライベートオブジェクトのみをアップロードできるよう制限する必要があるとします。以下のポリシーによって、PutObjectリクエストの送信時に必ずx-cos-aclヘッダーを含め、かつヘッダー値を`private`とするよう要求します。

```
{
    "version":"2.0",
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
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
                "string_equal":{
                    "cos:x-cos-acl":"private"
                }
            }
        },
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"deny",
            "action":[
                "name/cos:PutObject"
            ],
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ],
            "condition":{
                "string_not_equal_if_exist":{
                    "cos:x-cos-acl":"private"
                }
            }
        }
    ]
}
```

<span id="prefix"></span>
### 指定ディレクトリ下のオブジェクトのリストアップのみを許可する（cos:prefix）

#### 条件キーcos:prefix

条件キー`cos:prefix`によってリクエストパラメータprefixを制限することができます。


>! prefixの値が特殊文字（中国語、`/`など）の場合は、バケットポリシーに書き込む前にurlencodeを経る必要があります。
>

#### 事例1：バケットの指定ディレクトリ下のオブジェクトのリストアップのみを許可する

ルートアカウント（uin:100000000001）がバケットexamplebucket-1250000000を所有し、サブユーザー（uin:100000000002）にバケットのfolder1ディレクトリ下のオブジェクトのみをリストアップできるよう制限する必要があるとします。以下のバケットポリシーによって、サブユーザーが送信するGetBucketリクエストには必ずprefixパラメータを含め、かつその値を“folder1”とするよう規定します。


```
{
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"allow",
            "action":[
                "name/cos:GetBucket"
            ],
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ],
            "condition":{
                "string_equal":{
                    "cos:prefix":"folder1"
                }
            }
        },
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect":"deny",
            "action":[
                "name/cos:GetBucket"
            ],
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ],
            "condition":{
                "string_equal_if_exist":{
                    "cos:prefix":"folder1"
                }
            }
        }
    ],
    "version":"2.0"
}
```

<span id="tls-version"></span>
### 指定されたバージョンのTLSプロトコルの使用のみを許可（cos:tls-version）

#### 条件キー cos:tls-version

条件キー`cos:tls-version`によってHTTPSリクエストのTLSバージョンを制限することができます。この条件キーはNumricタイプであり、1.0、1.1、1.2などの浮動小数点数の入力が可能です。


#### 事例1：TLSプロトコルのバージョンが1.2であるHTTPSリクエストにのみ権限を承認する


|リクエストのシナリオ   |予測|
|---|---|
|HTTPSリクエスト、TLSバージョンは1.0|403、失敗|
|HTTPSリクエスト、TLSバージョンは1.2|200、成功|

ポリシーの例は次のとおりです。

```
{
    "version":"2.0",
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
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
                "numeric_equal":{
                    "cos:tls-version":1.2
                }
            }
        }
    ]
}
```


#### 事例2：TLSプロトコルのバージョンが1.2より低いHTTPSリクエストを拒否する

|リクエストのシナリオ  |  予測   |
|---|---|
|HTTPSリクエスト、TLSバージョンは1.0|    403、失敗   |
|HTTPSリクエスト、TLSバージョンは1.2|    200、成功   |


ポリシーの例は次のとおりです。


```
{
    "version":"2.0",
    "statement":[
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
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
                "numeric_greater_than_equal":{
                    "cos:tls-version":1.2
                }
            }
        },
        {
            "principal":{
                "qcs":[
                    "qcs::cam::uin/100000000001:uin/100000000002"
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
                "numeric_less_than_if_exist":{
                    "cos:tls-version":1.2
                }
            }
        }
    ]
}
```


<span id="request_tag"></span>
### バケット作成時に指定のバケットタグを強制的に設定（qcs:request_tag）

>?
>条件キーrequest_tagはPutBucket、PutBucketTagging操作にのみ適用可能です。GetService、PutObject、PutObjectTaggingなどの操作はこの条件キーをサポートしていません。
>


#### 条件キー qcs:request_tag

条件キー`qcs:request_tag`によって、ユーザーがPutBucket、PutBucketTaggingリクエストを送信する際に、必ず指定したバケットタグを含めるよう制限することができます。

#### 事例：ユーザーのバケット作成時に必ず指定したバケットタグを含めるよう制限する

多くのユーザーはバケットタグによってバケットを管理しています。次のポリシーの例は、ユーザーがバケットを作成する際、指定のバケットタグ`<a,b>`および`<c,d>`を設定した場合にのみ権限を取得できるよう制限するものです。

バケットタグは複数設定することができ、バケットタグのキー値、タグの数が異なると、それらはすべて異なるセットとなります。ユーザーの持つ複数のパラメータ値をセットA、条件で規定する複数のパラメータ値をセットBと仮定します。この条件キーを使用する際、限定語for_any_value、for_all_valueの組み合わせによって異なる意味を表すことができます。
- `for_any_value:string_equal`はAとBに共通部分が存在する場合に発効することを表します。
- `for_any_value:string_equal`はAがBのサブセットである場合に発効することを表します。

`for_any_value:string_equal`を使用する場合、対応するポリシーとリクエストは次のように表されます。

|リクエストのシナリオ     |予測|
|---|---|
|PutBucket、リクエストヘッダー`x-cos-tagging: a=b&c=d`|200、成功|
|PutBucket、リクエストヘッダー`x-cos-tagging: a=b`|200、成功|
|PutBucket、リクエストヘッダー`x-cos-tagging: a=b&c=d&e=f`|200、成功|

ポリシーの例は次のとおりです。

```
{
    "version": "2.0",
    "statement":[
        {
            "principal":{
                "qcs": [
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect": "allow",
            "action":[
                "name/cos:PutBucket"
            ],
            "resource": "*",
            "condition":{
                "for_any_value:string_equal":{
                    "qcs:request_tag": [
                        "a&b",
                        "c&d"
                    ]
                }
            }
        }
    ]
}
```


`for_all_value:string_equal`を使用する場合、対応するポリシーとリクエストは次のように表されます。



|リクエストのシナリオ   |予測|
|---|---|
|PutBucket、リクエストヘッダー`x-cos-tagging: a=b&c=d`|200、成功|
|PutBucket、リクエストヘッダー`x-cos-tagging: a=b`|200、成功|
|PutBucket、リクエストヘッダー`x-cos-tagging: a=b&c=d&e=f`|403、失敗|


ポリシーの例は次のとおりです。

```
{
    "version": "2.0",
    "statement":[
        {
            "principal":{
                "qcs": [
                    "qcs::cam::uin/100000000001:uin/100000000002"
                ]
            },
            "effect": "allow",
            "action":[
                "name/cos:PutBucket"
            ],
            "resource": "*",
            "condition":{
                "for_all_value:string_equal": {
                    "qcs:request_tag": [
                        "a&b",
                        "c&d"
                    ]
                }
            }
        }
    ]
}
```



