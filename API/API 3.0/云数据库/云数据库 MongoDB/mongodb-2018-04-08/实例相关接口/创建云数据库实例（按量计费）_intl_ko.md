﻿﻿﻿﻿﻿﻿## 1. API 설명

API 요청 도메인 이름: mongodb.tencentcloudapi.com.

본 API(CreateDBInstanceHour)는 사용량 기반 요금제의 TencentDB for MongoDB 인스턴스(마스터 인스턴스, 재해 복구 인스턴스와 읽기 전용 인스턴스 포함)를 생성하는 데 사용됩니다. 인스턴스 사양, 인스턴스 유형, MongoDB 버전, 구매 시간과 수량 등의 정보 가져오기를 통해 TencentDB 인스턴스를 생성할 수 있습니다.

기본 API 요청 빈도 제한: 20회/초.

주의: 본 API는 금융 지역을 지원합니다. 금융 지역과 비금융 지역은 서로 격리되어 있습니다. 따라서 공통 매개변수 Region이 금융 지역(예: ap-shanghai-fsi)일 때, 금융 지역 이름(Region의 지역과 일치하는 것이 가장 좋음)이 포함된 도메인 이름을 동시에 지정해야 합니다. 예: mongodb.ap-shanghai-fsi.tencentcloudapi.com.



## 2. 입력 매개변수

다음 요청 매개변수 리스트는 API 요청 매개변수와 일부 공통 매개변수만 나열하였습니다. 전체 공통 매개변수 리스트는 [공통 요청 매개변수](https://cloud.tencent.com/document/api/240/31800)를 참조하십시오.

| 매개변수 이름 | 필수 여부 | 유형 | 설명 |
|---------|---------|---------|---------|
| Action | 예 | String | 공통 매개변수. 해당 API의 값: CreateDBInstanceHour |
| Version | 예 | String | 공통 매개변수. 해당 API의 값: 2018-04-08 |
| Region | 예 | String | 공통 매개변수. 제품이 지원하는 [지역 리스트](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/240/31800#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) 참조 |
| Memory | 예 | Integer | 인스턴스 메모리 크기. 단위: GB |
| Volume | 예 | Integer | 인스턴스 디스크 크기. 단위: GB |
| ReplicateSetNum | 예 | Integer | 복제본 세트 개수. 1은 단일 복제본 집합 인스턴스이며, 1보다 큰 것은 샤딩 클러스터 인스턴스입니다. 최대 10을 초과할 수 없습니다. |
| SecondaryNum | 예 | Integer | 모든 복제본 세트 내의 슬레이브 노드 수량. 현재 지원하는 슬레이브 노드 수량은 2개입니다. |
| EngineVersion | 예 | String | MongoDB 엔진 버전입니다. 값은 MONGO_2, MONGO_3_MMAP, MONGO_3_WT, MONGO_3_ROCKS와 MONGO_36_WT를 포함합니다. |
| Machine | 예 | String | 인스턴스 유형입니다. GIO: 고성능 IO형. TGIO: 10G급 IO형 |
| GoodsNum | 예 | Integer | 인스턴스 수. 기본값은 1이며 최소값은 1, 최대값은 10입니다. |
| Zone | 예 | String | 가용 영역 정보. 형식 예: ap-guangzhou-2 |
| InstanceRole | 예 | String | 인스턴스 역할. 지원되는 값: MASTER-마스터 인스턴스, DR-재해 복구 인스턴스, RO-읽기 전용 인스턴스. |
| InstanceType | 예 | String | 인스턴스 유형. REPLSET-복제본 세트, SHARD-샤딩 클러스터 |
| Encrypt | 아니요 | Integer | 데이터 암호화 여부. 엔진 버전 MONGO_3_ROCKS에서만 암호화를 할 수 있습니다. |
| VPCID | 아니요 | String | 사설망 ID. 입력하지 않을 경우 기본적으로 기본 네트워크가 선택됩니다. |
| SubnetId | 아니요 | String | VPC의 서브넷 ID. VpcId를 설정했을 경우, SubnetId를 반드시 입력해야 합니다. |
| ProjectId | 아니요 | Integer | 프로젝트 ID. 입력하지 않으면 기본 프로젝트로 설정됩니다. |
| SecurityGroup.N | 아니요 | Array of String | 보안 그룹 매개변수 |

## 3. 출력 매개변수

| 매개변수 이름 | 유형 | 설명 |
|---------|---------|---------|
| DealId | String | 주문 ID |
| RequestId | String | 유일한 요청 ID. 요청할 때마다 반환됩니다. 문제를 지정할 때 해당 요청의 RequestId를 제공해야 합니다. |

## 4. 예제

### 예제1 TencentDB 인스턴스 생성(사용량 기반 요금제)

사용자는 API를 통해 사용량 기반 요금제의 TencentDB 인스턴스를 생성해야 합니다.

#### 입력 예제

```
https://mongodb.tencentcloudapi.com/?Action=CreateDBInstanceHour
&Memory=4
&Volume=250
&ReplicateSetNum=1
&SecondaryNum=2
&EngineVersion=MONGO_3_WT
&Machine=TGIO
&GoodsNum=1
&Zone=ap-guangzhou-3
&InstanceRole=MASTER
&InstanceType=REPLSET
&<공통 요청 매개변수>
```

#### 출력 예제

```
{
    "Response": {
        "RequestId": "d3aecf52-5abf-49e4-bf79-1a6c47a406d4",
        "DealId": "28920"
    }
}
```


## 5. 개발자 리소스

### API Explorer

**이 도구는 온라인 호출, 서명 검증, SDK 코드 생성과 API 빠른 검색 등의 기능을 제공하며 클라우드 API 사용 난이도를 크게 낮추어 사용을 추천합니다.

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=mongodb&Version=2018-04-08&Action=CreateDBInstanceHour)

### SDK

클라우드 API 3.0은 맞춤형 개발도구 모음(SDK)을 제공하며 다양한 프로그래밍 언어를 지원하여 더욱 편리하게 API를 호출할 수 있습니다.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://intl.cloud.tencent.com/document/product/1013/33463)

## 6. 오류 코드

해당 API는 비즈니스 로직과 관련된 오류 코드가 없습니다. 다른 오류 코드는 [공통 오류 코드](https://cloud.tencent.com/document/api/240/31803#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)를 참조하십시오.







