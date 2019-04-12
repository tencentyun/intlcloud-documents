완전한 Tencent Cloud API 요청은 공통 요청 매개변수와 API 요청 매개변수가 필요합니다. 이 문서에서는 Tencent Cloud API 요청에 필요한 6개 공통 요청 매개변수에 대해 설명합니다. API 요청 매개변수에 대한 자세한 설명은 API 요청 매개변수 섹션을 참조하십시오.
공통 요청 매개변수는 모든 API에서 사용해야 하는 요청 매개변수입니다. 개발자가 Tencent Cloud API로 요청을 보낼 때마다 공통 요청 매개변수를 전달해야 합니다. 그렇지 않으면 요청이 실패합니다. 공통 요청 매개변수의 첫 문자는 대문자이므로 API 요청 매개변수와 구별됩니다.

공통 요청 매개변수의 구체적인 리스트는 다음과 같습니다.

|매개변수 이름   | 필수 여부  |  유형 | 설명  |
| ------------ | ------------ | ------------ | ------------ |
| Action |  예 | String |  구체적인 조작에 대한 명령 API 이름. 예를 들어 페더레이션 ID 임시 자격 증명 API를 호출하려면 GetFederationToken을 선택합니다. |
| Region  |  아니요 | String  |  지역 매개변수, 호출할 STS 서비스가 속한 지역을 식별하는 데 사용됩니다. 주의 사항: 1.현재 ap-guangzhou 및 ap-shanghai만 대외적으로 공개되었으며 다른 지역은 내부 테스트 중입니다. 2.기본값은 ap-guangzhou입니다.|
|  Timestamp | 예  | UInt  | 현재 UNIX 타임스탬프, API 요청이 시작된 시점을 기록할 수 있습니다.  |
|  Nonce | 예  |  UInt | 랜덤 양의 정수, 재전송 공격을 막기 위해 Timestamp와 결합합니다. |
| SecretId  | 예  |  String |  [Cloud API 키](https://console.cloud.tencent.com/capi)에서 신청된 신분을 식별하는 SecretId입니다. 하나의 SecretId는 하나의 SecretKey에 해당하며 SecretKey는 요청 서명을 생성하는 데 사용됩니다. 자세한 내용은 [서명 방법](https://cloud.tencent.com/document/api/377/4214) 섹션을 참조할 수 있습니다. |
|  Signature |  예 |  String |  요청 서명, 요청의 유효성을 확인하는 데 사용되며 사용자가 실제 입력 매개변수를 기반으로 계산해야 합니다. 계산 방법은 [서명 방법](https://cloud.tencent.com/document/api/377/4214) 섹션을 참조할 수 있습니다. |
|  SignatureMethod | 예  | String  | 서명 방식, 현재 HmacSHA256 및 HmacSHA1을 지원합니다. 이 매개변수가 HmacSHA256으로 지정된 경우에만 HmacSHA256 알고리즘으로 서명을 검증할 수 있습니다. 다른 경우는 HmacSHA1로 서명을 확인합니다. 서명 계산 방법은 [서명 방법](https://cloud.tencent.com/document/api/377/4214) 페이지를 참조할 수 있습니다.  |


**사용 예제**

다음 예제는 Tencent Cloud 제품의 API 요청 링크에서 공통 요청 매개변수가 어떻게 표시되는지 보여줍니다. 예를 들어 광저우 지역의 Tencent Cloud CVM 인스턴스 목록을 조회하려는 경우 요청 링크는 다음과 같아야 합니다.
```
https://cvm.api.qcloud.com/v2/index.php?
Action=DescribeInstances
&SecretId=xxxxxxx
&Region=ap-guangzhou
&Timestamp=1465055529
&Nonce=59485
&Signature=mysignature
&SignatureMethod=HmacSHA256
&<API 요청 매개변수>
```
