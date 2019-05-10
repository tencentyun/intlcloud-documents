## 설명

이 문서는 API를 사용할 때 필요한 공통 요청 헤더(Request Header)를 소개하며, 본문에서 설명할 헤더는 다른 구체적인 API 문서에서 다시 서술하지 않습니다.

##  요청 헤더 리스트

| 헤더 이름           | 설명                                       | 유형     | 필수 선택   |
| ------------------ | ---------------------------------------- | ------ | ---- |
| Authorization      | 인증 정보를 지침하며 요청의 유효성 검증에 사용하는 서명 정보입니다. 공개 읽기 파일의 경우, 이 헤더를 가질 필요가 없습니다. | String | 아니요    |
| Content-Length     | RFC 2616에서 정의한 HTTP 요청 내용 길이(바이트)로 PUT 유형의 API 작업에 흔히 사용됩니다. | String | 아니요    |
| Content-Type       | text/plain과 같이 RFC 2616에서 정의한 HTTP 요청 내용 유형(MIME)입니다. 동시에 charset 속성을 설정할 수 있고, 클라이언트가 파일 다운로드 후 기본 인코딩 방식으로 파일을 열기 때문에 글자가 깨지는 것을 막을 수 있습니다. | String | 아니요   |
| Content-MD5        | RFC 1864에서 정의한 Base64로 인코딩돈 128-bit 내용 MD5 검증값입니다. 이 헤더는 파일 내용에 변화 발생 여부를 검사하는 데 사용됩니다. | String | 아니요    |
| Date               | RFC 1123에서 정의한 GMT 시간입니다. 예: Wed, 30 Mar. 2016 23:00:00 GMT. | String | 아니요    |
| Expect             | Expect: 100-continue를 사용할 때, 서버 확인을 수신해야 요청 내용을 발송하게 됩니다. 해당 옵션은 헤더 유효 여부를 인증하는 데 사용되며, 데이터 내용을 발송할 필요가 없습니다.<br />유효값: 100-continue. | String | 아니요    |
| Host               | 요청 CVM. 형식은 &lt;BucketName&gt;-&lt;APPID&gt;.cos.&lt;Region&gt;.myqcloud.com입니다. | String | 예    |
| Cache-Control |	RFC 2616에서 정의한 캐시 정책으로 Object 메타데이터로 저장됩니다.| String|아니요
|x-cos-security-token | 임시 보안 인증서를 사용할 때 입력해야 할 보안 토큰 필드입니다. [임시 보안 인증서 관련 설명](https://cloud.tencent.com/document/product/436/31315#.E4.B8.B4.E6.97.B6.E5.AE.89.E5.85.A8.E5.87.AD.E8.AF.81)을 참조하십시오.|  String  | 아니요

