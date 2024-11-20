Tencent Cloud API는 각 액세스 요청에 대해 자격 증명을 진행하고 각 요청은 공통 요청 매개변수 중에 서명 정보(Signature)를 포함시켜 요청자의 ID를 확인해야 합니다.
서명 정보는 보안 자격 증명에서 생성되며, 보안 자격 증명에는 SecretId 및 SecretKey가 포함됩니다. 사용자가 보안 자격 증명이 없을 경우, [클라우드 API 키 페이지](https://console.cloud.tencent.com/capi)에서 신청하십시오. 그렇지 않으면 클라우드 API를 호출할 수 없습니다.

## 1. 보안 자격 증명 신청
최초로 클라우드 API를 사용하기 전에 [클라우드 API 키 페이지](https://console.cloud.tencent.com/capi)에서 보안 자격 증명을 신청하십시오.
보안 자격 증명은 SecretId 및 SecretKey로 구성됩니다.
* SecretId    API 호출자의 ID를 식별하는 데 사용됩니다.
* SecretKey는 서명 문자열 암호화 및 서버측 서명 문자열 인증에 사용되는 키입니다.
* <font color='red'>사용자는 보안 자격 증명을 철저히 관리하여 누출되지 않도록 해야 합니다.</font>

보안 자격 증명 신청의 구체적 단계:

1. [Tencent Cloud 콘솔](https://console.cloud.tencent.com/)에 로그인합니다.
1. [클라우드 API 키](https://console.cloud.tencent.com/capi)의 콘솔 페이지로 갑니다.
1. [클라우드 API 키](https://console.cloud.tencent.com/capi) 페이지에서 [키 생성]을 클릭하면 SecretId/SecretKey 한 쌍을 생성할 수 있습니다.

주의: 개발사 계정은 최대 SecretId / SecretKey 두 쌍을 보유할 수 있습니다.

## 2. 서명 문자열 생성

보안 인증서 SecretId와 SecretKey가 있으면 서명 문자열을 생성할 수 있습니다. 다음은 서명 문자열 생성의 상세 절차입니다.

사용자의 SecretId와 SecretKey는 각각 다음과 같습니다.

* SecretId: AKID**********************0123456789EXAMPLE
* SecretKey: sk0123456789********************EXAMPLE

**주의: 이것은 단지 예시일 뿐입니다. 사용자는 실제 신청한 SecretId와 SecretKey에 따라 후속 작업을 수행하십시오!**

CVM으로 인스턴스 리스트 조회(DescribeInstances) 요청을 예로 들면, 사용자가 이 API를 호출하였을 때 해당 요청 매개변수는 다음과 같습니다.

| 매개변수 이름 | 한국어 | 매개변수 값 |
|---------|---------|---------|
| Action | 방법명 | DescribeInstances |
| SecretId | 키 ID | AKID**********************0123456789EXAMPLE |
| Timestamp | 현재 타임스탬프 | 1465185768 |
| Nonce | 랜덤 양의 정수 | 11886 |
| Region | 인스턴스 소재 지역 | ap-guangzhou |
| InstanceIds.0 | 조회 대기 중인 인스턴스 ID | ins-09dx96dg |
| Offset | 오프셋 | 0 |
| Limit | 최대 허용 출력 | 20 |
| Version | API 버전 번호 | 2017-03-12 |


### 2.1. 매개변수 정렬

먼저 모든 요청 매개변수에 대하여 매개변수 이름의 사전순(ASCII 코드)에 따라 오름차순으로 정렬합니다. 주의: 1)매개변수 이름에 의해서만 정렬하여 매개변수 값이 대응하면 되며, 크기 비교에는 참여하지 않습니다. 2)ASCII 코드에 따라 크기를 비교합니다. 예를 들어, InstanceIds.2는 InstanceIds.12 뒤에 오고 알파벳이나 값에 따라 정렬하지 않습니다. 사용자가 프로그래밍 언어 중의 관련 정렬 함수(예: php의 ksort 함수)를 통해 이 기능을 실현할 수 있습니다. 위 예시의 함수 정렬 결과는 다음과 같습니다.

```
{
    'Action' : 'DescribeInstances',
    'InstanceIds.0' : 'ins-09dx96dg',
    'Limit' : 20,
    'Nonce' : 11886,
    'Offset' : 0,
    'Region' : 'ap-guangzhou',
    'SecretId' : 'AKID**********************0123456789EXAMPLE',
    'Timestamp' : 1465185768,
    'Version': '2017-03-12',
}
```
기타 프로그래밍 언어를 사용하여 위의 예시 중 매개변수를 정렬할 수 있으며, 얻게 되는 결과가 같으면 됩니다.

### 2.2. 요청 문자열 합치기

이 단계는 요청 문자열 생성 절차입니다.
이전 단계에서 정렬한 요청 매개변수를 "매개변수 이름"="매개변수 값"의 형식으로 형식화합니다. 예를 들어, Action 매개변수의 경우 매개변수 이름은 "Action", 매개변수 값은 "DescribeInstances"이기 때문에 형식화 이후에는 Action=DescribeInstances가 됩니다.
**주의: "매개변수 값"은 본래 값이며 URL 코딩 이후 값이 아닙니다.**

형식화된 각 매개변수를 "&"로 연결하여, 최종 생성된 요청 문자열은 다음과 같습니다.

```
Action=DescribeInstances&InstanceIds.0=ins-09dx96dg&Limit=20&Nonce=11886&Offset=0&Region=ap-guangzhou&SecretId=AKID**********************0123456789EXAMPLE&Timestamp=1465185768&Version=2017-03-12
```

### 2.3. 서명 원문 문자열 합치기
이 단계는 서명 원문 문자열 생성 절차입니다.
서명 원문 문자열은 다음 매개변수로 구성됩니다.

1. 요청 방법: POST와 GET 방식을 지원하며, 여기서는 GET 요청을 사용합니다. 모두 대문자로 작성해야 합니다.
2. 요청 CVM: 인스턴스 리스트 조회(DescribeInstances)의 요청 도메인 이름은 cvm.tencentcloudapi.com입니다. 실제의 요청 도메인 이름은 API 소속 모듈에 따라 달라지므로 각 API 설명을 참조하십시오.
3. 요청 경로: 현재 버전 클라우드 API의 요청 경로는 / 로 고정됩니다.
4. 요청 문자열: 이전 단계에서 생성한 요청 문자열입니다.

서명 원문열의 합치기 규칙: 요청 방법 + 요청 CVM +요청 경로 + ? + 요청 문자열

예시의 합치기 결과:

```
GETcvm.tencentcloudapi.com/?Action=DescribeInstances&InstanceIds.0=ins-09dx96dg&Limit=20&Nonce=11886&Offset=0&Region=ap-guangzhou&SecretId=AKID**********************0123456789EXAMPLE&Timestamp=1465185768&Version=2017-03-12
```

### 2.4. 서명 문자열 생성
서명 문자열 생성 절차입니다.
우선 HMAC-SHA1 알고리즘을 사용하여 이전 단계에서 획득한 **서명 원문 문자열**에 서명한 뒤, 생성한 서명열은 Base64를 사용하여 인코딩을 수행하면 최종 서명 문자열을 획득할 수 있습니다.

구체적인 코드는 PHP 언어를 예로 들면 다음과 같습니다.

```
$secretKey = 'sk0123456789********************EXAMPLE';
$srcStr = 'GETcvm.tencentcloudapi.com/?Action=DescribeInstances&InstanceIds.0=ins-09dx96dg&Limit=20&Nonce=11886&Offset=0&Region=ap-guangzhou&SecretId=AKID**********************0123456789EXAMPLE&Timestamp=1465185768&Version=2017-03-12';
$signStr = base64_encode(hash_hmac('sha1', $srcStr, $secretKey, true));
echo $signStr;
```

최종 획득한 서명 문자열은 다음과 같습니다.

```
EliP9YW3pW28FpsEdkXt/+WcGeI=
```

기타 프로그래밍 언어를 사용하여 개발 시, 위의 예시 중 원문을 사용하여 서명 인증을 진행할 수 있으며, 얻게 되는 서명열이 예시와 같으면 됩니다.

## 3. 서명열 인코딩

생성한 서명열은 요청 매개변수로 직접 사용할 수 없으며 URL 인코딩을 해야 합니다.

이전 단계에서 생성한 서명열은 EliP9YW3pW28FpsEdkXt/+WcGeI=이면, 최종적으로 얻는 서명열 요청 매개변수(Signature)는 EliP9YW3pW28FpsEdkXt%2f%2bWcGeI%3d이며, 최종 요청 URL을 생성하는 데 사용됩니다.

**주의: 사용자의 요청 방법이 GET이거나, 요청 방법이 POST인 동시에 Content-Type이 application/x-www-form-urlencoded일 경우, 요청 발송 시 모든 요청 매개변수의 값은 URL 인코딩을 해야 하며, 매개변수 키와 = 부호는 인코딩할 필요가 없습니다. 비 ACSII 문자는 URL 인코딩 전에 먼저 UTF-8로 인코딩해야 합니다.**

**주의: 일부 프로그래밍 언어의 http 라이브러리는 자동으로 모든 매개변수에 대해 urlencode를 실행할 수 있습니다. 이 경우, 서명열에 대해 URL 인코딩할 필요가 없습니다. 그렇지 않으면 두 번 URL 인코딩을 해서 서명이 실패할 수 있습니다.**

**주의: 기타 매개변수 값은 모두 인코딩을 진행해야 하며, 인코딩은 [RFC 3986](http://tools.ietf.org/html/rfc3986)으로 합니다. %XY를 통해 특수 문자 예를 들어 한자에 대해 백분율 인코딩을 진행하면 그 중 “X” 및 “Y”는 16진수 문자(0~9 및 대문자 A~F)이며, 소문자를 사용하면 오류가 발생합니다.**

## 4. 서명 실패
다음의 서명 실패 오류 코드가 존재할 수 있습니다. 실제 상황에 따라 처리하십시오.

| 오류 코드 | 오류 설명 |
|----------|---------|
| AuthFailure.SignatureExpire | 서명 만료됨 |
| AuthFailure.SecretIdNotFound | 키가 존재하지 않음 |
| AuthFailure.SignatureFailure | 서명 오류 |
| AuthFailure.TokenFailure | token 오류 |
| AuthFailure.InvalidSecretId | 잘못된 키(클라우드 API 키 유형이 아님) |

## 5. 서명 데모

실제 API 3.0 호출 시, 매칭되는 Tencent Cloud SDK 3.0을 사용하는 것이 좋습니다. SDK는 서명 프로세스를 캡슐화하고, 개발 중에 제품이 제공하는 특정 API에만 집중하면 되기 때문입니다. 세부 정보는 [SDK 센터](https://cloud.tencent.com/document/sdk)를 참조하십시오. 현재 지원하는 프로그래밍 언어는 다음과 같습니다.

* [Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [JavaScript](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [.NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

서명 프로세스를 더 명확하게 설명하기 위해, 다음에서는 실제 프로그래밍 언어를 예로 들어 위에서 설명한 서명 프로세스를 구체적으로 구현해보겠습니다. 요청 도메인 이름, 호출한 API 및 매개변수의 선택 값은 모두 위에서 설명한 서명 프로세스를 기준으로 합니다. 코드는 서명 프로세스를 설명하기 위한 것이며 범용이 아닙니다. 실제 개발 시에는 최대한 SDK를 사용하십시오.

가능한 최종 출력 url: `https://cvm.tencentcloudapi.com/?Action=DescribeInstances&InstanceIds.0=ins-09dx96dg&Limit=20&Nonce=11886&Offset=0&Region=ap-guangzhou&SecretId=AKID**********************0123456789EXAMPLE&Signature=EliP9YW3pW28FpsEdkXt%2F%2BWcGeI%3D&Timestamp=1465185768&Version=2017-03-12`

주의: 예시의 키는 가상이므로, 타임스탬프도 시스템 현재 시간이 아니며, 이 URL을 브라우저에서 열거나 curl과 같은 명령으로 호출하면 "서명 만료"의 인증 오류가 반환됩니다. 정상적으로 반환되는 URL을 얻으려면, 예시의 SecretId 및 SecretKey를 실제 키로 수정하고 시스템 현재 타임스탬프를 Timestamp로 사용해야 합니다.

주의: 다음의 예시에서 서로 다른 프로그래밍 언어는 물론이고 동일한 언어조차 매번 얻는 URL은 모두 서로 다를 수 있고 이는 매개변수의 순서가 다름으로 나타나지만 정확성에는 영향을 주지 않습니다. 모든 매개변수가 있고 서명 컴퓨팅이 정확하다면 됩니다.

주의: 다음의 코드는 API 3.0에만 적용되고, 다른 서명 프로세스에 직접 사용할 수 없습니다. 이전 버전의 API의 경우 미세한 차이가 존재하여 서명 컴퓨팅 오류가 발생할 수 있으므로 해당하는 실제 문서를 기준으로 하시기 바랍니다.

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
        // 서명 시 매개변수에 대하여 사전순으로 정렬해야 하며, 여기서는 TreeMap을 사용하여 순서를 보장합니다.
        for (String k : params.keySet()) {
            s2s.append(k).append("=").append(params.get(k).toString()).append("&");
        }
        return s2s.toString().substring(0, s2s.length() - 1);
    }

    public static String getUrl(TreeMap<String, Object> params) throws UnsupportedEncodingException {
        StringBuilder url = new StringBuilder("https://cvm.tencentcloudapi.com/?");
        // 실제 요청 URL에서 매개변수 순서에 대한 요구 사항은 없습니다.
        for (String k : params.keySet()) {
            // 요청 문자열에 대해 urlencode를 진행해야 하며, key가 모두 영문 알파벳이므로 여기서는 그 value에 대해서만 urlencode를 진행합니다.
            url.append(k).append("=").append(URLEncoder.encode(params.get(k).toString(), CHARSET)).append("&");
        }
        return url.toString().substring(0, url.length() - 1);
    }

    public static void main(String[] args) throws Exception {
        TreeMap<String, Object> params = new TreeMap<String, Object>(); // TreeMap은 자동으로 정렬될 수 있습니다.
        // 실제 호출 시 난수를 사용해야 합니다. 예: params.put("Nonce", new Random().nextInt(java.lang.Integer.MAX_VALUE)).
        params.put("Nonce", 11886); // 공통 매개변수
        // 실제 호출 시 시스템 현재 시간을 사용해야 합니다. 예: params.put("Timestamp", System.currentTimeMillis() / 1000).
        params.put("Timestamp", 1465185768); // 공통 매개변수
        params.put("SecretId", "AKID**********************0123456789EXAMPLE"); // 공통 매개변수
        params.put("Action", "DescribeInstances"); // 공통 매개변수
        params.put("Version", "2017-03-12"); // 공통 매개변수
        params.put("Region", "ap-guangzhou"); // 공통 매개변수
        params.put("Limit", 20); // 비즈니스 매개변수
        params.put("Offset", 0); // 비즈니스 매개변수
        params.put("InstanceIds.0", "ins-09dx96dg"); // 비즈니스 매개변수
        params.put("Signature", sign(getStringToSign(params), "sk0123456789********************EXAMPLE", "HmacSHA1")); // 공통 매개변수
        System.out.println(getUrl(params));
    }
}
```

### Python

주의: Python 2 환경에서 실행 중인 경우, 먼저 requests 의존 패키지인 pip install requests를 설치해야 합니다.

```python
# -*- coding: utf8 -*-
import base64
import hashlib
import hmac
import time

import requests

secret_id = "AKID**********************0123456789EXAMPLE"
secret_key = "sk0123456789********************EXAMPLE"

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
    # 여기에서 실제 호출을 합니다. 성공 후 과금될 수 있습니다
    # resp = requests.get("https://" + endpoint, params=data)
    # print(resp.url)
```
