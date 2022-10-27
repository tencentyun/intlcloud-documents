[](id:que1) 

### SES는 어떤 인증 메커니즘을 지원합니까?
SES는 DKIM(DomainKeys Identified Mail), SPF(Sender Policy Framework), DMARC(Domain-Based Message Authentication, Reporting and Conformance), MX 레코드(Mail Exchanger record)를 비롯한 모든 산업 표준 인증 메커니즘을 지원합니다.

[](id:que2) 
### 발신자 도메인은 어떻게 구성합니까?
<dx-tabs>
::: 1단계: DNS 페이지에서 구성
1. [발신자 도메인](https://console.cloud.tencent.com/ses/domain) 구성 페이지에서 **생성**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/57ab829c645dcb868dbb1643ffc3378d.png)
2. 도메인을 입력하고 **제출**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/43d669f7d15b74bd3f1d11dd3c61d969.png)
<dx-alert infotype="explain" title="">
- sampledomain.com은 예시일 뿐이며 발신자 도메인 이름으로 대체해야 합니다.
- sampledomain.com 형식의 도메인은 기본 도메인이고 abc.sampledomail.com 형식의 도메인은 기본이 아닌 도메인입니다. 다음 구성 단계는 도메인 유형(기본 또는 기본이 아닌)에 따라 다릅니다. 자세한 내용은 해당 설명을 참고하십시오.
</dx-alert>
3. [발신자 도메인](https://console.cloud.tencent.com/ses/domain) 구성 페이지로 돌아가서 **인증**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/305ea2b8c9b3c5f10e0dbbe6135b3666.png)
4. 팝업 창에 표시된 ‘레코드 값’을 기록합니다.[](id:step4)
>?아래는 예시입니다. 실제 내용은 해당 페이지에 표시된 대로입니다.
>
![](https://qcloudimg.tencent-cloud.cn/raw/70bfe55a17122848c7f829c5b4b86653.png)
5. Tencent Cloud로 도메인을 호스팅하는 경우 [DNSPod 콘솔](https://console.cloud.tencent.com/cns)에 로그인하여 인증 정보를 구성합니다. 발신자 도메인을 클릭하여 구성 페이지로 이동할 수 있습니다.
<dx-alert infotype="explain" title="">
도메인이 다른 도메인 서비스 제공 업체에서 호스팅되는 경우 체크리스트의 지침에 따라 구성합니다.
</dx-alert>
6. 기본 도메인 sampledomain.com을 예로 들어 레코드를 추가합니다. 위의 [4단계](#step4)에서 얻은 ‘레코드 값’을 입력합니다.
  - MX 인증
    호스트 레코드: `@`
    레코드 유형: MX
    레코드 값: `mxbiz1.qq.com.` 이메일 서버가 있는 경우 레코드 값에 이메일 서버 주소를 입력합니다.
<dx-alert infotype="explain" title="">
- 기본이 아닌 도메인(예: abc.sampledomain.com)의 경우 호스트 레코드는 abc여야 합니다.
- 레코드 값이 ‘.’로 끝나는지 확인하십시오. 일부 도메인 서비스 제공 업체는 기본적으로 MX 레코드의 끝에 ‘.’를 추가합니다.
</dx-alert>
  - SPF 인증:
  호스트 레코드: `@`
  레코드 유형: TXT
  레코드 값: `v=spf1 include:qcloudmail.com ~all`
<dx-alert infotype="explain" title="">
- 기본이 아닌 도메인(예: abc.sampledomain.com)의 경우 호스트 레코드는 abc여야 합니다.
- 여러 이메일 푸시 서비스 제공 업체가 있는 경우 이러한 모든 서비스 제공 업체의 도메인을 포함해야 합니다(예: v=spf1 include:qcloudmail.com include:domain1.com ~all ). 여기서 domain1.com은 다른 이메일 푸시 서비스 제공 업체의 도메인을 나타냅니다. 발신 도메인의 DNS 구성에 SPF 레코드가 하나만 있는지 확인합니다.
</dx-alert>
  - DKIM 인증:
    호스트 레코드: `qcloud._domainkey`
  레코드 유형: TXT
  레코드 값은 귀하의 ‘레코드 값’이어야 합니다.
<dx-alert infotype="explain" title="">
기본이 아닌 도메인(예: abc.sampledomain.com)의 경우 호스트 레코드는 qcloud._domainkey.abc여야 합니다.
</dx-alert>
- DMARC 인증:
  호스트 레코드: `_dmarc`
  레코드 유형: TXT
  레코드 값: `v=DMARC1; p=none`
  <dx-alert infotype="explain" title="">
- 기본이 아닌 도메인(예: abc.sampledomain.com)의 경우 호스트 레코드는 _dmarc.abc여야 합니다.
- DMARC 레코드는 v 및 p 플래그를 포함해야 합니다. DMARC에 대해 많이 알고 있는 경우 필요에 따라 다른 플래그를 추가하거나 플래그 값을 수정할 수 있습니다.
</dx-alert>

7. [4단계](#step4) 인터페이스로 돌아가 **제출**을 눌러 인증합니다. ‘현재 값’은 위의 DNS 구성에서 구성한 것을 보여줍니다. 인증 상태가 **인증됨**이 되면 구성이 완료된 것입니다.

:::
::: 2단계: 결과 인증
<dx-alert infotype="explain" title="">
‘1단계’의 구성 작업이 완료되고 발신자 도메인이 ‘인증됨’인 경우 이 인증 단계를 건너뜁니다.
</dx-alert>
본문은 dig 명령으로 DNS 도메인 서버를 쿼리하고 발신자 도메인이 올바르게 설정되었는지 확인하는 방법을 설명합니다.
명령 라인에 다음 명령을 각각 입력하고 엔터 키를 눌러 반환된 값이 발신자 도메인 구성 페이지에 표시된 값과 동일한지 확인합니다.
- `dig mx +short sampledomain.com`
![](https://qcloudimg.tencent-cloud.cn/raw/76cf66d8a42bee99a696b505eb8d8b2c.png)
- `dig txt +short sampledomain.com`
![](https://qcloudimg.tencent-cloud.cn/raw/f5fe74ee3c0c8312253359f8a3457db1.png)
- `dig txt +short _dmarc.sampledomain.com`
![](https://qcloudimg.tencent-cloud.cn/raw/2c53ae3c3789e220e7f939be536152bf.png)
- `dig txt +short qcloud._domainkey.sampledomain.com`
![](https://qcloudimg.tencent-cloud.cn/raw/5c773b8278d5d424a652b396f42fc591.png)


<dx-alert infotype="explain" title="">
상기 명령의 sampledomain.com은 예시일 뿐이며 발신자 도메인 이름으로 대체해야 합니다.
</dx-alert>




:::
</dx-tabs>

<dx-alert infotype="explain" title="">

- 위와 같이 구성 및 확인 후에도 문제가 지속되면 지원을 위해 [티켓 제출](https://console.cloud.tencent.com/workorder/category) 하시기 바랍니다.
- Dnspod 확인을 사용했지만 dig 명령으로 찾을 수 없는 경우 도메인에 대한 ID 확인이 완료되지 않아 레지스트리가 확인을 중지했기 때문일 수 있습니다.
</dx-alert>
