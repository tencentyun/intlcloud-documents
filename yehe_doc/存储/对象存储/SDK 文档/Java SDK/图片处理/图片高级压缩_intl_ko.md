## 소개

본 문서는 이미지 고급 압축에 대한 API 개요 및 SDK 예시 코드를 제공합니다.


|API           |  작업 설명               |
| :--------------- |  :--------------------- |
| [이미지 고급 압축](https://intl.cloud.tencent.com/document/product/436/40119)|이미지 고급 압축은 이미지를 TPG 또는 HEIF 등 압축 비율이 높은 포맷으로 변환하여 이미지 전송 링크 및 로딩 시 소모되는 시간을 효과적으로 단축하고 대역폭 및 트래픽 비용을 절감합니다.|

#### 예시 코드

[//]: # ".cssg-snippet-process-with-pic-operation"
```java
GetObjectRequest getObj = new GetObjectRequest(bucketName, key);
// 다음은 이미지 압축 매개변수이며 자세한 내용은 CI API를 참조하십시오. 이것은 예시일 뿐입니다.
String compress = "imageMogr2/format/tpg";
getObj.putCustomQueryParameter(compress, null);
```