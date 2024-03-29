## 1\. **배경**

이 모듈은 고객 ID 및 액세스 관리(CIAM)(“**기능**”)를 사용하는 경우에 적용됩니다. 이 모듈은 (“[DPSA](https://intl.cloud.tencent.com/document/product/301/17347 )”)에 있는 데이터 처리 및 보안 계약에 포함됩니다. 이 모듈에서 사용되었지만 정의되지 않은 용어는 DPSA에서 정의된 것과 같은 의미를 갖습니다. DPSA와 이 모듈 간에 상충이 있는 경우, 이 모듈은 해당 상충 범위까지 적용됩니다.


## 2\. **처리**

당사는 기능과 관련하여 다음과 같은 데이터를 처리합니다.

| **개인 정보**                                     | **사용**                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| **사용자 관리 구성 데이터:** 귀하가 사전 설정한 사용자 속성(설명, 국적, 사용자 위치, 생일, 성별, 주소), 사용자 그룹(사용자 그룹 목록, 이름, 내역, 생성 시간, 포함된 사용자 목록) | 당사는 귀하에게 기능을 제공하기 위한 목적으로만 이 데이터를 처리합니다.<br/> 이 데이터는 TencentBD for MongoDB(MongoDB) 및 기능에 통합, 저장, 백업되며, TencentDB for Redis(Redis) 기능과도 통합됩니다. |
| **애플리케이션 관리 데이터:** <br><li>M2M 애플리케이션: 아이콘, 애플리케이션 이름, 애플리케이션 유형, 업종, ClientID, 암호 키, 애플리케이션 설명, 액세스 토큰 유효성, 보안 도메인, 구성된 CORS의 특정 URI,<br><li>미니 프로그램 애플리케이션: 스타일 애플리케이션 다운로드, 구성 가이드, 아이콘, 애플리케이션 이름, 애플리케이션 유형, 업종, ClientID, 암호 키, 애플리케이션 설명, 리디렉션 URI, 로그 아웃 리디렉션 URI, 액세스 토큰 유효성, 새로 고침 토큰, 클레임, 등록 및 로그인 프로세스 구성, 특정 보안 도메인 CORS 구성의 URI,<br><li>모바일 애플리케이션: 아이콘, 애플리케이션 이름, 애플리케이션 유형, 업종, ClientID, 암호 키, 애플리케이션 설명, 리디렉션 URI, 로그 아웃 리디렉션 URI, 액세스 토큰 유효성, 새로 고침 토큰, 클레임, 등록 프로세스, 로그인 프로세스, MFA 프로세스, 암호 분실 프로세스, 사용자 이름 분실 프로세스, 프로토콜 관리, 특정 보안 도메인 CORS 구성의 URI,<br><li>웹 애플리케이션: 아이콘, 애플리케이션 이름, 애플리케이션 유형, 업종, ClientID, 암호 키, 애플리케이션 설명, 리디렉션 URI, 로그 아웃 리디렉션 URI, 액세스 토큰 유효성, 새로 고침 토큰, 클레임, 등록 프로세스, 로그인 프로세스, MFA 프로세스, 암호 분실 프로세스, 사용자 이름 분실 프로세스, 프로토콜 관리, 특정 보안 도메인 CORS 구성의 URI | 당사는 귀하에게 기능을 제공하기 위한 목적으로만 이 데이터를 처리합니다. <br/> 이 데이터는 Cloud Object Storage(COS) 및 MongoDB 기능에 통합, 저장 및 백업된다는 점에 유의하십시오. |
| **데이터 동기화 설정 데이터:** 데이터 소스 이름, 데이터 소스 ID, 설명, 구성 가이드, ClientID, 클라이언트 암호 키, 토큰, 사용자 URL, 그룹 URL | 당사는 귀하에게 기능을 제공하기 위한 목적으로만 이 데이터를 처리합니다.<br/> 이 데이터는 MongoDB 기능에 통합, 저장 및 백업된다는 점에 유의하십시오. |
| **증명 관리 데이터:** <br><li>일반 인증 소스: 인증 소스 아이콘, 인증 소스 이름, 인증 소스 속성, 인증 소스 설명, 암호 정책, SMS 확인 코드 길이, SMS 확인 코드 유효 기간, 이메일 확인 코드 길이, 이메일 확인 코드 유효 기간, <br><li>소셜 인증 소스: 인증 소스 아이콘, 인증 소스 이름, 인증 소스 설명, AppID, 애플리케이션 암호 키, 속성 매핑 | 당사는 귀하에게 기능을 제공하기 위한 목적으로만 이 데이터를 처리합니다.<br/> 이 데이터는 COS 및 MongoDB 기능에 통합, 저장 및 백업된다는 점에 유의하십시오. 단문 메시지 서비스(Short Message Service, SMS) 및 단순 이메일 서비스(Simple Email Service, SES) 서비스를 구매한 경우, 일반 인증 소스 데이터 또한 SMS, SES 기능에 통합됩니다. |
| **개인화 데이터:** <br><li>도메인 이름 설정: 귀하가 설정 및 제공한 도메인 이름(또는 필요에 따라 당사가 제공하는 표준 도메인 이름), <br><li>템플릿 설정(SMS 및/또는 SES 기능 사용 옵션과 관련된 구성 설정): SMS 템플릿(SMS 서버, SMS 로그인 서명, SMS 템플릿 ID), 메일박스 템플릿(이메일 서버, 확인 코드 템플릿 ID, 암호 템플릿 ID 검색, 사용자 이름 템플릿 ID 검색), <br><li>실명 인증 템플릿(실명 인증 서비스 공급자, API 호출인의 보안 자격 증명(비밀 ID, 비밀 키)) | 당사는 귀하에게 기능을 제공하기 위한 목적으로만 이 데이터를 처리합니다.<br/> 이 데이터는 MongoDB 기능에 통합, 저장 및 백업된다는 점에 유의하십시오. SMS 및 SES 서비스를 구매한 경우, 템플릿 설정 데이터 또한 SMS, SES 기능에 통합됩니다. |
| **기본 제공 사용자 속성 데이터:** 잘못된 로그인 시간, 잠금 시간, Alipay 사용자 ID, 이메일 주소, 업데이트 시간, 사용자의 시간대, 지리적 위치, 최근 로그인 시간, 전화 번호 , 생성 시간, 사용자 그룹, 사용자 풀, 사용자 별명, 사용자 ID, 사용자 이름, WeChat 오픈 ID, 최초 로그인 여부, 사용자 소스, Wechatunion ID, 사용자 상태, QQ 오픈 ID, QQunion ID, 실명 인증 여부, 실명 인증 방법 이름, ID 번호, 기본 계정 여부 | 당사는 귀하에게 기능을 제공하기 위한 목적으로만 이 데이터를 처리합니다.<br/> 이 데이터는 MongoDB 및 기능에 통합, 저장, 백업되며, Redis 기능과도 통합된다는 점에 유의하십시오. SMS 및 SES 서비스를 구매하신 경우, 전화번호 또한 SMS 기능에 통합되며, 이메일 주소는 SES 기능에 통합됩니다. |


## 3\. **서비스 지역**

DPSA에 명시된 바와 같습니다.


## 4\. **하위 프로세서**

DPSA에 명시된 바와 같습니다.


## 5\. **데이터 보존**

당사는 기능과 관련하여 처리된 개인 데이터를 다음과 같이 저장합니다.

| **개인 정보**                                     | **보존 방침**                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 사용자 관리 구성 데이터 애플리케이션 관리 데이터 데이터 동기화 설정 데이터 증명 관리 데이터 개인화 데이터  기본 제공 사용자 속성 데이터 | 당사는 이러한 데이터를 귀하가 수동으로 삭제할 때까지 보존합니다. 당사는 귀하가 계정을 삭제하거나 기능의 사용을 종료하는 경우, 이러한 데이터를 삭제합니다. |

귀하는 DPSA에 따라 이러한 개인 데이터의 삭제를 요청할 수 있습니다.


## 6\. **특수 조건**

개인 데이터 처리에 동의할 수 있는 최소 연령 이상인 최종 사용자만 이 기능을 사용할 수 있습니다. 이는 최종 사용자의 관할권에 따라 다를 수 있습니다.