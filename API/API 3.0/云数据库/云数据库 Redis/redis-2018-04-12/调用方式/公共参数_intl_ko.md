공통 매개변수는 사용자 식별과 API 인증에 사용되는 매개변수입니다. 필요하지 않은 경우, 각 API의 단독 문서에서 해당 매개변수에 대해 다시 설명하지 않지만, 요청 시마다 이러한 매개변수를 지참해야만 정상적으로 요청할 수 있습니다.

## 서명 방법 v3

TC3-HMAC-SHA256 서명 방법 사용 시, 공통 매개변수는 HTTP Header 요청 헤더에 통일적으로 배치되어야 합니다. 예:

| 매개변수 이름 | 유형 | 필수 항목 여부 | 설명 |
|--------|----|----|----|
| X-TC-Action | String | 예 | 작업의 API 이름입니다. 값은 API 문서에 입력 매개변수 공통 매개변수 Action의 설명을 참조하십시오. 예를 들어 CVM의 인스턴스 리스트 조회 API의 경우 값은 DescribeInstances입니다.|
| X-TC-Region | String | 예 | 지역 매개변수로 작업하려는 지역의 데이터 식별에 사용됩니다. API가 가능한 값은 API 문서 중 입력 매개변수 공통 매개변수의 Region 설명을 참조하십시오. 주의: 일부 API의 경우 해당 매개변수를 전달할 필요가 없으며(API 문서에 이 점에 대해 설명했습니다) 이때 이 매개변수를 전달하여도 적용하지 않습니다.|
| X-TC-Timestamp | Integer | 예 | 현재 UNIX 타임스탬프, API 요청이 시작된 시점을 기록할 수 있습니다. 예를 들어 1529223702입니다. 주의: 서버 시간과의 차이가 5분을 초과하면, 서명 만료 오류가 발생할 수 있습니다.|
| X-TC-Version | String | 예 | 작업의 API 버전입니다. 값은 API 문서 중 입력 매개변수 공통 매개변수의 Version 설명을 참조하십시오. 예, CVM의 버전: 2017-03-12.|
| Authorization |String | 예 | HTTP 표준 ID 인증 헤더 필드입니다. 예: <br/>TC3-HMAC-SHA256 Credential=AKIDEXAMPLE/Date/service/tc3_request, SignedHeaders=content-type;host, Signature=fe5f80f77d5fa3beca038a248ff027d0445342fe2855ddc963176630326f1024.<br/>여기에서 <br/>- TC3-HMAC-SHA256: 서명 방법. 현재 고정으로 해당 값 선택. <br/>- Credential: 서명 자격 증명. AKIDEXAMPLE은 SecretId입니다. Date는 UTC 기준 일자이며 값은 공통 매개변수 X-TC-Timestamp를 환산한 UTC 기준 일자와 일치해야 합니다. service는 제품명으로 반드시 호출한 제품 도메인 이름과 일치해야 합니다. 예를 들어 cvm입니다.<br/>- SignedHeaders: 서명 컴퓨팅에 포함된 헤더 정보, content-type 와 host는 필수 선택 헤더입니다.<br/>- Signature: 서명 요약입니다. |
| X-TC-Token | String | 아니요 | 임시 인증서에 사용한 Token이며, 임시 키와 결합하여 함께 사용해야 합니다. 임시 키 및 Token은 CAM에서 API를 호출하여 획득해야 합니다. 장기 키는 Token이 필요하지 않습니다.|

만약 사용자가 광저우 지역의 CVM 인스턴스 리스트를 조회하고자 한다면, 해당 요청 구조는 요청 URL, 요청 헤더, 요청 본문에 따라 다음과 같습니다.

HTTP GET 요청 구조 예시:

```
https://cvm.tencentcloudapi.com/?Limit=10&Offset=0

Authorization: TC3-HMAC-SHA256 Credential=AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE/2018-10-09/cvm/tc3_request, SignedHeaders=content-type;host, Signature=5da7a33f6993f0614b047e5df4582db9e9bf4672ba50567dba16c6ccf174c474
Content-Type: application/x-www-form-urlencoded
Host: cvm.tencentcloudapi.com
X-TC-Action: DescribeInstances
X-TC-Version: 2017-03-12
X-TC-Timestamp: 1539084154
X-TC-Region: ap-guangzhou
```

HTTP POST(application/json) 요청 구조 예시:

```
https://cvm.tencentcloudapi.com/

Authorization: TC3-HMAC-SHA256 Credential=AKIDEXAMPLE/2018-05-30/cvm/tc3_request, SignedHeaders=content-type;host, Signature=582c400e06b5924a6f2b5d7d672d79c15b13162d9279b0855cfba6789a8edb4c
Content-Type: application/json
Host: cvm.tencentcloudapi.com
X-TC-Action: DescribeInstances
X-TC-Version: 2017-03-12
X-TC-Timestamp: 1527672334
X-TC-Region: ap-guangzhou

{"Offset":0,"Limit":10}
```

HTTP POST(multipart/form-data) 요청 구조 예시(특정 API만 지원):

```
https://cvm.tencentcloudapi.com/

Authorization: TC3-HMAC-SHA256 Credential=AKIDEXAMPLE/2018-05-30/cvm/tc3_request, SignedHeaders=content-type;host, Signature=582c400e06b5924a6f2b5d7d672d79c15b13162d9279b0855cfba6789a8edb4c
Content-Type: multipart/form-data; boundary=58731222010402
Host: cvm.tencentcloudapi.com
X-TC-Action: DescribeInstances
X-TC-Version: 2017-03-12
X-TC-Timestamp: 1527672334
X-TC-Region: ap-guangzhou

--58731222010402
Content-Disposition: form-data; name="Offset"

0
--58731222010402
Content-Disposition: form-data; name="Limit"

10
--58731222010402--
```

