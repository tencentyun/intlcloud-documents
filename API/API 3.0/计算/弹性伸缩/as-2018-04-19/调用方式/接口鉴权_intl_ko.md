Tencent Cloud API 는 각 액세스 요청에 대해서 ID 검증을 합니다. 즉, 각 요청은 모두 공통 요청 매개변수 중 서명 정보(Signature)를 포함해 요청자 ID를 검증해야 합니다.
서명 정보는 보안 자격 증명의 의해 생성되고 보안 자격 증명은 SecretId와 SecretKey를 포함합니다. 사용자가 보안 자격 증명이 없으면 [클라우드 API 키 페이지](https://console.cloud.tencent.com/capi)로 가서 신청하고 그렇지 않으면 클라우드 API를 호출할 수 없습니다.

## 1. 보안 자격 증명 신청
처음 클라우드 API를 사용하기 전에 [클라우드 API 키 페이지](https://console.cloud.tencent.com/capi)에서 보안 자격 증명을 신청하십시오.
보안 자격 증명은 SecretID와 SecretKey를 포함합니다.
* SecretID    API 호출자 ID를 식별하는 데 사용됩니다.
* SecretKey는 서명 문자열 암호화와 서버에서 서명 문자열 검증에 사용됩니다.
* <font color='red'>사용자는 보안 자격 증명을 잘 보관해 유출되지 않도록 해야 합니다.</font>

보안 자격 증명 신청 절차는 다음과 같습니다.

1. [Tencent Cloud 콘솔](https://console.cloud.tencent.com/)에 로그인합니다.
1. [클라우드 API 키](https://console.cloud.tencent.com/capi)의 콘솔 페이지로 이동합니다.
1. [클라우드 API 키](https://console.cloud.tencent.com/capi) 페이지로 가서 [생성]을 클릭하면 SecretId/SecretKey 한 쌍을 생성할 수 있습니다.

주의: 개발자 계정은 최대 SecretId/SecretKey 두 쌍을 보유할 수 있습니다.

## 2. 서명 문자열 생성

보안 자격 증명 SecretId와 SecretKey가 있으면 서명 문자열을 생성할 수 있습니다. 서명 문자열 생성의 상세 과정은 다음과 같습니다.

사용자의 SecretId와 SecretKey는 각각 다음과 같습니다.

* SecretId: AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE
* SecretKey: Gu5t9xGARNpq86cd98joQYCN3EXAMPLE

**주의: 이것은 단지 예시일 뿐, 사용자가 실제 신청한 SecretId와 SecretKey 에 따라 후속 작업을 수행하십시오!**

CVM 인스턴스 리스트 보기(DescribeInstances) 요청을 예로 들자면 사용자가 해당 API를 호출할 경우 가능한 요청 매개변수는 다음과 같습니다.

| 매개변수 이름 | 한국어 | 매개변수 값 |
|---------|---------|---------|
| Action | 방법명 | DescribeInstances |
| SecretId | 키 ID | AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE |
| Timestamp | 현재 타임스탬프 | 1465185768 |
| Nonce | 랜덤 양의 정수 | 11886 |
| Region | 인스턴스 소재 지역 | ap-guangzhou |
| InstanceIds.0 | 조회 대기 인스턴스 ID | ins-09dx96dg |
| Offset | 오프셋 | 0 |
| Limit | 최대 허용 출력 | 20 |
| Version | API 버전 번호 | 2017-03-12 |


### 2.1. 매개변수 정렬

먼저 모든 요청 매개변수에 대해서 매개변수 이름 사전 순서(ASCII 코드)대로 오름차순으로 정렬합니다. 주의: 1)매개변수 이름에 따라 정렬하고 매개변수 값은 대응하는 값을 유지하기만 하면 되고 크기 비교하지 않습니다. 2)ASCII 코드에 따라 크기 비교합니다. 예를 들어 InstanceIds.2는 InstanceIds.12 뒤에 정렬해야 합니다. 알파벳 순이나 숫자에 따르는 것이 아닙니다. 사용자는 프로그래밍 언어 중 관련 정렬 함수로 해당 기능을 구현할 수 있습니다. 예를 들어 PHP의 Ksort 함수입니다. 위의 예시 매개변수 정렬 결과는 다음과 같습니다.

```
{
    'Action' : 'DescribeInstances',
    'InstanceIds.0' : 'ins-09dx96dg',
    'Limit' : 20,
    'Nonce' : 11886,
    'Offset' : 0,
    'Region' : 'ap-guangzhou',
    'SecretId' : 'AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE',
    'Timestamp' : 1465185768,
    'Version': '2017-03-12',
}
```
다른 프로그래밍 언어를 통해 개발하는 경우 위 예시의 매개변수를 정렬할 수 있고 얻은 결과는 일치합면 됩니다.

### 2.2. 요청 문자열 합치기

요청 문자열 생성 절차입니다.
위의 정렬된 요청 매개변수를 "매개변수 이름" = "매개변수 값"의 형식으로 포맷합니다. 예를 들어 Action 매개변수는 해당 매개변수 이름이 "Action"이고 매개변수 값은 "DescribeInstances"입니다. 따라서 포맷한 후 Action=DescribeInstances가 됩니다.
**주의: "매개변수 값"은 원시값이고 URL 인코딩된 값이 아닙니다.**

포맷된 각 매개변수를 "&"로 연결하여 최종 생성된 요청 문자열은 다음과 같습니다.

```
Action=DescribeInstances&InstanceIds.0=ins-09dx96dg&Limit=20&Nonce=11886&Offset=0&Region=ap-guangzhou&SecretId=AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE&Timestamp=1465185768&Version=2017-03-12
```

### 2.3. 서명 원문 문자열 합치기
서명 원문 문자열 생성 절차입니다.
서명 원문 문자열은 다음 매개변수로 구성됩니다.

1. 요청 방식: POST와 GET 방식을 지원합니다. 여기서는 GET 요청을 사용합니다. 요청 방법은 모두 대문자로 작성해야 합니다.
2. 요청 서버: 인스턴스 리스트 보기(DescribeInstances)의 요청 도메인 이름은 cvm.tencentcloudapi.com입니다. 실제 요청 도메인 이름은 API 속한 모듈에 따라 달라집니다. 각 API 설명을 참조하십시오.
3. 요청 경로: 현재 버전의 Cloud API의 요청 경로는 / 입니다.
4. 요청 문자열: 이전 단계에서 생성한 요청 문자열입니다.

서명 원문 문자열 합치기 규칙은 다음과 같습니다. 요청 방식 + 요청 CVM +요청 경로 + ? + 요청 문자열

예시의 합치기 결과는 다음과 같습니다.

```
GETcvm.tencentcloudapi.com/?Action=DescribeInstances&InstanceIds.0=ins-09dx96dg&Limit=20&Nonce=11886&Offset=0&Region=ap-guangzhou&SecretId=AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE&Timestamp=1465185768&Version=2017-03-12
```

### 2.4. 서명 문자열 생성
서명 문자열 생성 절차입니다.
우선 HMAC-SHA1 알고리즘을 사용하여 이전 단계에서 획득한 **서명 원문 문자열**에 서명한 뒤, 생성한 서명열은 Base64로 인코딩을 수행하면 최종 서명 문자열을 획득할 수 있습니다.

구체적인 코드는 다음과 같습니다. PHP 언어를 예로 합니다.

```
$secretKey = 'Gu5t9xGARNpq86cd98joQYCN3EXAMPLE';
$srcStr = 'GETcvm.tencentcloudapi.com/?Action=DescribeInstances&InstanceIds.0=ins-09dx96dg&Limit=20&Nonce=11886&Offset=0&Region=ap-guangzhou&SecretId=AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE&Timestamp=1465185768&Version=2017-03-12';
$signStr = base64_encode(hash_hmac('sha1', $srcStr, $secretKey, true));
echo $signStr;
```

최종 획득한 서명 문자열은 다음과 같습니다.

```
EliP9YW3pW28FpsEdkXt/+WcGeI=
```

다른 프로그래밍 언어를 통해 개발하는 경우 위와 같이 서명 인증을 진행할 수 있고 얻은 서명 문자열는 예와 일치하면 됩니다.

## 3. 서명 문자열 인코딩

생성한 서명열은 요청 매개변수로 직접 사용할 수 없으며 URL 인코딩을 해야 합니다.

예를 들어 이전 단계에서 생성한 서명 문자열이 EliP9YW3pW28FpsEdkXt/+WcGeI=이면 최종적으로 얻은 서명 문자열 요청 매개변수(Signature)는 EliP9YW3pW28FpsEdkXt%2f%2bWcGeI%3d이고 최종 요청 URL 생성에 사용합니다.

**주의: 사용자의 요청 방식이 GET이거나 요청 방식이 POST이고 동시에 Content-Type이 application/x-www-form-urlencoded이면 요청 전송 시 모든 요청 매개변수의 값은 모두 URL 인코딩을 해야 합니다. 매개변수 키와 "= "부호는 인코딩할 필요가 없습니다. 비 ASCII 문자는 URL 인코딩 이전에 먼저 UTF-8로 인코딩해야 합니다.**

**주의: 일부 프로그래밍 언어의 Http 라이브러리는 자동으로 모든 매개변수에 대해서 urlencode를 진행합니다. 해당 경우에서 서명 문자열에 대해서 URL 인코딩을 할 필요가 없고 그렇지 않으면 두 번 URL 인코딩으로 인해 서명이 실패할 수 있습니다.**

**주의: 기타 매개변수 값도 인코딩을 해야 하며 [RFC 3986](http://tools.ietf.org/html/rfc3986)으로 인코딩합니다. %XY를 사용하여 한자와 같은 특수 문자에 대해서 백분율 인코딩을 수행하며 이 중 "X"와 "Y"는 16진 문자(0-9와 대문자 알파벳 A-F)여야 하고 소문자를 사용하면 오류가 발생합니다.**

## 4. 서명 실패
실제 상황에 따라 다음의 서명 실패 오류 코드가 반환될 수 있습니다. 실제 상황에 따라 해결하십시오.

| 오류 코드 | 오류 설명 |
|----------|---------|
| AuthFailure.SignatureExpire | 서명 만료됨 |
| AuthFailure.SecretIdNotFound | 키가 존재하지 않음 |
| AuthFailure.SignatureFailure | 서명 오류 |
| AuthFailure.TokenFailure | token 오류 |
| AuthFailure.InvalidSecretId | 잘못된 키(클라우드 API 키 유형이 아님) |

## 5. 서명 예제

실제로 API 3.0을 호출할 경우 Tencent Cloud SDK 3.0 사용을 권장하며 SDK는 서명 과정을 캡슐화하여 개발 시 제품에 제공되는 구체적인 API에 유의하면 됩니다. 상세한 정보는 [SDK 센터](https://cloud.tencent.com/document/sdk)를 참조하십시오. 현재 지원되는 프로그래밍 언어는 다음과 같습니다.

* [Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [JavaScript](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [.NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

서명 과정을 더 명확하게 설명하기 위해서 실제 프로그래밍 언어를 예로 상기 서명 과정을 구현합니다. 요청한 도메인 이름, 호출한 API와 매개변수 값은 모두 상기 서명 과정을 기준으로 하고 코드는 서명 과정 해석만을 위한 것으로 일반적으로 사용하면 안되며 실제 개발은 가능한 한 SDK를 사용하십시오.

가능한 최종 출력 URL: `https://cvm.tencentcloudapi.com/?Action=DescribeInstances&InstanceIds.0=ins-09dx96dg&Limit=20&Nonce=11886&Offset=0&Region=ap-guangzhou&SecretId=AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE&Signature=EliP9YW3pW28FpsEdkXt%2F%2BWcGeI%3D&Timestamp=1465185768&Version=2017-03-12`.

주의: 예시의 키는 가상이고 타임스탬프 역시 시스템 현재 시간이 아니기 때문에 URL은 브라우저에서 열거나 CURL 등 명령으로 호출 시 서명이 만료되었다는 인증 오류를 반환합니다. 정상적으로 반환된 URL을 얻기 위해서 예시의 SecretId 와 SecretKey를 진정한 키로 수정해야 하고 시스템 현재 타임스탬프를 Timestamp로 사용해야 합니다.

주의: 다음의 예시에서 서로 다른 프로그래밍 언어는 심지어 동일한 언어로 실행할 때마다 얻는 URL이 다를 수 있고 매개변수 순서가 다른 것으로 나타납니다. 단, 이는 정확성에 영향을 주지 않습니다. 모든 매개변수가 있고 서명 컴퓨팅이 정확하면 됩니다. 

주의: 다음의 코드는 API 3.0에만 적용하고 기타의 서명 프로세스에 직접 사용할 수 없습니다. 이전 버전의 API여도 세부적인 차이가 존재하기 때문에 서명 컴퓨팅 오류를 초래할 수 있으니 대응하는 실제 문서를 기준으로 해야 합니다.

### Java

```java
import java.io.UnsupportedEncodingException;
import java.net.URLEncoder;
import java.util.Random;
import java.util.TreeMap;
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
import javax.xml.bind.DatatypeConverter;

public class TencentCloudAPIDemo {
    private final static String CHARSET = "UTF-8";

    public static String sign(String s, String key, String method) throws Exception {
        Mac mac = Mac.getInstance(method);
        SecretKeySpec secretKeySpec = new SecretKeySpec(key.getBytes(CHARSET), mac.getAlgorithm());
        mac.init(secretKeySpec);
        byte[] hash = mac.doFinal(s.getBytes(CHARSET));
        return DatatypeConverter.printBase64Binary(hash);
    }

    public static String getStringToSign(TreeMap<String, Object> params) {
        StringBuilder s2s = new StringBuilder("GETcvm.tencentcloudapi.com/?");
        // 서명 시 매개변수에 대해서 사전 정렬을 요구합니다 순서를 보장하기 위해 TreeMap을 사용합니다.
        for (String k : params.keySet()) {
            s2s.append(k).append("=").append(params.get(k).toString()).append("&");
        }
        return s2s.toString().substring(0, s2s.length() - 1);
    }

    public static String getUrl(TreeMap<String, Object> params) throws UnsupportedEncodingException {
        StringBuilder url = new StringBuilder("https://cvm.tencentcloudapi.com/?");
        // 실제 요청한 URL에서 매개변수 순서에 대한 요구가 없습니다.
        for (String k : params.keySet()) {
            // 요청 문자열에 대해 urlencode를 해야 합니다. key는 모두 영어 알파벳이기 때문에 해당 value에 대해서만 urlencode을 실행하면 됩니다.
            url.append(k).append("=").append(URLEncoder.encode(params.get(k).toString(), CHARSET)).append("&");
        }
        return url.toString().substring(0, url.length() - 1);
    }

    public static void main(String[] args) throws Exception {
        TreeMap<String, Object> params = new TreeMap<String, Object>(); // TreeMap은 자동 정렬할 수 있습니다.
        // 실제 호출 시 난수를 사용해야 합니다. 예를 들어 params.put("Nonce", new Random().nextInt(java.lang.Integer.MAX_VALUE))입니다.
        params.put("Nonce", 11886); // 공통 매개변수
        // 실제 호출 시 시스템 현재 시간을 사용해야 합니다. 예를 들어 params.put("Timestamp", System.currentTimeMillis() / 1000)입니다.
        params.put("Timestamp", 1465185768); // 공통 매개변수
        params.put("SecretId", "AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE"); // 공통 매개변수
        params.put("Action", "DescribeInstances"); // 공통 매개변수
        params.put("Version", "2017-03-12"); // 공통 매개변수
        params.put("Region", "ap-guangzhou"); // 공통 매개변수
        params.put("Limit", 20); // 비즈니스 매개변수
        params.put("Offset", 0); // 비즈니스 매개변수
        params.put("InstanceIds.0", "ins-09dx96dg"); // 비즈니스 매개변수
        params.put("Signature", sign(getStringToSign(params), "Gu5t9xGARNpq86cd98joQYCN3EXAMPLE", "HmacSHA1")); // 공통 매개변수
        System.out.println(getUrl(params));
    }
}
```

### Python

주의: Python 2 환경에서 시행하면 먼저 requests 의존 패키지 `pip install requests`를 설치해야 합니다.

```python
# -*- coding: utf8 -*-
import base64
import hashlib
import hmac
import time

import requests

secret_id = "AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE"
secret_key = "Gu5t9xGARNpq86cd98joQYCN3EXAMPLE"

def get_string_to_sign(method, endpoint, params):
    s = method + endpoint + "/?"
    query_str = "&".join("%s=%s" % (k, params[k]) for k in sorted(params))
    return s + query_str

def sign_str(key, s, method):
    hmac_str = hmac.new(key.encode("utf8"), s.encode("utf8"), method).digest()
    return base64.b64encode(hmac_str)

if __name__ == '__main__':
    endpoint = "cvm.tencentcloudapi.com"
    data = {
        'Action' : 'DescribeInstances',
        'InstanceIds.0' : 'ins-09dx96dg',
        'Limit' : 20,
        'Nonce' : 11886,
        'Offset' : 0,
        'Region' : 'ap-guangzhou',
        'SecretId' : secret_id,
        'Timestamp' : 1465185768, # int(time.time())
        'Version': '2017-03-12'
    }
    s = get_string_to_sign("GET", endpoint, data)
    data["Signature"] = sign_str(secret_key, s, hashlib.sha1)
    print(data["Signature"])
    # 여기서 실제 호출해야 하며 호출 성공 후 비용이 발생할 수 있습니다.
    # resp = requests.get("https://" + endpoint, params=data)
    # print(resp.url)
```

