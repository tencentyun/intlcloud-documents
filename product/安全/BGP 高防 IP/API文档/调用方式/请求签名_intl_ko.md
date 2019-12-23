

Tencent Cloud API는 모든 접근 요청에 대해 ID 인증을 진행합니다. 즉, 모든 요청은 공용 요청 매개변수에 서명 정보(Signature)를 포함하여 사용자 ID를 인증하여야 합니다. 서명 정보는 사용자가 보유한 보안 인증서로 생성되며, 보안 인증서는 SecretId와 SecretKey를 포함합니다. 사용자에게 보안 인증서가 없을 경우, Tencent Cloud 홈페이지에서 신청해야 합니다. 그렇지 않으면 클라우드 API를 호출할 수 없습니다.

## 보안 인증서 신청
처음 Tencent Cloud API를 사용하기 전, 사용자는 [Tencent Cloud 콘솔] > [[API 키 관리](https://console.cloud.tencent.com/cam/capi) ]에서 보안 인증서를 신청해야 합니다. 보안 인증서는 SecretId와 SecretKey를 포함합니다.

- **SecretId:** API 호출자 ID를 식별하는 데 사용합니다.
- **SecretKey:** 서명 문자열 암호화와 서버에서 서명 문자열 인증에 사용됩니다.

>API 키는 Tencent Cloud API 요청을 생성하는 중요한 자격 증명입니다. Tencent Cloud API를 사용하면 모든 Tencent Cloud 리소스를 조작할 수 있습니다. 자산과 서비스 보안을 보장하기 위해 키를 잘 보관하고 주기적으로 키를 교체하십시오. 키를 교체하는 경우, 이전 키를 즉시 삭제하십시오.


#### 보안 인증서 신청 절차

1. [Tencent Cloud 콘솔](https://console.cloud.tencent.com/)에 로그인합니다.
2. [클라우드 제품]을 클릭하고 [관리 도구]의 [클라우드 API 키]에서 클라우드 API 키 관리 페이지에 진입합니다.
![](//mc.qcloudimg.com/static/img/a771465c47830d54730f8f431d586991/image.png)
3. [ API 키 관리](https://console.cloud.tencent.com/capi) 페이지에서 [키 생성]을 클릭하면 SecretId/SecretKey 한 쌍을 생성할 수 있습니다.

>
> - 개발사 계정은 최대 SecretId / SecretKey 두 쌍을 보유할 수 있습니다.
> - 개발사에 의해 추가된 서브 사용자 QQ 계정은 다른 개발사 콘솔에서도 별도의 보안 인증서를 신청할 수 있습니다.
> - 서브 사용자의 보안 자격 증명로 현재 일부 클라우드 API만 호출할 수 있습니다.

##  서명열 생성
보안 자격 증명 SecretId와 SecretKey가 있으면 서명열을 생성할 수 있습니다. 서명열 생성 상세 과정은 다음과 같습니다.

![](//mc.qcloudimg.com/static/img/3a3a616ba175bb95be68123d86715e77/image.png)

사용자의 SecretId와 SecretKey는 각각 다음과 같습니다.
SecretId： AKIDz8krbsJ5yKBZQpn74WFkmLPx3gnPhESA
SecretKey： Gu5t9xGARNpq86cd98joQYCN3Cozk1qA

>이것은 단지 예시일 뿐, 사용자는 자신의 실제 SecretId와 SecretKey, 요청 매개변수에 따라 후속 작업을 수행하십시오.

Tencent Cloud CVM을 예로 들면, 사용자가 Tencent Cloud CVM의 [인스턴스 리스트 조회](https://cloud.tencent.com/document/api/213/15728) (DescribeInstances) API를 호출하였을 때, 요청 매개변수는 다음과 같습니다.

| 매개변수 이름 | 설명 | 매개변수 값 | 
|---------|---------|---------|
| Action | 방법명 | DescribeInstances | 
| SecretId | 키 ID  | AKIDz8krbsJ5yKBZQpn74WFkmLPx3gnPhESA | 
| Timestamp | 현재 타임스탬프 | 1465185768 | 
| Nonce | 랜덤 정수 | 11886 | 
| Region | 인스턴스 소재 지역 | ap-guangzhou | 
| SignatureMethod | 서명 방식 | HmacSHA256 | 
| InstanceIds.0 | 조회 대기 인스턴스 ID | ins-09dx96dg | 

### 1. 매개변수 정렬
우선 모든 요청 매개별수를 매개변수 이름 사전 순서대로 오름차순으로 정렬합니다(사전 순서 오름차순 정렬이란 직관적으로 사전에 정렬된 단어 순서와 동일한 정렬을 가리키며, 알파벳표 또는 숫자표의 오름차순에 따르는 것을 가리킵니다. 우선 첫 번째 알파벳에 따라 정렬한 뒤, 똑같은 경우에 두 번째 알파벳에 따르는 식으로 정렬해 갑니다). PHP의 ksort 함수와 같이 프로그래밍 언어의 관련 정렬 함수를 이용하여 이 기능을 실현할 수도 있습니다. 상기 예시 매개변수 정렬 결과는 다음과 같습니다.

```shell
{
    "Action" : "DescribeInstances",
    "InstanceIds.0" : "ins-09dx96dg",
    "Nonce" : 11886,
    "Region" : "ap-guangzhou",
    "SecretId" : "AKIDz8krbsJ5yKBZQpn74WFkmLPx3gnPhESA",
    "SignatureMethod" : "HmacSHA256",
    "Timestamp" : 1465185768
}
```
기타 프로그래밍 언어를 사용하여 위의 예시 중 매개변수를 정렬할 수 있으며 얻게 되는 결과가 같으면 됩니다.

### 2. 요청 문자열 합치기
요청 문자열 생성 절차입니다.
이전 단계에서 정렬한 요청 매개변수를 `"매개변수 이름"="매개변수 값"`의 형식으로 포맷합니다. Action 매개변수의 경우 매개변수 이름은 `"Action"` 매개변수 값은 `"DescribeInstances"`이기 때문에 포맷 이후 `Action=DescribeInstances`가 됩니다.

>
- '매개변수 값'은 본래값이며 URL 코딩 이후 값이 아닙니다.
- 입력한 매개변수의 Key에 밑줄이 포함되어 있으면 `.`으로 전환해야 합니다. 단, Value의 밑줄은 전환할 필요가 없습니다. 예를 들면, `Placement_Zone=CN_GUANGZHOU`의 경우 `Placement.Zone=CN_GUANGZHOU`。로 전환해야 합니다.

포맷된 각 매개변수를 `"&"`로 연결하여, 최종 생성된 요청 문자열은 다음과 같습니다(문장 중 줄 바꿈을 무시해도 됨).

```shell
Action=DescribeInstances
&InstanceIds.0=ins-09dx96dg
&Nonce=11886
&Region=ap-guangzhou
&SecretId=AKIDz8krbsJ5yKBZQpn74WFkmLPx3gnPhESA
&SignatureMethod=HmacSHA256
&Timestamp=1465185768
```

### 3. 서명 원문 문자열 합치기
서명 원문 문자열 생성 절차입니다.
서명 원문 문자열 합치기 규칙은 다음과 같습니다.
> **요청 방법 + 요청 CVM +요청 경로 + ? + 요청 문자열**

매개변수 구성 설명:
* **요청 방법:** POST와 GET 방식을 지원하며, 여기서는 GET 요청을 사용합니다. 모두 대문자로 작성해야 합니다.
* **요청 CVM:** 즉 CVM 도메인 이름으로 요청 도메인 이름은 API 소속 제품 또는 소속 제품의 모듈로 결정합니다. 제품별 또는 제품의 모듈별 요청 도메인 이름이 달라집니다. 예를 들어 Tencent Cloud CVM의 인스턴스 리스트 조회(DescribeInstances)의 요청 도메인 이름은 `cvm.api.qcloud.com`입니다. 구체적인 제품 요청 도메인 이름은 API별 설명을 참조하십시오.
* **요청 경로:** 해당 API에 다응하는 Tencent Cloud 제품의 요청 경로입니다. 일반적으로 하나의 제품이 하나의 고정 경로와 대응합니다. 예를 들어 Tencent Cloud CVM 요청 경로는 `/v2/index.php`로 고정됩니다.
* **요청 문자열:** 이전 단계에서 생성한 요청 문자열입니다.


그렇기 때문에 위에서 예로 제시한 서명 원문 문자열 합치기 결과는(본문 중 줄 바꿈을 무시) 다음과 같습니다.
```shell
GETcvm.api.qcloud.com/v2/index.php?Action=DescribeInstances
&InstanceIds.0=ins-09dx96dg
&Nonce=11886
&Region=ap-guangzhou
&SecretId=AKIDz8krbsJ5yKBZQpn74WFkmLPx3gnPhESA
&SignatureMethod=HmacSHA256
&Timestamp=1465185768
```

### 4. 서명열 생성
서명열 생성 절차입니다.
>서명 계산 방법은 HmacSHA256과 HmacSHA1 두 가지이며 여기서는 지정한 서명 알고리즘(즉 SignatureMethod 매개변수)에 따라 서명열을 생성합니다. SignatureMethod를 HmacSHA256으로 지정할 경우, HmacSHA256을 사용하여 서명을 계산해야 합니다. 기타 상황은 HmacSHA1 계산 서명을 사용하십시오.

우선 서명 알고리즘(HmacSHA256 또는 HmacSHA1)을 사용하여 이전 단계에서 획득한 **서명 원문 문자열**에 서명한 뒤, 생성한 서명열은 Base64를 사용하여 인코딩을 수행하면 최종 서명열을 획득할 수 있습니다.

구체적인 코드는 다음과 같으며, PHP 언어를 예로 들자면, 이 예에서 사용한 서명 알고리즘이 **HmacSHA256**이기 때문에 서명열 생성 코드는 다음과 같습니다(다른 프로그래밍 언어를 사용할 경우, 위 예시 중 원문 문자열을 사용하여 서명 인증을 수행할 수 있으며, 획득한 서명열이 예시의 문자열과 일치하면 됩니다).

```php
$secretKey = 'Gu5t9xGARNpq86cd98joQYCN3Cozk1qA';
$srcStr = 'GETcvm.api.qcloud.com/v2/index.php?Action=DescribeInstances&InstanceIds.0=ins-09dx96dg&Nonce=11886&Region=ap-guangzhou&SecretId=AKIDz8krbsJ5yKBZQpn74WFkmLPx3gnPhESA&SignatureMethod=HmacSHA256&Timestamp=1465185768';
$signStr = base64_encode(hash_hmac('sha256', $srcStr, $secretKey, true));
echo $signStr;
```

최종 획득한 서명열은 다음과 같습니다.

```
0EEm/HtGRr/VJXTAD9tYMth1Bzm3lLHz5RCDv1GdM8s=
```

마찬가지로 서명 알고리즘을 **HmacSHA1**로 지정하면 생성한 서명열 코드는 다음과 같습니다.
```php
$secretKey = 'Gu5t9xGARNpq86cd98joQYCN3Cozk1qA';
$srcStr = 'GETcvm.api.qcloud.com/v2/index.php?Action=DescribeInstances&InstanceIds.0=ins-09dx96dg&Nonce=11886&Region=ap-guangzhou&SecretId=AKIDz8krbsJ5yKBZQpn74WFkmLPx3gnPhESA&SignatureMethod=HmacSHA1&Timestamp=1465185768';
$signStr = base64_encode(hash_hmac('sha1', $srcStr, $secretKey, true));
echo $signStr;
```

최종 획득한 서명열은 다음과 같습니다.
```
nPVnY6njQmwQ8ciqbPl5Qe+Oru4=
```


##  서명열 인코딩
생성한 서명열은 요청 매개변수로 직접 사용할 수 없으며 URL 인코딩을 해야 합니다.
예를 들어 이전 단계에서 생성한 서명열이 `0EEm/HtGRr/VJXTAD9tYMth1Bzm3lLHz5RCDv1GdM8s=`이면 인코딩 후는 `0EEm%2FHtGRr%2FVJXTAD9tYMth1Bzm3lLHz5RCDv1GdM8s%3D`가 됩니다. 그렇기 때문에 최종 획득한 서명열 요청 매개변수(Signature)는 `0EEm%2FHtGRr%2FVJXTAD9tYMth1Bzm3lLHz5RCDv1GdM8s%3D`이며, 최종 요청 URL 생성에 사용됩니다.

>사용자의 요청 방법이 GET이면, 모든 요청 매개변수의 매개변수 값을 URL 인코딩해야 합니다. 그 외에 일부 언어 라이브러리는 URL을 자동으로 인코딩하기 때문에 중복 인코딩으로 인해 서명 검사가 실패하게 됩니다.

## 인증 실패
인증을 통과하지 못하면, 아래 표와 같은 오류가 나타날 수 있습니다.

| 오류 코드 | 오류 유형 | 오류 설명|
|---------|---------|---------|
| 4100 | ID 인증 실패 | ID 인증 실패. 요청 매개변수의 Signature는 상기 절차에 따라 정확히 계산되는지 확인하십시오. 특별히 주의할 점은 Signature는 URL 코딩된 이후 요청해야 합니다.|
| 4101 | API에 접근 권한 없음 | 해당 서브 사용자가 이 API를 호출할 권한을 부여받지 않았습니다. 개발사에게 연락하여 권한을 부여하도록 요청하십시오. 세부 정보는 [권한 부여 전략](https://intl.cloud.tencent.com/document/product/598/10601)을 참조하십시오.|
| 4102 | 본 API에서 조작된 리소스에 접근 권한 없음 | 요청한 리소스 매개변수 중, 개발사에 의해 접근 권한을 부여받지 않은 리소스가 존재합니다. message 필드에서 접근 권한이 없는 리소스 ID를 확인하십시오.</br>개발사에게 연락하십시오. 세부 정보는 [권한 부여 전략](https://intl.cloud.tencent.com/document/product/598/10601)을 참조하십시오.|
| 4103 | 비 개발사 SecretId는 본 API를 호출할 수 없음 | 서브 사용자의 SecretId는 이 API 호출을 지원하지 않으므로 개발사만 호출할 권한이 있습니다.|
| 4104 | SecretId가 존재하지 않음 | 서명에 사용한 SecretId가 존재하지 않거나 키 상태 오류일 수 있으니 API 키가 올바르고 활성화되었는지 확인하십시오.|
| 4110 | 인증 실패 | 권한 검사 실패. 해당 리소스에 접근할 권한이 있는 확인하십시오.|
| 4500 | 재전송 공격 오류 | Nonce 매개변수는 2회 요청에서 중복될 수 없으며, Timestamp와 Tencent 서버 시간 차이는 2시간을 초과할 수 없습니다.|

