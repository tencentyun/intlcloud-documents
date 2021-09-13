## 관계망 시스템 소개

IM은 사용자 관계망 호스팅 기능을 지원하여 관계망과 관련된 완벽한 솔루션을 제공합니다. App 사용자 간의 친구 관계를 자체적으로 개발, 관리하지 않고 보다 간편한 방법으로 친구 추가, 삭제 기능 등을 사용하고 싶다면 IM의 관계망 호스팅 서비스를 선택하십시오.

- IM은 관계망 저장 기능을 제공하여 데이터 원격 재해 복구, 다중 리전 배포 및 자동 용량 확장/축소가 가능합니다. 이를 통해 서버 다운, 마스터/슬레이브 멀티 복사, 용량 확장/축소 등 복잡한 프로세스를 손쉽게 해결할 수 있습니다.
- IM은 업계 범용 비즈니스 처리 프로세스를 제공하므로, 사용자 관계망 로직에 대해 걱정할 필요가 없습니다.
- IM은 전문적인 운영 프로세스 및 운영 팀을 통해 연간 99.99%에 이르는 품질 안정성을 보장하여, 사용자에게 검증받은 안정적인 서비스 제공할 수 있도록 합니다. 
- IM은 손쉽게 사용할 수 있는 서비스 인터페이스와 빠른 액세스 가이드를 제공하여 전 과정에서 최고급 서비스를 선사합니다.

관계망은 사용자와 다른 사용자 관계를 설명하는데 사용되는 데이터 세트로, IM은 현재 친구 리스트와 블랙리스트 2가지 종류를 지원합니다.

## 관계망 필드 [](id:relationship)
IM 관계망 시스템은 표준 관계망 필드와 사용자 정의 관계망 필드를 지원합니다. 관계망 필드의 특징은 다음과 같습니다.

- 관계망 필드는 Key-Value 형식으로 표시됨.
- Key는 String 유형이며, 이름은 영어 알파벳 대소문자, 숫자, 언더바로 구성.
- Value 유형:
 a. uint64_t 유형의 정수(사용자 정의 관계망 필드 미지원)
 b. string 유형의 문자열(string 길이 500 바이트 이하)
 c. bytes 유형의 buffer(buffer 길이 500 바이트 이하)
 d. string 유형의 문자열 배열(모든 string 길이 500 바이트 이하, 친구 리스트의 Tag_SNS_IM_Group 필드에만 사용 가능)

## 친구 리스트
IM의 친구 리스트는 최대 3000명까지 추가할 수 있습니다.
친구 리스트는 표준 친구 필드와 사용자 정의 친구 필드를 지원합니다.

### 표준 친구 필드
현재 IM이 지원하는 표준 친구 필드는 다음과 같습니다. 

| 필드 이름     | 유형      | 설명     |
|---------|---------|---------|
|Tag_SNS_IM_Group | Array  |친구 리스트: <br />1. 리스트 수량: 최대 32개. <br />2. 리스트 이름: 공란 불가. <br />3. 리스트 이름 길이: 최대 30 바이트. <br />4. 동일 친구 여러 리스트 중복 추가 가능. |
|Tag_SNS_IM_Remark|string|친구 설명: <br />1. 설명 길이: 최대 96 바이트.|
|Tag_SNS_IM_AddSource|string|친구 출처 추가: <br />1. 친구 출처 추가 필드는 접두사와 키워드 두 부분을 포함. <br />2. 친구 출처 추가 필드의 접두사: AddSource_Type_. <br />3. 키워드: 최대 8 바이트의 영어 알파벳으로 구성하며, 영어 단어 또는 약자 사용 권장. <br />4. 예시: 친구 출처 추가 키워드가 Android일 경우, 친구 출처 필드는 AddSource_Type_Android가 됨. <br />|
|Tag_SNS_IM_AddWording|string|친구 추가 메시지: <br />1. 친구 추가 메시지 길이: 최대 256 바이트.<br />|


### 사용자 정의 친구 필드

