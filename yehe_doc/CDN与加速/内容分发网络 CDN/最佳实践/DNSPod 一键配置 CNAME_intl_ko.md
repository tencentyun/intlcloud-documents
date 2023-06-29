

Tencent Cloud CDN과 [DNSPod](https://console.dnspod.cn/)에 리졸브 설정 기능이 연결되었습니다. Tencent Cloud DNSPod에 호스팅된 도메인의 경우 [CDN 콘솔](https://console.cloud.tencent.com/cdn/domains)을 통해 CNAME을 원클릭 설정하여, 설정 작업 절차 및 시간을 줄이고 빠르게 CDN 가속 서비스를 활성화할 수 있습니다.

>! 중국 포털만 지원합니다(글로벌 포털 미지원).

## 배경

도메인에 CDN을 연결한 후, 시스템은 자동으로 `.cdn.dnsv1.com`을 확장자로 하는 CNAME 도메인을 할당하며, CDN 콘솔 [도메인 관리](https://console.cloud.tencent.com/cdn/domains) 페이지에서 확인할 수 있습니다. CNAME 도메인은 직접 액세스할 수 없으므로, 도메인 서비스 공급자측에서 CNAME 설정을 완료해야 합니다. CNNAME 레코드가 적용된 후, 즉시 CDN 가속 서비스를 활성화할 수 있습니다.

## 시나리오

Tencent Cloud CDN 및 DNSPod을 동시에 사용하는 사용자는, CNAME 레코드을 설정하고 CDN 가속 서비스를 활성화합니다.

## 운영 가이드

### DNSPod에 도메인 호스팅하기

우선 DNSPod에 도메인 리졸브를 호스팅해야 합니다. 자세한 내용은 [DNSPod에 도메인 리졸브 호스팅](https://docs.dnspod.cn/dns/60b99ba0e90008112f815bde/)을 참고하십시오.

### CDN 서비스 이용

#### 도메인 연결

[CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인하고 왼쪽 메뉴에서**도메인 관리**를 클릭하여 도메인 관리 페이지로 이동한 후, **도메인 추가**를 클릭하여 가속할 도메인을 추가합니다. 자세한 내용은 [도메인 연결](https://intl.cloud.tencent.com/document/product/228/5734)을 참고하십시오.

#### CNAME 설정

CDN 콘솔 [도메인 관리](https://console.cloud.tencent.com/cdn/domains) 페이지에서 해당 가속 도메인을 찾아, 마우스를 CNAME 앞의 아이콘에 갖다 대면 관련 알림을 볼 수 있습니다. **원클릭 설정**을 클릭하여 CNAME을 설정합니다.



선택한 도메인의 가속 서비스를 정식 활성화하기 위해 도메인 DNSPod측 리졸브 레코드에 대해 다음과 같은 처리 작업을 수행합니다.

1. 도메인에 리졸브 레코드를 미설정한 경우: 기본 회선 유형의 Tencent Cloud CDN CNAME 레코드를 추가합니다. TTL 기본값: 600.
2. 도메인에 리졸브 레코드를 설정한 경우: 설정된 모든 리졸브 레코드를 일시 중지하고, 기본 회선 유형의 Tencent Cloud CDN CNAME 레코드를 추가합니다. TTL 기본값: 600.
**참고: 도메인에 설정된 모든 리졸브 레코드를 일시 중지하면 도메인의 현재 DNS 리졸브 서비스에 영향을 미칠 수 있으므로 주의하시기 바랍니다.**


[DNSPod 콘솔](https://console.dnspod.cn/dns/list)로 이동하여 리졸브 레코드를 관리할 수 있습니다. 


>! 현재 계정에 해당 도메인에 대한 관리 권한이 있는지 확인하십시오. 
>서브 계정 또는 협업 파트너 계정인 경우 루트 계정을 통해 권한을 받으십시오. 예: 해당 CDN 가속 도메인의 쓰기 권한 + QcloudDNSPodFullAccess 권한 부여.

### CNAME 설정 완료

리졸브 원클릭 설정을 제출하면 약 1분 정도 후에 적용되오니 잠시만 기다려주십시오. CDN 콘솔 [도메인 관리](https://console.cloud.tencent.com/cdn/domains)페이지를 새로고침하여 CNAME이 활성화 상태로 바뀐 후 마우스를 CNAME 앞의 아이콘에 갖다 대면 ‘가속 서비스 정상 실행 중’이라는 알림을 볼 수 있습니다. 

>?해당 기능을 사용하지 않고 CNAME을 직접 설정하려면 [CNAME 설정](https://intl.cloud.tencent.com/document/product/228/3121)을 참고하십시오.

## 기타
추후에 해당 가속 도메인을 삭제하는 경우, 삭제 후 당사는 사용자의 DNSPod측 리졸브 레코드를 운영하지 않으므로, 필요에 따라 리졸브 레코드를 자체 수정하시기 바랍니다.

