## 1. API 설명

API 요청 도메인 이름: cdb.tencentcloudapi.com.

이 API(UpgradeDBInstance)는 데이터베이스 인스턴스 업그레이드에 사용합니다. 지원되는 인스턴스 유형은 마스터 인스턴스, 재해 복구 인스턴스 및 읽기 전용 인스턴스입니다.

기본적 API 요청 빈도 제한: 20회/초.

주의: 이 API는 금융 지역을 지원합니다. 금융 지역과 비금융 지역은 격리되어 있고 서로 통하지 않아서, 공통 매개변수 Region이 금융 지역 도메인(예: ap-shanghai-fsi)일 경우, 금융 지역의 도메인 이름을 동시에 지정해야 하며, Region의 도메인과 일치시키는 것이 가장 좋습니다. 예: cdb.ap-shanghai-fsi.tencentcloudapi.com.



## 2. 입력 매개변수

다음 요청 매개변수 리스트에는 API 요청 매개변수 및 일부 공통 매개변수만 나열되며, 완전한 공통 매개변수 리스트는 [공통 요청 매개변수](/document/api/236/15833)를 참조하십시오.

| 매개변수 이름 | 필수 항목 여부 | 유형 | 설명 |
|---------|---------|---------|---------|
| Action | 예 | String | 공통 매개변수, 이 API 값: UpgradeDBInstance |
| Version | 예 | String | 공통 매개변수, 이 API 선택 값: 2017-03-20 |
| Region | 아니요 | String | 공통 매개변수, 자세한 내용은 제품의 지원되는 [지역 리스트](/document/api/236/15833#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)를 참조하십시오. |
| InstanceId | 예 | String | 인스턴스 ID, 형식 예: cdb-c1nl9rpv 또는 cdbro-c1nl9rpv. TencentDB 콘솔 페이지에 표시된 인스턴스 ID와 동일합니다. [인스턴스 리스트 조회](https://cloud.tencent.com/document/api/236/15872) API를 사용하여 획득할 수 있으며, 그 값은 출력 매개변수 중 필드 InstanceId의 값입니다. |
| Memory | 예 | Integer | 업그레이드 후의 메모리 크기, 단위: MB, 유효한 Memory 값을 입력하기 위하여 [데이터베이스 판매 가능 사양 획득](https://cloud.tencent.com/document/product/236/17229) API를 사용하여 업그레이드 가능한 메모리 사양을 확인하십시오. |
| Volume | 예 | Integer | 업그레이드 후 디스크 크기, 단위: GB, 유효한 Volume 값을 입력하기 위해 [데이터베이스 판매 가능 사양 획득](https://cloud.tencent.com/document/product/236/17229) API를 사용하여 업그레이드 가능한 디스크 범위를 확인하십시오. |
| ProtectMode | 아니요 | Integer | 데이터 복제 방식, 지원 값: 0-비동기화 복제, 1-반동기화 복제, 2-강제 동기화 복제. 마스터 인스턴스 업그레이드 시 해당 매개변수를 지정할 수 있으며, 읽기 전용 인스턴스 또는 재해 복구 인스턴스 업그레이드 시에는 해당 매개변수를 지정해도 의미가 없습니다. |
| DeployMode | 아니요 | Integer | 배치 모드, 기본값은 0, 지원 값은 0-단일 가용 영역 배치, 1-멀티 가용 영역 배치입니다. 마스터 인스턴스 업그레이드 시 해당 매개변수를 지정할 수 있으며, 읽기 전용 인스턴스 또는 재해 복구 인스턴스 업그레이드 시 해당 매개변수를 지정해도 의미가 없습니다. |
| SlaveZone | 아니요 | String | 슬레이브 데이터베이스1의 가용 영역 정보, 기본적으로 인스턴스의 매개변수 Zone과 일치합니다. 마스터 인스턴스를 멀티 가용 영역 배치로 업그레이드 시 이 매개변수를 지정할 수 있으며, 읽기 전용 인스턴스 또는 재해 복구 인스턴스 업그레이드 시 이 매개변수를 지정해도 의미가 없습니다. [데이터베이스 판매 가능 사양 획득](https://cloud.tencent.com/document/product/236/17229) API를 통하여 지원되는 가용 영역을 조회할 수 있습니다. |
| EngineVersion | 아니요 | String | 마스터 인스턴스 데이터베이스 엔진 버전, 지원 값: 5.5, 5.6 및 5.7 |
| WaitSwitch | 아니요 | Integer | 새로운 인스턴스 접급 전환 방식, 기본값은 0이며, 마스터 인스턴스 업그레이드 시, 해당 매개변수를 지정할 수 있고, 읽기 전용 인스턴스 또는 재해 복구 인스턴스 업그레이드 시, 해당 매개변수를 지정해도 의미가 없습니다. 지원 값: 0-즉시 전환, 1-특정 시간 창에 전환. 해당 값이 1일 때, 업그레이드 중 새로운 인스턴스 접근 전환 프로세스는 시간 창 내에서 진행되거나 사용자가 직접 [새로운 인스턴스 접근 전환](https://cloud.tencent.com/document/product/236/15864) API를 호출하여 해당 프로세스를 트리거할 수 있습니다. |
| BackupZone | 아니요 | String | 슬레이브 데이터베이스2의 가용 영역 ID, 기본값은 0입니다. 마스터 인스턴스 업그레이드 시 해당 매개변수를 지정할 수 있으며, 읽기 전용 인스턴스 또는 재해 복구 인스턴스 업그레이드 시에는 해당 매개변수를 지정해도 의미가 없습니다. |
| InstanceRole | 아니요 | String | 인스턴스 유형, 기본값은 master, 지원 값은 master-마스터 인스턴스, dr-재해 복구 인스턴스, or-읽기 전용 인스턴스입니다. |

## 3. 출력 매개변수

| 매개변수 이름 | 유형 | 설명 |
|---------|---------|---------|
| DealIds | Array of String | 주문 ID |
| AsyncRequestId | String | 비동기화 태스크의 요청 ID, 이 ID를 사용하여 비동기화 태스크의 실행 결과를 조회할 수 있습니다. |
| RequestId | String | 유일한 요청 ID, 매회 요청 시마다 반환됩니다. 문제를 찾을 경우 해당 요청의 RequestId를 제공해야 합니다. |

## 4. 예시

### 예시1 데이터베이스 인스턴스 업그레이드

#### 입력 예시

```
https://cdb.tencentcloudapi.com/?Action=UpgradeDBInstance
&InstanceId=cdb-6si6qy6p
&Memory=1000
&Volume=50
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response":{
        "RequestId": "6EF60BEC-0242-43AF-BB20-270359FB54A7",
        "DealIds":[
            "20171204110077"
        ],
        "AsyncRequestId":"a6040589-3b098df5-b551d9e5-81c6bfdc"
    }
}
```


## 5. 개발자 리소스

### API Explorer

**이 도구는 온라인 호출, 서명 인증, SDK 코드 생성 및 빠른 인덱스 API 등의 기능을 제공하여, 클라우드 API의 어려움을 크게 줄일 수 있으므로 사용을 추천합니다.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cdb&Version=2017-03-20&Action=UpgradeDBInstance)

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
| FailedOperation.StatusConflict | 태스크 상태 충돌. |
| InternalError.DatabaseAccessError | 데이터베이스 내부 오류. |
| InternalError.TradeError | 거래 시스템 오류. |
| InvalidParameter | 매개변수 오류. |

