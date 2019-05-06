## 개요

이 문서는 요청 오류 시 반환한 오류 코드와 해당 오류 정보를 소개합니다.

## 오류 정보 반환 형식

### 반환 헤더

Content-Type: application/xml

해당 HTTP 상태 코드: 3XX, 4XX, 5XX

### 반환 내용

**구문 형식**

```XML
<?xml version="1.0" encoding="UTF-8"?>
<Error>
  <Code>[오류 코드]</Code>
  <Message>[오류 정보]</Message>
  <Resource>[리소스 주소]</Resource>
  <RequestId>[요청 ID]</RequestId>
  <TraceId>[오류 ID]</TraceId>
</Error>
```
<style  rel="stylesheet"> table th:nth-of-type(1) { width: 200px; }</style>

**요소 설명**

| 요소 이름      | 설명                                       | 유형        |
| --------- | ---------------------------------------- | --------- |
| Error     | 모든 오류 정보를 포함합니다.                               | Container |
| Code      | 오류 코드는 유일한 오류 조건을 찾고 오류 시나리오를 확인하는 데 사용됩니다. 구체적인 오류 코드는 아랫글을 참조하십시오.        | String    |
| Message   | 구체적인 오류 정보를 포함합니다.                               | String    |
| Resource  | 리소스 주소: Bucket 주소 또는 Object 주소입니다.                 | String    |
| RequestId | 요청 발송 시, 서버는 요청에 유일한 ID 1개를 자동 생성합니다. 문제가 발생하면 request-id는 COS가 문제를 지정하는 데 도움이 됩니다. | String    |
| TraceId   | 요청 오류 발생 시, 서버는 오류에 유일한 ID 1개를 자동 생성합니다. 문제가 발생하면 trace-id는 COS가 문제를 지정하는 데 도움이 됩니다. 요청에 오류 발생 시, trace-id와 request-id는 일일이 대응합니다. | String    |

## 오류 코드 리스트

**3XX 유형 오류**

| 오류 코드               | 설명                                       | HTTP 상태 코드             |
| ----------------- | ---------------------------------------- | --------------------- |
| PermanentRedirect | 해당 리소스는 이미 영구적으로 위치가 변경되었습니다. HTTP Location을 이용하여 정확하고 새로운 위치에 방향 지정합니다. | 301 Moved Permanently |
| TemporaryRedirect | 해당 리소스는 이미 위치가 임시 변경되었습니다. HTTP Location을 이용하여 정확하고 새로운 위치에 방향 지정합니다. | 302 Moved Temporarily |
| Redirect          | 임시 리디렉션                                    | 307 Moved Temporarily |
| TemporaryRedirect | DNS 업데이트 기간 동안 임시 리디렉션됩니다                        | 307 Moved Temporarily |

**4XX 유형 오류**

