## 배경 정보
WebShell 서버 용량 확장 및 업데이트로 인해 2021년 4월 1일부터 WebShell 프록시 IP 주소에 신규 IP 대역이 추가됩니다. 보안 그룹에서 새로 추가된 WebShell 프록시 IP 대역 및 원격 로그인 포트(기본값: 22 포트)를 개방할 수 있습니다.
>?WebShell 로그인 방식은 [표준 로그인 방식을 사용한 Linux 인스턴스 로그인(권장)](https://intl.cloud.tencent.com/document/product/213/5436)을 참조하십시오. 
>



## 조정 상세 내용
- 신규 프록시 IP 대역은 다음과 같습니다.
81.69.102.0/24
106.55.203.0/24
101.33.121.0/24
101.32.250.0/24
- 신규 및 기존 프록시 IP 주소/대역은 병행 사용됩니다. 아래 IP 주소/대역이 포함됩니다.
>?인스턴스가 WebShell에 정상적으로 로그인할 수 있도록 보안 그룹의 소스(인바운드)인 신규 및 기존 프록시 IP 대역 및 원격 로그인 포트를 개방하십시오.
>
81.69.102.0/24
106.55.203.0/24
101.33.121.0/24
101.32.250.0/24
115.159.198.247
115.159.211.178
119.28.7.195
119.28.22.215
119.29.96.147
211.159.185.38


## 관련 작업
- [표준 방식으로 Linux 인스턴스 로그인(권장)](https://intl.cloud.tencent.com/document/product/213/5436)
- [보안 그룹 규칙 추가](https://intl.cloud.tencent.com/document/product/213/34272)
