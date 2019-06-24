Tencent Cloud COS는 XML API를 사용합니다. 이는 경량급의 연결하지 않은 상태의 API이므로, 이 API를 호출하면 HTTP/HTTPS를 통해 요청을 발송하고 응답을 수신하여 Tencent Cloud COS 백그라운드의 인터랙션 작업을 구현할 수 있습니다.

각기 다른 데이터 전송 프레임을 사용하였기 때문에 COS는 클라우드 API의 독립적인 API와 독립적인 SDK를 제공합니다. COS의 [API 작업 리스트](https://cloud.tencent.com/document/product/436/10111)에서 세부 정보를 파악하거나 COS의 [SDK 리스트](https://cloud.tencent.com/document/product/436/6474)에서 필요한 SDK를 다운로드할 수 있습니다. 클라우드 API 가이드와 이에 대응하는 SDK는 COS의 작업 기능을 포함하지 않습니다.

>!
>- COS의 가용 지역(Region) 세부 정보는 [지역과 접근 도메인 이름](https://cloud.tencent.com/document/product/436/6224) 문서를 참조하십시오. 
>- API 또는 SDK를 사용하여 요청을 개시하기 전, [요청 생성 개요](https://cloud.tencent.com/document/product/436/31315) 문서를 참조하여 접근 개시 도메인 이름, 보안 인증 개념 및 사설/공인 접근 검사 등 정보를 파악하십시오.
>- COS는 XML과 JSON 두 가지 버전의 API가 존재하며, 두 가지 버전의 API 프로토콜은 다르지만 접근 데이터는 상호 연결됩니다.
>- Tencent Cloud는 XML API 사용을 권장하며, 히스토리 버전의 JSON API는 2018년 이후 출시된 새로운 기능을 더는 제공하지 않습니다.

## 용어 정보
문장 중 출현할 수 있는 일부 주요 개념과 용어:
<style rel="stylesheet">
table th:nth-of-type(1) {
width: 150px;	
}
table th:nth-of-type(2) {
width:550px;	
}
</style>

|이름|	설명|
|---|---|
| APPID	|개발자가 COS 서비스에 접근할 때 보유한 사용자 차원의 고유 리소스 ID로 리소스 식별에 사용됩니다.|
| SecretId | 개발자가 보유한 프로젝트 신분 식별 ID로 신분 인증에 사용됩니다.|
| SecretKey	| 개발자가 보유한 프로젝트 신분 키|
| Bucket|	 COS 중 데이터 저장에 사용되는 컨테이너|
| Object|	 COS에 저장한 구체적인 파일로 저장의 기본 엔터니입니다.|
| Region|	도메인 이름의 지역 정보입니다. 열거값은 [가용 지역](https://cloud.tencent.com/document/product/436/6224) 문서를 참조하십시오. 예: ap-beijing, ap-hongkong, eu-frankfurt 등 |
| ACL |	접근 제어 리스트(Access Control List), 특정 Bucket 또는 Object의 접근 제어 정보 리스트를 가리킵니다.|
| CORS | 크로스 도메인 리소스 공유(Cross-Origin Resource Sharing), <br>요청을 개시한 리소스 소재 지역이 해당 요청은 보낼 대상 리소스 소재 지역과 다른 HTTP 요청입니다 |
| Multipart Uploads |멀티파트 업로드, Tencent Cloud COS가 파일 업로드를 위해 제공하는 멀티파트 업로드 모드입니다.|

## 시작 가이드

Tencent Cloud COS API를 사용하려면 우선 다음 절차를 실행해야 합니다.

1. Tencent Cloud COS 서비스를 구매합니다.
2. Tencent Cloud [COS 콘솔](https://console.cloud.tencent.com/cos5)에 Bucket 1개를 생성합니다.
2. 접근 관리 콘솔의 [클라우드 API 키](https://console.cloud.tencent.com/capi) 페이지에서 APPID, SecretId, SecretKey 내용을 획득합니다.
2. 요청 서명 알고리즘 프로세스를 프로그래밍(또는 임의의 서버 SDK를 사용)합니다.
3. 서명을 계산하고 API 실행 작업을 호출합니다.

## 히스토리 버전 API
[히스토리 버전 API 소개](https://cloud.tencent.com/document/product/436/6052)를 참조하십시오.