| 오류 코드                                 | 설명                                | HTTP 상태 코드                             |
| ----------------------------------- | --------------------------------- | ----------------------------------- |
| InvalidSHA1Digest                        | 요청 내용의 sha1 검사가 잘못되었습니다                        | 400 Bad Request  |
| NoSuchUpload                        |	멀티파트 업로드시 지정한 uploadid는 존재하지 않습니다                    | 400 Bad Request  |
| InvalidPart                         |  멀티파트가 누락되었습니다                                       | 400 Bad Request  |
| InvalidPartOrder                      | 멀티파트 업로드 번호가 연속되어 있지 않습니다                               | 400 Bad Request  |
| ObjectNotAppendable                  | 지정한 파일은 추가할 수 없습니다                               | 400 Bad Request  |
| AppendPositionErr                     | 추가된 파일 길이가 위치와 일치하지 않습니다                 | 400 Bad Request  |
| NoSuchVersion                        | 지정 버전이 존재하지 않습니다                                   | 400 Bad Request  |
| NoLifecycle                          | 수명 주기가 존재하지 않습니다                                   | 400 Bad Request  |
| PreconditionFailed                   | 사전 조건 매칭 실패                                  | 400 Bad Request  |
| UnexpectedContent                    | 요청은 관련 내용을 지원하지 않습니다                                | 400 Bad Request  |
| MultiBucketNotSupport                 | 지역 간 복사는 1개의 대상 bucket만 설정할 수 있습니다                    | 400 Bad Request  |
| NotSupportedStorageClass              | 지정 스토리지 클래스가 잘못되었습니다                              | 400 Bad Request  |
| BadDigest                           | 제공한 x-cos-SHA-1 값이 서버측에 수신한 파일 SHA-1 값에 부합하지 않습니다. | 400 Bad Request                     |
| EntityTooSmall                      | 업로드 파일 크기가 요구한 최소값을 만족시키지 못하며, 멀티파트 업로드에서 자주 볼 수 일어납니다          | 400 Bad Request                     |
| EntityTooLarge                      | 업로드 파일 크기가 요구한 최대값을 초과하였습니다                   | 400 Bad Request                     |
| ImcompleteBody                      | 요청의 실제 내용 길이가 지정한 Conent-Length에 부합하지 않습니다            | 400 Bad Request                     |
| IncorrectNumberOfFilesInPostRequest | Post 요청은 매번 1개 파일 업로드만 허가합니다                 | 400 Bad Request                     |
| InlineDataTooLarge                  | 내부 연결 데이터 크기가 요구한 최대값보다 큽니다                    | 400 Bad Request                     |
| InvalidArgument                     | 요청 매개변수가 잘못되었습니다                   | 400 Bad Request                     |
| InvalidBucketName                   | Bucket 이름이 잘못되었습니다                       | 400 Bad Request                     |
| InvalidDigest                       | x-cos-SHA-1 값이 잘못되었습니다                   | 400 Bad Request                     |
| InvalidPart                         | 멀티파트가 누락되었거나 SectionID 오류입니다                 | 400 Bad Request                     |
| InvalidPolicyDocunment              | 정책 구성 파일이 잘못되었습니다                         | 400 Bad Request                     |
| InvalidURI                          | URI가 잘못되었습니다                            | 400 Bad Request                     |
| KeyTooLong                          | 사용자 지정 헤더가 너무 깁니다                            | 400 Bad Request                     |
| MalformedACLError                   | 지정된 ACL 정책이 XML 구문에 부합하지 않습니다                  | 400 Bad Request                     |
| MalformedPOSTRequest                | 해당 POST 요청의 본문 내용이 잘못되었습니다         | 400 Bad Request                     |
| MalformedXML                        | 본문이 XML 구문에 부합하지 않습니다                 | 400 Bad Request                     |
| MaxMessageLengthExceeded            | 요청이 너무 깁니다                              | 400 Bad Request                     |
| MaxPostPreDataLengthExceededError   | 해당 POST 요청의 선행 데이터 필드가 과도하게 길며, 멀티파트 업로드에서 흔히 볼 수 있습니다            | 400 Bad Request                     |
| MatadataTooLarge                    | 메타데이터 크기가 요구한 최대값을 초과하였습니다                     | 400 Bad Request                     |
| MissingRequestBodyError             | 요청 본문이 누락되었습니다                          | 400 Bad Request                     |
| MissingSecurityHeader               | 필요한 헤더가 누락되었습니다                        | 400 Bad Request                     |
| MissingContentMD5             | 요청 헤더에 Content-MD5가 없습니다                         | 400 Bad Request                     |
| MissingAppid                  |   요청 헤더에 Appid가 없습니다.  | 400 Bad Request                     |
| MissingHost                   |  요청 헤더에 Host가 없습니다.    | 400 Bad Request                     |
| RequestIsNotMultiPartContent        | Post 요청 Content-Type이 잘못되었습니다            | 400 Bad Request                     |
| RequestTimeOut                      | 데이터 읽기가 시간 초과하였을 경우, 네트워크가 너무 느리거나 동시 업로드 수가 과도하게 큰지 검사합니다          | 400 Bad Request           |
| TooManyBucket                       | bucket 수량이 한도(200)를 초과하였습니다                       | 400 Bad Request                     |
| UnexpectedContent                   | 요청은 관련 내용을 지원하지 않습니다                         | 400 Bad Request                     |
| UnresolvableGrantByUID              | 제공한 UID가 존재하지 않습니다                         | 400 Bad Request                     |
| UserKeyMustBeSpecified              | Bucket의 Post 작업에 대해 반드시 명확한 경로를 지정해야 합니다           | 400 Bad Request                     |
| ExpiredToken                       | 서명 문자열이 만료되었습니다                                 | 403 Forbidden                       |
| AccessDenied                        | 서명 또는 권한이 정확하지 않아 접근을 거절하였습니다                 | 403 Forbidden                       |
| AccountProblem                     | 계정이 이 작업을 거절하였습니다                       | 403 Forbidden                       |
| InvaildAccessKeyId                  | AccessKey가 존재하지 않습니다                      | 403 Forbidden                       |
| InvalidObjectState                  | 요청 내용이 Object 속성과 서로 충돌합니다                  | 403 Forbidden                       |
| InvalidSecurity                     | 서명 문자열이 잘못되었습니다                            | 403 Forbidden                       |
| RequestTimeTooSkewed                | 요청 시간이 권한 유효 시간을 초과하였습니다                      | 403 Forbidden                       |
| SignatureDoesNotMatch               | 제공한 서명이 규칙에 부합하지 않습니다                  | 403 Forbidden                       |
| NoSuchBucket                        | 지정한 버킷이 존재하지 않습니다                      | 404 Not Found                       |
| NoSuchUpload                        | 지정한 멀티파트 업로드가 존재하지 않습니다                        | 404 Not Found                       |
| NoSuchBucket                        | 지정한 버킷 정책이 존재하지 않습니다                    | 404 Not Found                       |
| MethodMotAllowed                    | 이 리소스는 해당 HTTP 방법을 지원하지 않습니다                     | 405 Method Not Allowed              |
| BucketAlreadyExists                 | CreateBucket이 지정한 BucketName은 이미 사용 중이기 때문에 새로운 BucketName을 선택하십시오               | 409 Conflict                        |
| BucketNotEmpty                      | DeleteBucket을 하기 전, 우선 파일과 완성되지 않은 멀티파트 업로드 태스크를 삭제하십시오                    | 409 Conflict                        |
| InvalidBucketState                  | 버킷 상태와 작업 요청이 충돌합니다. 예를 들어 다중 버전 관리와 지역 간 복사의 충돌                  | 409 Conflict                        |
| OperationAborted                    | 지정 리소스는 이러한 유형의 작업을 지원하지 않거나 파일 전송이 훼손되어 완전하지 않은 경우, 다운로드 시 해당 오류 코드를 보고합니다          | 409 Conflict   |
| MissingContentLength                | 헤더 Content-Length가 없습니다           | 411 Length Required                 |
| PreconditionFailed                  | 사전 조건 매칭 실패                          | 412 Precondition                    |
| InvalidRange                        | 요청 파일 범위가 잘못되었습니다                        | 416 Requested Range Not Satisfiable |



**5XX 유형 오류**

| 오류 코드                | 설명               | HTTP 상태 코드                 |
| ------------------ | ---------------- | ----------------------- |
| InternalErrror     | 서버 내부 오류          | 500 Internal Server     |
| NotImplemented     | 헤더에 처리할 수 없는 방법이 존재합니다 | 501 Not Implemented     |
| ServiceUnavailable | 서버 내부 오류, 다시 시도하십시오   | 503 Service Unavailable |
| SlowDown           | 접근 빈도를 낮추십시오          | 503 Slow Down           |

**기타 유형 오류**

| 오류 코드                     | 설명         | HTTP 상태 코드 |
| ----------------------- | ---------- | ------- |
| InvaildAddressingHeader | 익명 캐릭터를 사용하여 접근해야 합니다 | N/A     |
