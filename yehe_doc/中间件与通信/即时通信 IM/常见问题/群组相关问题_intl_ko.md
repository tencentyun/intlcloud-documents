### 그룹 채팅에서 그룹 구성원을 음소거 또는 음소거 해제하려면 어떻게 합니까?
음소거는 그룹 구성원의 메시지 발송을 제어하는 방법입니다. 음소거된 구성원은 음소거된 기간 동안 메시지를 보낼 수 없습니다. 구성원 음소거 방법에 대한 자세한 내용은 다음 SDK 문서를 참고하십시오.
- [그룹 구성원 음소거(Android)](https://intl.cloud.tencent.com/document/product/1047/36271)
- [그룹 구성원 음소거(iOS)](https://intl.cloud.tencent.com/document/product/1047/36257)
- [그룹 구성원 음소거(Web)](https://intl.cloud.tencent.com/document/product/1047/34330)


또한, 앱 관리자는 REST API를 통해 모든 그룹의 구성원을 음소거할 수 있습니다. 자세한 내용은 [RES API: 일괄 음소거 및 음소거 해제](https://intl.cloud.tencent.com/document/product/1047/34951)를 참고하십시오.


### 음소거된 구성원과 음소거 기간은 어떻게 조회합니까?
그룹 관리자와 그룹 소유자는 IM SDK에서 제공하는 API를 통해 구성원을 음소거하거나 음소거를 해제할 수 있습니다. (구성원 음소거를 해제하려면 음소거 시간을 0으로 설정합니다.)
구성원 음소거 관련 정보를 조회하려면, 그룹 구성원 프로필 정보를 조회합니다. 자세한 내용은 다음 SDK 문서를 참고하십시오.
- [그룹에서 자신의 프로필 정보 가져오기(Android)](https://intl.cloud.tencent.com/document/product/1047/36271)
- [그룹에서 자신의 프로필 정보 가져오기(iOS)](https://intl.cloud.tencent.com/document/product/1047/36257)
- [그룹 구성원 목록 가져오기(Web)](https://intl.cloud.tencent.com/document/product/1047/34330)

또한 앱 관리자는 REST API를 통해 구성원 음소거 정보를 쿼리할 수 있습니다. 자세한 내용은 [REST API: 음소거된 구성원 목록 가져오기](https://intl.cloud.tencent.com/document/product/1047/34964)를 참고하십시오.

### 그룹 참여 전 그룹 메시지를 보려면 어떻게 합니까?

그룹 참여 전의 그룹 메시지 기록을 보려면, 이 그룹 유형에 대한 메시지 기록이 클라우드 스토리지를 지원해야 합니다. 그룹 유형 및 시나리오에 따라 다음 설정이 적용됩니다.
- **라이브 방송 그룹(AVChatRoom)** 및 이전 버전의 **온라인 방송 채팅방(BChatRoom)**은  메시지 기록 저장이 지원되지 않습니다. 따라서 이 두 가지 유형의 그룹은 참여 전 메시지를 볼 수 없습니다.
- 라이브 방송 그룹 외 기타 그룹의 경우, **업무 그룹(Work)** 및 **공개 그룹(Public)**은 기본적으로 구성원이 그룹 참여 전 메시지 기록을 볼 수 있도록 허용하지 않는 반면, **회의 그룹(Meeting)**은 기본적으로 구성원이 메시지 기록을 볼 수 있도록 허용합니다. 이러한 기본 설정은 [티켓 제출](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=40&source=0&data_title=%E4%BA%91%E9%80%9A%E4%BF%A1%20%20IM&step=1)을 통해 변경 신청할 수 있습니다.

라이브 방송 그룹 외 기타 그룹의 메시지 기록의 기본 저장 기간은 7일(울티메이트 버전의 경우 30일)입니다. 이 기간을 연장하려면 [콘솔](https://console.cloud.tencent.com/im) > [기능 설정]에서 설정할 수 있습니다.메시지 저장 기간 연장은 유료 부가 가치 서비스입니다. 과금 관련 자세한 내용은 [요금 안내](https://intl.cloud.tencent.com/document/product/1047/34350)를 참고하십시오.

### AVChatRoom과 Meeting(이전 버전의 ChatRoom)의 차이점은 무엇입니까?

이 두 가지 유형의 그룹은 서로 다른 시나리오에 맞게 설계되었습니다. Meeting는 중간 규모의 그룹(구성원 6,000명 미만)에 적합합니다. AVChatRoom은 인원 제한이 없는 대규모 라이브 방송 시나리오에 적합합니다. 주요 차이점은 다음 표와 같습니다.

| 그룹 기능                      | Meeting                                                      | AVChatRoom                  |
| ------------------------------ | ------------------------------------------------------------ | --------------------------- |
| 그룹 인원 제한                 | 6000명                                                       | 무제한                      |
| 그룹 구성원 정보 저장          | 모든 구성원 정보                                             | 구성원 정보를 저장하지 않음 |
| 그룹 소유자의 그룹 관리자 설정 | 지원                                                         | 미지원                      |
| 그룹 구성원 삭제               | 그룹 관리자, 그룹 소유자, App 관리자는 그룹 구성원 삭제 지원 | 미지원                      |
| 메시지 로밍                    | 지원                                                         | 미지원                      |
| 그룹 가입 전 메시지 기록 보기  | 메시지 기록 저장 기간 내 메시지 보기 지원(기본값)            | 미지원                      |
| 구성원 변경 알림               | 미지원                                                       | 지원                        |
| App 관리자의 그룹 가져오기     | 지원                                                         | 미지원                      |

### 그룹/그룹 구성원 레벨의 사용자 정의 필드의 값을 가져올 수 없는 이유는 무엇입니까?

다음 방법으로 문제를 진단합니다.
1. 콘솔에서 사용자 정의 필드가 올바르게 구성되었는지 확인합니다.
2. 요청자에게 읽기 권한이 있고 그룹 유형이 사용자 정의 필드를 지원하는지 쿼리 요청에서 확인합니다.
3. 사용자 정의 필드의 구성 요청이 성공했는지 확인합니다.
4. 그룹 사용자 정의 필드의 경우:
   - iOS: IM SDK에 로그인하기 전에 TIMManager > setUserConfig > TIMUserConfig > TIMGroupInfoOption > groupCustom으로 이동하여 설정합니다.
   - Android: IM SDK에 로그인하기 전에 TIMManager > setUserConfig > TIMUserConfig > TIMGroupSettings > groupInfoOptions > setCustomTags로 이동하여 설정합니다.
5. 그룹 구성원 사용자 정의 필드의 경우:
   - iOS: IM SDK에 로그인하기 전에 TIMManager > setUserConfig > TIMUserConfig > TIMGroupMemberInfoOption > memberCustom으로 이동하여 설정합니다.
   - Android: IM SDK에 로그인하기 전에 TIMManager > setUserConfig > TIMUserConfig > TIMGroupSettings > memberInfoOptions > setCustomTags로 이동하여 설정합니다.
