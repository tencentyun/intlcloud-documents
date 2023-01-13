## 소개

조건은 액세스 정책 언어의 일부입니다. 완전한 조건에는 다음 요소가 포함됩니다.
- 조건 키: 조건의 유형을 지정합니다(예: 사용자 액세스 소스 IP 및 권한 부여 시간).
- 조건 연산자: 조건 결정 방법을 지정합니다.
- 조건 값: 조건 키의 값을 지정합니다.

자세한 내용은 [Conditions](https://www.tencentcloud.com/document/product/598/10608)를 참고하십시오.

>? 
>- 버킷 정책을 작성 시 조건 키를 사용할 때 최소 권한 원칙을 준수하고, 해당 조건 키를 해당 요청(action)에만 추가하며, 작업 지정(action) 시 “\*” 와일드 카드를 사용하지 마십시오. 와일드카드를 사용하면 요청이 실패합니다.
>- 액세스 관리(CAM) 콘솔을 사용하여 정책을 생성할 때, version, principal, statement, effect, action, resource, condition 구문 요소의 첫 번째 글자는 대문자이거나 모두 소문자여야 합니다.


## 조건 예시

다음 버킷 정책 예시에서 조건(condition)은 `cos:PutObject` 권한 부여 작업이 10.217.182.3/24 또는 111.21.33.72/24 IP 범위에서만 완료될 수 있음을 지정합니다.
- **조건 키**는 `qcs:ip`이며 조건 유형이 IP임을 나타냅니다.
- **조건 연산자**는 `ip_equal`로, 조건 판단 방법이 IP 주소 일치 여부를 판단하는 것임을 나타냅니다.
- **조건 값**은 조건 결정을 위해 지정된 값을 나열하는 `["10.217.182.3/24","111.21.33.72/24"]` 배열입니다. 사용자의 IP가 어레이의 지정된 IP 범위에 있는 경우 조건은 true로 결정됩니다.

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

## COS에서 지원하는 조건 키


>? 현재 `tls-version` 조건 키는 베이징 리전에서만 지원됩니다. 추후 다른 리전에서도 지원될 예정입니다.
>


COS는 IP, VPC 및 HTTPS를 포함한 모든 요청에 적용 가능한 조건 키와 요청 헤더 및 요청 매개변수의 조건 키, 일반적으로 요청 헤더 또는 요청 매개변수를 전달해야 하는 요청에만 적용할 수 있는 두 가지 유형의 조건 키를 지원합니다. 이러한 조건 키에 대한 설명 및 사용 사례는 [Descriptions and Use Cases of Condition Keys](https://intl.cloud.tencent.com/document/product/436/46206)를 참고하십시오.

>? 조건 및 조건 키는 사용자 요청의 액세스 관리에만 적용됩니다. 수명 주기 및 버킷 복제 규칙이 유효한 경우 삭제 및 복제와 같은 작업은 사용자가 아닌 COS에서 시작하므로 조건 키의 해당 범위에 포함되지 않습니다.
>

### 모든 요청에 적용 가능한 조건 키

모든 요청에 적용할 수 있는 조건 키는 각각 `qcs:ip`, `qcs:vpc`, `cos:secure-transport`로 요청의 소스 IP 범위, 요청의 소스 VPC ID, HTTPS 사용 여부를 나타냅니다.

| 조건 키 |적용 요청 |의미 |유형|
|:----------|:----------|:----------|:----------|
|[cos:secure-transport](https://intl.cloud.tencent.com/document/product/436/46206#secure-transport) |모든 요청 |요청의 HTTPS 사용 여부 |  Boolean  |
|[qcs:ip](https://intl.cloud.tencent.com/document/product/436/46206#RestrictUserAccessIP) |모든 요청 |요청의 소스 IP 범위|  IP|
|[qcs:vpc](https://intl.cloud.tencent.com/document/product/436/46206#requester_vpc) |모든 요청 |요청의 소스 VPC ID  | String  |
|[cos:tls-version](https://intl.cloud.tencent.com/document/product/436/46206#tls-version) |모든 https 요청|https 요청에 사용되는 TLS 버전 |Numeric|


### 요청 헤더 및 요청 매개변수의 조건 키

요청마다 요청 헤더(Header) 및 요청 매개변수(Param)가 다르기 때문에 요청 헤더 및 요청 매개변수의 조건 키는 이러한 요청 헤더 또는 요청 매개변수를 포함하는 요청에만 적용할 수 있습니다.

예를 들어 조건 키 `cos:content-type`은 요청 헤더 `Content-Type`을 사용해야 하는 업로드 요청(예: PutObject)에 적용할 수 있는 반면 조건 키 `cos:response-content-type`은 GetObject 요청에만 적용할 수 있습니다. GetObject 요청만 요청 매개변수 `response-content-type`을 지원합니다.

아래 표에는 요청 헤더 및 요청 매개변수의 조건 키와 해당하는 해당 요청이 나열되어 있습니다.


|조건 키   |적용 요청 | 요청 헤더 또는 요청 매개변수 확인 |유형|
|:----------|:----------|:----------|:----------|
|[cos:x-cos-storage-class](https://intl.cloud.tencent.com/document/product/436/46206#x-cos-storage-class) |PutObject<br>PostObject<br>InitiateMultipartUpload<br>AppendObject |요청 헤더: x-cos-storage-class |String|
|[cos:versionid](https://intl.cloud.tencent.com/document/product/436/46206#versionid) |GetObject<br>DeleteObject<br>PostObjectRestore<br>PutObjectTagging<br>GetObjectTagging<br>DeleteObjectTagging<br>HeadObject |요청 매개변수: versionid |String|
|[cos:prefix](https://intl.cloud.tencent.com/document/product/436/46206#prefix) |GetBucket（List Objects）<br>GET Bucket Object versions<br>List Multipart Uploads<br>ListLiveChannels |요청 매개변수: prefix |String|
|[cos:x-cos-acl](https://intl.cloud.tencent.com/document/product/436/46206#x-cos-acl) |PutObject<br>PostObject<br>PutObjectACL<br>PutBucket<br>PutBucketACL<br>AppendObject<br>Initiate Multipart Upload |요청 헤더: x-cos-acl |String|
|[cos:content-length](https://intl.cloud.tencent.com/document/product/436/46206#content-length) |이 요청 헤더는 적용 가능한 범위가 넓으며 일반적으로 요청 본문이 있는 요청 |요청 헤더: Content-Length |Numeric|
|[cos:content-type](https://intl.cloud.tencent.com/document/product/436/46206#content-type) |이 요청 헤더는 적용 가능한 범위가 넓으며 일반적으로 요청 본문이 있는 요청 |요청 헤더: Content-Type |String|
|[cos:response-content-type](https://intl.cloud.tencent.com/document/product/436/46206#response-content-type) |GetObject |요청 매개변수: response-content-type |String|
|[qcs:request_tag](https://intl.cloud.tencent.com/document/product/436/46206#request_tag) |PutBucket<br>PutBucketTagging |요청 헤더: x-cos-tagging<br>요청 매개변수: tagging|String|



## 조건 연산자

COS는 문자열(String), 숫자(Numeric), 부울(Boolean) 및 IP 유형의 조건 키에 적용할 수 있는 다음 조건 연산자를 지원합니다.

|조건 연산자 |설명 |유형 |
|:----------|:----------|:----------|
|string_equal |같은 문자열(대소문자 구분) |String |
|string_not_equal |같지 않은 문자열(대소문자 구분) |String |
|string_like |유사한 문자열(대소문자 구분), 현재 와일드카드(`*`)를 문자열에 접두사 또는 접미사로 사용 가능, 예시 `image/*` |String |
|ip_equal |IP 같음 |IP |
|ip_not_equal |IP가 같지 않음 |IP |
|numeric_equal |같은 숫자 |Numeric |
|numeric_not_equal |같지 않은 숫자 |Numeric |
|numeric_greater_than |큰 숫자 |Numeric |
|numeric_greater_than_equal |크거나 같은 숫자 |Numeric |
|numeric_less_than |작은 숫자 |Numeric |
|numeric_less_than_equal |작거나 같은 숫자 |Numeric |

### _if_exist의 의미

이전 조건 연산자의 끝에 `_if_exist`를 추가하여 `string_equal_if_exist`와 같은 새 조건 연산자를 구성할 수 있습니다. `_if_exist`가 있는 조건 연산자와 없는 조건 연산자의 차이점은 다음과 같습니다.

- `string_equal`과 같이 `_if_exist`가 없는 조건 연산자의 경우 요청에 지정된 요청 헤더 또는 매개변수가 포함되어 있지 않으면 기본적으로 조건이 충족된(`False`) 것으로 간주됩니다.
- `string_equal_if_exist`와 같이 `_if_exist`가 있는 조건 연산자의 경우 요청에 지정된 요청 헤더 또는 매개변수가 포함되어 있지 않으면 기본적으로 조건이 충족된(`True`) 것으로 간주됩니다.

## License 요청 예시


### 예시1: 지정된 버전의 객체 다운로드 허용

이 예시의 버킷 정책에서 Effect는 allow이며 요청 매개변수 versionid가 ‘MTg0NDUxNTc1NjIzMTQ1MDAwODg’인 GetObject 요청을 허용합니다. 권한 부여 allow 정책에 따라 조건이 충족되면(True) 요청이 허용됩니다. 조건이 충족되지 않으면(False) 요청이 허용되지 않고 실패합니다.

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

아래 표는 조건 연산자 `string_equal` 및 `string_equal_if_exist`의 condition 충족 및 요청 허용 세부 정보를 나열합니다.

|조건 연산자  |요청 |condition 충족 |요청 허용 여부|
|:----------|:----------|:----------|:----------|
|string_equal |versionid 가 없는 경우 |FALSE |No |
|string_equal_if_exist |versionid 가 없는 경우 |TRUE |Yes |
|string_equal |값이 지정된 versionid 사용 |TRUE |Yes |
|string_equal_if_exist |값이 지정된 versionid 사용 |TRUE |Yes |
|string_equal |값이 지정되지 않은 versionid 사용 |FALSE |No |
|string_equal_if_exist |값이 지정되지 않은 versionid 사용 |FALSE |No |

### 예시2: 지정된 버전의 객체 다운로드 금지

이 예시의 버킷 정책에서 Effect는 deny이며 요청 매개변수 versionid가 ‘MTg0NDUxNTc1NjIzMTQ1MDAwODg’인 GetObject 요청을 허용하지 않습니다. deny 권한 부여 정책에 따라 조건이 충족되면(True) 요청이 실패합니다. 조건이 충족되지 않으면(False) 요청이 거부되지 않습니다.

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

아래 표는 조건 연산자 `string_equal` 및 `string_equal_if_exist`의 condition 충족 및 요청 거부 세부 정보를 나열합니다.

| 조건 연산자 |요청 |condition 충족 |요청 거부 여부|
|:----------|:----------|:----------|:----------|
|string_equal |versionid 가 없는 경우 |FALSE |No |
|string_equal_if_exist |versionid 가 없는 경우 |TRUE |Yes |
|string_equal |값이 지정된 versionid 사용 |TRUE |Yes |
|string_equal_if_exist |값이 지정된 versionid 사용 |TRUE |Yes |
|string_equal |값이 지정되지 않은 versionid 사용 |FALSE |No |
|string_equal_if_exist |값이 지정되지 않은 versionid 사용 |FALSE |No |


## 관련 설명

### 특수 문자에는 urlencode 필요

요청 매개변수의 특수 문자에는 모두 urlencode가 필요하므로 요청 매개변수의 조건 키를 사용하는 버킷 정책에도 urlencode가 필요합니다. 예를 들어 버킷 정책에서 `cos:response-content-type` 조건 키를 사용하려는 경우 버킷 정책에 입력하기 전에 조건 값 "image/jpeg"를 "image%2Fjpeg"로 urlencode해야 합니다.

### 최소 권한 원칙 및 \* 와일드카드 없음

조건 키를 사용할 때 최소 권한 원칙을 준수하고 권한을 설정하려는 action만 추가하고 ‘\*’ 와일드카드를 사용하지 마십시오. ‘\*’ 와일드카드를 잘못 사용하면 일부 요청이 실패할 수 있습니다. 아래 예에서 GetObject 이외의 요청은 요청 매개변수 response-content-type 사용을 지원하지 않습니다.

deny + string_equal_if_exist의 경우 조건 키가 요청에 없으면 기본적으로 true로 간주됩니다. 따라서 PutObject 및 PutBucket과 같은 요청을 시작하면 deny statement가 충족되고 요청이 거부됩니다.

allow + string_equal의 경우 조건 키가 요청에 없으면 기본적으로 false로 간주됩니다. 따라서 PutObject 및 PutBucket과 같은 요청을 시작할 때 allow statement가 충족되지 않고 요청이 허용되지 않습니다.

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

또는 allow+string_equal_if_exist 및 deny + string_not_equal을 사용하여 response-content-type 요청 매개변수 없이 요청을 허용할 수 있습니다.

deny + string_equal의 경우 조건 키가 요청에 없으면 기본적으로 false로 간주됩니다. 따라서 PutObject 및 PutBucket과 같은 요청을 시작할 때 deny statement가 충족되지 않고 요청이 거부되지 않습니다.

allow + string_equal_if_exist의 경우 조건 키가 요청에 없으면 기본적으로 true로 간주됩니다. 따라서 PutObject 및 PutBucket과 같은 요청을 시작할 때 allow statement가 충족되고 요청이 허용됩니다.

그러나 이러한 방식으로 조건 연산자를 사용하면 GetObject 요청의 response-content-type 요청 매개변수 전달 여부를 제한할 수 없습니다. response-content-type 요청 매개변수가 없는 GetObject 요청은 다른 요청과 마찬가지로 기본적으로 허용됩니다. GetObject 요청이 response-content-type 요청 매개변수를 전달하는 경우에만 지정된 조건을 사용하여 요청 매개변수의 내용이 조건부 승인을 구현할 것으로 예상하는 내용과 동일한지 확인할 수 있습니다.

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


따라서 보다 안전한 방법은 최소 권한 원칙을 준수하고 ‘\*‘ 와일드카드를 사용하지 않고 GetObject 요청에 대한 action을 제한하는 것입니다.

아래 예시 정책에서 볼 수 있듯이 정책 조건은 값이 "image%2Fjpeg"인 response-content-type 요청 매개변수를 전달하는 GetObject 요청에 대해서만 권한 부여가 수행되도록 엄격하게 지정합니다.

다른 요청은 이 예시에서 정책의 영향을 받지 않으며 최소 권한 원칙에 따라 별도로 권한을 부여할 수 있습니다.

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


