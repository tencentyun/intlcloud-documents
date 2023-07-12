## 개요

Tencent Cloud Global Content Delivery(GCD)는 Tencent Cloud의 고성능 가속 노드를 전 세계 각지로 확장하는 제품으로, 전 세계 곳곳에 Static Content Delivery(SCD), Download Delivery(DD), 멀티미디어 VOD 가속 등 다양한 기능을 제공합니다.
현재 Tencent Cloud GCD는 베타 테스트를 실시하고 있으며, 테스트 정원이 한정되어 있으니 사용을 원하시면 베타 테스트 신청서를 제출하시기 바랍니다. CDN에서 GCD를 설정하는 자세한 방법은 다음과 같습니다.

>GCD 제품의 사용을 원하시면 먼저 활성화를 위한 신청을 해야 합니다.

## 적용 시나리오

- 해외 단말 사용자에 접근 시, 가속 액세스를 구현하고 액세스 딜레이를 단축하려는 경우
- 지역, 국가, 대륙 간 GB에서 TB 용량의 데이터를 전송할 경우
- 같은 콘텐츠를 짧은 시간에 반복적으로 다운로드할 경우

## 관련 설명

GCD 제품의 사용 신청이 승인되면 Tencent Cloud의 [GCD 콘솔](https://console.cloud.tencent.com/cdn/open_oversea)로 이동해 COS의 XML 액세스 도메인을 추가하여 가속 기능을 경험할 수 있습니다.
현재는 COS 콘솔에서 액세스 콘텐츠를 **공개**로 설정해야 GCD 도메인을 정상적으로 바인딩 및 이용하여 COS에 있는 콘텐츠에 액세스할 수 있습니다.

## 작업 순서
[Policy 권한 설정] > [GCD 액세스] > [CNAME 설정]의 작업 순서에 따라 설정하십시오.

### Policy 권한 설정

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인한 뒤 왼쪽 메뉴에서 [버킷 리스트]를 클릭하여 버킷 리스트 페이지로 이동합니다.
2. Policy 권한을 설정할 버킷을 클릭하여 버킷 관리 페이지로 이동합니다.
3. [권한 관리]를 클릭한 뒤 [Policy 권한 설정]을 찾아 공개 액세스 정책을 추가합니다.
4. [정책 추가]를 클릭한 뒤 다음 조건에 따라 **사용자**, **리소스**, **작업**을 설정합니다.
 - 효력: 허용
 - 사용자: 모든 사용자
 - 리소스: 모든 버킷
 - 작업: 읽기 작업 권한
![](https://main.qcloudimg.com/raw/3b29c902ad3ea3b64ef07485b813bf53.png)
5. [확인]을 클릭하여 Policy 권한 설정 사항을 저장합니다.

### GCD 액세스

1. COS 도메인 획득
[COS 콘솔](https://console.cloud.tencent.com/cos5)에서 가속화할 버킷의 액세스 도메인을 획득합니다. 예시:
```shell
examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
```
이미 정적 웹 사이트 기능을 활성화한 버킷을 가속화하고, 정적 웹 사이트의 관련 기능을 이용하려면 다음과 같은 정적 웹 사이트 도메인을 사용하십시오.
```shell
examplebucket-1250000000.cos-website.ap-guangzhou.myqcloud.com
```
2. 도메인 연결
Tencent Cloud의 [GCD 콘솔](https://console.cloud.tencent.com/cdn/open_oversea)에 로그인한 뒤 COS를 외부 원본으로 하여 도메인 하나를 추가합니다. 다음은 설정 항목에 관한 설명입니다.
 - Domain(도메인): GCD 플랫폼에서 바인딩할 액세스 도메인을 입력합니다.
 - Service Type(서비스 유형): COS는 보통 비정형 데이터입니다. 정적 가속 Static Content를 선택하시길 권장합니다.
 - Origin Type(원본 서버 유형): 외부 원본 External을 선택합니다.
 - Origin Domain(원본 서버 도메인): COS의 XML API 도메인이나 정적 웹 사이트 도메인을 입력합니다.
 - **Host header(원본 Host): 원본 서버 도메인과 동일하게 입력해야 합니다**.
![](https://main.qcloudimg.com/raw/691da49e660fb3a5675d371821e702d9.png)
기타 항목은 실제 상황에 맞게 설정하십시오.

### CNAME 설정
본인의 DNS 서비스 제공업체로 이동해 원하는 CNAME 기록을 추가하십시오. 설정 방법은 CDN의 [CNAME 설정](https://intl.cloud.tencent.com/document/product/228/3121) 문서를 참조하십시오.

## FAQ
- 미등록 도메인으로 GCD 액세스 가능 여부와 같은 사항이 궁금하다면 COS의 [FAQ](https://intl.cloud.tencent.com/document/product/436/30590) 문서를 참조하십시오.