## 서명 방법 v1

HmacSHA1 및 HmacSHA256 서명 방법 사용 시, 공통 매개변수는 통일적으로 요청 문자열 중에 다음과 같이 배치되어야 합니다.

| 매개변수 이름 | 유형 | 필수 항목 여부 | 설명 |
|:---------|:---------|:-----|:---- |
| Action | String | 예 | 작업의 API 이름입니다. 값은 API 문서에 입력 매개변수 공통 매개변수 Action의 설명을 참조하십시오. 예를 들어 CVM의 인스턴스 리스트 조회 API의 경우 값은 DescribeInstances입니다.|
| Region| String | 예 | 지역 매개변수로 작업하려는 지역의 데이터 식별에 사용됩니다. API가 가능한 값은 API 문서 중 입력 매개변수 공통 매개변수의 Region 설명을 참조하십시오. 주의: 일부 API의 경우 해당 매개변수를 전달할 필요가 없으며(API 문서에 이 점에 대해 설명했습니다) 이때 이 매개변수를 전달하여도 적용하지 않습니다.|
| Timestamp | Integer | 예 | 현재 UNIX 타임스탬프, API 요청이 시작된 시점을 기록할 수 있습니다. 예를 들어 1529223702입니다. 현재 시간과의 차이가 너무 크면, 서명 만료 오류가 발생할 수 있습니다.|
| Nonce | Integer | 예 | 랜덤 양의 정수, 재전송 공격을 막기 위해 타임스탬프와 결합합니다.|
| SecretId | String | 예 | <a href="https://console.cloud.tencent.com/capi">클라우드 API 키</a>에서 신청된 신분을 식별하는 SecretId입니다. 하나의 SecretId는 하나의 SecretKey에 해당하며 SecretKey는 요청 서명을 생성하는 데 사용됩니다.|
| Signature | String | 예 | 요청 서명, 요청의 유효성을 검증하는 데 사용되며, 사용자가 실제 입력 매개변수에 따라 컴퓨팅해야 합니다. 구체적인 컴퓨팅 방법은 API 인증 문서를 참조하십시오.|
| Version | String | 예 | 작업의 API 버전입니다. 값은 API 문서 중 입력 매개변수 공통 매개변수의 Version 설명을 참조하십시오. 예, CVM의 버전: 2017-03-12.|
| SignatureMethod | String | 아니요 | 서명 방식, 현재 HmacSHA256 및 HmacSHA1을 지원합니다. 이 매개변수가 HmacSHA256으로 지정된 경우에만 HmacSHA256 알고리즘으로 서명을 검증할 수 있습니다. 다른 경우는 HmacSHA1로 서명을 검증합니다.|
| Token | String | 아니요 | 임시 인증서에 사용한 Token이며, 임시 키와 결합하여 함께 사용해야 합니다. 임시 키 및 Token은 반드시 CAM에서 API룰 호출하여 획득해야 합니다. 장기 키는 Token이 필요하지 않습니다.|


만약 사용자가 광저우 지역의 CVM 인스턴스 리스트를 조회하고자 할 경우, 해당 요청 구조는 요청 URL, 요청 헤더, 요청 본문에 따라 다음과 같습니다.

HTTP GET 요청 구조 예시:
```
https://cvm.tencentcloudapi.com/?Action=DescribeInstances&Version=2017-03-12&SignatureMethod=HmacSHA256&Timestamp=1527672334&Signature=37ac2f4fde00b0ac9bd9eadeb459b1bbee224158d66e7ae5fcadb70b2d181d02&Region=ap-guangzhou&Nonce=23823223&SecretId=AKIDEXAMPLE

Host: cvm.tencentcloudapi.com
Content-Type: application/x-www-form-urlencoded
```

HTTP POST 요청 구조 예시:

```
https://cvm.tencentcloudapi.com/

Host: cvm.tencentcloudapi.com
Content-Type: application/x-www-form-urlencoded

Action=DescribeInstances&Version=2017-03-12&SignatureMethod=HmacSHA256&Timestamp=1527672334&Signature=37ac2f4fde00b0ac9bd9eadeb459b1bbee224158d66e7ae5fcadb70b2d181d02&Region=ap-guangzhou&Nonce=23823223&SecretId=AKIDEXAMPLE
```


## 지역 리스트

본 제품의 모든 API Region 필드에 대한 선택 가능 값은 다음 표에 나와 있습니다. API가 해당 표에 나와 있는 모든 지역을 지원하지 않을 경우, API 문서에서 별도로 설명합니다.


| 지역 | 값 |
|------|------|
|아시아･태평양 지역(방콕)|ap-bangkok|
|화북 지역(베이징)|ap-beijing|
|서남 지역(청두)|ap-chengdu|
|서남 지역(충칭)|ap-chongqing|
|화남 지역(광저우)|ap-guangzhou|
|동남아 지역(중국 홍콩)|ap-hongkong|
|아시아 태평양 지역(뭄바이)|ap-mumbai|
|아시아･태평양 지역(서울)|ap-seoul|
|화동 지역(상하이)|ap-shanghai|
|화동 지역(상하이 금융)|ap-shanghai-fsi|
|화남 지역(선전 금융)|ap-shenzhen-fsi|
|동남아 지역(싱가포르)|ap-singapore|
|아시아 태평양 지역(도쿄)|ap-tokyo|
|유럽 지역(프랑크푸르트)|eu-frankfurt|
|유럽 지역(모스크바)|eu-moscow|
|미국 동부(버지니아)|na-ashburn|
|미국 서부(실리콘 밸리)|na-siliconvalley|
|북미 지역(토론토)|na-toronto|
