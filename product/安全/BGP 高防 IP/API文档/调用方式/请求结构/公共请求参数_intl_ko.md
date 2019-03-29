[//]: # (chinagitpath:XXXXX)

완전한 Tencent Cloud API 요청은 두 가지의 요청 매개변수, 즉 공용 요청 매개변수와 API 요청 매개변수가 필요합니다. 본 문서는 Tencent Cloud API 요청에 필요한 6개의 공용 요청 매개변수를 소개합니다. API 요청 매개변수 관련 상세 설명은 [API 요청 매개변수](https://cloud.tencent.com/document/product/1014/31225)를 참조하십시오.
공용 요청 매개변수는 모든 API에 필요한 요청 매개변수로, 개발자가 Tencent Cloud API를 사용하여 요청을 발송할 때마다 이 공용 요청 매개변수를 지참하지 않으며 요청이 실패됩니다. 공용 요청 매개변수의 이니셜은 대문자이며 API 요청 매개변수와 구별됩니다.

공용 요청 매개변수 리스트는 다음과 같습니다.
>**주의:**
>본 문서 중 API 인스턴스는 Tencent Cloud CVM을 예로 하며 기타 Tencent Cloud 제품별 사용법은 해당 제품 문서를 참조하십시오.

| 매개변수 이름 | 설명 | 유형 |필수 여부|
|---------|---------|---------|---------|
| Action | 작업별 API 명령어의 이름입니다. 예를 들어 Tencent Cloud CVM 사용자가 [인스턴스 리스트 조회](https://cloud.tencent.com/document/api/213/9388) API를 호출하면, Action 매개변수는 DescribeInstances가 됩니다. | String |네|
| Region | 지역 매개변수. 작업하려는 인스턴스가 소재 지역을 식별하는 데 사용합니다. 상세 정보는 [지역과 가용 영역](https://cloud.tencent.com/document/product/213/6091) 리스트를 참조하거나 [지역 리스트 조회](https://cloud.tencent.com/document/api/213/9456) API를 사용하여 조회할 수 있습니다. <br>**주의:** 1. 일반적으로 이 매개변수는 필수입니다. 필요 없을 경우, 해당 API에서 표시됩니다.<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2. 일부 지역은 내부 테스트 중이므로 현재 일부 사용자만 사용할 수 있습니다.| String |아니요|
| Timestamp | 현재 UNIX 타임스탬프로 API 요청한 시간을 기록할 수 있습니다.| UInt |네|
| Nonce | 랜덤 양의 정수. Timestamp와 결합하여 재전송 공격 방지에 사용됩니다.| UInt |네|
| SecretId | [클라우드 API 키](https://console.cloud.tencent.com/capi)에서 신청한 ID의 식별에 사용됩니다. SecretId 1개는 유일한 SecretKey와 대응하며, SecretKey는 요청 서명 Signature 생성에 사용됩니다. 상세 정보는 [서명 방법](https://cloud.tencent.com/document/product/215/1693)을 참고할 수 있습니다.|String|네|
| Signature | 요청 서명입니다. 요청의 유효성을 검증하는 데 사용하며, 사용자가 실제 입력한 매개변수에 따라 계산해야 합니다. 계산 방법은 [서명 방법](https://cloud.tencent.com/document/product/215/1693)을 참조하십시오.|String|네|
| SignatureMethod | 서명 방식입니다. 현재 HmacSHA256과 HmacSHA1을 지원합니다. 이 매개변수를 HmacSHA256으로 지정해야만 HmacSHA256 알고리즘을 사용하여 서명을 검증합니다. 다른 상황에서는 HmacSHA1을 사용하여 서명을 검증합니다. 서명 알고리즘 방법에 대한 자세한 설명은 [서명 방법](https://cloud.tencent.com/document/product/215/1693)을 참조하십시오.|String|아니요|
| Token | 임시 인증서에서 사용한 Token입니다. 임시 키와 결합하여 함께 사용해야 합니다. 장기간 키는 Token이 필요하지 않습니다.|String|아니요|

### 사용 사례
Tencent Cloud 제품 API 요청 링크에서 공용 요청 매개변수 형식은 다음과 같습니다. Tencent Cloud CVM을 예로, 사용자가 광저우 지역의 CVM 인스턴스 리스트를 조회해야 할 경우, 요청 링크 형식은 다음과 같습니다.

<pre>
https://cvm.api.qcloud.com/v2/index.php?
Action=DescribeInstances
&SecretId=xxxxxxx
&Region=ap-guangzhou
&Timestamp=1465055529
&Nonce=59485
&Signature=mysignature
&SignatureMethod=HmacSHA256
&<API 요청 매개변수>
</pre>



