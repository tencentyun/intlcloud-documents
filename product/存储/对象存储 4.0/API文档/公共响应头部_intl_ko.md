## 설명

이 문서는 API를 사용할 때의 공통 응답 헤더(Response Header)를 소개하며, 본문에서 설명할 헤더는 다른 구체적인 API 문서에서는 다시 서술하지 않습니다.

##  응답 헤더 리스트

| 헤더 이름         | 설명                                       | 유형     |
| ---------------- | ---------------------------------------- | ------ |
| Content-Length   | RFC 2616에서 정의한 HTTP 요청 내용 길이(바이트)            | String |
| Content-Type     | RFC 2616에서 정의한 HTTP 요청 내용 유형(MIME)          | String |
| Connection       | 클라이언트와 서비스 간의 통신 상태.<br />열거형 값: keep-alive，close | Enum   |
| Date             | 서버의 응답 시간, 시간 형식은 RFC 1123에서 정의한 GMT 시간 형식에 따릅니다.       | String |
| Etag             | ETag(전체 이름은 Entity Tag)는 객체가 생성될 때 객체 내용을 식별하는 정보 태그입니다. 이 매개변수는 MD5 값을 반드시 반환하지는 않으며, 요청별 상황에 따라 참조하십시오. ETag의 값은 객체의 내용이 변경되었는지 여부를 검사하는 데 사용됩니다. | String |
| Server           | 요청을 생성한 서버 이름. 기본값: tencent-cos              | String |
| x-cos-request-id | 요청을 발송할 때마다 서버가 요청에 대해 자동 생성한 ID.                | String |
| x-cos-trace-id   | 요청 오류 때마다 서버가 이 오류에 대해 생성한 ID.              | String |


