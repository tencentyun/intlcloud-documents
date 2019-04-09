## 1. API 설명

API 요청 도메인 이름: as.tencentcloudapi.com.

본 API(CreateScheduledAction)는 시간 제한 태스크 생성에 사용됩니다.

기본 API 요청 빈도 제한: 20회/초.

주의: 본 API는 금융 지역을 지원합니다. 금융 지역과 비금융 지역은 격리되어 서로 연결되지 않기 때문에 공통 매개변수 Region이 금융 지역인 경우(예: ap-shanghai-fsi) 금융 지역을 포함한 지역명을 동시에 지정해야 하며 가장 좋은 것은 Region의 지역과 일치하는 것입니다. 예를 들어, as.ap-shanghai-fsi.tencentcloudapi.com입니다.



## 2. 입력 매개변수

다음 요청 매개변수 리스트에는 API 요청 매개변수와 일부 공통 매개변수만 나열합니다. 완전한 공통 매개변수 리스트는 [공통 매개변수](/document/api/377/20426)를 참조하십시오.

| 매개변수 이름 | 필수 여부 | 유형 | 설명 |
|---------|---------|---------|---------|
| Action | 예 | String | 공통 매개변수, 본 API 값: CreateScheduledAction |
| Version | 예 | String | 공통 매개변수, 본 API 값: 2018-04-19 |
| Region | 예 | String | 공통 매개변수, 세부 정보는 제품이 지원하는 [지역 리스트](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)를 참조하십시오 |
| AutoScalingGroupId | 예 | String | 조정 그룹 ID |
| ScheduledActionName | 예 | String | 시간 제한 태스크 이름입니다. 이름은 중문, 영문, 숫자, 밑줄, 구분 기호 "-", 소수점만을 지원하고 60바이트를 초과할 수 없습니다. 동일 조정 그룹에는 유일해야 합니다. |
| MaxSize | 예 | Integer | 시간 제한 태스크 트리거 시 설정한 조정 그룹의 최대 인스턴스 수입니다. |
| MinSize | 예 | Integer | 시간 제한 태스크 트리거 시 설정한 조정 그룹의 최소 인스턴스 수입니다. |
| DesiredCapacity | 예 | Integer | 시간 제한 태스크 트리거 시 설정한 조정 그룹 에상 인스턴스 수입니다. |
| StartTime | 예 | Timestamp | 시간 제한 태스크가 처음 트리거된 시간입니다. 값은 `베이징 시간`(UTC+8)으로 `ISO8601` 표준에 따르며 형식은 `YYYY-MM-DDThh:mm:ss+08:00`입니다. |
| EndTime | 아니요 | Timestamp | 시간 제한 태스크의 종료 시간입니다. 값은 `베이징 시간`(UTC+8)으로 `ISO8601` 표준에 따르며 형식은 `YYYY-MM-DDThh:mm:ss+08:00`입니다.<br><br>해당 매개변수와 `Recurrence`는 동시에 지정해야 하고 종료 시간에 도달한 후 시간 제한 태스크는 더 이상 적용되지 않습니다. |
| Recurrence | 아니요 | String | 시간 제한 태스크의 중복 방식입니다. 표준 [Cron](https://zh.wikipedia.org/wiki/Cron) 방식입니다. <br><br>해당 매개변수와 `EndTime`은 동시에 지정해야 합니다. |

## 3. 출력 매개변수

| 매개변수 이름 | 유형 | 설명 |
|---------|---------|---------|
| ScheduledActionId | String | 시간 제한 태스크 ID. |
| RequestId | String | 유일한 요청 ID, 매회 요청 시마다 반환됩니다. 문제를 찾을 경우 해당 요청의 RequestId를 제공해야 합니다. |

## 4. 예시

### 예제 1 일회성 시간 제한 태스크 생성

시간 제한 태스크를 생성하고 지정 시간(베이징 시간 2018년 8월 28일 23시)에 조정 그룹의 최대 인스턴스 수, 최소 인스턴스 수 및 에상 인스턴스 수를 10, 4, 6으로 조정합니다.

#### 입력 예시

```
https://as.tencentcloudapi.com/?Action=CreateScheduledAction
&AutoScalingGroupId=asg-2nr9xh8h
&ScheduledActionName=scheduled-action-0
&MaxSize=10
&MinSize=4
&DesiredCapacity=6
&StartTime=2018-08-28T23:00:00+08:00
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response": {
        "ScheduledActionId": "asst-chwbkq4c",
        "RequestId": "193a710f-8dbf-46aa-8b4a-195532244df8"
    }
}
```

### 예제 2 중복 실행하는 시간 제한 태스크 생성

시간 제한 태스크를 생성하고 베이징 시간 2018년 8월 28일부터 매일 23:00에 조정 그룹의 최대 인스턴스 수, 최소 인스턴스 수 및 에상 인스턴스 수를 7, 2, 3으로 조정하고 베이징 시간 2019년 1월 1일 00:00 후에 종료합니다.

#### 입력 예시

```
https://as.tencentcloudapi.com/?Action=CreateScheduledAction
&AutoScalingGroupId=asg-2nr9xh8h
&ScheduledActionName=scheduled-action-1
&MaxSize=7
&MinSize=2
&DesiredCapacity=3
&StartTime=2018-08-28T23:00:00+08:00
&EndTime=2019-01-01T00:00:00+08:00
&Recurrence=0 23 */1 * *
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response": {
        "ScheduledActionId": "asst-le3us530",
        "RequestId": "502fd6fa-44ff-4c79-b77e-ee20f72bddc0"
    }
}
```


## 5. 개발자 리소스

### API Explorer

**해당 도구는 온라인 호출, 서명 인증, SDK 코드 생성과 빠른 검색 API 등 기능을 제공하고 클라우드 API 사용 난이도를 대폭 낮춰 사용을 추천합니다.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=CreateScheduledAction)

