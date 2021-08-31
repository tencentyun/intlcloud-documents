사용자 도메인이 CDN에 액세스하면 시스템은 자동으로 사용자에게 `.cdn.dnsv1.com`을 확장자로 하는 CNAME 도메인을 할당하며, CDN 콘솔 [도메인 관리 페이지](https://console.cloud.tencent.com/cdn/domains)에서 확인할 수 있습니다. CNAME 도메인은 직접 액세스할 수 없으므로 도메인 서비스 공급자 측에서 CNAME 설정을 완료해야 합니다. 설정이 적용되면 바로 CDN 가속 서비스를 이용할 수 있습니다.
![img](https://main.qcloudimg.com/raw/073b948565743f7947aae8503eef995d.png)

## 설정 순서

본 문서는 Tencent Cloud 및 Alibaba Cloud의 CNAME 설정 방법을 설명합니다. 도메인 서비스 제공 업체에 따라 설정하십시오.

- [Tencent Cloud 설정 방법](#m1)
- [Alibaba Cloud 설정 방법](#m2)

[](id:m1)

### Tencent Cloud 설정 방법

> !리졸브의 각 기록 유형 간에는 우선순위의 차이가 있으므로 CVM 기록이 동일한 경우 같은 회선에 서로 다른 기록 유형이 공존할 수 없으며, 충돌이 발생할 수 있습니다. CNAME 기록은 다른 모든 기록 유형과 충돌하므로 설정하기 전에 먼저 다른 기록을 삭제해야 합니다.


1. [도메인 서비스](https://console.cloud.tencent.com/domain) 콘솔에 로그인한 후, 리스트에서 CNAME 기록을 추가할 도메인이 있는 행을 찾은 다음 작업 열에서 [리졸브]를 클릭합니다.

2. DNSPOD 페이지로 이동하여 해당 페이지에서 [기록 추가]를 클릭하고 다음 순서에 따라 CNAME 기록을 추가합니다.
   ![img](https://main.qcloudimg.com/raw/36f84a0d21b51bc56d79544943f0f752.png)
	
	- **CVM 기록**: 서브 도메인을 입력합니다. 예를 들어 `www.dnspod.com` 도메인 리졸브를 추가하는 경우 'CVM 기록'에서 'www'를 선택하면 되고, `dnspod.com` 도메인 리졸브만 추가하려면 '@'을 선택하면 됩니다.
	- **기록 유형**: 'CNAME'을 선택합니다.
	- **회선 유형**: '기본' 유형을 선택합니다. DNSPod는 여러 방식에 따라 회선을 구분하며, 해당 기록에 액세스할 사용자를 지정할 수 있습니다. 자세한 설명은 [리졸브 회선 설명](https://docs.dnspod.cn/dns/5f4775898ae73e11c5b01afc/)을 참조하십시오.
	- **기록 값**: 지정 도메인의 경우 일반적으로 가속 도메인의 CNAME 값인 xxx.xxx.com.cdn.dnsv1.com으로 입력합니다. 기록이 생성된 후 도메인 뒤에 '.'이 자동으로 추가되며, 이는 정상적인 현상입니다.
	- **가중치**: 동일한 CVM 기록을 가진 회선은 각 기록 값에 대해 가중치를 설정할 수 있으며, 리졸브 시 설정한 가중치 비율에 따라 반환합니다. 입력 범위는
		0~100까지의 정수입니다.
	- **MX 우선순위**: 입력할 필요 없습니다.
	- **TTL**: 캐시 시간입니다. 값이 작을수록 변경 기록이 더 빨리 적용되며 기본값은 600초입니다.
3. 입력 완료 후 [확인]을 클릭하면 CNAME 설정이 완료됩니다.

   

####  확장 설정
- 단일 CVM 기록의 [회선 유형]을 '기본'으로 설정하면 전체 사이트에 가속 서비스가 활성화됩니다.
예를 들어, 모든 사용자를 `1.com`으로 지정해야 할 경우, 회선이 기본 유형이고 기록 값이 `1.com`인 CANME 기록을 추가하여 구현할 수 있습니다.
![img](https://main.qcloudimg.com/raw/0c146a23008acc3c0e4884aa1c4d3a3c.png)

- 회선을 구분하여 가속 서비스를 활성화할 수도 있습니다.
China Mobile 사용자는 `1.com`으로, China Unicom 사용자는 `2.com`으로 지정해야 할 경우, [회선 유형]이 'China Mobile'이고 기록 값이 `1.com`인 기록과 [회선 유형]이 China Unicom이고 기록 값이 `2.com`인 CNAME 기록 2개를 추가하여 구현할 수 있습니다.
 ![](https://main.qcloudimg.com/raw/ecf4d1ad94eaf897473647459b923209.png)

>?회선 설정에 대한 자세한 설명은 [리졸브 회선 설명](https://docs.dnspod.cn/dns/5f4775898ae73e11c5b01afc/)을 참조하십시오.


[](id:m2)
### Alibaba Cloud 설정 방법

DNS 서비스 제공 업체가 Alibaba Cloud인 경우 다음 순서에 따라 CNAME 기록을 추가할 수 있습니다.

1. Alibaba Cloud 콘솔 클라우드 DNS에 로그인합니다.
2. 리졸브할 도메인을 클릭하여 리졸브 기록 페이지로 이동합니다.
3. 리졸브 기록 페이지에 들어간 후 [기록 추가] 버튼을 클릭하여 리졸브 기록 설정을 시작합니다.
4. CNAME 리졸브 기록을 설정하려면 기록 유형을 CNAME으로 선택해야 합니다. CVM 기록은 도메인의 접두사이며 임의로 입력할 수 있습니다(예: `www`). 기록 값은 현재 도메인에서 지정된 다른 도메인을 입력하고, 리졸브 회선은 TTL 기본 값으로 설정하면 됩니다.
![img](https://main.qcloudimg.com/raw/6b8bb9ce4f998b8d17ca27fd10512dc6.png)
5. 입력 완료 후 [확인]을 클릭하면 리졸브 설정이 완료됩니다.



## CNAME 적용 여부 검증

마지막으로, DNS 서비스 제공 업체에 따라 CNAME 적용 시간이 조금씩 다르며, 일반적으로 30분 내에 적용됩니다. nslookup 또는 dig 방식으로 CNAME 적용 여부를 확인할 수 있으며, 응답 CNAME 기록이 설정한 CNAME인 경우 설정이 완료되었고 가속 서비스가 활성화되었다는 의미입니다.

- `nslookup -qt=cname <가속 도메인>`
  ![img](https://main.qcloudimg.com/raw/89faaf228a2b88e23b82d0a839367c76.png)
- `dig <가속 도메인>`
  ![img](https://main.qcloudimg.com/raw/2ba5ec76f1671c3b8ee345cef896de10.png)
