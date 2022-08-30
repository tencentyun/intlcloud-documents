### 그룹 채팅에서 그룹 구성원을 음소거 또는 음소거 해제하려면 어떻게 합니까?
음소거는 그룹 구성원의 메시지 발송을 제어하는 방법입니다. 음소거된 구성원은 음소거된 기간 동안 메시지를 보낼 수 없습니다. 구성원 음소거 방법에 대한 자세한 내용은 다음 SDK 문서를 참고하십시오.
- [그룹 구성원 음소거(Android)](https://intl.cloud.tencent.com/document/product/1047/48466)
- [그룹 구성원 음소거(iOS)](https://intl.cloud.tencent.com/document/product/1047/48181)
- [그룹 구성원 음소거(Web)](https://intl.cloud.tencent.com/document/product/1047/48180)


또한, 앱 관리자는 REST API를 통해 모든 그룹의 구성원을 음소거할 수 있습니다. 자세한 내용은 [REST API: 일괄 음소거 및 음소거 해제](https://intl.cloud.tencent.com/document/product/1047/34951)를 참고하십시오.


### 음소거된 구성원과 음소거 기간은 어떻게 조회합니까?
그룹 관리자와 그룹 소유자는 IM SDK에서 제공하는 API를 통해 구성원을 음소거하거나 음소거를 해제할 수 있습니다. (구성원 음소거를 해제하려면 음소거 시간을 0으로 설정합니다.)
구성원 음소거 관련 정보를 조회하려면, 그룹 구성원 프로필 정보를 조회합니다. 자세한 내용은 다음 SDK 문서를 참고하십시오.
- [그룹 구성원 프로필 가져오기(Android)](https://intl.cloud.tencent.com/document/product/1047/48178)
- [그룹 구성원 프로필 가져오기(iOS)](https://intl.cloud.tencent.com/document/product/1047/48178)
- [그룹 구성원 목록 가져오기(Web)](https://intl.cloud.tencent.com/document/product/1047/48180)

또한 앱 관리자는 REST API를 통해 구성원 음소거 정보를 쿼리할 수 있습니다. 자세한 내용은 [REST API: 음소거된 구성원 목록 가져오기](https://intl.cloud.tencent.com/document/product/1047/34964)를 참고하십시오.

### 그룹 참여 전의 그룹 로밍 메시지를 보려면 어떻게 합니까?

그룹 참여 전의 그룹 로밍 메시지 기록을 보려면, 이 그룹 유형에 대한 메시지 기록이 클라우드 스토리지를 지원해야 합니다. 그룹 유형 및 시나리오에 따라 다음 설정이 적용됩니다.
- **라이브 방송 그룹(AVChatRoom)** 및 이전 버전의 **온라인 방송 채팅방(BChatRoom)**은  메시지 기록 저장이 지원되지 않습니다. 따라서 이 두 가지 유형의 그룹은 참여 전의 로밍 메시지를 볼 수 없습니다.
- 라이브 방송 그룹 외 그룹, 즉 **업무 그룹(Work)** 및 **공개 그룹(Public)**은 기본적으로 그룹 참여 전의 로밍 메시지 보기가 허용되지 않습니다. **회의 그룹(Meeting)** 및 **커뮤니티(Community)**, 그룹 구성원은 기본적으로 그룹에 참여하기 전의 로밍 메시지를 볼 수 있습니다. 기본 설정을 수정하려면 [**콘솔**](https://console.cloud.tencent.com/im) > **기능 설정>그룹 설정>그룹 메시지 설정**에서 수정하십시오.

라이브 방송 그룹 외 기타 그룹의 메시지 기록의 기본 저장 기간은 7일(플래그십 버전의 경우 30일)입니다. 이 기간을 연장하려면 [콘솔](https://console.cloud.tencent.com/im) >**기능 설정**에서 설정할 수 있습니다. 메시지 저장 기간 연장은 유료 부가 가치 서비스입니다. 과금 관련 자세한 내용은 [요금 안내](https://intl.cloud.tencent.com/document/product/1047/34350)를 참고하십시오.

### AVChatRoom과 Meeting(이전 버전의 ChatRoom)의 차이점은 무엇입니까?

이 두 가지 유형의 그룹은 서로 다른 시나리오에 맞게 설계되었습니다. Meeting는 중간 규모의 그룹(구성원 6,000명 미만)에 적합합니다. AVChatRoom은 인원 제한이 없는 대규모 라이브 방송 시나리오에 적합합니다. 주요 차이점은 다음 표와 같습니다.

| 그룹 기능                  | Meeting                                | AVChatRoom            |
| ------------------------- | --------------------------------------- | --------------------- |
| 그룹 인원 제한                | 6000명                                 | 무제한                |
| 그룹 구성원 정보                | 모든 그룹 구성원 정보 저장                      | 구성원 정보 저장 안함 |
| 그룹 소유자의 그룹 관리자 설정  | 지원                                    | 미지원                |
| 그룹 구성원 삭제                | 그룹 관리자, 그룹 소유자, App 관리자는 그룹 구성원 삭제 지원 | 미지원                |
| 메시지 로밍          | 지원                                    | 미지원                |
| 그룹 가입 전 메시지 기록 보기    | 메시지 기록 저장 기간 내 메시지 보기 지원(기본값)          | 미지원                |
| 구성원 변경 알림      | 미지원                                  | 지원                  |
| App 관리자의 그룹 가져오기 | 지원                                    | 미지원                |

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
   
   
 ### 라이브 방송 그룹의 접속자 수는 어떻게 획득하나요?
AVChatRoom의 접속자 수는 ([Android](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a56840105a4b3371eeab2046d8c300bce
), [iOS](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#ada2eadb44f6865e9848df94fb5bae4ae), [Web](https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#getGroupOnlineMemberCount), [Flutter](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_group_manager/V2TIMGroupManager/getGroupOnlineMemberCount.html)) 또는 [REST API](https://intl.cloud.tencent.com/document/product/1047/38521) 인터페이스를 통해 획득할 수 있습니다.

### 그룹 메시지 제한은 40개/초입니다. 관련 안내가 없습니다. 40개/초 제한을 초과했는지 여부를 어떻게 판단할 수 있습니까?
빈도 제어 초과 후, 기본적으로 빈도 제한 오류 코드는 호출측에게 반환되지 않습니다. 호출측에 오류 코드([10023](https://intl.cloud.tencent.com/document/product/1047/34348))를 반환되게 하려면, 플랫폼에 [구성 변경 요청 티켓](https://intl.cloud.tencent.com/document/product/1047/44322)을 제출하십시오.
