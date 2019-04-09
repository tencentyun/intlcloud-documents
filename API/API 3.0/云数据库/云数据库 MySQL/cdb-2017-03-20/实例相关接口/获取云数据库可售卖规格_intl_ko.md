## 1. API 설명

API 요청 도메인 이름: cdb.tencentcloudapi.com.

이 API(DescribeDBZoneConfig)는 생성 가능한 데이터베이스 지역별 판매 가능 사양 구성을 조회하는 데 사용됩니다.

기본적 API 요청 빈도 제한: 20회/초.

주의: 이 API는 금융 지역을 지원합니다. 금융 지역과 비금융 지역은 격리되어 있고 서로 통하지 않아서, 공통 매개변수 Region이 금융 지역 도메인(예: ap-shanghai-fsi)일 경우, 금융 지역의 도메인 이름을 동시에 지정해야 하며, Region의 도메인과 일치시키는 것이 가장 좋습니다. 예: cdb.ap-shanghai-fsi.tencentcloudapi.com.



## 2. 입력 매개변수

다음 요청 매개변수 리스트에는 API 요청 매개변수 및 일부 공통 매개변수만 나열되며, 완전한 공통 매개변수 리스트는 [공통 요청 매개변수](/document/api/236/15833)를 참조하십시오.

| 매개변수 이름 | 필수 항목 여부 | 유형 | 설명 |
|---------|---------|---------|---------|
| Action | 예 | String | 공통 매개변수, 이 API 값: DescribeDBZoneConfig |
| Version | 예 | String | 공통 매개변수, 이 API 선택 값: 2017-03-20 |
| Region | 아니요 | String | 공통 매개변수, 자세한 내용은 제품의 지원되는 [지역 리스트](/document/api/236/15833#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)를 참조하십시오. |

## 3. 출력 매개변수

| 매개변수 이름 | 유형 | 설명 |
|---------|---------|---------|
| TotalCount | Integer | 판매 가능 지역 구성 수량 |
| Items | Array of [RegionSellConf](/document/api/236/15878#RegionSellConf) | 판매 가능 지역 구성 세부 정보 |
| RequestId | String | 유일한 요청 ID, 매회 요청 시마다 반환됩니다. 문제를 찾을 경우 해당 요청의 RequestId를 제공해야 합니다. |

## 4. 예시

### 예시1 데이터베이스 인스턴스 판매 가능 사양 획득

#### 입력 예시

```
https://cdb.tencentcloudapi.com/?Action=DescribeDBZoneConfig
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response": {
        "TotalCount": 17,
        "Items": [
            {
                "RegionName": "광저우",
                "Area": "중국 화남",
                "IsDefaultRegion": 0,
                "Region": "ap-guangzhou",
                "ZonesConf": [
                    {
                        "Status": 1,
                        "ZoneName": "광저우 2지역",
                        "IsCustom": true,
                        "IsSupportDr": true,
                        "IsSupportVpc": true,
                        "HourInstanceSaleMaxNum": 30,
                        "IsDefaultZone": false,
                        "IsBm": false,
                        "PayType": [
                            "0",
                            "1",
                            "2"
                        ],
                        "DrZone": [
                            "ap-shanghai-1",
                            "ap-shanghai-2",
                            "ap-beijing-1",
                            "ap-beijing-2",
                            "ap-guangzhou-open-1",
                            "ap-guangzhou-3",
                            "ap-guangzhou-4",
                            "ap-chengdu-1",
                            "ap-chengdu-2"
                        ],
                        "ProtectMode": [
                            "0",
                            "1",
                            "2"
                        ],
                        "ZoneConf": {
                            "DeployMode": [
                                0
                            ],
                            "MasterZone": [
                                "ap-guangzhou-2"
                            ],
                            "SlaveZone": [
                                "ap-guangzhou-2"
                            ],
                            "BackupZone": [
                                "ap-guangzhou-2"
                            ]
                        },
                        "Zone": "ap-guangzhou-2",
                        "SellType": [
                            {
                                "TypeName": "Z3",
                                "EngineVersion": [
                                    "5.5",
                                    "5.6",
                                    "5.7"
                                ],
                                "Configs": [
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 1000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 1000,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 수만 명의 미니 게임 응용프로그램 또는 백만 명 규모의 도구 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 2000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 2400,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 수만 명의 미니 게임 응용프로그램 또는 백만 명 규모의 도구 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 4000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 4400,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 십만 명 이상 규모의 중형 게임 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 8000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 7200,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 백만 명 규모의 대형 게임 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 16000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 18000,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 백만 명 규모의 대형 게임 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 32000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 25000,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 백만 명 규모의 대형 게임 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 64000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 37689,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 백만 명 규모의 대형 게임 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 96000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 40919,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 백만 명 규모의 대형 게임 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 128000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 61378,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 백만 명 규모의 대형 게임 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 244000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 122755,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 백만 명 규모의 대형 게임 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 488000,
                                        "Cpu": 0,
                                        "VolumeMin": 6000,
                                        "VolumeMax": 6000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 245509,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 백만 명 규모의 대형 게임 응용프로그램",
                                        "Status": 0
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Status": 1,
                        "ZoneName": "광저우 3지역",
                        "IsCustom": true,
                        "IsSupportDr": true,
                        "IsSupportVpc": true,
                        "HourInstanceSaleMaxNum": 30,
                        "IsDefaultZone": false,
                        "IsBm": false,
                        "PayType": [
                            "0",
                            "1"
                        ],
                        "DrZone": [
                            "ap-shanghai-1",
                            "ap-shanghai-2",
                            "ap-beijing-1",
                            "ap-beijing-2",
                            "ap-guangzhou-open-1",
                            "ap-guangzhou-2",
                            "ap-guangzhou-4",
                            "ap-seoul-1",
                            "ap-chengdu-1",
                            "ap-chengdu-2"
                        ],
                        "ProtectMode": [
                            "0",
                            "1",
                            "2"
                        ],
                        "ZoneConf": {
                            "DeployMode": [
                                0
                            ],
                            "MasterZone": [
                                "ap-guangzhou-3"
                            ],
                            "SlaveZone": [
                                "ap-guangzhou-3"
                            ],
                            "BackupZone": [
                                "ap-guangzhou-3"
                            ]
                        },
                        "Zone": "ap-guangzhou-3",
                        "SellType": [
                            {
                                "TypeName": "Z3",
                                "EngineVersion": [
                                    "5.5",
                                    "5.6",
                                    "5.7"
                                ],
                                "Configs": [
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 1000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 1000,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 수만 명의 미니 게임 응용프로그램 또는 백만 명 규모의 도구 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 2000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 2400,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 수만 명의 미니 게임 응용프로그램 또는 백만 명 규모의 도구 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 4000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 4400,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 십만 명 이상 규모의 중형 게임 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 8000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 7200,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 백만 명 규모의 대형 게임 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 16000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 18000,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 백만 명 규모의 대형 게임 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 32000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 25000,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 백만 명 규모의 대형 게임 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 64000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 37689,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 백만 명 규모의 대형 게임 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 96000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 40919,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 백만 명 규모의 대형 게임 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 128000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 61378,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 백만 명 규모의 대형 게임 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 244000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 122755,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 백만 명 규모의 대형 게임 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 488000,
                                        "Cpu": 0,
                                        "VolumeMin": 6000,
                                        "VolumeMax": 6000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 245509,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 백만 명 규모의 대형 게임 응용프로그램",
                                        "Status": 0
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Status": 4,
                        "ZoneName": "광저우 1지역",
                        "IsCustom": true,
                        "IsSupportDr": false,
                        "IsSupportVpc": true,
                        "HourInstanceSaleMaxNum": 30,
                        "IsDefaultZone": false,
                        "IsBm": false,
                        "PayType": [
                            "0",
                            "1",
                            "2"
                        ],
                        "ProtectMode": [
                            "0",
                            "1",
                            "2"
                        ],
                        "ZoneConf": {
                            "DeployMode": [
                                0
                            ],
                            "MasterZone": [
                                "ap-guangzhou-1"
                            ],
                            "SlaveZone": [
                                "ap-guangzhou-1"
                            ],
                            "BackupZone": [
                                "ap-guangzhou-1"
                            ]
                        },
                        "Zone": "ap-guangzhou-1",
                        "SellType": [
                            {
                                "TypeName": "Z3",
                                "EngineVersion": [
                                    "5.5",
                                    "5.6",
                                    "5.7"
                                ],
                                "Configs": [
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 360,
                                        "Cpu": 0,
                                        "VolumeMin": 10,
                                        "VolumeMax": 500,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 120,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 수만 명의 미니 게임 응용프로그램 또는 백만 명 규모의 도구 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 1000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 500,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 1000,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 수만 명의 미니 게임 응용프로그램 또는 백만 명 규모의 도구 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 2000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 500,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 2400,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 수만 명의 미니 게임 응용프로그램 또는 백만 명 규모의 도구 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 4000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 1000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 4400,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 십만 명 이상 규모의 중형 게임 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 8000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 1000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 7200,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 백만 명 규모의 대형 게임 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 12000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 1000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 15000,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 백만 명 규모의 대형 게임 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 16000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 1000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 18000,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 백만 명 규모의 대형 게임 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 24000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 1000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 23000,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 백만 명 규모의 대형 게임 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 48000,
                                        "Cpu": 0,
                                        "VolumeMin": 1000,
                                        "VolumeMax": 1000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 37000,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 백만 명 규모의 대형 게임 응용프로그램",
                                        "Status": 0
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Status": 2,
                        "ZoneName": "광저우 4지역",
                        "IsCustom": true,
                        "IsSupportDr": true,
                        "IsSupportVpc": true,
                        "HourInstanceSaleMaxNum": 30,
                        "IsDefaultZone": true,
                        "IsBm": false,
                        "PayType": [
                            "0",
                            "1",
                            "2"
                        ],
                        "DrZone": [
                            "ap-shanghai-1",
                            "ap-shanghai-2",
                            "ap-shanghai-3",
                            "ap-beijing-1",
                            "ap-beijing-2",
                            "ap-guangzhou-open-1",
                            "ap-guangzhou-2",
                            "ap-guangzhou-3",
                            "na-ashburn-1",
                            "ap-chengdu-1",
                            "ap-chengdu-2",
                            "ap-bangkok-1"
                        ],
                        "ProtectMode": [
                            "0",
                            "1",
                            "2"
                        ],
                        "ZoneConf": {
                            "DeployMode": [
                                0
                            ],
                            "MasterZone": [
                                "ap-guangzhou-4"
                            ],
                            "SlaveZone": [
                                "ap-guangzhou-4"
                            ],
                            "BackupZone": [
                                "ap-guangzhou-4"
                            ]
                        },
                        "Zone": "ap-guangzhou-4",
                        "SellType": [
                            {
                                "TypeName": "Z3",
                                "EngineVersion": [
                                    "5.5",
                                    "5.6",
                                    "5.7"
                                ],
                                "Configs": [
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 1000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 1000,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 수만 명의 미니 게임 응용프로그램 또는 백만 명 규모의 도구 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 2000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 2400,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 수만 명의 미니 게임 응용프로그램 또는 백만 명 규모의 도구 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 4000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 4400,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 십만 명 이상 규모의 중형 게임 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 8000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 7200,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 백만 명 규모의 대형 게임 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 16000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 18000,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 백만 명 규모의 대형 게임 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 32000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 25000,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 백만 명 규모의 대형 게임 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 64000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 37689,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 백만 명 규모의 대형 게임 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 96000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 40919,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 백만 명 규모의 대형 게임 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 128000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 61378,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 백만 명 규모의 대형 게임 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 244000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 122755,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 백만 명 규모의 대형 게임 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 488000,
                                        "Cpu": 0,
                                        "VolumeMin": 6000,
                                        "VolumeMax": 6000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 245509,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 백만 명 규모의 대형 게임 응용프로그램",
                                        "Status": 0
                                    }
                                ]
                            }
                        ]
                    }
                ]
            },
            {
                "RegionName": "방콕",
                "Area": "아시아 태평양 지역",
                "IsDefaultRegion": 0,
                "Region": "ap-bangkok",
                "ZonesConf": [
                    {
                        "Status": 2,
                        "ZoneName": "방콕 1지역",
                        "IsCustom": true,
                        "IsSupportDr": true,
                        "IsSupportVpc": true,
                        "HourInstanceSaleMaxNum": 30,
                        "IsDefaultZone": true,
                        "IsBm": false,
                        "PayType": [
                            "0",
                            "1"
                        ],
                        "DrZone": [
                            "ap-guangzhou-4"
                        ],
                        "ProtectMode": [
                            "0",
                            "1",
                            "2"
                        ],
                        "ZoneConf": {
                            "DeployMode": [
                                0
                            ],
                            "MasterZone": [
                                "ap-bangkok-1"
                            ],
                            "SlaveZone": [
                                "ap-bangkok-1"
                            ],
                            "BackupZone": [
                                "ap-bangkok-1"
                            ]
                        },
                        "Zone": "ap-bangkok-1",
                        "SellType": [
                            {
                                "TypeName": "Z3",
                                "EngineVersion": [
                                    "5.5",
                                    "5.6",
                                    "5.7"
                                ],
                                "Configs": [
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 1000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 1000,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 수만 명의 미니 게임 응용프로그램 또는 백만 명 규모의 도구 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 2000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 2400,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 수만 명의 미니 게임 응용프로그램 또는 백만 명 규모의 도구 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 4000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 4400,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 십만 명 이상 규모의 중형 게임 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 8000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 7200,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 백만 명 규모의 대형 게임 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 16000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 18000,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 백만 명 규모의 대형 게임 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 32000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 25000,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 백만 명 규모의 대형 게임 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 64000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 37689,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 백만 명 규모의 대형 게임 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 96000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 40919,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 백만 명 규모의 대형 게임 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 128000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 61378,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 백만 명 규모의 대형 게임 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 244000,
                                        "Cpu": 0,
                                        "VolumeMin": 25,
                                        "VolumeMax": 3000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 122755,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 백만 명 규모의 대형 게임 응용프로그램",
                                        "Status": 0
                                    },
                                    {
                                        "Device": "Z3",
                                        "Type": "고가용 버전",
                                        "CdbType": "CUSTOM",
                                        "Memory": 488000,
                                        "Cpu": 0,
                                        "VolumeMin": 6000,
                                        "VolumeMax": 6000,
                                        "VolumeStep": 5,
                                        "Connection": 0,
                                        "Qps": 245509,
                                        "Iops": 0,
                                        "Info": "일일 활성 사용자 백만 명 규모의 대형 게임 응용프로그램",
                                        "Status": 0
                                    }
                                ]
                            }
                        ]
                    }
                ]
            }
        ],
        "RequestId": "f1ccdafe-6803-455e-bb84-e33c08ba8247"
    }
}
```


## 5. 개발자 리소스

### API Explorer

**이 도구는 온라인 호출, 서명 인증, SDK 코드 생성 및 빠른 인덱스 API 등의 기능을 제공하여, 클라우드 API의 어려움을 크게 줄일 수 있으므로 사용을 추천합니다.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cdb&Version=2017-03-20&Action=DescribeDBZoneConfig)

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
| InvalidParameter | 매개변수 오류. |

