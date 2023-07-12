액세스 정책을 사용하여 권한을 부여할 때 정책 [조건](https://intl.cloud.tencent.com/document/product/436/18023)을 지정할 수 있습니다. 예를 들어 정책 조건을 사용하여 업로드할 파일의 스토리지 클래스와 사용자 액세스 소스를 제한할 수 있습니다.

이 문서는 버킷 정책에서 COS(Cloud Object Storage) 조건 키를 사용하는 일반적인 예시를 제공합니다. [조건](https://intl.cloud.tencent.com/document/product/436/46205) 문서에서 COS 및 해당 요청이 지원하는 모든 조건 키를 볼 수 있습니다.

>? 
>- 버킷 정책을 작성 시 조건 키를 사용할 때 최소 권한 원칙을 준수하고, 해당 조건 키를 해당 요청(action)에만 추가하며, 작업 지정(action) 시 “\*” 와일드카드를 사용하지 마십시오. 와일드카드를 사용하면 요청이 실패합니다. 조건 키에 대한 자세한 내용은 [조건](https://intl.cloud.tencent.com/document/product/436/46205) 문서를 참고하십시오.
>- 액세스 관리(CAM) 콘솔을 사용하여 정책을 생성할 때, version, principal, statement, effect, action, resource, condition 구문 요소의 첫 번째 글자는 대문자이거나 모두 소문자여야 합니다.


## 조건 키의 사용 사례

<span id="RestrictUserAccessIP"></span>
### 사용자 액세스 IP 제한(qcs:ip)

#### 조건 키 qcs:ip

조건 키 `qcs:ip`를 사용하여 사용자 액세스 IP를 제한할 수 있습니다. 조건 키는 모든 요청에 적용할 수 있습니다.

#### 예시: 지정 IP의 사용자의 액세스만 허용

다음은 ID가 100000000001(APPID는 1250000000)인 루트 계정에 속하는 ID가 100000000002인 서브 계정이 베이징 리전의 버킷 examplebucket-bj와 광저우 리전의 버킷 examplebucket-gz의 객체 exampleobject에 대해, 액세스 IP가 IP 범위 `192.168.1.0/24`에 속하거나 액세스가 IP가 `101.226.100.185` 또는 `101.226.100.186` 대역인 경우 객체 업로드 및 객체 다운로드 권한을 부여하는 정책 예시입니다.

```
{
    "version": "2.0",
    "principal":{
        "qcs":[
            "qcs::cam::uin/100000000001:uin/100000000002"
        ]
    },
    "statement": [
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
### vpcid 제한(vpc:requester_vpc)

#### 조건 키 vpc:requester_vpc

조건 키 `vpc:requester_vpc`를 사용하여 사용자 액세스 vpcid를 제한할 수 있습니다. vpcid에 대한 자세한 내용은 Tencent Cloud 제품 [Virtual Private Cloud](https://www.tencentcloud.com/document/product/215)를 참고하십시오.

#### 예시: vpcid를 aqp5jrc1로 제한

이 예시의 정책은 vpcid가 aqp5jrc1인 조건에서 ID 100000000001(APPID: 1250000000)의 루트 계정에 속하는 ID 100000000002의 서브 계정이 examplebucket-1250000000 버킷에 액세스하도록 허용합니다.

```
{
  "statement": [
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
        "qcs":[
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
### 객체의 최신 버전 또는 지정 버전(cos:versionid) 액세스만 허용

#### 요청 매개변수 versionid

요청 매개변수 `versionid`는 객체의 버전 번호를 지정합니다. 버전 관리에 대한 자세한 내용은 [버전 제어 개요](https://intl.cloud.tencent.com/document/product/436/19883)를 참고하십시오. 객체를 다운로드(GetObject)하거나 객체를 삭제할 때(DeleteObject) 요청 매개변수 `versionid`를 사용하여 작업할 객체 버전을 지정할 수 있습니다. versionid에는 세 가지 다른 경우가 있습니다.

- `versionid`가 없음: 요청은 기본적으로 최신 버전의 객체에 적용됩니다.
- `versionid`가 빈 문자열인 경우: `versionid` 요청 매개변수가 전달되지 않은 경우와 동일합니다.
- `versionid`가 `"null"`인 경우: 버킷에 대해 버전 관리가 활성화되기 전에 업로드된 객체의 경우 버전 관리가 활성화된 후 버전 번호가 `"null"` 문자열이 됩니다.


#### 조건 키 cos:versionid 

조건 키 `cos:versionid`를 사용하여 요청 매개변수 `versionid`를 제한할 수 있습니다.


#### 예시1: 사용자가 지정된 버전의 객체를 가져오도록 허용

examplebucket-1250000000 버킷을 소유하는 uin 100000000001의 루트 계정이 다음 버킷 정책을 사용하여 uin이 100000000000인 서브 계정이 지정된 버전의 객체만 가져오도록 허용한다고 가정합니다.

정책에 따르면 uin이 100000000002인 서브 계정으로 전송된 객체 다운로드 요청은 versionid 매개변수를 전달하고 versionid 값이 버전 번호 ‘MTg0NDUxNTc1NjIzMTQ1MDAwODg’인 경우에만 성공할 수 있습니다.

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

#### 거부 정책 추가

상기 정책을 사용하여 서브 계정에게 권한을 부여하고 서브 계정이 다른 수단을 통해 조건을 부여하지 않고 동일한 권한을 얻는 경우 더 광범위한 권한 부여 정책이 적용됩니다. 예를 들어 서브 계정이 사용자 그룹에 있고 루트 계정이 아무런 조건 없이 사용자 그룹에 GetObject 권한을 부여하면 상기 정책의 버전 번호에 대한 제한이 적용되지 않습니다.

이에 대처하기 위해 위의 정책을 기반으로 명시적 거부 정책(deny)을 추가하여 더 엄격한 권한 제한을 달성할 수 있습니다. 다음 deny 정책은 서브 사용자가 versionid 매개변수를 포함하지 않는 객체 다운로드 요청을 시작하거나 versionid에 의해 지정된 버전 번호가 ‘MTg0NDUxNTc1NjIzMTQ1MDAwODg’가 아닌 경우 요청이 거부되도록 지정합니다. deny 정책의 우선 순위가 다른 정책보다 높기 때문에 거부 정책을 추가하면 권한 취약성을 최대한 방지할 수 있습니다.

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

#### 예시2: 사용자가 최신 버전의 객체만 가져올 수 있도록 허용

버킷 examplebucket-1250000000을 소유하는 uin 100000000001의 루트 계정이 다음 버킷 정책을 사용하여 uin이 100000000002인 서브 계정이 최신 버전의 객체만 가져오도록 허용한다고 가정합니다.

정책에 따라 `versionid`가 전달되지 않거나 해당 값이 빈 문자열인 경우 GetObject 요청은 기본적으로 최신 버전의 객체를 다운로드합니다. 따라서 다음 조건에서 string_equal_if_exsit를 사용할 수 있습니다.
1. versionid가 전달되지 않으면 기본적으로 조건이 충족된 것으로 간주(true)되어 allow 정책이 적용되어 요청이 allow됩니다.
2. versionid가 빈 문자열(`“”`)인 경우 allow 정책도 적용되며 최신 버전의 객체 다운로드 요청만 승인됩니다.
```
	"condition":{
		"string_equal_if_exist": {
			"cos:versionid": ""
		}
	}
```
명시적 거부 정책이 추가된 후 전체 버킷 정책은 다음과 같습니다.
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

#### 예시3: 버전 관리 활성화 전 업로드된 객체를 사용자가 삭제하는 것을 허용하지 않음

버전 관리가 활성화되기 전에 버킷에 업로드된 일부 객체가 있을 수 있으며 이러한 객체의 버전 번호는 버전 관리가 활성화된 후에 "null"이 됩니다. 경우에 따라 이러한 객체에 대한 추가 보호를 활성화해야 할 수 있습니다. 예를 들어 사용자가 이러한 객체를 영구적으로 삭제하지 못하도록 하는 것, 즉 버전 번호가 있는 객체의 삭제를 거부하는 것입니다.

아래 예시에는 두 가지 버킷 정책이 있습니다.
1. 서브 계정에 DeleteObject 요청을 사용하여 버킷의 객체를 삭제할 수 있는 권한을 부여합니다.
2. DeleteObject 요청에 대한 조건을 제한합니다. DeleteObject 요청이 값이 "null"인 요청 매개변수 versionid를 전달하면 요청이 거부됩니다.

따라서 버전 관리가 활성화되기 전에 객체 A가 버킷 examplebucket-1250000000에 업로드된 경우 버전 관리가 활성화된 후 객체 A의 버전 번호는 "null" 문자열이 됩니다.

버킷 정책이 추가되면 객체 A가 보호됩니다. 서브 사용자가 객체 A를 삭제하기 위해 시작한 DeleteObject 요청에 버전 번호가 없으면 버전 관리가 활성화되어 있기 때문에 객체 A가 영구적으로 삭제되지 않습니다. 대신 객체 A에 대한 삭제 표시가 추가됩니다. 요청에 객체 A의 "null" 버전 번호가 포함되어 있으면 요청이 거부되고 객체 A는 영구적으로 삭제되지 않습니다.

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
### 업로드 파일 크기 제한(cos:content-length)

#### 요청 헤더 Content-Length
RFC 2616에 정의된 바이트 단위의 HTTP 요청 콘텐츠 길이는 PUT 및 POST 요청에서 자주 사용됩니다. 자세한 내용은 [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728)를 참고하십시오.

#### 조건 키 cos:content-length

객체를 업로드할 때 조건 키 `cos:content-length`를 사용하여 요청 헤더 `Content-Length`를 제한하고 업로드할 객체의 파일 크기를 제한할 수 있습니다. 이러한 방식으로 저장 공간을 유연하게 관리하고 너무 크거나 작은 파일을 업로드하여 저장 공간과 네트워크 대역폭을 낭비하지 않도록 할 수 있습니다.

아래 두 예시에서는 루트 계정(uin: 100000000001)이 버킷 examplebucket-1250000000을 소유하고 있다고 가정하며, `cos:content-length` 조건 키를 사용하여 서브 계정(uin: 100000000002)에서 업로드한 요청의 Content-Length 헤더 값을 제한할 수 있습니다.

#### 예시1: 요청 헤더 Content-Length의 최대값 제한

PutObject 및 PostObject 업로드 요청이 10 바이트 이하의 값을 가진 Content-Length 헤더를 전달해야 한다고 제한합니다.

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

#### 예시2: 요청 헤더 Content-Length의 최소값 제한

PutObject 및 PostObject 업로드 요청이 2 바이트 이상의 값을 가진 Content-Length 헤더를 전달해야 한다고 제한합니다.

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
### 업로드할 파일 형식 제한(cos:content-type)

#### 요청 헤더 Content-Type 

Content-Type은 `application/xml` 및 `image/jpeg`와 같이 RFC 2616(MIME)에 정의된 HTTP 요청 콘텐츠 유형이어야 합니다. 자세한 내용은 [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728)를 참고하십시오.

#### 조건 키 cos:content-type

조건 키 `cos:content-type`을 사용하여 요청 헤더 `Content-Type`을 제한할 수 있습니다.


#### 예시1: PutObject 요청의 Content-Type을 "image/jpeg"로 제한

버킷 examplebucket-1250000000을 소유하는 uin이 100000000001인 루트 계정이 `cos:content-type` 조건 키를 사용하여 uin이 100000000002인 서브 계정이 시작한 업로드 요청에서 Content-Type 헤더의 콘텐츠를 제한한다고 가정합니다.

이 예시의 버킷 정책은 객체 업로드 요청(PutObject)이 Content-Type 헤더와 ‘image/jpeg’ 값을 포함해야 하는 것을 제한하는 것입니다.

string_equal은 요청이 지정된 값과 정확히 동일한 값을 가진 Content-Type 헤더를 전달해야 함을 요구합니다. 실제 요청에서는 **요청의 Content-Type 헤더를 명시적으로 지정해야 합니다**. 그렇지 않고 요청에 Content-Type 헤더가 없으면 요청이 실패합니다. 또한 특정 도구를 사용하여 요청을 시작하고 Content-Type을 명시적으로 지정하지 않으면 도구에서 예기치 않은 Content-Type 헤더를 요청에 자동으로 추가할 수 있으며 요청도 실패할 수 있습니다.

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
### 다운로드 요청에서 반환되는 파일 형식 제한(cos:response-content-type)

#### 요청 매개변수 response-content-type

GetObject API를 사용하면 요청 매개변수인 `response-content-type`을 추가하여 응답의 Content-Type 헤더 값을 지정할 수 있습니다.

#### 조건 키 cos:response-content-type

`cos:response-content-type` 조건 키를 사용하여 요청이 요청 매개변수인 `response-content-type`을 전달해야 하는지 여부를 지정할 수 있습니다.

#### 예시1: GetObject 요청 매개변수 response-content-type을 ‘image/jpeg’로 제한

버킷 examplebucket-1250000000을 소유하고 uin이 100000000001인 루트 계정이 다음 버킷 정책을 사용하여 uin이 100000000002인 서브 사용자가 시작한 GetObject 요청이 “image/jpeg” 값과 함께 response-content-type 요청 매개변수를 전달해야 한다고 가정합니다. `response-content-type` 매개변수는 요청 매개변수이며 요청이 시작될 때 urlencode가 필요합니다(urlencode된 값: `response-content-type=image%2Fjpeg`). 따라서 Policy를 설정할 때 "image/jpeg"도 인코딩(urlencode)해야 하며 "image%2Fjpeg"를 입력해야 합니다.

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
### HTTPS 요청만 허용(cos:secure-transport)

#### 조건 키 cos:secure-transport

조건 키 `cos:secure-transport`를 사용하여 HTTPS 프로토콜 사용 요청 제한

#### 예시1: HTTPS를 사용하도록 다운로드 요청 제한

버킷 examplebucket-1250000000을 소유하고 uin이 100000000001인 루트 계정이 다음 버킷 정책을 사용하여 uin이 100000000002인 서브 계정에서 보낸 HTTPS 기반 GetObject 요청만 허용한다고 가정합니다.

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

#### 예시2: 비 HTTPS 요청 거부

버킷 examplebucket-1250000000을 소유하고 uin이 100000000001인 루트 계정이 다음 버킷 정책을 사용하여 uin이 1000000000002인 서브 계정에서 보낸 비 HTTPS 요청을 거부한다고 가정합니다.

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
### 지정된 스토리지 클래스 설정 허용(cos:x-cos-storage-class)

#### 요청 헤더 x-cos-storage-class

요청 헤더 `x-cos-storage-class`를 사용하여 객체를 업로드할 때 객체의 스토리지 클래스를 지정하거나 수정할 수 있습니다.

#### 조건 키 cos:x-cos-storage-class

조건 키 `cos:x-cos-storage-class`를 사용하여 요청 헤더 `x-cos-storage-class`를 제한하여 스토리지 클래스 수정 요청을 제한할 수 있습니다.

COS의 스토리지 클래스 필드에는 STANDARD, MAZ_STANDARD, STANDARD_IA, MAZ_STANDARD_IA, INTELLIGENT_TIERING, MAZ_INTELLIGENT_TIERING, ARCHIVE 및 DEEP_ARCHIVE가 있습니다.

#### 예시1: PutObject 요청 시 스토리지 클래스를 반드시 STANDARD로 설정

버킷 examplebucket-1250000000을 소유하는 uin이 100000000001인 루트 계정이 다음 버킷 정책을 사용하여 값이 STANDARD인 x-cos-storage-class 헤더를 전달하기 위해 uin이 100000000002인 서브 계정에서 보낸 PutObject 요청을 제한한다고 가정합니다.

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
### 지정된 버킷/객체 ACL 설정 허용(cos:x-cos-acl)

#### 요청 헤더 x-cos-acl

객체를 업로드하거나 버킷을 생성할 때 요청 헤더 `x-cos-acl`을 사용하여 ACL을 지정하거나 객체 또는 버킷 ACL을 수정할 수 있습니다. ACL에 대한 자세한 내용은 [ACL](https://intl.cloud.tencent.com/document/product/436/30583)을 참고하십시오.

- 버킷용 사전 설정 ACL: `private`, `public-read`, `public-read-write`, `authenticated-read`.
- 객체에 대한 사전 설정 ACL: `default`, `private`, `public-read`, `authenticated-read`, `bucket-owner-read`, `bucket-owner-full-control`.

#### 조건 키 cos:x-cos-acl

조건 키 `cos:x-cos-acl`을 사용하여 요청 헤더 `x-cos-acl`을 제한하고 객체/버킷 ACL 수정 요청을 제한할 수 있습니다.

#### 예시1: PutObject 요청에서 객체 ACL을 비공개로 설정 필요

examplebucket-1250000000 버킷을 소유하는 uin 100000000001의 루트 계정이 다음 버킷 정책을 사용하여 uin이 100000000002인 서브 계정을 제한하여 프라이빗 객체만 업로드한다고 가정합니다. 정책은 모든 PutObject 요청이 `private` 값을 가진 x-cos-acl 헤더를 전달하도록 요구합니다.

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
### 지정된 디렉터리에서만 객체 나열 허용(cos:prefix)

#### 조건 키 cos:prefix

조건 키 `cos:prefix`를 사용하여 요청 매개변수 prefix를 제한할 수 있습니다.


>! prefix 값에 중국어 및 `/`와 같은 특수 문자가 포함된 경우 버킷 정책에 쓰기 전에 값을 인코딩(urlencode)해야 합니다.
>

#### 예시1: 버킷의 지정된 디렉터리에 있는 객체만 나열 허용

버킷 examplebucket-1250000000을 소유하는 uin이 100000000001인 루트 계정이 다음 버킷 정책을 사용하여 버킷의 folder1 디렉터리에 있는 객체만 나열하도록 uin이 100000000002인 서브 계정을 제한한다고 가정합니다. 정책에서는 모든 GetBucket 요청이 값 “folder1”과 함께 prefix 매개변수를 전달해야 합니다.


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
### 지정된 버전의 TLS 프로토콜만 사용 허용(cos:tls-version)

#### 조건 키 cos:tls-version

조건 키 `cos:tls-version`을 사용하여 HTTPS 요청의 TLS 버전을 제한할 수 있습니다. 해당 값은 Numric 유형이며 1.0, 1.1 또는 1.2와 같은 부동 소수점을 지원합니다.


#### 예시1: TLS v1.2를 사용하는 HTTP 요청만 승인


|요청 시나리오   |예상 결과|
|---|---|
|TLS v1.0을 사용한 HTTPS 요청|403, 실패|
|TLS v1.2를 사용한 HTTPS 요청|200, 성공|

정책 예시는 다음과 같습니다.

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


#### 예시2: v1.2 이전의 TLS를 사용하는 HTTP 요청 거부

|요청 시나리오  |  예상 결과   |
|---|---|
|TLS v1.0을 사용한 HTTPS 요청|    403, 실패   |
|TLS v1.2를 사용한 HTTPS 요청|    200, 성공   |


정책 예시는 다음과 같습니다.


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
### 버킷 생성 시 지정된 버킷 태그 강제 설정(qcs:request_tag)

>?
>request_tag 조건 키는 PutBucket 및 PutBucketTagging 작업에만 적용되며 GetService, PutObject 또는 PutObjectTagging에는 적용되지 않습니다.
>


#### 조건 키 qcs:request_tag

조건 키 `qcs:request_tag`를 사용하여 PutBucket 또는 PutBucketTagging 요청을 시작할 때 사용자가 지정된 버킷 태그를 포함하도록 제한할 수 있습니다.

#### 예시: 사용자가 버킷을 생성할 때 지정된 버킷 태그를 포함하도록 제한

많은 사용자가 버킷 태그를 사용하여 버킷을 관리할 수 있습니다. 다음 정책 예시는 사용자가 버킷 생성 시 지정된 버킷 태그 `<a,b>` 및 `<c,d>`를 설정한 후에만 권한을 얻을 수 있음을 나타냅니다.

여러 버킷 태그를 설정할 수 있습니다. 각기 다른 버킷 태그 키/값 및 태그 수량은 각각 다른 조합으로 사용됩니다. 요청 양식 세트 A에서 사용자가 여러 매개변수 값을 가지고 있고 조건 양식 세트 B에 지정된 여러 매개변수 값을 가지고 있다고 가정합니다. 이 조건 키를 통해 사용자는 for_any_value 및 for_all_value 한정어의 다양한 조합을 사용하여 다른 의미를 나타낼 수 있습니다.
- `for_any_value:string_equal`은 A와 B가 교차하는 경우 요청이 적용됨을 나타냅니다.
- `for_all_value:string_equal`은 A가 B의 subset인 경우 요청이 적용됨을 나타냅니다.

`for_any_value:string_equal`을 사용하는 경우 해당 정책 및 요청은 다음과 같습니다.

|요청 시나리오     |예상 결과|
|---|---|
|PutBucket, 요청 헤더 `x-cos-tagging: a=b&c=d`|200, 성공|
|PutBucket, 요청 헤더 `x-cos-tagging: a=b`|200, 성공|
|PutBucket, 요청 헤더 `x-cos-tagging: a=b&c=d&e=f`|200, 성공|

정책 예시는 다음과 같습니다.

```
{
    "version": "2.0",
    "statement": [
        {
            "principal":{
                "qcs":[
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


`for_all_value:string_equal`을 사용하는 경우 해당 정책 및 요청은 다음과 같습니다.



|요청 시나리오   |예상 결과|
|---|---|
|PutBucket, 요청 헤더 `x-cos-tagging: a=b&c=d`|200, 성공|
|PutBucket, 요청 헤더 `x-cos-tagging: a=b`|200, 성공|
|PutBucket, 요청 헤더 `x-cos-tagging: a=b&c=d&e=f`|403, 실패|


정책 예시는 다음과 같습니다.

```
{
    "version": "2.0",
    "statement": [
        {
            "principal":{
                "qcs":[
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



