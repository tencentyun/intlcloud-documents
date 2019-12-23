## 기능 설명

반환된 결과의 오류 코드는 사용자가 Cloud API를 호출한 결과를 나타냅니다.

- 코드는 모든 모듈의 API에 적용될 수 있는 공통 오류 코드입니다. 코드가 0이면 호출이 성공하고 그렇지 않으면 호출 실패함을 나타납니다. 호출이 실패하면 사용자는 공통 오류 코드 리스트에 따라 오류 원인을 확인하고 해당 조치를 취할 수 있습니다.
- codeDesc는 모듈과 관련된 오류를 나타내는 모듈 오류 코드입니다. 호출이 실패하면 사용자는 모듈 오류 코드 리스트에 따라 오류 원인을 확인하고 해당 조치를 취할 수 있습니다.

## 오류 코드 리스트

### 공통 오류 코드

| 오류 코드 | 오류 유형     | 조치                                                     |
| -------- | ------------ | ------------------------------------------------------------ |
| 4000     | 잘못된 요청 매개변수 | 필수 매개변수가 누락되었거나 매개변수 값의 포맷이 올바르지 않습니다. 구체적인 오류 정보는 오류 설명 message 필드를 참조하십시오. |
| 4100     | 인증 실패     | 서명 인증에 실패했습니다.                                               |
| 4200     | 요청 만료     | 요청이 만료되었습니다.                                               |
| 4300     | 접근 거부     | 계정이 블록되었거나 API 대상 사용자의 범위 내에 있지 않습니다.                 |
| 4400     | 할당량 초과     | 요청 수가 할당량 한도를 초과하는 경우 [티켓 제출](https://console.cloud.tencent.com/workorder/category)하여 고객 서비스에 문의하십시오.           |
| 4500     | 재전송 공격     | 요청된 Nonce 및 Timestamp 매개변수는 각 요청이 서버 측에서 한 번만 실행되도록 보장하는 데 사용되므로 이번의 Nonce는 지난번의 것과 중복될 수 없으며 Timestamp는 Tencent 서버와 2시간 이상 차이나면 안 됩니다. |
| 4600     | 지원되지 않은 프로토콜   | 프로토콜이 지원되지 않습니다.                                                 |
| 5100     | 자격 증명 생성 오류 | API가 자격 증명을 생성할 때 오류가 발생하고 백 엔드 서비스 오류에 속합니다.                         |

### 모듈 오류 코드

| 오류 코드 | 모듈 오류 코드(codeDesc)                                        | 설명                                                         | 조치                                                 |
| ---- | ----------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 4000 | InvalidParameter.policyName.InUse               | 전략 이름이 이미 존재하므로 CAM은 동일한 계정의 전략 이름이 중복될 수 없도록 요구합니다           | 새로운 전략 이름을 사용하십시오                                             |
| 4000 | InvalidParameter                                | 잘못된 입력 매개변수                                                     | 반환된 오류 메시지를 참조하여 해당 매개변수를 확인하십시오                   |
| 5100 | InternalError                                   | 내부 시스템 오류                                                 |       -                                                       |
| 4000 | InvalidParameter.AttachmentFull                 | 사용자/사용자 그룹/역할에 바인딩된 전략 수가 상한에 도달했으며 하나의 사용자/사용자 그룹/역할에 연결될 수 있는 최대 전략 수가 200입니다. 계속 바인딩하면 실패할 것입니다 | 이전 전략을 언바인딩하십시오                                               |
| 4000 | InvalidParameter.principal.Error                | 전략 구문의 principal 필드 오류                                | 문서의 [principal](https://intl.cloud.tencent.com/document/product/598/10603#8..E7.AD.96.E7.95.A5.E6.A0.B7.E4.BE.8B) 필드에 대한 설명을 참조하십시오 |
| 4000 | InvalidParameter.action.Error                   | 전략 구문의 action 필드 오류                                   | 문서의 [action](https://intl.cloud.tencent.com/document/product/598/10603#8..E7.AD.96.E7.95.A5.E6.A0.B7.E4.BE.8B) 필드에 대한 설명을 참조하십시오 |
| 4000 | InvalidParameter.effect.Error                   | 전략 구문의 effect 필드 오류                                   | 문서의 effect 필드에 대한 설명을 참조하십시오                               |
| 4000 | MissingParameter.action                   | 전략 구문에 action 필드가 없습니다                                   | 전략 구문에 [action](https://intl.cloud.tencent.com/document/product/598/10603#8..E7.AD.96.E7.95.A5.E6.A0.B7.E4.BE.8B) 필드를 추가하십시오 |
| 4000 | InvalidParameter.policyName.TypeError           | 전략 이름 유형이 잘못되었습니다. 전략 이름은 문자열이어야 합니다                           | 전략 이름을 문자열로 수정하십시오                                   |
| 4000 | InvalidParameter.policyName.Error               | 전략 이름에 잘못된 문자가 있거나 길이가 한도를 초과합니다. 전략 이름의 최대 길이는 128바이트이며 전략 이름 문자는 문자, 숫자 또는 특수 문자 `+=,.@_-`만 가능합니다 | 설명에 따라 전략 내용을 조정하십시오                                       |
| 4000 | InvalidParameter.policyDocument.TypeError       | 전략 구문 유형 오류                                             | 전략 이름을 문자열로 수정하십시오                                   |
| 4000 | MissingParameter.version                        | 전략 구문에 version 필드가 없습니다                                    | [version](https://intl.cloud.tencent.com/document/product/598/10603#8..E7.AD.96.E7.95.A5.E6.A0.B7.E4.BE.8B) 매개변수를 입력하십시오 |
| 4000 | InvalidParameter.version.Error                  | 전략 구문 version 필드 오류                                    | 전략 구문의 [version](https://intl.cloud.tencent.com/document/product/598/10603#8..E7.AD.96.E7.95.A5.E6.A0.B7.E4.BE.8B) 포맷이 올바른지 확인하십시오 |
| 4000 | MissingParameter.statement                      | 전략 구문에 statement 필드가 없습니다                                  | [statement](https://intl.cloud.tencent.com/document/product/598/10603#8..E7.AD.96.E7.95.A5.E6.A0.B7.E4.BE.8B) 매개변수를 입력하십시오 |
| 4000 | InvalidParameter.statement.Error                | 전략 구문 statement 필드 오류                                  | 전략 구문의 [statement](https://intl.cloud.tencent.com/document/product/598/10603#8..E7.AD.96.E7.95.A5.E6.A0.B7.E4.BE.8B) 포맷이 올바른지 확인하십시오 |
| 4000 | InvalidParameter.policyDocument.LengthOverlimit | 전략 구문 길이가 제한을 초과하고 한도가 4096바이트입니다                   | 전략 설명의 길이를 줄이십시오. 전략 내용이 너무 많으면 여러 전략으로 나눌 수 있습니다           |
| 4000 | InvalidParameter.condition.Error                | 전략 구문 condition 필드 오류                                  | 전략 구문의 [condition](https://intl.cloud.tencent.com/document/product/598/10603#8..E7.AD.96.E7.95.A5.E6.A0.B7.E4.BE.8B)이 올바른지 확인하십시오 |
| 4000 | MissingParameter.resource                       | 전략 구문에 resource 필드가 없습니다                                   | [resource](https://intl.cloud.tencent.com/document/product/598/10603#8..E7.AD.96.E7.95.A5.E6.A0.B7.E4.BE.8B) 매개변수를 입력하십시오 |
| 4000 | InvalidParameter.resource.Error                 | 전략 구문 resource 필드 오류                                   | 전략 구문의 [resource](https://intl.cloud.tencent.com/document/product/598/10603#8..E7.AD.96.E7.95.A5.E6.A0.B7.E4.BE.8B) 포맷이 올바른지 확인하십시오 |
| 4000 | InvalidParameter.resource.user.Error            | 전략 구문의 resource는 자체 계정의 리소스가 아닙니다                       | 전략 구문의 [resource](https://intl.cloud.tencent.com/document/product/598/10603#8..E7.AD.96.E7.95.A5.E6.A0.B7.E4.BE.8B) 소유자를 현재 기본 계정으로 입력하십시오 |
| 4000 | InvalidParameter.description.LengthOverlimit    | 전략 설명 길이가 한도를 초과하고 한도가 300바이트입니다                    | 전략 설명의 길이를 줄이십시오                                           |
| 4000 | MissingParameter.policyName                     | 입력 매개변수 policyName이 없습니다                                         | policyName 매개변수를 입력하십시오                                       |
| 4000 | MissingParameter.policyDocument                 | 입력 매개변수 policyDocument가 없습니다                                     | policyDocument 매개변수를 입력하십시오                                   |
| 4000 | InvalidParameter.description.TypeError          | 전략 설명 유형이 잘못되었습니다. 전략 설명은 문자열이어야 합니다                       | 전략 설명 유형을 확인하십시오                                           |
| 4000 | InvalidParameter.policyId.NotExist              | 전략 ID가 없습니다                                               | 올바른 전략 ID를 사용하십시오                                          |
| 4000 | MissingParameter.policyId                       | 입력 매개변수 policyId가 없습니다                                           | policyId 매개변수를 입력하십시오                                         |
| 4000 | InvalidParameter.policyId.TypeError             | 전략 ID 유형이 잘못되었습니다. 전략 ID는 숫자여야 합니다                         | 전략 ID 유형을 확인하십시오                                           |
| 4000 | InvalidParameter.policyFull                     | 이 계정이 소유한 전략 수가 상한에 도달했습니다. 상한은 1000입니다                     | 더 이상 사용하지 않은 전략을 삭제하십시오                                             |
| 4000 | InvalidParameter.user.NotExist                  | 사용자가 존재하지 않거나 전략 구문 principal 필드의 사용자가 존재하지 않습니다            | 해당 사용자가 존재하는지 확인하십시오                                     |
| 4000 | InvalidParameter.group.NotExist                 | 사용자 그룹이 존재하지 않거나 전략 구문 principal 필드의 사용자 그룹이 존재하지 않습니다        | 해당 사용자 그룹이 존재하는지 확인하십시오                                   |
| 4000 | InvalidParameter.role.NotExist                  | 역할이 존재하지 않습니다                                                   | 해당 역할을 생성하십시오                                             |
| 4000 | InvalidParameter.roleName.TypeError             | 역할 이름 유형이 잘못되었습니다. 역할 이름은 문자열이어야 합니다                           | 설명에 따라 역할 이름 유형이 유효한지 확인하십시오                             |
| 4000 | InvalidParameter.roleName.Error                 | 역할 이름에 잘못된 문자가 있거나 길이가 한도를 초과합니다. 역할 이름의 최대 길이는 128바이트이며 전략 이름 문자는 문자, 숫자 또는 `+=,.@_-`만 가능합니다 | 설명에 따라 역할 이름이 유효힌지 확인하십시오                                 |
| 4000 | InvalidParameter.roleFull                       | 이 계정이 소유한 역할 수가 상한에 도달했습니다. 하나의 계정은 최대 250개의 역할을 가질 수 있습니다      | 더 이상 사용하지 않은 역할을 삭제하십시오                                             |
| 4000 | InvalidParameter.roleName.InUse                 | 역할 이름이 이미 존재합니다. 동일한 계정의 역할 이름이 중복될 수 없습니다                     | 새로운 역할 이름을 사용하거나 같은 이름의 기존 역할을 삭제하십시오                       |
| 4000 | CanNotGetOwnerUin                               | 사용자 OwnerUin을 획득할 수 없습니다                                        | 계정이 올바른지 확인하십시오                                           |
| 4000 | GetAppIdError                                   | 사용자 AppId를 획득할 수 없습니다                                           | 계정이 올바른지 확인하십시오                                           |
| 4000 | SetTimeOutOfTime                                | 사용자가 설정한 임시 자격 증명의 유효 기간이 최대 시간 제한을 초과했습니다                           | 구체적인 API의 매개변수 설명을 참조하십시오                                     |
| 4000 | StrategyInvalid                                 | 페더레이션 ID에 대한 임시 인증서를 획득 시 설정한 전략 정보가 잘못되었습니다                         | 메시지 정보를 참조하십시오                                          |
