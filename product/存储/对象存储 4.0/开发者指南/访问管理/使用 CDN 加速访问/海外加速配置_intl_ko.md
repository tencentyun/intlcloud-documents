## 개요

Tencent Cloud GCD는 Tencent Cloud의 고성능 가속 노드를 전 세계 각지에 확장하여 전 세계 범위 내에서 정적 콘텐츠 가속, 다운로드 배포 가속, 오디오/비디오 VOD 가속 등 다양한 기능 지원을 제공합니다.
현재 Tencent Cloud GCD는 공개판 단계에 있으며 테스트 인원수가 제한되어 있습니다. 사용을 원하시면 공개판 신청 티켓을 제출하십시오. 자세한 내용은 [신청 방식](https://cloud.tencent.com/document/product/673/30415)을 참조하여 세부 정보를 파악하십시오. 다음은 CDN GCD에 대한 구체적 소개입니다.

>!사용 신청을 통과해야만 GCD 제품을 사용할 수 있습니다.

## 적용 시나리오

- 해외 최종 사용자에게 전달하고 접근을 가속하며 접근 지연을 줄이는 시나리오.
- 지역 간, 국가 간, 대륙 간 GB 단위에서 TB 단위 까지의 데이터 전송이 필요하는 시나리오.
- 동일 콘텐츠의 고밀도로 반복적으로 다운로드하는 시나리오.

## 관련 설명

GCD 제품의 사용 신청이 통과되면 Tencent Cloud의 [GCD 콘솔](https://console.cloud.tencent.com/cdn/open_oversea)에서 COS의 XML 접근 도메인 이름을 추가하여 가속할 수 있습니다.
현재, COS에서 접근 콘텐츠를 **공개**로 설정하면 COS 콘텐츠에 정상 바인딩할 수 있고 GCD 도메인 이름을 사용하여 COS의 콘텐츠에 접근할 수 있습니다.

## 작업 절차
다음 작업 절차를 읽고 순서에 따라 구성하십시오. [정책 권한 구성] > [GCD 구성] > [CNAME 구성].

### 정책 권한 구성

1. Tencent Cloud [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인하고 관리 페이지에 액세스합니다. [권한 관리] 탭을 클릭하여 공개 접근 정책을 추가합니다.
![](https://main.qcloudimg.com/raw/b1c0862f797da9d1447bc6a13929a927.png)
2. [정책 추가]를 클릭하고 다음 구성에 따라 **사용자**, **리소스**, **작업**을 설정하십시오.
 - 효력: 허용.
 - 사용자: 모든 사용자.
 - 리소스: 전체 버킷.
 - 작업: 파일 읽기 작업 권한
![](https://main.qcloudimg.com/raw/953311e15a9ca272dc5fece6a87ac6b7.png)

### GCD 구성

1. COS 도메인 이름 획득
[COS 콘솔](https://console.cloud.tencent.com/cos5)에서 가속할 버킷의 접근 도메인 이름을 획득합니다. 예:
```shell
examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
```
만약 정적 웹사이트 기능을 활성화한 버킷을 가속하고 정적 웹사이트의 관련 기능을 사용하고자 할 경우, 정적 웹사이트 도메인 이름을 사용하십시오. 예:
```shell
examplebucket-1250000000.cos-website.ap-guangzhou.myqcloud.com
```

2. 도메인 이름 바인딩
Tencent Cloud [GCD 콘솔](https://console.cloud.tencent.com/cdn/open_oversea)에 로그인하고 COS를 자체 서버로 사용하며 하나의 도메인 이름을 추가합니다. 구성 항목에 대한 설명은 다음과 같습니다.
 - 도메인 이름: GCD 플랫폼에 바인딩할 접근 도메인 이름을 입력합니다.
 - 비즈니스 유형: COS는 대부분 비구조화 데이터이므로 정적 가속 선택을 권장합니다.
 - 오리진 서버 유형: External(자체 오리진)
 -  오리진 서버(도메인 이름): COS의 XML API 도메인 이름 또는 정적 웹사이트 도메인 이름을 입력합니다.
 - **호스트 헤더(오리진 요청 호스트): 반드시 오리진 서버 도메인 이름과 일치하게 입력해야 합니다**.
![](https://main.qcloudimg.com/raw/691da49e660fb3a5675d371821e702d9.png)
다른 옵션은 실제 수요에 따라 설정하십시오. 더 자세한 내용은 GCD의 [시작 가이드](https://cloud.tencent.com/document/product/673/14422) 문서를 참조하십시오.

### CNAME 구성
DNS 서비스 업체에서 해당하는 CNAME 기록을 추가하십시오. 구성 방법은 CDN의 [CNAME 구성](https://cloud.tencent.com/document/product/228/3121) 문서를 참조하십시오.

## FAQ
ICP 라이센스가 없는 도메인 이름이 GCD에 액세스 가능 여부 등 문제는 COS [FAQ](https://cloud.tencent.com/document/product/436/30737#.E5.B0.9A.E6.9C.AA.E5.A4.87.E6.A1.88.E7.9A.84.E5.9F.9F.E5.90.8D.E5.8F.AF.E4.BB.A5.E6.8E.A5.E5.85.A5.E6.B5.B7.E5.A4.96.E5.8A.A0.E9.80.9F-gcd-.E5.B9.B3.E5.8F.B0.E5.90.97.EF.BC.9F) 문서를 참조하십시오.
CDN 가속에 대한 더 많은 질문은 GCD [FAQ](https://cloud.tencent.com/document/product/673/31673) 문서에서 솔루션을 찾아보십시오.

