## 기능 개요

COS 요청 툴은 COS(Cloud Object Storage)에서 제공하는 Web 디버깅 툴로, Cloud API 3.0 Explorer 플랫폼에 통합되어 API 디버깅에 사용할 수 있습니다.

>! COS 요청 툴에서 보낸 요청은 COS 비즈니스 서버로 전송됩니다. **모든 작업은 실제 작업과 동일하므로 DELETE와 같은 작업을 수행할 때는 주의하여 진행하십시오.**

COS 요청 툴은 XML API를 지원하며 JSON API는 지원하지 않습니다.
- JSON API는 XML API가 실행되기 전에 사용자가 COS에 액세스할 수 있도록 COS에서 제공하는 API입니다. JSON API에는 표준 XML API와 동일한 기본 아키텍처가 있습니다. 데이터는 상호 운용 가능하고 교차 사용할 수 있지만 두 API는 호환되지 않습니다.
- XML API는 JSON API보다 더 풍부한 기능과 이점을 제공합니다. COS용 XML API로 업그레이드하는 것이 좋습니다.

## 툴 주소

클릭하여 [COS 요청 툴](https://console.cloud.tencent.com/api/explorer?Product=cos)로 이동합니다.

## 사용 방법

제품 **COS**와 원하는 API를 선택합니다. API에 해당하는 매개변수를 입력하고 요청 보내기를 클릭하여 응답 결과를 얻습니다.

COS 요청 툴 페이지는 제품, API, 매개변수 및 결과 섹션(왼쪽에서 오른쪽으로)을 보여줍니다. 다음과 같이 다른 섹션에서 해당 작업을 수행하고 결과 섹션에서 요청을 보내 응답 결과와 프로세스 매개변수를 얻을 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/2304f363c6f61cef274e47804f34e3a4.png)

COS 요청 툴의 자세한 작업 단계는 다음과 같다.

**1. COS 제품 선택**

가장 왼쪽의 제품 섹션에서 **COS**를 클릭하면 API 섹션에서 COS 관련 API를 볼 수 있습니다.

>?COS 요청 툴은 많은 Tencent Cloud 제품에 대한 API 디버깅 도구를 제공하는 Cloud API 3.0 플랫폼에 통합되어 있습니다. 필요에 따라 다른 제품을 선택하여 플랫폼에서 해당 API를 디버그할 수도 있습니다.

**2. 디버깅할 API 선택**

필요에 따라 디버깅용 API를 선택할 수 있습니다. API 섹션에는 Service API, Bucket API 및 Object API의 세 가지 유형의 COS 관련 API가 표시됩니다.

