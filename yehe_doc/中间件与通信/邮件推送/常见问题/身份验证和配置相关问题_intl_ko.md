[](id:que1) 

### SES는 어떤 인증 메커니즘을 지원합니까?
SES는 DKIM(DomainKeys Identified Mail), SPF(Sender Policy Framework), DMARC(Domain-Based Message Authentication, Reporting and Conformance)를 비롯한 모든 산업 표준 인증 메커니즘을 지원합니다.

[](id:que2) 
### 발신자 도메인은 어떻게 구성합니까?
<dx-tabs>
::: 1단계: DNS 페이지에서 구성
1. [발신자 도메인](https://console.cloud.tencent.com/ses/domain) 구성 페이지에서 **도메인 생성**을 클릭한 후 도메인 이름을 입력하고 제출합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/00947cc2ff7a7dc6855baee29d1a77ee.png)
2. [DNSPod 콘솔](https://console.cloud.tencent.com/cns)에서 확인 정보를 구성합니다.
3. [](id:step2)[발신자 도메인](https://console.cloud.tencent.com/ses/domain) 구성 페이지로 돌아가서 **확인**을 클릭합니다.
4. 발신자 도메인 주소를 클릭하여 도메인 값을 볼 수 있는 구성 세부 정보 페이지로 이동합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/7f5e04d51b3a6976eec099353f62cc07.png)
5. 레코드를 추가하려면 [3단계](#step3)에서 보낸 사람 도메인 주소를 [DNSPod](https://console.cloud.tencent.com/cns) 페이지에 붙여넣습니다. 공백을 피하십시오.
 - DKIM 인증:
![](https://qcloudimg.tencent-cloud.cn/raw/db505d7e62fc62013e6d39d534dde126.png)
 - SPF 인증:
![](https://qcloudimg.tencent-cloud.cn/raw/c29031426e6fc6d7d8d073bb9bffea98.png)
 - _dmarc 레코드:
레코드 값으로 `v=DMARC1; p=none;rua=mailto:xxx@163.com;ruf=mailto:xxx@163.com;`를 입력합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/64dc22f5ec2da2840115bb869a1ba95e.png)
 <dx-alert infotype="explain"> `xxx@163.com`은 예시일 뿐입니다. 여기에서 예시를 발신 주소로 교체해야 합니다.</dx-alert>
6. [발신자 도메인](https://console.cloud.tencent.com/ses/domain) 구성 세부 정보 페이지로 돌아가서 **제출**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/b65213aa84bd379a250084e72c8c3a34.png)
:::
::: 2단계: 결과 확인
![](https://qcloudimg.tencent-cloud.cn/raw/275fb56fe9faa0a0ab3bd3735f3bd8c5.png)
![](https://qcloudimg.tencent-cloud.cn/raw/695ff02f3096d64481103a13e757362c.png)
![](https://qcloudimg.tencent-cloud.cn/raw/c9bc369664b4290a4048f94791f47209.png)

:::
::: 보충: 발신자 도메인이 레벨 3 도메인인 경우

1. [발신자 도메인](https://console.cloud.tencent.com/ses/domain) 구성 페이지에서 **도메인 생성**을 클릭하고 도메인 이름을 입력하고 제출합니다.
2. [DNSPod 콘솔](https://console.cloud.tencent.com/cns)에서 확인 정보를 구성합니다.
:::
</dx-tabs>

>?
>- 상기 구성 및 확인 후에도 문제가 지속되면 지원을 위해 [티켓 제출](https://console.cloud.tencent.com/workorder/category) 하시기 바랍니다.
>- Dnspod 확인이 등록되었지만 dig 명령으로 찾을 수 없는 경우 도메인에 대한 신원 확인이 완료되지 않아 레지스트리가 확인을 중지했기 때문일 수 있습니다.

