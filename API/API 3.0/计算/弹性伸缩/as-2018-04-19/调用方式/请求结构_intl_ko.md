## 1.서비스 주소

API 요청은 가장 가까운 지역으로 액세스할 수 있습니다. 본 제품의 가까운 지역 액세스 도메인 이름은 cvm.tencentcloudapi.com입니다. 또한 지정한 지역 도메인 이름 액세스를 지원합니다. 예를 들어 광저우 지역의 도메인 이름은 cvm.ap-guangzhou.tencentcloudapi.com입니다.

가까운 지역으로 액세스의 도메인 이름 사용을 권장합니다. API 호출 시 클라이언트 소재 위치에 따라 **가장 까가운** 지역의 서버로 해석합니다. 예를 들어 광저우에서 요청을 전송하면 광저우 서버로 자동으로 해석되고 이는 cvm.ap-guangzhou.tencentcloudapi.com을 지정하는 것과 똑 같습니다.

**주의 : 대기 시간에 민감한 비즈니스는 지역을 포함하는 도메인 이름을 지정하기를 권장합니다.**

현재 지원되는 도메인 이름 리스트는 다음과 같습니다.

| 액세스 지역 | 도메인 이름 |
|----------|------|
| 가까운 지역 액세스(권장. 비금융 지역만 지원) | cvm.tencentcloudapi.com|
| 화남 지역(광저우) | cvm.ap-guangzhou.tencentcloudapi.com|
| 화동 지역(상하이) | cvm.ap-shanghai.tencentcloudapi.com|
| 화북 지역(베이징) | cvm.ap-beijing.tencentcloudapi.com|
| 화남 지역(청두) | cvm.ap-chengdu.tencentcloudapi.com|
| 서남 지역(충칭) | cvm.ap-chongqing.tencentcloudapi.com|
| 동남아 지역(중국 홍콩) | cvm.ap-hongkong.tencentcloudapi.com |
| 동남아 지역(싱가포르) | cvm.ap-singapore.tencentcloudapi.com|
| 아시아 및 태평양 지역(방콕) | cvm.ap-bangkok.tencentcloudapi.com|
| 아시아 및 태평양 지역(뭄바이) | cvm.ap-mumbai.tencentcloudapi.com|
| 아시아 및 태평양 지역(서울) | cvm.ap-seoul.tencentcloudapi.com|
| 아시아 및 태평양 지역(도쿄) | cvm.ap-tokyo.tencentcloudapi.com |
| 미국 동부(버지니아) | cvm.na-ashburn.tencentcloudapi.com|
| 미국 서부(실리콘 밸리) | cvm.na-siliconvalley.tencentcloudapi.com|
| 북미 지역(토론토) | cvm.na-toronto.tencentcloudapi.com |
| 유럽 지역(프랑크푸르트) | cvm.eu-frankfurt.tencentcloudapi.com |
| 유럽 지역(모스크바) | cvm.eu-moscow.tencentcloudapi.com |

** 주의: [금융 지역](https://cloud.tencent.com/document/product/304/2766)과 비금융 지역은 서로 격리되어 연결되지 않기 때문에 금융 지역 서비스에 액세스할 경우(공통 매개변수 Region은 금융 지역임), 금융 지역을 포함한 도메인 이름을 동시에 지정해야 하고 가장 좋은 것은 Region의 지역과 일치하는 것입니다.

| 액세스 금융 지역 | 금융 지역 도메인 이름 |
|----------|------|
| 화동 지역(상하이 금융)| cvm.ap-shanghai-fsi.tencentcloudapi.com|
| 화남 지역(선전 금융)| cvm.ap-shenzhen-fsi.tencentcloudapi.com|

## 2. 통신 프로토콜

Tencent Cloud API의 모든 API는 HTTPS를 통해 통신하므로 높은 안전성을 보장합니다.

## 3. 요청 방식

지원하는 HTTP 요청 방식:

* POST(권장)
* GET

POST 요청이 지원하는 Content-Type 유형:

* application/json(권장), 반드시 TC3-HMAC-SHA256 서명 방법을 사용해야 합니다.
* application/x-www-form-urlencoded, 반드시 HmacSHA1 또는 HmacSHA256 서명 방법을 사용해야 합니다.
* multipart/form-data(일부 API만 지원), 반드시 TC3-HMAC-SHA256 서명 방법을 사용해야 합니다.

GET 요청 길이는 32KB를 초과해서는 안 됩니다. POST 요청에 사용하는 서명 방법은 HmacSHA1, HmacSHA256일 경우 길이는 1MB를 초과해서는 안 됩니다.

## 4. 문자 인코딩

모두 UTF-8로 인코딩됩니다.
