## 기능 개요

COS 요청 도구는 COS에서 제공하는 웹 측 디버깅 도구로, 클라우드 API 3.0 Explorer 플랫폼에 통합되어 있으며 API 디버깅에 사용할 수 있습니다.

>! COS 요청 도구가 보낸 요청은 COS 비즈니스 서버로 전송됩니다. **모든 작업은 실제 작업과 동일하므로 DELETE 클래스 작업을 수행 할 때는주의하십시오.**

COS 요청 도구는 XML API를 지원하며 JSON API를 지원하지 않습니다.
- JSON API는 사용자가 XML API를 시작하기 전에 COS에 액세스할 수 있도록 COS에서 제공하는 API입니다. JSON API는 표준 XML API의 기본 아키텍처가 동일합니다. 이들의 데이터는 상호 연결 가능하며 교차 사용 가능하지만 API는 호환되지 않습니다.
- XML API는 JSON API보다 다양한 기능과 이점을 제공합니다. COS에 대해 XML API로 업그레이드하는 것이 좋습니다.

## 사용 방법

[COS 요청 도구](https://console.cloud.tencent.com/api/explorer?Product=cos) 페이지를 클릭한 다음 "COS" 및 원하는 API를 선택하십시오. API에 해당하는 매개변수를 입력하고 요청 전송을 클릭하여 응답 결과를 가져옵니다.

COS 요청 도구 페이지에는 제품, API, 매개변수 및 결과 섹션이 표시됩니다(왼쪽에서 오른쪽으로). 서로 다른 섹션에서 해당 작업을 수행하고 결과 섹션에서 요청을 보내면 아래와 같이 응답 결과와 프로세스 매개변수를 얻을 수 있습니다.
![](https://main.qcloudimg.com/raw/6329b432ed56516ca311bcbe5720d13f.png)

COS 요청 도구의 상세한 작업은 다음과 같습니다.

**1. COS 제품을 선택합니다**

가장 왼쪽 제품 섹션에서 [COS]를 클릭하면 API 섹션에서 COS 관련 API를 볼 수 있습니다.

>?COS 요청 도구는 많은 Tencent Cloud 제품에 대한 API 디버깅 도구를 제공하는 클라우드 API 3.0 플랫폼에 통합되어 있습니다. 필요에 따라 다른 제품을 선택하여 플랫폼에서 API를 디버깅할 수도 있습니다.

**2. 디버깅할 API를 선택합니다**

필요에 따라 디버깅할 API를 선택할 수 있습니다. API 섹션에는 Service API, Bucket API 및 Object API가 표시됩니다.

- Service API를 소개하기 위해 GET Service를 예로 듭니다. GET Service API는 계정의 모든 버킷 정보를 나열할 수 있고 API 키 정보가 필요합니다. 특정 지역에서 계정의 버켓 정보를 얻으려면 매개변수 섹션에서 해당 지역을 선택할 수 있습니다. 이 API에 대한 자세한 내용은 [GET Service](https://cloud.tencent.com/document/product/436/8291) 문서를 참조하십시오.
- Bucket API는 PUT Bucket lifecycle과 같은 버킷을 조작하는 데 사용되는 API입니다. Bucket API에 대한 자세한 내용은 [Bucket API](https://cloud.tencent.com/document/product/436/7731)를 참조하십시오.
- Object API는 PUT Object와 같이 객체를 조작하는 데 사용되는 API입니다. Object API에 대한 자세한 내용은 [Object API](https://cloud.tencent.com/document/product/436/7739)를 참조하십시오.

**3. API에 필요한 매개변수를 입력합니다**

매개변수 섹션에는 선택한 API에 대한 해당 매개변수가 나열되어 있습니다. 다양한 COS 관련 API의 매개변수에 대한 자세한 내용은 [API 문서](https://cloud.tencent.com/document/product/436/10009)를 참조하십시오.

API 키 정보는 API 호출에 필요한 매개변수입니다. API를 사용하여 버킷 또는 객체와 같은 리소스를 작업할 때 이번 API 요청을 인증하려면 API 키 정보를 입력해야 합니다. API 키 정보는 CAM 콘솔의 [API 키 관리](https://console.cloud.tencent.com/cam/capi) 페이지에서 찾을 수 있습니다.

>?각 API에 대해 COS 요청 도구는 필수 매개변수 뒤에 빨간색 별표를 표시하여 필수 항목인지 알려줍니다. 매개변수 섹션에서 필요한 매개변수만 보려면 **필수 매개변수**를 선택할 수 있습니다.

**4. 요청을 보내고 응답 결과를 봅니다**

API를 선택하고 해당 매개변수를 입력한 다음 [온라인 호출] 탭에서 [요청 보내기]를 클릭하십시오. 이때 요청이 서버로 보내고 서버는 요청에 따라 버킷이나 해당 객체를 조작합니다.

>!COS 요청 도구가 보낸 요청은 COS 비즈니스 서버로 전송됩니다. **모든 작업은 실제 작업과 동일하므로 DELETE 클래스 작업을 수행 할 때는주의하십시오.**

요청이 보낸 후 반환된 결과와 요청 매개변수가 결과 섹션의 아래 부분에 표시됩니다. [요청 매개변수]는 HTTP 요청 본문을 나열합니다. [응답 결과]는 요청의 응답 본문을 나열합니다.[서명 프로세스]에는 요청에 관련된 서명 및 생성 프로세스가 나열됩니다. [Curl]은 Curl이 호출한 어구를 나열합니다.

**예시**

예를 들어, 아래와 같이 0001.txt이라는 파일을 얻기 위해 GET Object 요청이 전송됩니다. [요청 매개변수]는 요청의 해당 매개변수를 나열합니다. 다음과 같습니다.

```
GET https://bucketname-appid.cos.ap-region.myqcloud.com/0001.txt
Host: bucketname-appid.cos.ap-region.myqcloud.com
Authorization: q-sign-algorithm=sha1&q-ak=AKIDwqaGoCIWIG4hDWdJUTL5e3hn04xiD5kI&q-sign-time=1543398166;1543405366&q-key-time=1543398166;1543405366&q-header-list=host&q-url-param-list=&q-signature=f50ddd3e0b54a92df9d4efe2d0c3734a8c9007ec
```

첫 번째 라인에는 HTTP 동사와 방문한 링크가 표시됩니다. 두 번째 라인은 방문할 도메인을 보여줍니다. 마지막 라인에는 요청에 대한 서명 정보가 표시됩니다. PUT 유형의 요청의 경우 요청 헤더가 복잡하지만 몇 가지 일반적인 공통 요청 헤더가 있습니다. 공통 요청 헤더에 대한 자세한 내용은 [공통 요청 헤더](https://cloud.tencent.com/document/product/436/7728)를 참조하십시오.

요청에 포함된 서명 및 생성 프로세스는 [서명 프로세스]에서 확인할 수 있습니다. 서명 알고리즘에 대한 자세한 내용은 [요청 서명](https://intl.cloud.tencent.com/document/product/436/7778)을 참조하십시오. 요청 서명을 생성하고 디버깅해야 하는 경우 [COS 서명 도구](https://cos5.cloud.tencent.com/static/cos-sign/)를 사용하는 것이 좋습니다.

COS에서 반환한 응답 결과는 다음과 같습니다.

```
200 OK
content-type: text/plain
content-length: 6
connection: close
accept-ranges: bytes
date: Wed, 28 Nov 2018 09:42:49 GMT
etag: "5a8dd3ad0756a93ded72b823b19dd877"
last-modified: Tue, 27 Nov 2018 20:05:26 GMT
server: tencent-cos
x-cos-request-id: NWJmZTYzMTlfOWUxYzBiMDlfOTA4NF8yMWI2YjE=
x-cos-version-id: MTg0NDY3NDI1MzAzODkyMjUzNjM
hello!
```

첫 번째 라인의 `200 OK`는 요청에 의해 반환된 상태 코드입니다. 요청이 실패하면 해당 오류 코드가 반환됩니다. 오류 코드에 대한 자세한 내용은 [오류 코드](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 다른 내용은 응답 헤더입니다. 서로 다른 API의 응답 본문은 다르지만 몇 가지 공통 응답 헤더가 있습니다. 공통 응답 헤더에 대한 자세한 내용은 [공통 응답 헤더](https://cloud.tencent.com/document/product/436/7729)를 참조하십시오.



## 주의 사항
[요청 보내기]를 클릭하여 COS 서버에 필수 매개변수를 입력된 요청을 보낼 때, COS는 버킷 및 객체에 대해 해당 작업을 수행합니다. 작업을 실행 취소하거나 롤백할 수 없으므로 신중하게 작업하십시오.
