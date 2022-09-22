## 소개
Cloud Workload Protection Platform（CWPP）은 Tencent Security가 축적한 방대한 보안 리스크 데이터를 기반으로, 머신 러닝을 통해 사용자에게 제공하는 해커 침입 감지, 취약점 리스크 알람 등 보안 서비스입니다. 주로 비밀번호 크래킹 차단, 원격 로그인 알림, 트로이 목마 파일 감지, 고위험 취약점 모니터링 등 다양한 기능을 포함하고 있습니다. 서버가 직면한 네트워크 보안 리스크를 해결하고, 기업의 서버 보안 체계 구축을 지원하여, 데이터 유출을 방지합니다.

CWPP는 기본 보호와 전문 보호의 두 가지 버전으로 나뉩니다. Tencent Cloud CVM를 생성할 때 기본적으로 CWPP 기본 보호를 무료로 활성화하도록 선택할 수 있습니다.


<dx-alert infotype="explain" title="">
CWPP 기본 보호와 전문 보호 기능에 대한 소개 및 비교는 [기능 소개 및 버전 비교](https://intl.cloud.tencent.com/document/product/296/2222)를 참고하십시오.
</dx-alert>



## 과금 방식
CWPP 기본 보호는 서비스 요금이 부과되지 않습니다.


## CWPP 기본 보호 설치
실제 상황에 따라 다음과 같은 방법으로 CWPP 기본 보호를 설치할 수 있습니다.
<dx-tabs>
::: 클라우드 서버 생성 시 자동 설치
Tencent Cloud CVM을 생성할 때 기본적으로 CWPP 기본 보호를 무료로 활성화하도록 선택할 수 있습니다. CVM 인스턴스 구매 페이지의 ‘보안 강화’에서 ‘무료 활성화’를 선택하여 CWPP를 자동으로 설치합니다. 아래 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/0fdf0fddce3b59f80bdd337c1cf74e86.png)
:::
::: 기존 CVM에 수동 설치
기존 인스턴스에 CWPP를 설치해야 하는 경우 해당 인스턴스의 운영 체제에 따라 다음과 같이 설치하십시오.
- [Windows CVM 환경](https://intl.cloud.tencent.com/document/product/296/12236)
- [Linux CVM 환경](https://intl.cloud.tencent.com/document/product/296/12236)
:::
</dx-tabs>

설치 완료 후, [CVM 콘솔 개요 페이지](https://console.cloud.tencent.com/cvm/overview) 또는 [CWPP 콘솔](https://console.cloud.tencent.com/CWPP)에서 CVM의 보안 상태를 확인할 수 있습니다.


## 관련 문서
- CWPP의 기본 보호 및 전문 보호 [기능 소개 및 버전 비교](https://intl.cloud.tencent.com/document/product/296/2222)
- [보안 개요](https://intl.cloud.tencent.com/document/product/296/35234)
