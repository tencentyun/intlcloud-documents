## 1. API 설명

API 요청 도메인 이름: redis.tencentcloudapi.com.

이 API는 지정된 가용 영역 및 인스턴스 유형에서 TencentDB for Redis의 판매 사양을 조회하는 데에 사용됩니다. 화이트리스트 구매 리스트에 사용자가 없는 경우, 이 가용 영역 또는 이 유형의 판매 사양 세부 정보를 조회할 수 없습니다. 어느 지역의 화이트리스트를 구매 신청하면 티켓을 신청할 수 있습니다. 어느 지역의 회이트리스트를 신청하려면 티켓을 제출할 수 있습니다.

기본적 API 요청 빈도 제한: 20회/초.

주의: 이 API는 금융 지역을 지원합니다. 금융 지역과 비금융 지역은 격리되어 있고 서로 통하지 않아서, 공통 매개변수 Region이 금융 지역 도메인(예: ap-shanghai-fsi)일 경우, 금융 지역의 도메인 이름을 동시에 지정해야 하며, Region의 도메인과 일치시키는 것이 가장 좋습니다. 예: redis.ap-shanghai-fsi.tencentcloudapi.com.



## 2. 입력 매개변수

다음 요청 매개변수 리스트에는 API 요청 매개변수 및 일부 공통 매개변수만 나열되며, 완전한 공통 매개변수 리스트는 [공통 요청 매개변수](/document/api/239/20005)를 참조하십시오.

