## 1. API 설명

API 요청 도메인 이름: cdb.tencentcloudapi.com.

이 API(DescribeTasks)는 데이터베이스 인스턴스 태스크 리스트 조회에 사용합니다.

기본적 API 요청 빈도 제한: 100회/초.

주의: 이 API는 금융 지역을 지원합니다. 금융 지역과 비금융 지역은 격리되어 있고 서로 통하지 않아서, 공통 매개변수 Region이 금융 지역 도메인(예: ap-shanghai-fsi)일 경우, 금융 지역의 도메인 이름을 동시에 지정해야 하며, Region의 도메인과 일치시키는 것이 가장 좋습니다. 예: cdb.ap-shanghai-fsi.tencentcloudapi.com.



## 2. 입력 매개변수

다음 요청 매개변수 리스트에는 API 요청 매개변수 및 일부 공통 매개변수만 나열되며, 완전한 공통 매개변수 리스트는 [공통 요청 매개변수](/document/api/236/15833)를 참조하십시오.

| 매개변수 이름 | 필수 항목 여부 | 유형 | 설명 |
|---------|---------|---------|---------|
| Action | 예 | String | 공통 매개변수, 이 API 값: DescribeTasks |
| Version | 예 | String | 공통 매개변수, 이 API 선택 값: 2017-03-20 |
| Region | 아니요 | String | 공통 매개변수, 자세한 내용은 제품의 지원되는 [지역 리스트](/document/api/236/15833#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)를 참조하십시오. |
| InstanceId | 아니요 | String | 인스턴스 ID, 형식 예: cdb-c1nl9rpv, TencentDB 콘솔 페이지에 표시된 인스턴스 ID와 동일합니다. [인스턴스 리스트 조회](https://cloud.tencent.com/document/api/236/15872) API를 사용하여 획득할 수 있으며, 그 값은 출력 매개변수 중 필드 InstanceId의 값입니다 |
| AsyncRequestId | 아니요 | String | 비동기화 태스크 요청 ID, CDB 관련 조작 실행 시 반환된 AsyncRequestId입니다. |
| TaskTypes.N | 아니요 | Array of Integer | 태스크 유형, 값을 전달하지 않으면 모든 태스크 유형을 조회합니다. 가능한 값: 1-데이터베이스 롤백, 2-SQL 조작, 3-데이터 가져오기, 5-매개변수 설정, 6-초기화, 7-다시 시작, 8-GTID 시작, 9-읽기 전용 인스턴스 업그레이드, 10-데이터베이스 배치 롤백, 11-마스터 인스턴스 업그레이드, 12-데이터베이스 테이블 삭제, 13-마스터 인스턴스로 전환. |
| TaskStatus.N | 아니요 | Array of Integer | 태스크 상태, 값을 전달하지 않으면 모든 태스크 상태를 조회합니다. 가능한 값: -1-미정의; 0-초기화; 1-실행 중; 2-실행 성공; 3-실행 실패; 4-종료됨, 5-삭제됨, 6-정지됨; |
| StartTimeBegin | 아니요 | String | 첫번째 태스크의 시작 시간, 범위 조회에 사용하며, 시간 형식 예: 2017-12-31 10:40:01 |
| StartTimeEnd | 아니요 | String | 마지막 태스크의 시작 시간, 범위 조회에 사용하며, 시간 형식 예: 2017-12-31 10:40:01 |
| Offset | 아니요 | Integer | 오프셋 기록, 기본값은 0입니다. |
| Limit | 아니요 | Integer | 1회 요청의 반환 수량, 기본값은 20, 최대값은 100입니다. |

## 3. 출력 매개변수

| 매개변수 이름 | 유형 | 설명 |
|---------|---------|---------|
| TotalCount | Integer | 조회 조건에 부합하는 인스턴스 총수 |
| Items | Array of String | 반환된 인스턴스 태스크 정보|
| RequestId | String | 유일한 요청 ID, 매회 요청 시마다 반환됩니다. 문제를 찾을 경우 해당 요청의 RequestId를 제공해야 합니다. |

## 4. 예시

### 예시1 데이터베이스 인스턴스 태스크 리스트 조회

#### 입력 예시

```
https://cdb.tencentcloudapi.com/?Action=DescribeTasks
&InstanceIds.0=cdb-eb2w7dto
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response":{
        "RequestId": "6EF60BEC-0242-43AF-BB20-270359FB54A7",
        "TotalCount":13,
        "Items":[
            {
                "Status":2,
                "Code":0,
                "Data":[
                    {
                        "InstanceId":"cdb-gt70m8aa",
                        "Character_set_server":"utf8",
                        "Lower_case_table_names":"0",
                        "Vport":3306
                    }
                ],
                "JobId":15964,
                "StartTime":"2017-06-27 15:05:33",
                "Progress":100,
                "Message":"인스턴스 초기화 성공",
                "EndTime":"2017-06-27 15:06:36",
                "Type":6
            },
            {
                "Status":3,
                "Code":-5003,
                "Data":[
                    {
                        "Code":3,
                        "InstanceId":"cdb-atjl8gns",
                        "StartTime":"2017-07-21 17:19:30",
                        "Databases":[
                            {
                                "Message":"dial tcp :0: connection refused",
                                "Code":3,
                                "Database":"clear_test"
                            }
                        ],
                        "Message":"dial tcp :0: connection refused",
                        "EndTime":"2017-07-21 17:19:31"
                    }
                ],
                "JobId":51788,
                "StartTime":"2017-07-21 17:19:30",
                "Progress":0,
                "Message":"",
                "EndTime":"2017-07-21 17:19:31",
                "Type":2
            },
            {
                "Status":2,
                "Code":0,
                "Data":[
                    {
                        "InstanceId":"cdb-gt70m8aa",
                        "Before":{
                            "SlaveZoneFirst":160002,
                            "MasterZone":160002,
                            "Memory":1000,
                            "DeployMode":"",
                            "Volume":50,
                            "ProtectMode":"",
                            "SlaveZoneSecond":"",
                            "EngineVersion":"5.6",
                            "CdbType":"CUSTOM"
                        },
                        "After":{
                            "SlaveZoneFirst":160002,
                            "MasterZone":160002,
                            "Memory":2000,
                            "DeployMode":"",
                            "Volume":100,
                            "ProtectMode":"",
                            "SlaveZoneSecond":"",
                            "EngineVersion":"5.6",
                            "CdbType":"CUSTOM"
                        },
                        "DealName":"20170627160000060843141595228010"
                    }
                ],
                "JobId":15967,
                "StartTime":"2017-06-27 15:13:52",
                "Progress":100,
                "Message":"인스턴스 업그레이드 완료",
                "EndTime":"2017-06-27 15:16:57",
                "Type":11
            },
            {
                "Status":2,
                "Code":0,
                "Data":[
                    {
                        "InstanceId":"",
                        "Parameters":[
                            {
                                "Message":"ok",
                                "Code":0,
                                "Name":"back_log",
                                "OldValue":"210",
                                "CurrentValue":"2"
                            }
                        ]
                    }
                ],
                "JobId":15969,
                "StartTime":"2017-06-27 16:33:40",
                "Progress":100,
                "Message":"매개변수 설정 성공",
                "EndTime":"2017-06-27 16:34:25",
                "Type":5
            },
            {
                "Status":3,
                "Code":3,
                "Data":[
                    {
                        "InstanceId":"",
                        "Database":"test",
                        "CostTime":0,
                        "FileSize":"12",
                        "FileName":"skyler.sql"
                    }
                ],
                "JobId":15970,
                "StartTime":"2017-06-27 16:46:52",
                "Progress":5,
                "Message":"Warning: Using a password on the command line interface can be insecure.?ERROR 1064 (42000) at line 1: You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'joell=skyler' at line 1?dumper err?",
                "EndTime":"2017-06-27 16:47:23",
                "Type":3
            },
            {
                "Status":3,
                "Code":3,
                "Data":[
                    {
                        "InstanceId":"",
                        "Database":"test",
                        "CostTime":0,
                        "FileSize":"5857113",
                        "FileName":"joellwang_1_4.sql"
                    }
                ],
                "JobId":15971,
                "StartTime":"2017-06-27 16:49:13",
                "Progress":5,
                "Message":"Warning: Using a password on the command line interface can be insecure.?ERROR 2006 (HY000) at line 1: MySQL server has gone away?dumper err?",
                "EndTime":"2017-06-27 16:49:44",
                "Type":3
            },
            {
                "Status":2,
                "Code":0,
                "Data":[
                    {
                        "InstanceId":"",
                        "Database":"test",
                        "CostTime":19,
                        "FileSize":"28384",
                        "FileName":"LearningSQLExample.sql"
                    }
                ],
                "JobId":15972,
                "StartTime":"2017-06-27 17:02:29",
                "Progress":100,
                "Message":"success",
                "EndTime":"2017-06-27 17:03:00",
                "Type":3
            },
            {
                "Status":2,
                "Code":0,
                "Data":[
                    {
                        "InstanceId":"cdb-o8cacfkg",
                        "Before":{
                            "SlaveZoneFirst":160002,
                            "MasterZone":160002,
                            "Memory":8000,
                            "DeployMode":"",
                            "Volume":50,
                            "ProtectMode":"",
                            "SlaveZoneSecond":"",
                            "EngineVersion":"5.6",
                            "CdbType":"CUSTOM"
                        },
                        "After":{
                            "SlaveZoneFirst":160002,
                            "MasterZone":160002,
                            "Memory":8000,
                            "DeployMode":"",
                            "Volume":100,
                            "ProtectMode":"",
                            "SlaveZoneSecond":"",
                            "EngineVersion":"5.6",
                            "CdbType":"CUSTOM"
                        },
                        "DealName":"20170627160000060849699827143219"
                    }
                ],
                "JobId":15974,
                "StartTime":"2017-06-27 18:04:19",
                "Progress":100,
                "Message":"인스턴스 업그레이드 완료",
                "EndTime":"2017-06-27 18:08:25",
                "Type":11
            },
            {
                "Status":2,
                "Code":0,
                "Data":[
                    {
                        "InstanceId":"cdb-7262qp3q",
                        "Character_set_server":"utf8",
                        "Lower_case_table_names":"0",
                        "Vport":3306
                    }
                ],
                "JobId":15976,
                "StartTime":"2017-06-27 19:18:31",
                "Progress":100,
                "Message":"인스턴스 초기화 성공",
                "EndTime":"2017-06-27 19:19:34",
                "Type":6
            },
            {
                "Status":2,
                "Code":0,
                "Data":[
                    {
                        "Status":2,
                        "Code":0,
                        "InstanceId":"cdb-ewgjla5w",
                        "Databases":[
                            {
                                "DatabaseName":"test",
                                "NewDatabaseName":"test_bak"
                            }
                        ],
                        "Progress":100,
                        "Message":"롤백 성공",
                        "RollbackTime":"2017-04-06 16:00:00",
                        "DatabaseTables":[
                            {
                                "Tables":[
                                    {
                                        "TableName":"monitor_alarm",
                                        "NewTableName":"monitor_alarm_bak_1"
                                    }
                                ],
                                "Database":"monitor_master"
                            }
                        ]
                    }
                ],
                "JobId":51695,
                "StartTime":"2017-04-06 20:42:59",
                "Progress":100,
                "Message":"모든 인스턴스 롤백 성공",
                "EndTime":"2017-04-06 20:45:03",
                "Type":10
            }
        ]
    }
}
```


## 5. 개발자 리소스

### API Explorer

**이 도구는 온라인 호출, 서명 인증, SDK 코드 생성 및 빠른 인덱스 API 등의 기능을 제공하여, 클라우드 API의 어려움을 크게 줄일 수 있으므로 사용을 추천합니다.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cdb&Version=2017-03-20&Action=DescribeTasks)

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
| InternalError.DatabaseAccessError | 데이터베이스 내부 오류. |
| InternalError.DesError | 시스템 내부 오류. |
| InvalidParameter | 매개변수 오류. |
| InvalidParameter.InstanceNotFound | 인스턴스가 존재하지 않음. |
| OperationDenied | 작업이 허용되지 않음. |
| OperationDenied.WrongStatus | 백 엔드 태스크 상태 오류. |

