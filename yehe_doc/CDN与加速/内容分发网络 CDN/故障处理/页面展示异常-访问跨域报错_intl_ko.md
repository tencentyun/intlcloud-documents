
## 현상 설명

CORS 오류가 리포트되어 다음 이미지와 같이 페이지 오류 또는 예외적인 페이지 표시가 발생합니다.

![](https://main.qcloudimg.com/raw/af636dbb5bba454bb79234cd7b49dca2.png)

## 예상 원인

CORS 오류는 브라우저의 동일 출처 정책으로 인해 발생합니다. 웹 페이지 보안을 위해 이 요청에 대한 응답이 브라우저에 의해 차단되는 경우 프런트 엔드 오류 또는 예외적인 페이지 표시가 발생합니다. 요청한 URL의 **프로토콜, 도메인, 포트**중 하나라도 현재 페이지 URL과 다른 경우, 교차 사이트 요청으로 간주됩니다.

## 해결 방법

1. 다음과 같이 문제가 교차 사이트 요청으로 인해 발생했는지 확인합니다.
![](https://main.qcloudimg.com/raw/78d05383b9040d313c05add33a1737df.png)
2. CDN 콘솔에서 해당 HTTP 응답 헤더를 구성하고 이 리소스에 액세스할 수 있는 도메인을 정의합니다.

## 해결 절차

1. <a href="https://console.cloud.tencent.com/cdn/domains">CDN 콘솔</a>에 로그인하고 해당 도메인 이름 관리-고급 설정-HTTP 응답 헤더 설정에서 Access-Control-Allow-Origin 헤더 매개변수를 설정합니다. 다음과 같이 모든 도메인의 교차 사이트 요청을 허용합니다. 자세한 내용은 [Access-Control-Allow-Origin 매칭 모드 소개]를 참고하십시오(#ac).

2. 또는 다음과 같이 하나 또는 여러 개의 지정된 도메인 이름/IP에서 교차 사이트 요청을 허용하도록 설정할 수도 있습니다.
필요에 따라 Access-Control-Request-Method, Access-Control-Request-Headers, Access-Control-Max-Age 등 헤더 매개변수를 추가하여 브라우저의 모든 요청 수신 방법, 포함 가능한 헤더, 예비 요청의 유효 시간 등을 제한할 수 있습니다. 자세한 내용은 [지원되는 매개변수 리스트](#ap)를 참고하십시오.


>! COS 버킷에 교차 사이트 요청 액세스를 설정한 경우 정상적인 액세스를 위해 CDN 콘솔 <a href="https://intl.cloud.tencent.com/document/product/228/35320">HTTP 응답 헤더</a>에 교차 사이트 규칙을 설정하십시오.

[](id:ap)
### 지원되는 매개변수 리스트

| 헤더 매개변수                      | 설명                                                         |
| :---------------------------- | :----------------------------------------------------------- |
| Access-Control-Allow-Origin   | 리소스 교차 사이트 권한 문제를 해결하는데 사용되며, 리소스에 액세스할 수 있는 출처를 지정합니다. 허용된 출처의 요청은 Host에 의해 요청 헤더에 추가됩니다. 모든 출처의 요청을 허용하도록 ‘*’로 설정할 수도 있습니다. 자세한 내용은 [Access-Control-Allow-Origin 매칭 모드 소개](#ac)를 참고하십시오. `‘*’` 또는 여러 개의 도메인 / IP /도메인과 IP 혼합 입력을 지원합니다(반드시 `http://` 또는 `https://` 포함해야 함. 예: `http://test.com,http://1.1.1.1`, 쉼표로 구분) (주의: 입력 창은 최대 1000자 까지 입력 가능). |
| Access-Control-Allow-Methods  | 교차 사이트 요청에 허용되는 HTTP 메소드를 나타냅니다. Access-Control-Allow-Methods: `POST, GET, OPTIONS`와 같이 하나 이상의 메소드를 구성할 수 있습니다. |
| Access-Control-Max-Age   | 예비 요청의 유효 시간(단위: 초)을 지정합니다. 비 단순 교차 사이트 요청의 경우, 정식 통신 전에 교차 사이트 요청이 안전하고 수용 가능한지 확인하기 위해 ‘예비 요청’이라는 HTTP 쿼리 요청을 추가해야 합니다. GET, HEAD 또는 POST 요청이 아니거나 POST 요청이지만 요청 데이터 유형이 application / x-www-form-urlencoded, multipart / form-data, text / plain 이외의 유형(예: application / xml 또는 text / xml)인 경우, 비 단순 교차 사이트 요청으로 간주됩니다. 사용자 정의 요청 헤더가 ‘Access-Control-Max-Age: ‘1728000’인 경우 1728000초(20일) 내에 이 CORS에 대해 다른 예비 요청이 전송되지 않습니다. |
|Access-Control-Expose-Headers  |응답의 일부로 클라이언트에 노출될 수 있는 헤더를 지정합니다. 기본적으로 Cache-Control, Content-Language, Content-Type, Expires, Last-Modified, Pragma와 같은 6가지 헤더만 클라이언트에 노출 가능합니다. 클라이언트가 다른 헤더에 액세스할 수 있도록 하려면 여러 헤더를 쉼표로 구분합니다. 예를 들어, `Access-Control-Expose-Headers: Content-Length,X-My-Header`로 지정하면 클라이언트는 Content-Length 및 X-My-Header 두 헤더에 액세스할 수 있습니다. |

[](id:ac)
### Access-Control-Allow-Origin 매칭 모드 소개

| **매칭 모드**   | **도메인 값**                                                     | **설명**                                                     |
| :------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| 모두 허용         | `*`                                                              | `*`  로 설정할 경우, Access-Control-Allow-Origin:* 헤더가 응답에 추가됩니다. |
| 지정된 도메인       |`http://cloud.tencent.com` `https://cloud.tencent.com` `http://www.b.com` | 출처가 `https://cloud.tencent.com`이고 리스트를 히트한 경우, `Access-Control-Allow-Origin: https://cloud.tencent.com` 헤더가 응답에 추가됩니다. 출처가 `https://www.qq.com`이고 리스트를 히트하지 못한 경우, 응답이 변경되지 않습니다. |
| 2레벨 와일드카드 서브도메인 | 'https://*.tencent.com'                                       | 출처가 'https://cloud.tencent.com'이고 리스트를 히트한 경우, 'Access-Control-Allow-Origin: https://cloud.tencent.com' 헤더가 응답에 추가됩니다. 출처가 'https://cloud.qq.com'이고 리스트를 히트하지 못한 경우, 응답이 변경되지 않습니다. |
| 지정된 포트       | `https://cloud.tencent.com:8080`                             | 출처가 `https://cloud.tencent.com:8080`이고 리스트를 히트한 경우, `Access-Control-Allow-Origin:https://cloud.tencent.com:8080` 헤더가 응답에 추가됩니다. 출처가 `https://cloud.tencent.com`이고 리스트를 히트하지 못한 경우, 응답이 변경되지 않습니다. |

> !특수 포트가 있는 경우 목록에서 관련 정보를 입력해야 하며, 임의의 포트 매칭을 지원하지 않으므로 반드시 지정해야 합니다.