- Service API를 소개하기 위해 GET Service를 예로 들어 보겠습니다. GET Service API는 계정에 있는 모든 버킷의 정보를 나열할 수 있습니다. API 키가 필요합니다. 지정된 리전에서 계정의 버킷 정보를 얻으려면 매개변수 섹션에서 해당 리전을 선택하면 됩니다. 이 API에 대한 자세한 내용은 [GET Service](https://intl.cloud.tencent.com/document/product/436/8291)를 참고하십시오.
- Bucket API는 PUT Bucket lifecycle과 같이 Bucket을 작동하는 데 사용되는 API입니다. Bucket API에 대한 자세한 내용은 [Bucket API](https://www.tencentcloud.com/document/product/436/7731)를 참고하십시오.
- Object API는 PUT Object와 같은 Object를 작동하는 데 사용되는 API입니다. Object API에 대한 자세한 내용은 [Object API](https://www.tencentcloud.com/document/product/436/7739)를 참고하십시오.

**3. API에 대한 매개변수 입력**

매개변수 섹션에는 선택한 API에 대한 해당 매개변수가 나열됩니다. 다양한 COS 관련 API의 매개변수에 대한 자세한 내용은 [API Documentation](https://www.tencentcloud.com/document/product/436/10009)를 참고하십시오.

API 키는 API 호출에 필요한 매개변수입니다. API를 사용하여 버킷이나 객체와 같은 리소스를 작동하는 경우 이 API 요청을 승인하려면 API 키를 입력해야 합니다. API 키는 CAM 콘솔의 [API 키 관리](https://console.cloud.tencent.com/cam/capi) 페이지에서 찾을 수 있습니다.

>?각 API에 대해 COS 요청 툴은 각 필수 매개변수 뒤에 빨간색 별표를 표시하여 매개변수가 필수임을 알려줍니다. **필수 매개변수만**을 선택하여 매개변수 섹션에서 필수 매개변수만 볼 수도 있습니다.

**4. 요청 발송 및 응답 결과 조회**

API를 선택하고 해당 매개변수를 입력한 후 **온라인 호출** 탭에서 **요청 보내기**를 클릭합니다. 귀하의 요청이 서버로 전송되면 서버는 귀하의 요청에 따라 버킷 또는 객체를 작업합니다.

>!COS 요청 툴에서 보낸 요청은 COS 비즈니스 서버로 전송됩니다. **모든 작업은 실제 작업과 동일하므로 DELETE와 같은 작업을 수행할 때 주의하십시오.**

요청이 발송된 후 반환된 결과와 요청 매개변수가 결과 섹션의 하단에 표시됩니다. **요청 매개변수**는 HTTP 요청 본문을 나열합니다. **응답 결과**는 요청의 응답 본문을 나열합니다. **서명 프로세스**는 요청 및 생성 프로세스와 관련된 서명을 나열합니다. **Curl**은 Curl이 호출한 명령문을 나열합니다.

**예시**

예를 들어, GET Object 요청은 아래와 같이 0001.txt라는 파일을 얻기 위해 발송됩니다. **요청 매개변수**는 요청의 해당 매개변수를 나열합니다.
```http
GET https://bucketname-appid.cos.ap-region.myqcloud.com/0001.txt
Host: bucketname-appid.cos.ap-region.myqcloud.com
Authorization: q-sign-algorithm=sha1&q-ak=AKIDwqaGoCIWIG4hDWdJUTL5e3hn04xi****&q-sign-time=1543398166;1543405366&q-key-time=1543398166;1543405366&q-header-list=host&q-url-param-list=&q-signature=f50ddd3e0b54a92df9d4efe2d0c3734a8c90****
```

첫 번째 줄은 HTTP Verb와 방문할 링크를 보여줍니다. 두 번째 줄은 방문할 도메인을 보여줍니다. 마지막 줄은 요청에 대한 서명 정보를 보여줍니다. PUT 유형 요청의 경우 요청 헤더가 복잡하지만 몇 가지 공통 요청 헤더가 있습니다. 공통 요청 헤더에 대한 자세한 내용은 [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728)를 참고하십시오.

요청과 관련된 서명 및 생성 프로세스는 **서명 프로세스**에서 찾을 수 있습니다. 서명 알고리즘에 대한 자세한 내용은 [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)을 참고하십시오. 요청 서명을 생성하고 디버깅해야 하는 경우 COS 서명 툴을 사용하는 것이 좋습니다.

COS에서 반환하는 응답 결과는 다음과 같습니다.

```http
200 OK
content-type: text/plain
content-length: 6
connection: close
accept-ranges: bytes
date: Wed, 28 Nov 2018 09:42:49 GMT
etag: "5a8dd3ad0756a93ded72b823b19dd877"
last-modified: Tue, 27 Nov 2018 20:05:26 GMT
server: tencent-cos
x-cos-request-id: NWJmZTYzMTlfOWUxYzBiMDlfOTA4NF8yMWI2****
x-cos-version-id: MTg0NDY3NDI1MzAzODkyMjU****
hello!
```

첫 번째 줄의 200 OK는 요청에서 반환된 상태 코드입니다. 요청이 실패하면 해당 오류 코드가 반환됩니다. 오류 코드에 대한 자세한 내용은 [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730)를 참고하십시오. 다른 콘텐츠는 응답 헤더입니다. 다른 API의 응답 본문은 다르지만 몇 가지 공통 응답 헤더가 있습니다. 공통 응답 헤더에 대한 자세한 내용은 [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7729)를 참고하십시오.



## 주의 사항
**요청 보내기**를 클릭하여 필수 매개변수가 입력된 요청을 COS 서버에 보내면 COS가 버킷 및 객체에 대해 해당 작업을 수행합니다. 작업을 회수하거나 롤백할 수 없으므로 주의하여 사용하십시오.
