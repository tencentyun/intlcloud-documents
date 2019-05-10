## 기능 설명

이 문서는 API 요청 오류 시 반환한 오류 코드와 해당 오류 정보를 소개합니다. HTTP StatusCode 및 Body를 기반으로 문제를 확인할 수 있습니다. 본문의 형식은 다음과 같습니다.
```
{
    "errorcode" : "<ErrorCode>",
    "errormessage" : "<ErrorMessage>"
}
```
## 오류 코드 리스트

| HTTP 상태 코드(StatusCode) | 오류 코드(ErrorCode)       | 설명(ErrorMessage)                |
| -------------------- | -------------------- | ------------------------------- |
| 400                  | InvalidAuthorization | 무효한 서명열 형식                        |
| 400                  | InvalidCompressType  | 지정된 x-cls-compress-type은 지원되지 않음       |
| 400                  | InvalidContent       | 메시지 본문 오류. 압축 해제 또는 구문 분석 실패                |
| 400                  | InvalidContentType   | 지정된 Content-Type은 지원되지 않음              |
| 400                  | InvalidParam         | 필수 매개변수가 누락되었거나 일부 매개변수가 무효함                 |
| 400                  | MissingAgentIp       | x-cls-agent-ip가 누락됨                |
| 400                  | MissingAgentVersion  | x-cls-agent-version이 누락됨.           |
| 400                  | MissingAuthorization | Authorization이 누락됨                 |
| 400                  | MissingContent       | 메시지 본문이 비어 있음                          |
| 400                  | MissingContentType   | Content-Type이 누락됨                  |
| 400                  | TopicClosed          | 지정된 로그 토픽에 대해 콜렉션 기능이 사용 불가능          |
| 400	               | IndexRuleEmpty	      | 지정된 로그 토픽에 인덱스 규칙을 설정하지 않음          |
| 400	               | LogsetNotEmpty       | 지정된 로그 집합이 비어 있지 않으며 로그 토픽이 포함됨            |
| 401                  | Unauthorized         | ID 오류, 반복적인 서명 사용 또는 서명 컴퓨팅 오류로 인해 인증에 실패함 |
| 403                  | LogsetExceed         | 로그 집합의 수가 한계를 초과함(최대 20개)                 |
| 403                  | LogSizeExceed        | 제출한 로그의 크기가 한계를 초과함(최대 5MB)               |
| 403                  | MachineGroupExceed   | 서버 그룹의 수가 한계를 초과함(최대 200개)        |
| 403                  | NotAllowed           | 해당 작업을 허용하지 않음                          |
| 403                  | TopicExceed          | 로그 토픽의 수가 한계를 초과함(최대 10개)                |
| 403                  | ShipperExceed        | 배달 규칙의 수가 한계를 초과함(최대 10개)        |
| 403                  | TaskReadOnly         | 실패한 배달 태스크만 다시 시작할 수 있으며 다른 상태일 경우 수정할 수 없음   |
| 404                  | CursorNotExist       | 지정된 위치에서 다운로드할 로그가 없음          |
| 404                  | TaskNotExist         | 지정된 배달 태스크가 존재하지 않음                      |
| 404                  | IndexNotExist        | 지정된 인덱스 규칙이 존재하지 않음                      |
| 404                  | LogsetNotExist       | 지정된 로그 집합이 존재하지 않음                       |
| 404                  | MachineGroupNotExist | 지정된 서버 그룹이 존재하지 않음                       |
| 404                  | ShipperNotExist      | 지정된 배달 규칙이 존재하지 않음                      |
| 404                  | TopicNotExist        | 지정된 로그 토픽이 존재하지 않음                      |
| 404                  | ConsumerNotExist     | 지정된 로그 토픽에 소비 태스크가 존재하지 않음              |
| 405                  | NotSupported         | 해당 작업을 허용하지 않음                          |
| 409                  | IndexConflict        | 같은 인덱스 규칙이 이미 존재함.                      |
| 409                  | LogsetConflict       | 같은 로그 집합이 이미 존재함                       |
| 409                  | MachineGroupConflict | 서버 그룹이 이미 존재함                       |
| 409                  | ShipperConflict      | 배달 규칙이 이미 존재함                      |
| 409                  | TopicConflict        | 같은 로그 토픽이 이미 존재함                      |
| 409                  | ConsumerConflict     | 로그 토픽에 대한 소비 태스크가 이미 존재함              |
| 500                  | InternalError        | 내부 오류                            |