### SDK

클라우드 API 3.0은 일체화된 SDK를 제공하고 여러 종류의 프로그래밍 언어를 지원하여 편리하게 API를 호출할 수 있습니다.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. 오류 코드

다음은 API 비즈니스 로직과 관련된 오류 코드만 나열하며 다른 오류 코드는 [공통 오류 코드](/document/api/377/20428#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)를 참조하십시오.

| 오류 코드 | 설명 |
|---------|---------|
| InternalError | 내부 오류 |
| InvalidParameterValue.CronExpressionIllegal | 시간 제한 태스크에 지정된 Cron 식이 잘못되었습니다. |
| InvalidParameterValue.EndTimeBeforeStartTime | 시간 제한 태스크의 설정한 종료 시간이 시작 시간 이전입니다. |
| InvalidParameterValue.InvalidScheduledActionNameIncludeIllegalChar | 시간 제한 태스크 이름에 잘못된 문자부호가 포함되어 있습니다. |
| InvalidParameterValue.ScheduledActionNameDuplicate | 시간 제한 태스크 이름이 중복됩니다. |
| InvalidParameterValue.Size | 조정 그룹 최대 수량, 최소 수량, 에상 인스턴스 수의 값이 잘못되었습니다. |
| InvalidParameterValue.StartTimeBeforeCurrentTime | 시간 제한 태스크의 설정한 시작 시간이 현재 시간 이전입니다. |
| InvalidParameterValue.TimeFormat | 시간 형식 오류. |
| InvalidParameterValue.TooLong | 값이 너무 많습니다. |
| LimitExceeded.DesiredCapacityLimitExceeded | 에상 인스턴스 수가 한도를 초과했습니다. |
| LimitExceeded.MaxSizeLimitExceeded | 최대 인스턴스 수가 한도보다 큽니다. |
| LimitExceeded.MinSizeLimitExceeded | 최소 인스턴스 수가 한도보다 작습니다. |
| LimitExceeded.ScheduledActionLimitExceeded | 시간 제한 태스크 수량이 한도를 초과했습니다. |
| MissingParameter | 매개변수 결함 오류. |
| ResourceNotFound.AutoScalingGroupIdNotFound | 조정 그룹이 존재하지 않습니다. |