| 매개변수 이름 | 필수 여부 | 유형 | 설명 |
|---------|---------|---------|---------|
| Action | 예 | String | 공통 매개변수, 이 API 값: DescribeProductInfo |
| Version | 예 | String | 공통 매개변수, 이 API 값: 2018-04-12 |
| Region | 예 | String | 공통 매개변수, 자세한 내용은 제품이 지원되는 [지역 리스트](/document/api/239/20005#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)를 참조하십시오. |

## 3. 출력 매개변수

| 매개변수 이름 | 유형 | 설명 |
|---------|---------|---------|
| RegionSet | Array of [RegionConf](/document/api/239/20022#RegionConf) | 지역 구매 정보|
| RequestId | String | 유일한 요청 ID, 매회 요청 시마다 반환됩니다. 문제를 찾을 경우 해당 요청의 RequestId를 제공해야 합니다. |

## 4. 예시

### 예시 1 요청 예시

#### 입력 예시

```
https://redis.tencentcloudapi.com/?Action=DescribeProductInfo
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response":{
        "RegionSet":[
            {
                "RegionId":"ap-guangzhou",
                "RegionName":"광저우",
                "RegionShortName":"GZ",
                "Area":"화남 지역",
                "ZoneSet":[
                    {
                        "ZoneId":"ap-guangzhou-2",
                        "ZoneName":"광저우 2지역",
                        "IsSaleout":false,
                        "IsDefault":false,
                        "NetWorkType":[
                            "basenet",
                            "vpcnet"
                        ],
                        "ProductSet":[
                            {
                                "Type":7,
                                "TypeName":"Redis 클러스터 버전",
                                "MinBuyNum":1,
                                "MaxBuyNum":10,
                                "Saleout":false,
                                "Engine":"Redis 커뮤니티 버전",
                                "Version":"Redis 4.0",
                                "TotalSize":[
                                    "12",
                                    "20",
                                    "32",
                                    "64",
                                    "96",
                                    "128",
                                    "256",
                                    "384",
                                    "512",
                                    "768",
                                    "1024",
                                    "2048",
                                    "3072",
                                    "4096"
                                ],
                                "ShardSize":[
                                    "4",
                                    "8",
                                    "12",
                                    "16",
                                    "20",
                                    "24",
                                    "32"
                                ],
                                "ReplicaNum":[
                                    "1",
                                    "2",
                                    "3",
                                    "4",
                                    "5"
                                ],
                                "ShardNum":[
                                    "3",
                                    "5",
                                    "8",
                                    "12",
                                    "16",
                                    "24",
                                    "32",
                                    "40",
                                    "48",
                                    "64",
                                    "80",
                                    "96",
                                    "128"
                                ],
                                "PayMode":"1",
                                "EnableRepicaReadOnly":true
                            },
                            {
                                "Type":4,
                                "TypeName":"CKV 클러스터 버전",
                                "MinBuyNum":1,
                                "MaxBuyNum":10,
                                "Saleout":false,
                                "Engine":"Tencent Cloud CKV",
                                "Version":"Redis 3.2",
                                "TotalSize":[
                                    "12",
                                    "20",
                                    "32",
                                    "64",
                                    "96",
                                    "128",
                                    "256",
                                    "384",
                                    "512",
                                    "768",
                                    "1024",
                                    "2048",
                                    "3072",
                                    "4096"
                                ],
                                "ShardSize":[
                                    "4",
                                    "8",
                                    "16",
                                    "24",
                                    "32",
                                    "48",
                                    "64",
                                    "80",
                                    "96",
                                    "128",
                                    "160",
                                    "192",
                                    "256",
                                    "320",
                                    "384"
                                ],
                                "ReplicaNum":[
                                    "1",
                                    "2",
                                    "3",
                                    "4",
                                    "5"
                                ],
                                "ShardNum":[
                                    "3",
                                    "5",
                                    "8",
                                    "12",
                                    "16",
                                    "24",
                                    "32",
                                    "40",
                                    "48",
                                    "64",
                                    "80",
                                    "96",
                                    "128"
                                ],
                                "PayMode":"1",
                                "EnableRepicaReadOnly":false
                            },
                            {
                                "Type":2,
                                "TypeName":"Redis 마스터/슬레이브 버전",
                                "MinBuyNum":1,
                                "MaxBuyNum":10,
                                "Saleout":false,
                                "Engine":"Redis 커뮤니티 버전",
                                "Version":"Redis 2.8",
                                "TotalSize":[
                                    "1",
                                    "2",
                                    "4",
                                    "8",
                                    "12",
                                    "16",
                                    "20",
                                    "24",
                                    "32",
                                    "40",
                                    "48",
                                    "60",
                                    "0.25"
                                ],
                                "ShardSize":[
                                    "1",
                                    "2",
                                    "4",
                                    "8",
                                    "12",
                                    "16",
                                    "20",
                                    "24",
                                    "32",
                                    "40",
                                    "48",
                                    "60",
                                    "0.25"
                                ],
                                "ReplicaNum":[
                                    "1"
                                ],
                                "ShardNum":[
                                    "1"
                                ],
                                "PayMode":"1",
                                "EnableRepicaReadOnly":false
                            },
                            {
                                "Type":5,
                                "TypeName":"Redis 스탠드 얼로운",
                                "MinBuyNum":1,
                                "MaxBuyNum":10,
                                "Saleout":false,
                                "Engine":"Redis 커뮤니티 버전",
                                "Version":"Redis 2.8",
                                "TotalSize":[
                                    "1",
                                    "2",
                                    "4",
                                    "8",
                                    "12",
                                    "16",
                                    "20",
                                    "24",
                                    "32",
                                    "40",
                                    "48",
                                    "60"
                                ],
                                "ShardSize":[
                                    "1",
                                    "2",
                                    "4",
                                    "8",
                                    "12",
                                    "16",
                                    "20",
                                    "24",
                                    "32",
                                    "40",
                                    "48",
                                    "60"
                                ],
                                "ReplicaNum":[
                                    "0"
                                ],
                                "ShardNum":[
                                    "1"
                                ],
                                "PayMode":"1",
                                "EnableRepicaReadOnly":false
                            },
                            {
                                "Type":2,
                                "TypeName":"Redis 마스터/슬레이브 버전",
                                "MinBuyNum":1,
                                "MaxBuyNum":10,
                                "Saleout":false,
                                "Engine":"Redis 커뮤니티 버전",
                                "Version":"Redis 2.8",
                                "TotalSize":[
                                    "1",
                                    "2",
                                    "4",
                                    "8",
                                    "12",
                                    "16",
                                    "20",
                                    "24",
                                    "32",
                                    "40",
                                    "48",
                                    "60"
                                ],
                                "ShardSize":[
                                    "1",
                                    "2",
                                    "4",
                                    "8",
                                    "12",
                                    "16",
                                    "20",
                                    "24",
                                    "32",
                                    "40",
                                    "48",
                                    "60"
                                ],
                                "ReplicaNum":[
                                    "1"
                                ],
                                "ShardNum":[
                                    "1"
                                ],
                                "PayMode":"0",
                                "EnableRepicaReadOnly":false
                            },
                            {
                                "Type":3,
                                "TypeName":"CKV 스탠드 얼로운",
                                "MinBuyNum":1,
                                "MaxBuyNum":10,
                                "Saleout":false,
                                "Engine":"Tencent Cloud CKV",
                                "Version":"Redis 3.2",
                                "TotalSize":[
                                    "4",
                                    "8",
                                    "16",
                                    "24",
                                    "32",
                                    "48",
                                    "64",
                                    "80",
                                    "96",
                                    "128",
                                    "160",
                                    "192",
                                    "256",
                                    "320",
                                    "384"
                                ],
                                "ShardSize":[
                                    "4",
                                    "8",
                                    "16",
                                    "24",
                                    "32",
                                    "48",
                                    "64",
                                    "80",
                                    "96",
                                    "128",
                                    "160",
                                    "192",
                                    "256",
                                    "320",
                                    "384"
                                ],
                                "ReplicaNum":[
                                    "0"
                                ],
                                "ShardNum":[
                                    "1"
                                ],
                                "PayMode":"1",
                                "EnableRepicaReadOnly":false
                            }
                        ]
                    }
                ]
            }
        ],
        "RequestId":"3c5730c6-02f2-46fd-8bf1-725b8b608fb9"
    }
}
```


## 5. 개발자 리소스

### API Explorer

**이 도구는 온라인 호출, 서명 인증, SDK 코드 생성 및 빠른 인덱스 API 등의 기능을 제공하여, 클라우드 API의 어려움을 크게 줄일 수 있으므로 사용을 추천합니다.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=redis&Version=2018-04-12&Action=DescribeProductInfo)

### SDK

클라우드 API 3.0은 매칭되는 소프트웨어 개발 키트(SDK)를 제공하고 여러 가지 프로그래밍 언어를 지원하여 더욱 편리한 API 호출이 가능합니다.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. 오류 코드

다음은 API 비즈니스 로직과 관련된 오류 코드만 나열하며 다른 오류 코드는 [공통 오류 코드](/document/api/239/20007#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)를 참조하십시오.

| 오류 코드 | 설명 |
|---------|---------|
| FailedOperation.SystemError | 내부 시스템 오류, 비즈니스와 관련이 없습니다. |
| InvalidParameter | 매개변수 오류 |
| InvalidParameter.EmptyParam | 매개변수가 비어 있습니다. |

