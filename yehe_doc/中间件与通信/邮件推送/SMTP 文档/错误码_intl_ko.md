## 입력 매개변수
| 필드                        | 설명        | 비고                                                                                                                               |
| ------------------------- | --------- | -------------------------------------------------------------------------------------------------------------------------------- |
| Bcc                       | 블라인드 카본 카피 주소      | 현재 미지원                                                                                                                            |
| Cc                        | 주소 복사      | 현재 미지원                                                                                                                            |
| Content-Transfer-Encoding | 콘텐츠 전송 인코딩 방식 | 현재 미사용. 비워둘 수 있음. 첨부 파일을 제외한 콘텐츠는 암호화할 필요가 없음                                                                                                    |
| Content-Type              | 컨텐츠 유형     | 현재는 text/plain; charset=UTF-8,text/html; charset=UTF-8 multipart/mixed, multipart/related 및 multipart/alternative만 전달 가능. 그렇지 않으면 오류가 보고됨 |
| Date                      | 날짜와 시간     | 현재 미사용                                                                                                                           |
| Delivered-To              | 수신자 주소      | 현재 미사용                                                                                                                           |
| From                      | 발신자 주소     | 필수                                                                                                                               |
| Message-ID                | 메시지 ID     | 현재 미사용                                                                                                                           |
| MIME-Version              | MIME 버전   | 현재 미사용. 비워 두거나 1.0 전달. 그렇지 않으면 오류가 보고됨                                                                                                            |
| Received                  | 전송 경로      | 현재 미사용                                                                                                                           |
| Reply-To                  | 회신 주소      | 현재 미사용                                                                                                                           |
| Return-Path               | 회신 주소      | 현재 미사용                                                                                                                           |
| Subject                   | 주제        | 필수                                                                                                                               |
| To                        | 수신자 주소     | 필수                                                                                                                               |

### 첨부 파일 매개변수(첨부 파일 전송 시)
| 필드                        | 설명        | 비고                             |
| ------------------------- | --------- | ------------------------------ |
| Content-Type              | 컨텐츠 유형     | 파일에 대해 application/octet-stream 전달 권장  |
| Content-Transfer-Encoding | 콘텐츠 전송 인코딩 방식 | 현재 Base64만 지원되며 다른 값을 전달하면 오류 보고됨           |
| Content-Disposition       | 콘텐츠 배치 방법   | 현재는 첨부파일만 전달할 수 있으며, 다른 값을 전달하면 첨부파일을 보낼 수 없음 |
| Content-ID                | 콘텐츠 ID    | 현재 미지원                          |
| Content-Location          | 콘텐츠 위치(경로) | 현재 미지원                          |
| Content-Base              | 콘텐츠 기반 위치    | 현재 미지원                          |

>?입력 매개변수 검증 요구 사항은 일반적으로 [SendEmail](https://intl.cloud.tencent.com/document/product/1084/39408)과 동일하며 수신자 수, 이메일 본문 크기, 첨부 파일 형식, 첨부 파일 크기 제한이 있습니다.

## 응답 매개변수
SMTP API에는 응답 매개변수가 없으며 err 정보 반환만 지원합니다. nil이 반환되면 API 호출이 성공했음을 나타내지만 실제 이메일 전송이 반드시 성공하지 않았을 수 있습니다. 전송 상태를 확인하려면 [GetSendEmailStatus](https://intl.cloud.tencent.com/document/product/1084/39502)를 참고하십시오

## 오류 코드
### 시스템 오류
1. 이메일 body의 한 줄에 2000자 이상의 문자가 있습니다.
`554 5.0.0 Error: transaction failed, blame it on the weather: smtp: too longer line in input stream` 또는 `too longer`이 포함된 로그.
`write tcp *.*.*.*:60575->*.*.*.*:25: write: broken pipe`

2. 첨부 파일이 너무 큽니다.
첨부 파일의 크기가 약 9M인 경우 EOF가 반환됩니다. 총 첨부 파일 크기를 8M 미만으로 유지하고 총 메시지 크기를 10M 미만으로 유지하는 것이 좋습니다. 그렇지 않으면 콘텐츠가 잘리고 Base64 디코딩 실패와 같은 기타 예외 오류가 보고됩니다.
				
### 비즈니스 오류
비즈니스 오류의 형식은 다음과 같습니다.
`
554 5.0.0 Error: transaction failed, blame it on the weather: ##SES-response-json: {"Response":{"RequestId":"bee4e9fb-8127-48cc-b606-bbb1e801596b","QcloudError":{"Error":{"Code":"FailedOperation.MissingEmailContent.작업 실패. 이메일 내용 누락(TemplateData 및 Simple 둘 다 비어 있을 수 없음).
`
 `##SES-response-json:` 이후는 보내는 API에서 반환한 구조의 `json` 형식입니다. 필드는 다음과 같습니다.

| 필드          | 유형   | 설명    |
| ----------- | ------ | ----- |
| RequestId   | string | 요청 LD  | 
| QcloudError | stuct  | 오류 구조 | 

QcloudError:

| 필드          | 유형   | 설명    | 
| ----------- | ------ | ----- | 
| Code   | string | 에러 코드  | 
| Message | string  | 에러 메시지 | 



일반 비즈니스 오류 설명:

| 에러 코드                                | 오류 설명                                                               | 비고                                    |
| ---------------------------------- | ------------------------------------------------------------------ | ------------------------------------- |
| FailedOperation                    | msg.From is null                                                   | 발신자가 비어 있음                                 |
| FailedOperation                    | msg.Subject is null                                                | 제목이 비어 있음                                |
| FailedOperation                    | msg.Body is null                                                   | 메시지 본문이 비어 있음                                |
| FailedOperation                    | Content-Transfer-Encoding must in...                               | 입력 매개변수 설명에 대해 Content-Transfer-Encoding 매개변수 확인 |
| FailedOperation                    | Content-Type must in...                                            | 입력 매개변수 설명에 대해 Header의 Content-Type 매개변수 확인         |
| FailedOperation                    | Mime-Version must in...                                            | Header의 Mime-Version 매개변수를 입력 매개변수 설명과 비교하여 확인         |
| FailedOperation                    | The email is too large. Remove some content...                     | 첨부 파일 이외의 이메일 본문은 1M를 초과할 수 없음                     |
| FailedOperation                    | Incorrect attachment content. Make sure the base64 content is...   | 첨부 콘텐츠는 Base64로 인코딩되어야 함                       |
| FailedOperation                    | The attachments are too large. Make sure they do not exceed the... | 단일 첨부 파일의 크기가 5M를 초과하거나 모든 첨부 파일의 총 크기 10M 초과(조정 가능)      |
| RequestLimitExceeded.SmtpRateLimit | smtp sending frequency limit...                                    | SMTP 호출 속도 제한 도달                          |

### 기타 비즈니스 오류
[SendEmail](https://intl.cloud.tencent.com/document/product/1084/39408)에서 오류 코드에 대한 설명을 참고할 수 있습니다.
