도메인이 CDN에 연결되면 시스템은 자동으로 사용자를 위해 `.cdn.dnsv1.com` 형식의 CNAME 도메인 이름을 할당하며, CDN 콘솔 [Domain Management 페이지](https://console.cloud.tencent.com/cdn/domains)에서 확인할 수 있습니다. CNAME 도메인에 직접 액세스할 수 없으므로 도메인 서비스 공급자에서 CNAME 설정을 완료해야 합니다. 설정이 적용되면 바로 CDN 가속화 서비스를 이용할 수 있습니다.
![img](https://main.qcloudimg.com/raw/073b948565743f7947aae8503eef995d.png)

## 설정 순서

본 문서에서는 Tencent Cloud, Alibaba Cloud 및 새 네트워크의 CNAME 설정 순서를 설명합니다.

- [Tencent Cloud 설정 방법](https://intl.cloud.tencent.com/document/product/228/3121#.E8.85.BE.E8.AE.AF.E4.BA.91.E8.AE.BE.E7.BD.AE.E6.96.B9.E6.B3.95)
- [Alibaba Cloud 설정 방법](https://intl.cloud.tencent.com/document/product/228/3121#.E9.98.BF.E9.87.8C.E4.BA.91.E8.AE.BE.E7.BD.AE.E6.96.B9.E6.B3.95)
- [새 네트워크 설정 방법](https://intl.cloud.tencent.com/document/product/228/3121#.E6.96.B0.E7.BD.91.E8.AE.BE.E7.BD.AE.E6.96.B9.E6.B3.95)



<span ID ="m1"></span>
### Tencent Cloud 설정 방법

>! 리졸브의 다양한 기록 유형 간에는 우선 순위의 차이가 있어 동일한 호스트 기록의 경우 동일 회선에 다른 기록 유형이 공존할 수 없으며, 충돌이 발생할 수 있습니다. CNAME 기록은 다른 기록 유형과 충돌하므로 설정하기 전에 다른 기록을 삭제해야 합니다.

1. [도메인 서비스](https://console.cloud.tencent.com/domain) 콘솔에 로그인한 후, 리스트에서 CNAME 기록을 추가할 도메인 라인을 찾아 작업 표시줄에서 [리졸브]를 클릭합니다.
![CNAME 설정](https://main.qcloudimg.com/raw/dd299f2ef44538523622a7de978d5995.png)
2. DNSPOD 페이지로 이동하여 [기록 추가]를 클릭하고 다음 순서에 따라 CNAME 기록을 추가합니다.
![img](https://main.qcloudimg.com/raw/36f84a0d21b51bc56d79544943f0f752.png)
	- **호스트 기록**: 서브 도메인을 작성합니다. 예를 들어 `www.dnspod.com` 리졸브를 추가하려면 "호스트 기록"에서 “www”를 선택하고, `dnspod.com` 리졸브만 추가하려면 "호스트 기록"에서 "@"을 선택하면 됩니다. "@" CNAME은 MX 기록의 정상적인 리졸브에 영향을 미치므로 추가할 때 신중하게 고려하십시오.
	- **기록 유형**: "CNAME"을 선택합니다.
	- **회선 유형**: "기본" 유형을 선택합니다. DNSPod는 다양한 방식에 따라 회선을 분할하여 지정된 사용자가 해당 기록을 액세스할 수 있도록 지원합니다. 자세한 설명은 [리졸브 회선 설명](https://docs.dnspod.cn/dns/5f4775898ae73e11c5b01afc/)을 참조하십시오.
	- **기록값**: CNAME이 가리키는 도메인으로, 도메인만 입력할 수 있습니다. 기록 생성 후 도메인 뒤에 "."가 자동으로 추가되며, 이는 정상적인 현상입니다.
	- **가중치**: 호스트 기록이 동일한 회선에 서로 다른 기록값에 초점을 맞춰 가중치를 설정할 수 있으며, 리졸브 시 설정한 가중치 비중에 따라 반환됩니다. 가중치는 0~100 사이의 정수를 입력할 수 있습니다.
	- **MX 우선순위**: 작성할 필요 없습니다.
	- **TTL**: 캐시 시간입니다. 값이 작을수록 변경 기록이 더 빨리 적용되며, 기본적으로 600초로 설정되어 있습니다.

### Tencent Cloud 회선 분할 가속 활성화

- 호스트 기록 회선을 "기본" 유형으로 설정할 수 있으며 전체 사이트의 가속 서비스가 활성화됩니다.
	 예를 들어 모든 사용자를 1.com으로 유도해야 하는 경우 회선 유형이 기본이고 기록값이 `1.com`인 CNAME 기록을 추가해 구현할 수 있습니다.
![img](https://main.qcloudimg.com/raw/be770e0f8b91c33ae7c41f1e50e633af.png)
- 회선을 분할하여 가속 서비스를 활성화할 수도 있습니다.
예를 들어 China Unicom 사용자를 `2.com`으로, 모바일 사용자를 `1.com`으로 유도해야 하는 경우 회선 유형이 모바일, 기록값이 `1.com`인 CNAME 기록과 회선 유형이 China Unicom, 기록값이 `2.com`인 CNAME 기록을 추가하여 구현할 수 있습니다. 설정에 대한 자세한 설명은 [리졸브 회선 설명](https://docs.dnspod.cn/dns/5f4775898ae73e11c5b01afc/)을 참조하십시오.
![](https://main.qcloudimg.com/raw/a10e6be051e2b90a323cb8e07081fb63.png)

<span ID ="m2"></span>
### Alibaba Cloud 설정 방법

DNS 서비스 제공 업체가 Alibaba Cloud인 경우 다음 순서에 따라 CNAME 기록을 추가할 수 있습니다.

1. Alibaba Cloud 콘솔에 로그인하여 클라우드 리졸브 DNS로 이동합니다.
2. 리졸브하려는 도메인을 클릭하여 리졸브 기록 페이지로 이동합니다.
3. 리졸브 기록 페이지에서 [기록 추가] 버튼을 클릭하여 설정을 시작합니다.
4. CNAME 리졸브 기록을 설정하려면 기록 유형을 CNAME으로 선택합니다. 호스트 기록은 도메인 접두사이며 임의로 입력할 수 있습니다(예: `www`). 기록 값은 현재 도메인에서 유도하는 다른 도메인을 입력하고, 리졸브 회선과 TTL은 기본 설정으로 두면 됩니다.
   ![img](https://main.qcloudimg.com/raw/1e5d2b3e6e142b5f0900cc4065bd0864.png)
5. 입력 완료 후 [확인]을 클릭하여 리졸브 설정을 완료합니다.



<span ID ="m3"></span>
### 새 네트워크 설정 방법

DNS 서비스 제공 업체가 새 네트워크인 경우 아래 순서에 따라 CNAME 기록을 추가할 수 있습니다.
**별명 설정(CNAME 기록)**
즉, 별명 기록으로, 여러 이름을 동일한 컴퓨터에 매핑할 수 있도록 허용합니다. 일반적으로 WWW와 MAIL 서비스를 모두 제공하는 컴퓨터에서 사용됩니다. 예를 들어 `host.mydomain.com`(A 기록) 이라는 컴퓨터가 사용자의 서비스 액세스 편의를 위해 WWW와 MAIL 서비스를 모두 제공하는 경우, 해당 컴퓨터에 다음 이미지와 같이 WWW와 MAIL의 별명(CNAME)을 각각 설정할 수 있습니다.
![img](https://main.qcloudimg.com/raw/2e93d51c7fe8502670475d71bbfb20cb.png)

## CNAME 유효성 검사

DNS 서비스 제공 업체별 CNAME 적용 시간은 약간씩 다르며 일반적으로 30분 내에 적용됩니다. nslookup 또는 dig를 사용하여 CNAME이 생성되었는지 확인할 수 있습니다.

- `nslookup -qt=cname <가속 도메인>`
- `dig <가속 도메인>`
  ![img](https://main.qcloudimg.com/raw/2ba5ec76f1671c3b8ee345cef896de10.png)
