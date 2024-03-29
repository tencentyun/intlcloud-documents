## 1.배경

이 모듈은 Tencent Cloud Conference 기능("**기능**")을 사용하는 경우 적용됩니다. 이 모듈은 "[**DPSA**](https://intl.cloud.tencent.com/document/product/301/17347)"에 있는 데이터 개인 정보 보호 및 보안 계약에 통합됩니다. 이 모듈에서 사용되었지만 정의되지 않은 용어는 DPSA에 정의된 의미를 갖습니다. DPSA와 이 모듈 간에 충돌이 발생할 경우, 이 모듈은 상충하는 범위까지만 적용됩니다.


## 2.처리

당사는 기능과 관련하여 다음과 같은 데이터를 처리합니다(기능의 일부로 이러한 데이터를 처리하는 데 필요한 관련 기능을 통합하도록 사용자가 지시한 범위까지).

| **개인 정보**                                                | **이용**                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| **구성 데이터** 콘텐츠 관리: 컨퍼런스 정보, 일정 정보, 연사 정보(이미지, 이름 및 소개), 전시 정보, 제품 정보, 비즈니스 기회 정보(이름, 이메일, 연락처 번호, 제품 이름, 메모) 액세스 관리: 역할/액세스 권한(잠재고객, 참가업체) 템플릿 관리: 페이지 구성, 테마, 템플릿 설문지: 제목, 질문 미니 프로그램/웹 페이지 구성: appID, appSecret, PC 및 H5 설정 | 이를 통해 기능을 설계, 구성, 관리할 수 있습니다.             |
| **사용자 관리 데이터** 관리 콘솔 내에서 사용자가 지정한 데이터 필드(전화 번호, 이름, 회사 이름, 이메일 주소, 주소, 국가/지역, 관심사, 연령, 산업, 직업, 성별 등). | 이를 통해 기능 사용자를 관리할 수 있습니다.                  |
| **대시보드 데이터** 페이지 보기, 최고 방문 순위, 방문자 데이터(지역 분포/배포, 관심사, 산업, 성별, 연령, 직업), 라이브 비디오 볼륨, 라이브 비디오 시청 기간 또는 사용자가 지정한 기타 데이터 필드(위의 사용자 관리 데이터에 지정한 데이터 세트 포함) | 이는 컨퍼런스와 관련된 사용자 상호 작용 및 통계 정보에 대한 개관을 용이하게 합니다. |
| **OCR 데이터** 명함 데이터(스캔한 명함 상에 명시된 바와 같음) | 이를 통해 기능에 사용자 데이터를 업로드할 수 있습니다.       |
| **회의 데이터** 통계: 회사 이름, 관리자 이름, 지정 회사 이름, 지정 관리자 이름, 예약된 회의 시간, 회의 상태 엔터프라이즈 정보 관리: 사용자, 역할, 엔터프라이즈 표준 이름, 대표자 이름, 평가 및 운영 | 이를 통해 기능에 회의 일정을 관리할 수 있습니다.             |
| **푸시 데이터** 사용자 전화 번호, 이메일 주소                | 이를 통해 기능 사용자에게 메시지를 푸시 할 수 있습니다.      |
| **대화형 이벤트 데이터** 기본 설정, 상품 설정, 참가자 설정(이름, 전화 번호 및 성별은 위의 사용자 관리 데이터에서 동기화하거나 사용자가 직접 수집) | 이를 통해 기능 내에서 대화형 이벤트를 관리할 수 있습니다.    |
| **티켓 관리 데이터** 티켓 유형, 가격, 총 티켓 볼륨 제한, 승인 요구 사항, 기본 티켓 설정, 디스플레이 설정, 티켓 주문 정보, 주문 번호, 주문 시간, 이름, 전화 번호, 티켓 유형, 단일 가격, 볼륨, 총 금액 | 이를 통해 기능 내에서 티켓을 관리할 수 있습니다.             |
| **LVB 데이터** LVB 관리: LVB 유형, LVB 이름 및 소개, 방송 시간, 스트리밍 이름, pushStreamURL, 리플레이 여부, 댓글 설정, 조정 설정(해당하는 경우) 댓글 검토: LVB 이름, 발급 시간, 사용자 이름, 댓글 및 작업(통과/삭제) | 이를 통해 기능 내에서 라이브 방송을 관리할 수 있습니다.      |
| **참가 업체 관리 데이터** 역할 설정 데이터, 하위 계정 정보 (참가 업체 계정 이름, 암호, 계정 소유자, 전화 번호, 역할 및 전시 템플릿) | 이를 통해 기능 내에서 참가 업체 계정을 관리할 수 있습니다.   |

 

## 3.서비스 지역

DPSA에 명시된 바와 같습니다.


## 4.하위 프로세서

DPSA에 명시된 대로, Tencent Cloud Computing (Beijing) Co., Ltd., First App Holdings Limited, Aceville Pte Ltd. 등.




## 5.데이터 보유

데이터는 실시간 시청만을 위해 처리되는 대시보드 데이터를 제외하고 고객의 지시에 따라 보관됩니다(서비스 종료 후 30일 이내에 삭제).

DPSA에 따라 이러한 개인 데이터의 삭제를 요청할 수 있습니다.



## 6.특수 조건

개인 데이터 처리에 동의할 수 있는 최소 연령을 만족하는 개인이나 부모의 동의를 얻은 최소 연령 미만의 개인인 최종 사용자만 이 기능을 사용할 수 있습니다. 이는 최종 사용자의 해당 지역에 따라 다를 수 있습니다.