사용자 정의 친구 필드는 각 App에서 비즈니스 니즈에 맞게 설정한 친구 데이터입니다. 사용자 정의 친구 필드를 통해 App은 추가 데이터를 친구에 적용할 수 있고 기존 인터페이스를 통해 읽기/쓰기 작업을 할 수 있습니다. 
App 관리자는 IM [콘솔](https://console.cloud.tencent.com/im) >**애플리케이션 설정**>**기능 설정**을 통해 사용자 정의 친구 필드를 신청할 수 있으며 신청 제출 후 5분 내에 적용됩니다. 

사용자 정의 친구 필드의 이름 생성 규칙은 다음과 같습니다. 
- 사용자 정의 친구 필드 이름 구성: 접두사, 키워드.
- 사용자 정의 친구 필드의 접두사: Tag_SNS_Custom.
- 키워드: 8바이트 이하의 영어 알파벳으로 구성하며, 영어 단어 또는 약자 사용 권장.
- 예시: App에서 신청하려는 사용자 정의 친구 필드의 키워드가 Test일 경우, 사용자 정의 친구 필드의 이름은 Tag_SNS_Custom_Test가 됨.

사용자 정의 친구 필드 신청 시, 모든 사용자 정의 친구 필드에 다음과 같은 정보를 제출해야 합니다. 
- 사용자 정의 친구 필드 이름(Key).
- 사용자 정의 친구 필드 유형(Value): 자세한 내용은 [관계망 필드](#relationship)를 참고하십시오.



### 친구 추가

IM이 지원하는 친구 추가 모드: 일괄 추가, 승인 없이 추가, 승인 후 추가. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/1047/34902">친구 추가</a>를 참고하십시오.

양방향 친구: 사용자 A의 친구 리스트에 B가 있고, B의 리스트에도 A가 있습니다. 
단방향 친구: 사용자 A의 친구 리스트에는 B가 있지만 B의 테이블에는 A가 없습니다. 
친구 추가 인증 방식: 모든 사용자는 다른 사용자에게 친구로 추가되는 방식을 선택할 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/1047/33520">표준 프로필 정보 필드</a>의 친구 추가 인증 방식 필드를 참고하십시오.
승인 없이 추가: 계정 A가 설정한 친구 추가 인증 방식이 AllowType_Type_AllowAny인 경우, 누구든 A를 친구로 추가할 수 있습니다. 이렇게 요청하면 바로 친구 추가가 완료되는 시나리오를 1단계 친구 추가라고 합니다.
승인 후 추가: 계정 A가 설정한 친구 추가 인증 방식이 AllowType_Type_NeedConfirm인 경우, 누구든 A를 추가하면 A는 친구 추가 인증 메시지를 받습니다. 이를 1단계라고 하며, A의 친구 요청 승인을 2단계라고 합니다. 이렇게 친구 추가에 인증이 필요한 시나리오를 2단계 친구 추가라고 합니다. 

### 친구 삭제
IM은 단방향 및 양방향 친구 삭제 2가지 삭제 모드를 지원합니다. 


| 삭제 모드 | DeleteType | 설명 |
|---------|---------|---------|
| 단방향 친구 삭제 | Delete_Type_Single | To_Account만 From_Account의 친구 리스트에서 삭제하고 From_Account는 To_Account 친구 리스트에서 삭제하지 않음. |
|양방향 친구 삭제|Delete_Type_Both| To_Account를 From_Account의 친구 리스트에서 삭제하고From_Account도 To_Account의 친구 리스트에서 삭제.|


IM은 친구 일괄 삭제를 지원합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/1047/34905"> 친구 삭제</a>를 참고하십시오.


### 친구 검증

IM은 다음과 같이 단방향 친구 관계 검증, 양방향 친구 관계 검증 2가지 검증 모드를 지원합니다.

| 검증 모드 | CheckType | 설명 |
|---------|---------|---------|
| 단방향 친구 관계 검증| CheckResult_Type_Single | From_Account의 친구 리스트에 To_Account가 있는지만 확인하고 To_Account의 친구 리스트에 From_Account가 있는지는 확인하지 않음.|
| 양방향 친구 관계 검증 | CheckResult_Type_Both | From_Account의 친구 리스트에 To_Account가 있는지 확인하고 To_Account의 친구 리스트에 From_Account가 있는지도 확인함. |


단방향 친구 관계 검증 시, 다음과 같은 결과가 나올 수 있습니다. 

| Relation| 설명 |
|---------|---------|
| CheckResult_Type_NoRelation | From_Account의 친구 리스트에 To_Account는 없지만 To_Account의 친구 리스트에 From_Account가 있는지는 확인할 수 없음. |
| CheckResult_Type_AWithB | From_Account의 친구 리스트에 To_Account는 있지만 To_Account의 친구 리스트에 From_Account가 있는지는 확인할 수 없음. |


양방향 친구 관계 검증 시, 다음과 같은 결과가 나올 수 있습니다. 

| Relation| 설명|
|---------|---------|
| CheckResult_Type_BothWay |From_Account의 친구 리스트에 To_Account가 있고 To_Account의 친구 리스트에도 From_Account가 있음.|
|CheckResult_Type_AWithB|From_Account의 친구 리스트에 To_Account가 있지만 To_Account의 친구 리스트에는 From_Account가 없음.|
|CheckResult_Type_BWithA|From_Account의 친구 리스트에 To_Account가 없지만 To_Account의 친구 리스트에는 From_Account가 있음. |
|CheckResult_Type_NoRelation|From_Account의 친구 리스트에 To_Account가 없고 To_Account의 친구 리스트에도 From_Account가 없음.|

친구 검증에 더 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/1047/34907"> 친구 검증</a>을 참고하십시오.

## 블랙리스트
모든 사용자는 자신이 차단한 사용자를 저장하는 블랙리스트가 있습니다.
사용자 A가 사용자 B를 블랙리스트에 추가하면 A와 B의 친구 관계(친구 관계였다면)는 제거되고 A와 B 사이에는 다시 친구 요청을 할 수 없습니다. 
IM 블랙리스트에 최대 1000개의 계정을 추가할 수 있습니다.

### 블랙리스트 추가
IM은 블랙리스트 일괄 추가를 지원합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/1047/34911"> 블랙리스트 추가</a>를 참고하십시오.

### 블랙리스트 삭제
IM은 블랙리스트 일괄 삭제를 지원합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/1047/34912"> 블랙리스트 삭제</a>를 참고하십시오.

### 블랙리스트 풀링
IM은 페이지별 전체 블랙리스트 풀링을 지원합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/1047/34914"> 블랙리스트 풀링</a>을 참고하십시오.

### 블랙리스트 검증
IM은 다음과 같이 단방향 블랙리스트 관계 검증, 양방향 블랙리스트 관계 검증 2가지 검증 모드를 지원합니다. 


|검증 모드 | CheckType | 설명 |
|---------|---------|---------|
|단방향 블랙리스트 관계 검증 |BlackCheckResult_Type_Single | From_Account의 블랙리스트에 To_Account가 있는지 확인하고 To_Account의 블랙리스트에 From_Account가 있는지는 확인하지 않음.|
|양방향 블랙리스트 관계 검증|BlackCheckResult_Type_Both| From_Account의 블랙리스트에 To_Account가 있는지 검사하고 To_Account의 블랙리스트에 From_Account가 있는지도 확인. |

단방향 블랙리스트 관계 검증 시 다음과 같은 결과가 나올 수 있습니다. 

| Relation | 설명 |
|---------|---------|
| BlackCheckResult_Type_AWithB | From_Account의 블랙리스트에 To_Account가 있지만 To_Account의 블랙리스트에 From_Account가 있는지 확인할 수 없음. |
|BlackCheckResult_Type_NO|From_Account의 블랙리스트에 To_Account가 없지만 To_Account의 블랙 리스트에 From_Account가 있는지 확인할 수 없음. |

양방향 블랙리스트 관계 검증 시, 다음과 같은 결과가 나올 수 있습니다. 

| Relation | 설명 |
|---------|---------|
| BlackCheckResult_Type_BothWay | From_Account의 블랙리스트에 To_Account가 있고 To_Account의 블랙리스트에도 From_Account가 있음. |
|BlackCheckResult_Type_AWithB|From_Account의 블랙리스트에 To_Account가 있지만 To_Account의 블랙리스트에는 From_Account가 없음.|
|BlackCheckResult_Type_BWithA|From_Account의 블랙리스트에는 To_Account가 없지만 To_Account의 블랙리스트에는 From_Account가 있음.|
|BlackCheckResult_Type_NO|From_Account의 블랙리스트에는 To_Account가 없고 To_Account의 블랙리스트에도 From_Account가 없음.|

블랙리스트 검증에 대한 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/1047/34913"> 블랙리스트 검증</a>을 참고하십시오.


## 관련 문서

- [사용자 프로필 정보 및 관계망(Android)](https://intl.cloud.tencent.com/document/product/1047/34332)
- [사용자 프로필 정보 및 관계망(iOS)](https://intl.cloud.tencent.com/document/product/1047/34333)
- [개요(Windows)](https://intl.cloud.tencent.com/document/product/1047/34304)
- [사용자 프로필 정보(Web & 미니프로그램)](https://intl.cloud.tencent.com/document/product/1047/34334)
