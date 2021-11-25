![](https://qcloudimg.tencent-cloud.cn/raw/1d6aa270579356fd95585e86c8d375b2.png)

## 준비 작업

### 도메인 연결
CNAME을 설정하기 전에 [도메인 연결](https://intl.cloud.tencent.com/document/product/228/5734)을 완료해야 합니다. 도메인 액세스를 완료한 경우 다음 단계를 진행하시기 바랍니다.


## 작업 단계

### 설정 단계

DNS 서비스 제공업체에 따라 도메인이 있는 서비스 제공 업체에서 설정해야 합니다. 본 문서에서는 Tencent Cloud 및 Alibaba Cloud를 설정 방법을 안내합니다.

- [Tencent Cloud 설정 방법](#m1)
- [Alibaba Cloud 설정 방법](#m2)

[](id:m1)
### Tencent Cloud 설정 방법

#### 원클릭 설정

도메인 공급자가 Tencent Cloud인 경우 CNAME 원클릭 설정 기능을 사용하는 것이 좋으며, 자세한 내용은 [DNSPod를 통한 CNAME 설정](https://intl.cloud.tencent.com/document/product/228/42353)을 참고하십시오.



#### 수동 설정

1. [CDN 콘솔](https://console.cloud.tencent.com/cdn)에서 CNAME 주소를 복사합니다.
   도메인이 성공적으로 리졸브되기 전에 CNAME에 icon이 표시됩니다. 이 곳의 CNAME 값을 복사합니다.

2. [DNS 리졸브 DNSPod 콘솔](https://console.cloud.tencent.com/cns)에 로그인 후 **리졸브**버튼을 클릭합니다.

3. CNAME 레코드를 추가하고 **확인**을 클릭합니다.

4. 설정이 적용될 때까지 기다려주십시오.

**설정 항목 상세 설명:**

| 설정 항목   | 설정 설명                                                     |
| :------- | :----------------------------------------------------------- |
| 호스트 레코드 | 호스트 레코드는 도메인의 접두사와 동일합니다. <br><br>**예시:** `dnspod.com` 도메인의 리졸브를 추가하려면, ‘호스트 레코드’에서 ‘@’를 선택합니다. `www.dnspod.com` 도메인의 리졸브를 추가하려면, ‘호스트 레코드’에서 ‘www’를 선택합니다. |
| 레코드 유형 | ‘CNAME’ 선택.                                               |
| 회선 유형 | '기본' 유형을 선택합니다. DNSPod는 여러 방식에 따라 회선을 구분하며, 해당 레코드에 액세스할 사용자를 지정할 수 있습니다. 자세한 설명은 [리졸브 회선 설명](https://docs.dnspod.cn/dns/5f4775898ae73e11c5b01afc/)을 참고하십시오. |
| 레코드 값   | 지정 도메인의 경우 가속 도메인의 CNAME 값인 xxx.xxx.com.cdn.dnsv1.com을 입력합니다. 레코드가 생성된 후 도메인 뒤에 '.'이 자동으로 추가됩니다. |
| 가중치     | 동일한 CPM 레코드를 가진 회선은 각 레코드 값에 대해 가중치를 설정합니다. 리졸브 시 설정된 가중치 비율에 따라 반환됩니다. 입력 범위:0-100 |
| MX       | 우선순위 설정. 값이 낮을수록 우선순위가 높으므로 기본 값은 비어있는 상태로 유지하는 것이 좋습니다.       |
| TTL      | 캐시 시간. 값이 작을수록 레코드 변경이 더 빨리 적용되며 기본값은 600초입니다. |

[](id:m2)
### Alibaba Cloud 설정 방법

DNS 서비스 제공 업체가 Alibaba Cloud인 경우 다음 순서에 따라 CNAME 레코드를 추가할 수 있습니다.

1. [Tencent Cloud CDN 콘솔](https://console.cloud.tencent.com/cdn)에서 CNAME 주소를 복사합니다.
   도메인이 성공적으로 리졸브되기 전에 CNAME에 icon이 표시됩니다. 이 곳의 CNAME 값을 복사합니다.

2. Alibaba Cloud 콘솔에 로그인하여 클라우드 리졸브 DNS로 이동하십시오.
3. 리졸브하려는 도메인을 클릭하고 리졸브 레코드 페이지로 이동하십시오.
4. 리졸브 레코드 페이지에서 **레코드 추가** 버튼을 클릭하여 리졸브 레코드 설정을 시작합니다.
5. 레코드 유형으로 CNAME을 선택합니다. 호스트 레코드는 도메인 이름 접두사(예: www)입니다. 레코드 값은 1단계에서 복사한 CNAME 값을 입력합니다. ISP 회선 및 TTL에 대한 기본 설정을 유지합니다. 
<img src="https://main.qcloudimg.com/raw/6b8bb9ce4f998b8d17ca27fd10512dc6.png" width="80%">
6. 입력 완료 후 **확인**을 클릭하면 완료됩니다.

## 후속 작업

### CNAME 유효성 확인

DNS 서비스 제공 업체에 따라 CNAME 적용 시간이 조금씩 다르며, 일반적으로 30분 내에 적용됩니다. nslookup 또는 dig 방식으로 CNAME 적용 여부를 확인할 수 있으며, 응답 CNAME 레코드가 설정한 CNAME인 경우 설정이 완료되었고 가속 서비스가 활성화되었다는 의미입니다.

- nslookup -qt=cname <가속 도메인>
<img src="https://main.qcloudimg.com/raw/1f94ea7e3ee46fc761e8e839ce68a86d.png" width="70%">
- dig <가속 도메인></br>
<img src="https://main.qcloudimg.com/raw/fe9b8f9a1a26d3a7df5db614762caeaf.png" width="70%">

### 설정 가이드

CDN 서비스의 기본 설정이 완료되었습니다. CDN 서비스에 대한 자세한 설정은 [설정 가이드](https://intl.cloud.tencent.com/document/product/228/15417)의 해당 항목을 참고하십시오.

