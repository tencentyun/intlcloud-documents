[Tencent Cloud GME SDK](https://intl.cloud.tencent.com/product/tmg?idx=1)를 이용해주셔서 감사합니다. 개발자가 Tencent Cloud GME 제품 API를 테스트하는 편의성을 위해 GME SDK 액세스 매뉴얼을 소개드립니다.

GME 사용 시 하기 5개 프로세스를 진행합니다: 
1. [Tencent Cloud 콘솔에서 신규 GME 서비스를 구축합니다](#.E6.96.B0.E5.BB.BA.E6.9C.8D.E5.8A.A1);
2. [대응 버전의 클라이언트 SDK를 다운로드합니다](#.E4.B8.8B.E8.BD.BD-sdk);
3. [API 파일을 액세스하며, SDK를 프로그래밍에 포팅합니다](#.E7.9B.B8.E5.85.B3-api-.E6.96.87.E6.A1.A3);
4. [일상 운영 통계를 조회합니다](#.E6.8E.A7.E5.88.B6.E5.8F.B0.E7.94.A8.E9.87.8F.E7.BB.9F.E8.AE.A1);
5. [액세스 시 예외 사항 셀프 점검 및 피드백](#.E7.89.B9.E6.AE.8A.E9.97.AE.E9.A2.98.E5.A4.84.E7.90.86);


## 서비스 생성
### 1. 애플리케이션 생성
![](https://main.qcloudimg.com/raw/7b682f5aaf2f9995a6eef37a3296b7ac.png)

### 2. 대응한 정보
이 웹페이지에 필요한 메시지를 입력하고, 니즈별로 원하는 서비스를 선택합니다. 
- 음질이 다르면 요금 결제방식도 달라집니다. 요금 결제 관련 사항은 [제품 가격](https://cloud.tencent.com/document/product/607/17808)을 참조하거나, Tencent Cloud 비즈니스 담당자에게 문의하시기 바랍니다. 설정 완료 시 재수정할 수 있습니다.
- 혹 게임류 애플리케이션 일 경우, 대응하는 플랫폼 엔진을 선택해야 합니다.
- 음성 메시지 및 텍스트 변환 서비스는 설정 완료 후 재수정할 수 있습니다.

<!--![](https://main.qcloudimg.com/raw/8bed789287a2b1a0dfe4861fd052d70c.png)-->


### 3. 애플리케이션 조회
리스트의 AppID는 SDK를 액세스하여 개발하는 과정에 파라미터로 활용됩니다.
![](https://main.qcloudimg.com/raw/efbdf4105eb37cfa40e96223e2b7a840.png)


#### 4. 애플리케이션 설정
![](https://main.qcloudimg.com/raw/c3cef70b9fe48c050cfec1ce81b23979.png)

애플리케이션 정보 모듈, [수정]을 클릭하여 대응하는 메시지를 수정합니다.

### 5. 인증 정보
![](https://main.qcloudimg.com/raw/fa2ca0b76d1ac0f03aa769a4d5972308.png)
- 이 모듈의 권한 키는 파라미터로 활용되어 SDK에 액세스하는 과정입니다. 
- 웹페이지에서 보안키를 수정 시, 15분-1시간내에 적용됩니다. 잦은 변경은 금하여주세요.
-게임을 구축한 계정, 루트 계정과 전역 협업자만이 [보안키 리셋]을 조작할 수 있습니다.
- 인증 상세 내역은 [인증 보안키](https://intl.cloud.tencent.com/document/product/607/12218)를 참조하십시오.
 ![](https://main.qcloudimg.com/raw/e65e03a506eda099d3cedca85ea9685c.png)


### 6. 서비스 오픈/종료
여기에서 업무와 서비스를 오픈하거나 종료할 수 있습니다.
![](https://main.qcloudimg.com/raw/1e3d12f084942645714158eb68767acf.png)


## SDK 다운로드 
### 1. 다운로드 주소
[SDK 다운로드 매뉴얼](https://intl.cloud.tencent.com/document/product/607/18521)에서 관련 Demo와 SDK를 다운로드합니다.

### 2. 액세스 준비
SDK를 액세스하려면 Tencent Cloud에서 제공하는 appid와 권한 보안키를 적용해야 합니다. 즉 앱 관리 리스트의 AppID와 앱 설정의 인증 메시지 모듈을 사용해야 합니다.

플랫폼 관련 디테일한 설정은 각 플랫폼의 프로그래밍 설정 파일을 참조하십시오.

### 3. 공식 Demo 사용 시 주의사항
Demo에 Tencent Cloud 테스트 계정을 포함하므로, 성능을 체험할 수 있습니다. 혹 멤버를 교체하거나 회사 테스트 계정을 적용해야 할 경우, Demo 의 대응하는 인터페이스에서 Tencent Cloud 테스트 계정 AppID를 개발자가 콘솔에서 획득한 AppID로 변경해야 합니다. 또한 AVChatViewController-GetAuthBuffer함수에서 실시간 음성의 권한 보안키를 수정해야 합니다


## 관련 API 파일
사용하는 플랫폼 혹은 엔진에 따라 다음 파일을 참조하여 액세스할 수 있습니다:

Unity 관련 파일: 
[프로그래밍 설정 파일](https://intl.cloud.tencent.com/document/product/607/10783)
[API 파일](https://intl.cloud.tencent.com/document/product/607/15210)

Unreal Engine 관련 파일: 
[프로그래밍 설정 파일](https://intl.cloud.tencent.com/document/product/607/10783)
[API 파일](https://intl.cloud.tencent.com/document/product/607/15210)

Cocos2D 관련 파일:
[프로그래밍 설정 파일](https://intl.cloud.tencent.com/document/product/607/10783)
[API 파일](https://intl.cloud.tencent.com/document/product/607/15210)

Windows 관련 파일:
[프로그래밍 설정 파일](https://intl.cloud.tencent.com/document/product/607/10783)
[API 파일](https://intl.cloud.tencent.com/document/product/607/15210)

iOS 관련 파일:
[프로그래밍 설정 파일](https://intl.cloud.tencent.com/document/product/607/10783)
[API 파일](https://intl.cloud.tencent.com/document/product/607/15210)

Android 관련 파일:
[프로그래밍 설정 파일](https://intl.cloud.tencent.com/document/product/607/10783)
[API 파일](https://intl.cloud.tencent.com/document/product/607/15210)

Mac 관련 파일:
[프로그래밍 설정 파일](https://intl.cloud.tencent.com/document/product/607/10783)
[API 파일](https://intl.cloud.tencent.com/document/product/607/15210)

H5 관련 파일:
[프로그래밍 설정 파일](https://intl.cloud.tencent.com/document/product/607/10783)
[API 파일](https://intl.cloud.tencent.com/document/product/607/15210)



## 콘솔 사용량 통계
궁금한 사항은 [운영 매뉴얼](https://intl.cloud.tencent.com/document/product/607/17448)을 참고하십시오.


## 예외 사항 처리
궁금한 사항은 [일반 문제](https://intl.cloud.tencent.com/document/product/607/30254)를 참고하십시오.
궁금한 사항은 [에러코드](https://intl.cloud.tencent.com/document/product/607/15173)를 참고하십시오.



