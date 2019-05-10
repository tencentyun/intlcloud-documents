Tencent Cloud API는 모든 액세스 요청에 대해 ID 인증을 진행합니다. 즉, 요청자의 ID를 인증하기 위해 모든 요청은 공통 요청 매개변수에 서명 정보(Signature)가 포함되어 있어야 합니다.
서명 정보는 보안 자격 증명에 의해 생성됩니다. 보안 자격 증명은 SecretId와 SecretKey를 포함합니다. 사용자가 아직 보안 자격 증명이 없을 경우, [클라우드 API 키 페이지](https://console.cloud.tencent.com/capi)에서 신청하십시오. 그렇지 않으면 클라우드 API를 호출할 수 없습니다.

## 1. 보안 자격 증명 신청
처음 클라우드 API를 사용하기 전에 [클라우드 API 키 페이지](https://console.cloud.tencent.com/capi)에서 보안 자격 증명을 신청하십시오.
보안 자격 증명은 SecretID와 SecretKey를 포함합니다.
* SecretID    API 호출자 ID를 표시하는 데 사용됩니다.
* SecretKey 서명 문자열과 서버의 검증 서명 문자열의 키를 암호화하는 데 사용됩니다.
* <font color='red'>사용자는 반드시 보안 자격 증명을 철저히 보관하여 유출을 방지해야 합니다.</font>

보안 자격 증명의 구체적인 신청 절차는 다음과 같습니다.

1. [Tencent Cloud 콘솔](https://console.cloud.tencent.com/)에 로그인합니다.
1. [클라우드 API 키](https://console.cloud.tencent.com/capi)의 콘솔 페이지로 이동합니다.
1. [클라우드 API 키](https://console.cloud.tencent.com/capi) 페이지에서, [생성]을 클릭하면 한 쌍의 SecretId/SecretKey를 생성할 수 있습니다.

주의: 개발자 계정은 최대 두 쌍의 SecretId/SecretKey를 보유할 수 있습니다.

## 2. 서명열 생성

보안 자격 증명 SecretId와 SecretKey가 있으면 서명열을 생성할 수 있습니다. 다음은 서명열을 생성하는 세부 과정입니다.

사용자의 SecretId와 SecretKey를 다음으로 가정합니다.

* SecretId: AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE
* SecretKey: Gu5t9xGARNpq86cd98joQYCN3EXAMPLE

**주의: 이것은 단지 예제입니다. 사용자가 실제 신청한 SecretId와 SecretKey에 따라 후속 작업을 진행해주십시오!**

CVM의 인스턴스 리스트(DescribeInstances) 조회 요청을 예로 들면, 사용자가 이 API를 호출할 때 요청 매개변수는 다음과 같을 수 있습니다.

| 매개변수 이름 | 한국어 | 매개변수 값 |
|---------|---------|---------|
| Action | 방식 이름 | DescribeInstances |
| SecretId | 키 ID | AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE |
| Timestamp | 현재 타임스탬프 | 1465185768 |
| Nonce | 임의 양의 정수 | 11886 |
| Region | 인스턴스 소재 지역 | ap-guangzhou |
| InstanceIds.0 | 조회 대기 중인 인스턴스 ID | ins-09dx96dg |
| Offset | 오프셋 | 0 |
| Limit | 최대 허용 출력 | 20 |
| Version | API 버전 | 2017-03-12 |


### 2.1. 매개변수 정렬

먼저, 모든 요청 매개변수는 매개변수 이름의 사전(ASCII 코드) 오름차순으로 정렬됩니다. 주의: 1)매개변수 이름 기준만으로 정렬하며 매개변수 값은 순서정렬 필요 없이 대응 값을 그대로 유지하면 됩니다. 2)ASCII 코드 기준으로 크기를 정렬합니다. 예를 들어, InstanceIds.2는 InstanceIds.12의 뒤에 오는 것처럼 알파벳이나 값으로 정렬하는 것이 아닙니다. 사용자는 프로그래밍 언어 중의 관련 정렬 함수를 사용하여 이 기능을 구현할 수 있습니다(예, php의 ksort 함수). 위 예제의 매개변수 정렬 결과는 다음과 같습니다.

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
다른 프로그래밍 언어로 개발할 때 위 예제의 매개변수를 정렬하여 일치한 결과를 얻으면 됩니다.

### 2.2. 요청 문자열 합치기

이 단계에서는 요청 문자열을 생성합니다.
위에서 정렬한 요청 매개변수를 "매개변수 이름" = "매개변수 값"의 형식으로 만듭니다. 예를 들어, Action 매개변수의 경우 매개변수 이름이 "Action"이며 매개변수 값은 "DescribeInstances"이므로 올바른 형식으로 포맷하면 Action = DescribeInstances가 됩니다.
**주의: "매개변수 값"은 초기값이며 url 인코딩된 값이 아닙니다.**

포맷한 매개변수를 "&"로 합칩니다. 최종 생성된 요청 문자열은 다음과 같습니다.

```
Action=DescribeInstances&InstanceIds.0=ins-09dx96dg&Limit=20&Nonce=11886&Offset=0&Region=ap-guangzhou&SecretId=AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE&Timestamp=1465185768&Version=2017-03-12
```

### 2.3. 서명 원문 문자열 합치기
이 단계에서는 서명 원문 문자열을 생성합니다.
서명 원문 문자열은 다음의 몇 가지 매개변수로 구성되어 있습니다.

1. 요청 방식: POST와 GET 방식을 지원합니다. 여기서 GET 방식을 사용하여 요청을 발송합니다. 단, 방식은 모두 대문자인 점을 주의하시기 바랍니다.
2. 요청 CVM: 인스턴스 리스트 조회(DescribeInstances)의 요청 도메인 이름은 cvm.tencentcloudapi.com입니다. 실제 요청 도메인 이름은 API가 소속한 모듈에 따라 다릅니다. 자세한 내용은 각 API의 설명을 참조하십시오.
3. 요청 경로: 현재 버전의 클라우드 API 요청 경로는 모두 /입니다.
4. 요청 문자열: 이전 단계에서 생성한 요청 문자열입니다.

서명 원문 문자열의 합치기 규칙은 요청 방식 + 요청 CVM + 요청 경로+ ? + 요청 문자열입니다.

예제의 합친 결과는 다음과 같습니다.

```
GETcvm.tencentcloudapi.com/?Action=DescribeInstances&InstanceIds.0=ins-09dx96dg&Limit=20&Nonce=11886&Offset=0&Region=ap-guangzhou&SecretId=AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE&Timestamp=1465185768&Version=2017-03-12
```

### 2.4. 서명열 생성
이 단계에서는 서명열을 생성합니다.
먼저 HMAC-SHA1 알고리즘을 사용하여 이전 단계에서 얻은 **서명 원문 문자열**을 서명합니다. 그 후, 생성된 서명열을 Base64로 인코딩하면 서명열을 얻을 수 있습니다.

PHP 언어를 예로 하여 구체적인 코드는 다음과 같습니다.

```
$secretKey = 'Gu5t9xGARNpq86cd98joQYCN3EXAMPLE';
$srcStr = 'GETcvm.tencentcloudapi.com/?Action=DescribeInstances&InstanceIds.0=ins-09dx96dg&Limit=20&Nonce=11886&Offset=0&Region=ap-guangzhou&SecretId=AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE&Timestamp=1465185768&Version=2017-03-12';
$signStr = base64_encode(hash_hmac('sha1', $srcStr, $secretKey, true));
echo $signStr;
```

얻은 서명열은 다음과 같습니다.

```
EliP9YW3pW28FpsEdkXt/+WcGeI=
```

다른 프로그래밍 언어로 개발 시, 위 예제의 원문을 이용하여 서명 검증을 진행할 수 있으며 얻은 서명열이 예제와 일치하면 됩니다.

## 3. 서명열 인코딩

생성한 서명열은 요청 매개변수로 직접 사용할 수 없으며 URL 인코딩을 진행해야 합니다.

예를 들면, 이전 단계에서 생성한 서명열은 EliP9YW3pW28FpsEdkXt/+WcGeI= 이며, 최종적으로 얻은 서명열 요청 매개변수(Signature)는 EliP9YW3pW28FpsEdkXt%2f%2bWcGeI%3d입니다. 이것은 최종적인 요청 URL을 생성하는 데 쓰입니다.

**주의: 사용자의 요청 방식이 GET이거나 요청 방식이 POST이면서 Content-Type이 application/x-www-form-urlencoded일 경우, 요청 발송 시 모든 요청 매개변수 값은 URL 인코딩을 해야 합니다. 매개변수 키와 '=' 부호는 인코딩을 하지 않아도 됩니다. ASCII 문자가 아닌 경우, URL 인코딩 전, 먼저 UTF-8 코드로 인코딩해야 합니다.**

**주의: 일부 프로그래밍 언어의 http 라이브러리는 자동으로 모든 매개변수에 URLENCODE를 진행합니다. 이 상황에서는 서명열에 URL 인코딩을 진행할 필요가 없습니다. 그렇지 않으면 두 번의 URL 인코딩으로 인해 서명 실패하게 됩니다.**

**주의: 다른 매개변수 값도 인코딩을 진행해야 합니다. 인코딩은 [RFC 3986](http://tools.ietf.org/html/rfc3986)을 사용합니다. %XY를 사용하여 한자와 같은 특수문자에 백분율 인코딩합니다. 그 중 "X"와 "Y"는 16진수 문자(0-9와 대문자 A-F)입니다. 소문자를 사용할 경우 오류가 발생할 수 있습니다.**

## 4. 서명 실패
서명 실패 시 다음과 같은 오류 코드가 발생할 수 있습니다. 실제 상황에 따라 처리해 주십시오.

| 오류 코드 | 오류 설명 |
|----------|---------|
| AuthFailure.SignatureExpire | 서명 유효기간 만료 |
| AuthFailure.SecretIdNotFound | 키가 존재하지 않음 |
| AuthFailure.SignatureFailure | 서명 오류 |
| AuthFailure.TokenFailure | token 오류 |
| AuthFailure.InvalidSecretId | 잘못된 키(클라우드 API 키 유형이 아님) |

## 5. 서명 예제

API 3.0을 호출 시, 해당하는 Tencent Cloud SDK 3.0을 사용하는 것을 권장합니다. SDK는 서명 과정을 캡슐화하여 개발 시 제품에서 제공하는 특정 API에만 집중하면 됩니다. 자세한 내용은 [SDK 센터](https://cloud.tencent.com/document/sdk)를 참조하십시오. 현재 지원하는 프로그래밍 언어는 다음과 같습니다.

* [Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [JavaScript](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [.NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

서명 과정을 더욱 명확하게 설명하기 위해 실제 프로그래밍 언어를 예로 들어 상술한 서명 과정을 구체적으로 보여드리겠습니다. 요청한 도메인 이름, 호출한 API와 매개변수 값은 모두 위에 상술한 서명 과정을 기준으로 합니다. 코드는 서명 과정을 설명하기 위한 것이며 범용성을 갖고 있지 않습니다. 실제 개발에서는 SDK를 사용하는 것을 권장합니다.

최종 출력한 URL은 `https://cvm.tencentcloudapi.com/?Action=DescribeInstances&InstanceIds.0=ins-09dx96dg&Limit=20&Nonce=11886&Offset=0&Region=ap-guangzhou&SecretId=AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE&Signature=EliP9YW3pW28FpsEdkXt%2F%2BWcGeI%3D&Timestamp=1465185768&Version=2017-03-12`일 수 있습니다.

주의: 예제 중의 키는 가상 키이고 타임스탬프 역시 시스템의 현재 시간이 아니기 때문에 해당 URL을 브라우저로 열거나 CURL 등의 명령으로 호출할 경우 인증 오류 '서명 유효시간 만료'가 반환할 수 있습니다. 정상적으로 반환할 수 있는 URL을 얻으려면 예제의 SecretId와 SecretKey를 실제 키로 수정해야 하며 시스템의 현재 타임스탬프를 Timestamp로 사용해야 합니다.

주의: 다음의 예제 중, 다른 프로그래밍 언어, 심지어 같은 언어의 각 작업으로 얻은 URL은 각기 다를 수 있으며 매개변수의 순서 차이로 나타납니다. 그러나 이것이 정확성에 영향을 주진 않습니다. 모든 매개변수가 다 존재하고 서명 컴퓨팅이 정확하기만 하면 됩니다.

주의: 다음 코드는 API 3.0에서만 적용되며 다른 서명 과정에 직접 사용할 수 없습니다. 이전 버전의 API라도 세부적인 차이로 인해 서명 컴퓨팅에 오류가 발생할 수 있으니 코드의 실제 문서에 따라주십시오.

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
        // 서명 시, 매개변수를 사전순으로 정렬해야 합니다. 정확한 순서를 위해 여기서 TreeMap을 사용합니다.
        for (String k : params.keySet()) {
            s2s.append(k).append("=").append(params.get(k).toString()).append("&");
        }
        return s2s.toString().substring(0, s2s.length() - 1);
    }

    public static String getUrl(TreeMap<String, Object> params) throws UnsupportedEncodingException {
        StringBuilder url = new StringBuilder("https://cvm.tencentcloudapi.com/?");
        // 실제 요청의 URL 중 매개변수 순서에는 요구사항이 없습니다.
        for (String k : params.keySet()) {
            // 요청열에 url 인코딩을 수행해야 합니다. key는 모두 영문이기 때문에 여기서는 해당 value에만 url 인코딩을 진행합니다.
            url.append(k).append("=").append(URLEncoder.encode(params.get(k).toString(), CHARSET)).append("&");
        }
        return url.toString().substring(0, url.length() - 1);
    }

    public static void main(String[] args) throws Exception {
        TreeMap<String, Object> params = new TreeMap<String, Object>(); // TreeMap은 자동으로 정렬됩니다.
        // 실제 호출 시, 난수를 사용해야 합니다. 예: params.put("Nonce", new Random().nextInt(java.lang.Integer.MAX_VALUE)).
        params.put("Nonce", 11886); // 공통 매개변수
        // 실제 호출 시, 시스템의 현재 시간을 사용해야 합니다. 예:   params.put("Timestamp", System.currentTimeMillis() / 1000).
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

주의: Python 2 환경에서 실행한다면 우선 requests 의존 패키지 `pip install requests`를 설치하십시오.

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
    # 여기는 실제로 호출할 것이며 호출 성공 후, 비용이 발생할 수 있습니다.
    # resp = requests.get("https://" + endpoint, params=data)
    # print(resp.url)
```
