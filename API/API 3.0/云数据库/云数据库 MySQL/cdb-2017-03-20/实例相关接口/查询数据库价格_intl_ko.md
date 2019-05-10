## 1. API 설명

API 요청 도메인 이름: cdb.tencentcloudapi.com.

이 API(DescribeDBPrice)는 데이터베이스 인스턴스의 가격을 조회하는 데 사용됩니다. 사용량 기반 요금제 또는 연/월정액 요금제에 따른 가격 조회를 지원합니다. 인스턴스 유형, 구매 기간, 구매 수량, 메모리 크기, 디스크 크기 및 가용 영역 정보 등을 입력하여 인스턴스 가격을 조회할 수 있습니다.

주의: 특정 지역에 대해 가격 조회를 할 경우, 지역에 해당하는 액세스 포인트를 사용하시고, 액세스 포인트 정보는 <a href="https://cloud.tencent.com/document/api/236/15832">서비스 주소</a> 문서를 참조하십시오. 예: 광저우 지역에 대한 가격을 조회하려면 cdb.ap-guangzhou.tencentcloudapi.com으로 요청을 발송하십시오. 마찬가지로 상하이 지역에 대한 가격 조회는 cdb.ap-shanghai.tencentcloudapi.com으로 요청하시면 됩니다.

기본적 API 요청 빈도 제한: 20회/초.

주의: 이 API는 금융 지역을 지원합니다. 금융 지역과 비금융 지역은 격리되어 있고 서로 통하지 않아서, 공통 매개변수 Region이 금융 지역 도메인(예: ap-shanghai-fsi)일 경우, 금융 지역의 도메인 이름을 동시에 지정해야 하며, Region의 도메인과 일치시키는 것이 가장 좋습니다. 예: cdb.ap-shanghai-fsi.tencentcloudapi.com.



## 2. 입력 매개변수

다음 요청 매개변수 리스트에는 API 요청 매개변수 및 일부 공통 매개변수만 나열되며, 완전한 공통 매개변수 리스트는 [공통 요청 매개변수](/document/api/236/15833)를 참조하십시오.

| 매개변수 이름 | 필수 항목 여부 | 유형 | 설명 |
|---------|---------|---------|---------|
| Action | 예 | String | 공통 매개변수, 이 API 값: DescribeDBPrice |
| Version | 예 | String | 공통 매개변수, 이 API 선택 값: 2017-03-20 |
| Region | 아니요 | String | 공통 매개변수, 자세한 내용은 제품의 지원되는 [지역 리스트](/document/api/236/15833#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)를 참조하십시오. |
| Zone | 예 | String | 가용 영역 정보, 형식 예: "ap-guangzhou-2". 구성할 수 있는 구체적인 값은 <a href="https://cloud.tencent.com/document/api/236/17229">DescribeDBZoneConfig</a> API를 통해 조회하십시오. |
| GoodsNum | 예 | Integer | 인스턴스 수량, 기본값은 1, 최소값은 1, 최대값은 100입니다. |
| Memory | 예 | Integer | 인스턴스 메모리 크기, 단위: MB |
| Volume | 예 | Integer | 인스턴스 디스크 크기, 단위: GB |
| PayType | 예 | String | 지불 유형, 지원되는 값: PRE_PAID - 연/월정액 요금제, HOUR_PAID - 사용량 기반 요금제 |
| Period | 예 | Integer | 인스턴스 기간, 단위: 월, 최소값 1, 최대값 36, 사용량 기반 요금제 가격 조회 시, 이 필드는 유효하지 않습니다. |
| InstanceRole | 아니요 | String | 인스턴스 유형, 기본값은 master, 지원되는 값은 master-마스터 인스턴스, ro-읽기 전용 인스턴스, dr-재해 복구 인스턴스입니다. |
| ProtectMode | 아니요 | Integer | 데이터 복제 방식, 기본값은 0, 지원되는 값은 0-비동기화 복제, 1-반동기화 복제, 2-강제 동기화 복제입니다. |

## 3. 출력 매개변수

| 매개변수 이름 | 유형 | 설명 |
|---------|---------|---------|
| Price | Integer | 인스턴스 가격, 단위: 펀(위안화) |
| OriginalPrice | Integer | 인스턴스 원가, 단위: 펀(위안화) |
| RequestId | String | 유일한 요청 ID, 매회 요청 시마다 반환됩니다. 문제를 찾을 경우 해당 요청의 RequestId를 제공해야 합니다. |

## 4. 예시

### 예시1 데이터베이스 인스턴스 가격 조회

#### 입력 예시

```
https://cdb.tencentcloudapi.com/?Action=DescribeDBPrice
&Zone=ap-guangzhou-1
&GoodsNum=1
&Memory=1000
&Volume=25
&PayType=PRE_PAID
&Period=24
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response":{
        "RequestId": "6EF60BEC-0242-43AF-BB20-270359FB54A7",
        "Price":48000,
        "OriginalPrice":460800
    }
}
```


## 5. 개발자 리소스

### API Explorer

**이 도구는 온라인 호출, 서명 인증, SDK 코드 생성 및 빠른 인덱스 API 등의 기능을 제공하여, 클라우드 API의 어려움을 크게 줄일 수 있으므로 사용을 추천합니다.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cdb&Version=2017-03-20&Action=DescribeDBPrice)

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
| InternalError.DatabaseAccessError | 데이터베이스 내부 오류. |
| InternalError.TradeError | 거래 시스템 오류. |
| InvalidParameter | 매개변수 오류. |

