## 1. API 설명

API 요청 도메인 이름: cdb.tencentcloudapi.com.

이 API(DescribeDeviceMonitorInfo)는 데이터베이스 물리적 기기의 당일 모니터링 정보를 조회하는 데 사용하며, 현재는 488G 메모리 또는 6T 디스크의 인스턴스 조회만 지원합니다.

기본적 API 요청 빈도 제한: 20회/초.

주의: 이 API는 금융 지역을 지원합니다. 금융 지역과 비금융 지역은 격리되어 있고 서로 통하지 않아서, 공통 매개변수 Region이 금융 지역 도메인(예: ap-shanghai-fsi)일 경우, 금융 지역의 도메인 이름을 동시에 지정해야 하며, Region의 도메인과 일치시키는 것이 가장 좋습니다. 예: cdb.ap-shanghai-fsi.tencentcloudapi.com.



## 2. 입력 매개변수

다음 요청 매개변수 리스트에는 API 요청 매개변수 및 일부 공통 매개변수만 나열되며, 완전한 공통 매개변수 리스트는 [공통 요청 매개변수](/document/api/236/15833)를 참조하십시오.

| 매개변수 이름 | 필수 항목 여부 | 유형 | 설명 |
|---------|---------|---------|---------|
| Action | 예 | String | 공통 매개변수, 이 API 값: DescribeDeviceMonitorInfo |
| Version | 예 | String | 공통 매개변수, 이 API 선택 값: 2017-03-20 |
| Region | 아니요 | String | 공통 매개변수, 자세한 내용은 제품의 지원되는 [지역 리스트](/document/api/236/15833#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)를 참조하십시오. |
| InstanceId | 예 | String | 인스턴스 ID, 형식 예: cdb-c1nl9rpv. TencentDB 콘솔 페이지에 표시된 인스턴스 ID와 동일합니다. |
| Count | 아니요 | Integer | 당일 최근 Count개 5분 세분성 모니터링 데이터를 반환합니다. 최소값은 1, 최대값은 288입니다. 해당 매개변수를 전달하지 않으면 기본적으로 당일의 모든 5분 세분성 모니터링 데이터를 반환합니다. |

## 3. 출력 매개변수

| 매개변수 이름 | 유형 | 설명 |
|---------|---------|---------|
| Cpu | [DeviceCpuInfo](/document/api/236/15878#DeviceCpuInfo) | 인스턴스 CPU 모니터링 데이터 |
| Mem | [DeviceMemInfo](/document/api/236/15878#DeviceMemInfo) | 인스턴스 메모리 모니터링 데이터 |
| Net | [DeviceNetInfo](/document/api/236/15878#DeviceNetInfo) | 인스턴스 네트워크 모니터링 데이터 |
| Disk | [DeviceDiskInfo](/document/api/236/15878#DeviceDiskInfo) | 인스턴스 디스크 모니터링 데이터 |
| RequestId | String | 유일한 요청 ID, 매회 요청 시마다 반환됩니다. 문제를 찾을 경우 해당 요청의 RequestId를 제공해야 합니다. |

## 4. 예시

### 예시1 인스턴스의 물리적 기기 모니터링 정보 획득

#### 입력 예시

```
https://cdb.tencentcloudapi.com/?Action=DescribeDeviceMonitorInfo
&InstanceId=cdb-uns231ns
&Count=2
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response": {
        "Cpu": {
            "Load": [
                174,
                169
            ],
            "Rate": [
                {
                    "CpuCore": 0,
                    "Rate": [
                        4,
                        5
                    ]
                },
                {
                    "CpuCore": 0,
                    "Rate": [
                        7,
                        7
                    ]
                },
                {
                    "CpuCore": 1,
                    "Rate": [
                        15,
                        7
                    ]
                },
                {
                    "CpuCore": 2,
                    "Rate": [
                        7,
                        7
                    ]
                },
                {
                    "CpuCore": 3,
                    "Rate": [
                        6,
                        5
                    ]
                },
                {
                    "CpuCore": 4,
                    "Rate": [
                        4,
                        2
                    ]
                },
                {
                    "CpuCore": 5,
                    "Rate": [
                        4,
                        5
                    ]
                },
                {
                    "CpuCore": 6,
                    "Rate": [
                        7,
                        5
                    ]
                },
                {
                    "CpuCore": 7,
                    "Rate": [
                        7,
                        9
                    ]
                },
                {
                    "CpuCore": 8,
                    "Rate": [
                        8,
                        8
                    ]
                },
                {
                    "CpuCore": 9,
                    "Rate": [
                        6,
                        4
                    ]
                },
                {
                    "CpuCore": 10,
                    "Rate": [
                        4,
                        14
                    ]
                },
                {
                    "CpuCore": 11,
                    "Rate": [
                        2,
                        2
                    ]
                },
                {
                    "CpuCore": 12,
                    "Rate": [
                        6,
                        3
                    ]
                },
                {
                    "CpuCore": 13,
                    "Rate": [
                        10,
                        14
                    ]
                },
                {
                    "CpuCore": 14,
                    "Rate": [
                        12,
                        6
                    ]
                },
                {
                    "CpuCore": 15,
                    "Rate": [
                        5,
                        2
                    ]
                },
                {
                    "CpuCore": 16,
                    "Rate": [
                        4,
                        2
                    ]
                },
                {
                    "CpuCore": 17,
                    "Rate": [
                        2,
                        4
                    ]
                },
                {
                    "CpuCore": 18,
                    "Rate": [
                        4,
                        6
                    ]
                },
                {
                    "CpuCore": 19,
                    "Rate": [
                        14,
                        9
                    ]
                },
                {
                    "CpuCore": 20,
                    "Rate": [
                        6,
                        6
                    ]
                },
                {
                    "CpuCore": 21,
                    "Rate": [
                        5,
                        5
                    ]
                },
                {
                    "CpuCore": 22,
                    "Rate": [
                        3,
                        12
                    ]
                },
                {
                    "CpuCore": 23,
                    "Rate": [
                        2,
                        2
                    ]
                }
            ]
        },
        "Mem": {
            "Total": [
                65716676,
                65716676
            ],
            "Used": [
                57163160,
                57158148
            ]
        },
        "Net": {
            "Conn": [
                133,
                130
            ],
            "PackageIn": [
                960,
                960
            ],
            "PackageOut": [],
            "FlowIn": [
                150,
                112
            ],
            "FlowOut": [
                1342,
                1260
            ]
        },
        "Disk": {
            "Read": [
                0,
                0
            ],
            "Write": [
                740,
                797
            ],
            "IoRatioPerSec": [
                0,
                0
            ],
            "IoWaitTime": [
                61,
                65
            ]
        },
        "RequestId": "85b295bb-8f43-ce01-e35f-5a02e2beeeac"
    }
}
```


## 5. 개발자 리소스

### API Explorer

**이 도구는 온라인 호출, 서명 인증, SDK 코드 생성 및 빠른 인덱스 API 등의 기능을 제공하여, 클라우드 API의 어려움을 크게 줄일 수 있으므로 사용을 추천합니다.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cdb&Version=2017-03-20&Action=DescribeDeviceMonitorInfo)

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

다음은 API 비즈니스 로직과 관련된 오류 코드만 나열하며 다른 오류 코드는 [공통 오류 코드](/document/api/236/15835#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)를 참조하십시오.

| 오류 코드 | 설명 |
|---------|---------|
| CdbError | 백 엔드 오류 또는 프로세스 오류. |
| FailedOperation.StatusConflict | 태스크 상태 충돌. |
| InvalidParameter | 매개변수 오류. |
| InvalidParameter.InstanceNotFound | 인스턴스가 존재하지 않음. |
| OperationDenied | 작업이 허용되지 않음. |

