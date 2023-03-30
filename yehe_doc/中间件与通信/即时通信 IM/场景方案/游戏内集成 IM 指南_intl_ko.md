>- 인스턴트 메시징은 게임의 일반적인 요구 사항이며 인스턴트 채팅은 멀티플레이어 게임의 필수 기능이 되었습니다. 게임 플랫폼 자체에는 다양한 그룹 유형, 사용자 지정 메시지 유형(예: 게임 내 소품 선물 및 거래), 전역 액세스 및 기타 복잡한 요구 사항이 포함됩니다. 이 문서는 게임 내 채팅을 구축하는 과정에서 일반적인 요구 사항 구현 방법과 가능한 문제 및 고려 사항을 정리하여 개발자가 비즈니스를 빠르게 이해하고 요구 사항을 구현하도록 돕습니다.
>  ![](https://qcloudimg.tencent-cloud.cn/raw/41bda125b2276c6d70bfa8de480e8748.jfif)
>
>  ## 준비 작업
>
>  ### 키로 UserSig 계산하기
>
>  IM 계정 시스템에서 사용자 로그인에 필요한 암호는 IM에서 제공한 키를 사용하여 서버에서 계산합니다. 자세한 내용은 [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385)을 참고하십시오. 개발 단계에서 클라이언트의 개발 지연을 방지하기 위해 아래와 같이 [콘솔에서 UserSig 계산](https://console.cloud.tencent.com/im/tool-usersig)할 수도 있습니다.
>
>  ![](https://qcloudimg.tencent-cloud.cn/raw/3ebfcc9b831fac31ad9b8b722bb7dc50.png)
>
>  ### 관리자 계정 구성
>
>  게임 내 인스턴트 메시징을 관리하려면 관리자가 게임에 이메일 알림을 보내고 임시 팀 구성 메시지를 관리하는 등 [IM 서버 API](https://intl.cloud.tencent.com/document/product/1047/34621)를 통해 수행할 수 있습니다. 이러한 API를 호출하려면 [IM 관리자 계정 생성](https://console.cloud.tencent.com/im/account-management)이 필요합니다. 기본적으로 IM은 관리자의 사용자 ID가 있는 계정을 제공합니다. 필요에 따라 여러 관리자 계정을 만들 수도 있습니다. 최대 5개의 관리자 계정을 만들 수 있습니다.
>
>  ### 콜백 주소 구성 및 콜백 활성화
>
>  게임 내 팀 구성 및 기타 요구 사항을 구현하려면 특정 시나리오에서 IM 백엔드가 비즈니스 백엔드를 호출하는 콜백 이벤트를 사용합니다. 아래와 같이 HTTP API를 제공하고 [콘솔 > 콜백 구성](https://console.cloud.tencent.com/im/callback-setting) 모듈에서 구성하기만 하면 됩니다.
>
>  ![](https://qcloudimg.tencent-cloud.cn/raw/365705a8a72a1e15ec5259e164beeb06.png)
>
>  ### 클라이언트 SDK 통합
>
>  준비를 완료한 후 IM 클라이언트 SDK를 프로젝트에 통합해야 합니다. 필요에 따라 다른 통합 옵션을 선택할 수 있습니다. 자세한 지침은 [TUIKit 소개](https://intl.cloud.tencent.com/document/product/1047/34547)를 참고하십시오.
>
>  다음은 게임에 통합될 일반적인 IM 기능을 설명하고 구현 코드와 함께 모범 사례를 제공합니다.
>
>  ## 게임 채팅방 기능 개발 가이드
>
>  ### 사용자 프로필
>
>  #### 일반 사용자 프로필
>  게임 사업에 저장된 일반 사용자 프로필은 기본 정보 프로필과 기타 정보 프로필로 나눌 수 있습니다.
>
>  | 기본 정보                                          | 기타 정보               |
>  | -------------------------------------------------- | ----------------------- |
>  | 아이디, 성별, 생년월일, 등급, 역할, 휴대폰 번호 등 | 게임에 필요한 기타 정보 |
>
>  #### 프로필 저장
>  게임 비즈니스는 사용자가 많고 방대한 양의 사용자 데이터를 저장하기 어렵습니다. Tencent Cloud IM은 사용자 프로필 호스팅 기능을 통해 완벽한 프로필 솔루션 세트를 제공합니다. 다음은 사용자 프로필을 Tencent Cloud IM에 저장하는 것과 비즈니스 백그라운드에 저장하는 것을 비교한 것입니다.
>
>  | 아이템           | IM                                                           | 비즈니스 백그라운드                         |
>  | ---------------- | ------------------------------------------------------------ | ------------------------------------------- |
>  | 저장 용량        | 자동 스케일링 지원                                           | 제한되고 확장하기 어려운 용량               |
>  | 사용자 프로필    | 필드의 길이와 이름에 대한 제한이 있는 표준 및 사용자 정의 필드 제공 | 사용자 정의 가능, 더 유연함                 |
>  | 프로필 읽기/쓰기 | 사용하기 쉬운 서비스 API 및 가이드라인 제공                  | 자체 개발 필요                              |
>  | API              | API 호출 빈도: 초당 200회 이하                               | 필요에 따라 API 호출 및 기타 기능 개발 가능 |
>  | 보안성           | 원격 재해 복구 및 교차 리전 배포 지원                        | 자체 유지 보수 필요                         |
>
>  프로필 저장 및 읽기/쓰기 기능 외에도 IM에는 사용자 프로필 호스팅 서비스 덕분에 다음과 같은 이점이 있습니다.
>  1. IM은 원격 재해 복구, 리전 간 배포 및 오토스케일링 기능을 제공합니다. 이러한 방식으로 서버 다운타임, 다중 복사본 1차-2차 복제, 용량 스케일링과 같은 복잡한 처리 흐름을 손쉽게 해결할 수 있습니다.
>  2. IM은 업계에서 일반적으로 사용되는 비즈니스 처리 흐름을 제공하므로 사용자 프로필 비즈니스 로직에 대해 걱정할 필요가 없습니다.
>  3. IM은 전문적인 운영 프로세스와 팀을 제공하여 매년 99.99%의 서비스 품질을 보장하고 안정적인 서비스를 제공할 수 있도록 도와드립니다.
>  4. IM은 사용하기 쉬운 서비스 API와 액세스하기 쉬운 가이드라인을 제공하며 전체 프로세스에 걸쳐 프리미엄 서비스를 제공합니다.
>
>  #### IM 사용자 프로필 저장 방법
>  IM 저장 스키마에는 사용자 프로필 저장 및 읽기/쓰기 기능이 포함됩니다. 다음은 IM이 사용자 프로필, 친구 프로필 및 확장 데이터를 저장하는 방법을 설명합니다. 모든 데이터는 `Key-Value` 형식으로 저장됩니다. `Key`는 `String` 유형이며 영어 대문자와 소문자, 숫자 및 언더바만 지원합니다. `Value`는 다음 유형을 지원합니다.
>
>  | 유형        | 설명                                                         |
>  | ----------- | ------------------------------------------------------------ |
>  | uint64_t    | 정수(사용자 정의 필드에서 지원되지 않음)                     |
>  | string      | 문자열. 길이 500바이트 이하                                  |
>  | bytes       | buffer. 길이 500바이트 이하                                  |
>  | string 배열 | 문자열 배열. 각 문자열은 500바이트를 초과할 수 없으며 친구 목록의 Tag_SNS_IM_Group 필드에서만 사용 가능 |
>
>  - **사용자 프로필**: 사용자 프로필에는 표준 및 사용자 정의 필드가 포함됩니다. 사용자 정의 필드의 경우 아래 확장 데이터 부분을 참고하십시오. 현재 IM에서 지원하는 표준 필드는 [표준 프로필 정보 필드](https://intl.cloud.tencent.com/document/product/1047/33520)를 참고하십시오.
>  - **친구 프로필**: 친구 프로필에는 표준 및 사용자 지정 친구 필드가 포함됩니다. IM의 연락처 목록은 최대 3000명의 친구를 지원합니다. 표준 친구 필드는 다음과 같이 설명됩니다.
>  <table>
>  <thead>
>  <tr>
>  <th>필드 이름</th>
>  <th>유형</th>
>  <th>설명</th>
>  </tr>
>  </thead>
>  <tbody><tr>
>  <td>Tag_SNS_IM_Group</td>
>  <td>Array</td>
>  <td>친구 목록</td>
>  </tr>
>  <tr>
>  <td>Tag_SNS_IM_Remark</td>
>  <td>string</td>
>  <td>친구 비고</td>
>  </tr>
>  <tr>
>  <td>Tag_SNS_IM_AddSource</td>
>  <td>string</td>
>  <td>친구 신청 출처</td>
>  </tr>
>  <tr>
>  <td>Tag_SNS_IM_AddWording</td>
>  <td>string</td>
>  <td>친구 신청 내용</td>
>  </tr>
>  <tr>
>  <td>Tag_SNS_IM_AddTime</td>
>  <td>Integer</td>
>  <td>친구 요청의 타임스탬프</td>
>  </tr>
>  </tbody></table>
>  자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/1047/33521">표준 친구 필드</a>를 참고하십시오.
>  - **사용자 지정 프로필**: 사용자 지정 프로필 필드를 신청하려면 앱 관리자가 [IM 콘솔](https://console.cloud.tencent.com/im)에 로그인하여 > 애플리케이션 구성 > 기능 구성으로 이동할 수 있습니다. 신청을 제출한 후 5분 후에 사용자 지정 프로필 필드가 적용됩니다.
>   - 사용자 프로필 관리에 대한 자세한 내용은 [프로필 관리](https://intl.cloud.tencent.com/document/product/1047/33520)를 참고하십시오.
>   - 관계 체인 사용자 정의 프로필 관리에 대한 자세한 내용은 [사용자 정의 친구 필드](https://intl.cloud.tencent.com/document/product/1047/33521)를 참고하십시오.
>
>  #### IM 사용자 프로필 저장 제한
>  - **서비스 기능 제한**
>   - 데이터 저장: 각 string 또는 buffer는 500바이트를 초과할 수 없습니다.
>   - 사용자 정의 필드: 사용자 정의 필드의 키워드는 길이가 8바이트 이하인 영문자로 구성되어야 합니다. 사용자 정의 필드 값은 500바이트를 초과할 수 없습니다.
>   - 친구 관계망: 각 사용자는 최대 3000명의 친구를 가질 수 있습니다.
>  - **API 관련 제한**
>   - 계정 관리: 한 번에 최대 100개의 사용자 이름을 가져올 수 있으며 요청당 최대 500명의 사용자 상태를 쿼리할 수 있습니다.
>   - 기타 호출 빈도: 초당 최대 200회
>
>  사용 제한에 대한 자세한 내용은 [사용 제한](https://intl.cloud.tencent.com/document/product/236/7259)을 참고하십시오.
>
>  ### 이메일 시스템
>
>  이메일 시스템은 요즘 게임에서 거의 필수입니다. 이메일에는 문자 메시지뿐 아니라 게임 소품 및 보상과 같은 이메일 첨부 파일이 포함될 수 있습니다. 단일 사용자에게 이메일을 보내거나 이벤트 보상을 제공하기 위해 그룹 이메일로 보낼 수 있습니다. 다음은 이메일 수신 플레이어, 이메일 목록, 읽지 않은 이메일 수, 모든 회원에게 이메일 보내기, 이메일 유효 기간 등 다양한 측면에서 이메일 시스템의 기능을 구현하는 방법을 설명합니다.
>
>  #### 이메일 수신 및 전송
>
>  - **플레이어 이메일 수신**: 시스템 이메일이 성공적으로 전송되고 플레이어가 온라인 상태일 때 플레이어는 시스템 이메일을 제대로 수신할 수 있습니다. 플레이어는 이메일 대화의 메시지 목록을 가져와 기록 또는 최신 이메일을 얻을 수 있습니다. 또한 모든 유형의 새 메시지(텍스트, 사용자 지정 및 리치 미디어 메시지 포함)를 수신하기 위해 리스너를 추가하거나 삭제할 수 있습니다. Unity의 샘플 코드는 다음과 같습니다.
>  ```javascript
>  // 메시지 수신 이벤트 리스너 구성
>  TencentIMSDK.AddRecvNewMsgCallback((List<Message> messages, string user_data)=>{
>    foreach(Message message in messages)
>    {
>      foreach (Elem elem in message.message_elem_array)
>      {
>        // 다음 요소가 있습니다.
>        if (elem.elem_type == TIMElemType.kTIMElem_Text)
>        {
>           string text = elem.text_elem_content;
>        }
>      }
>    }
>  })
>  // `RecvNewMsgCallback` 콜백을 수신하여 메시지 수신
>  // 메시지 수신을 중지하려면 `RemoveRecvNewMsgCallback`을 호출하여 리스너를 제거합니다. 이 단계는 선택 사항이며 필요에 따라 수행할 수 있습니다.
>  ```
>  자세한 내용은 [Unity-Receiving a Message](https://intl.cloud.tencent.com/document/product/1047/48573)를 참고하십시오.
>  - **시스템 이메일 전송**: 시스템은 다음과 같이 설명된 다른 서버 API를 통해 사용자에게 시스템 이메일을 보낼 수 있습니다.
>  <table>
>  <thead>
>  <tr>
>  <th>API</th>
>  <th>특성</th>
>  <th>응용 시나리오</th>
>  </tr>
>  </thead>
>  <tbody><tr>
>  <td><a href="https://intl.cloud.tencent.com/document/product/1047/34919">Sending One-to-One Messages to One User</a></td>
>  <td>지정된 계정으로 메시지를 보냅니다. 수신자에게 표시되는 발신자는 관리자가 아니라 관리자가 지정한 계정입니다.</td>
>  <td>특정 사용자에게 메시지 전송(예: 사용자에게 게임 보상 메시지 전송)</td>
>  </tr>
>  <tr>
>  <td><a href="https://intl.cloud.tencent.com/document/product/1047/34920">Sending One-to-One Messages to Multiple Users</a></td>
>  <td>일대일 메시지는 한 번에 최대 500명의 사용자에게 보낼 수 있으며 최대 통화 빈도는 초당 200회입니다.</td>
>  <td>수신자 그룹을 만들지 않고도 특정 사용자에게 메시지를 보낼 수 있습니다. 받는 사람이 많으면 메시지를 일괄적으로 보내야 합니다.</td>
>  </tr>
>  <tr>
>  <td><a href="https://intl.cloud.tencent.com/document/product/1047/34959">Sending Ordinary Messages in a Group</a></td>
>  <td>그룹에 일반 메시지를 보낼 때 모든 수신자를 동일한 그룹에 추가해야 합니다.</td>
>  <td>다수의 사용자에게 일반 메시지 전송(community 그룹당 사용자 최대 10만명)</td>
>  </tr>
>  <tr>
>  <td><a href="https://intl.cloud.tencent.com/document/product/1047/37165">API for Pushing to All Users</a></td>
>  <td>App의 모든 사용자에게 메시지를 푸시합니다. 메시지 전송을 위한 사용자 태그 및 속성을 지정할 수 있습니다.</td>
>  <td>App의 모든 사용자 또는 캠페인 이메일과 같은 특정 특성 속성을 가진 다수의 사용자에게 메시지를 푸시합니다.</td>
>  </tr>
>  </tbody></table>
>  <dx-alert infotype="explain" title="">
>  ‘모든 사용자에게 푸시’는 플래그십 버전에서만 사용할 수 있습니다. 이를 사용하려면 [플래그십 버전 구매](https://www.tencentcloud.com/document/product/1047/34577) 후 [콘솔](https://console.cloud.tencent.com/im/login-message) > 기능 구성 > 로그인 및 메시지 > 모든 사용자에게 푸시를 선택하고 기능을 활성화해야 합니다.
>  </dx-alert>
>  다음은 그룹에서 일반 메시지를 보내기 위한 기본 요청의 예시입니다.
>
>  ```json
>  {
>      "GroupId": "@TGS#2C5SZEAEF",
>      "Random": 8912345, // 임의의 숫자입니다. 두 메시지의 임의의 숫자가 5분 이내에 동일하면 동일한 메시지로 간주됩니다.
>      "MsgBody": [ // element 배열로 구성된 메시지 본문입니다. 자세한 내용은 필드 설명을 참고하십시오.
>          {
>              "MsgType": "TIMTextElem", // 텍스트
>              "MsgContent": {
>              "Text": "red packet"
>              }
>          },
>          {
>              "MsgType": "TIMCustomElem", // 사용자 지정
>              "MsgContent": {
>              "Data": "message",
>              "Desc": "notification",
>              "Ext": "url",
>              "Sound":"dingdong.aiff"
>              }
>          }
>      ],
>  }
>  ```
>  `MsgBody`(메시지 본문)는 메시지 배열입니다. 보낼 텍스트 및 사용자 지정 메시지를 추가할 수 있습니다.
>
>  #### 이메일 목록
>
>  이메일 목록 기록 저장은 메시지 저장과 동일합니다. `C2C 메시지 기록 저장`과 `그룹 메시지 기록 저장`으로 구성됩니다. 그룹 채팅에는 최소 두 명의 사용자가 필요하므로 관리자가 지정한 계정과 저장을 위해 이메일을 받는 사용자를 포함하는 그룹을 만들 수 있습니다.
>
>  >? 무료 버전 및 프로 버전의 경우 저장 기간은 7일입니다. 플래그십 버전의 경우 저장 기간은 30일입니다. 프로 버전 및 플래그십 버전을 사용하면 저장 기간을 연장할 수 있습니다. [콘솔](https://console.cloud.tencent.com/im)에 로그인하여 관련 구성을 수정할 수 있습니다.
>  >메시지 기록 저장 기간을 연장하는 것은 유료 부가 서비스입니다. 청구에 대한 자세한 내용은 [부가 서비스 요금](https://www.tencentcloud.com/zh/document/product/1047/34350)을 참고하십시오.
>
>
>  네트워크가 정상이면 최신 클라우드 데이터를 가져옵니다. 비정상적인 경우 SDK는 로컬에 저장된 기록 메시지를 반환합니다. 페이징 풀링이 지원됩니다. 다음은 이전 이메일 목록을 풀링하기 위한 Unity 예시 코드입니다.
>  ```javascript
>  // 일대일 메시지 기록 풀링
>  // 첫 번째 풀링에 대해 msg_getmsglist_param_last_msg를 null로 설정
>  // msg_getmsglist_param_last_msg는 두 번째 풀링에 대해 반환된 메시지 목록의 마지막 메시지일 수 있습니다
>  var get_message_list_param = new MsgGetMsgListParam
>  {
>      msg_getmsglist_param_last_msg = LastMessage
>  };
>  TIMResult res = TencentIMSDK.MsgGetMsgList(conv_id, TIMConvType.kTIMConv_C2C, get_message_list_param, (int code, string desc, string user_data) => {
>  // 콜백 로직 프로세스
>  });
>  ```
>  메시지 기록을 가져오는 방법에 대한 자세한 내용은 [Historical Messages - Unity](https://intl.cloud.tencent.com/document/product/1047/48871)를 참고하십시오.
>
>  #### 읽지 않은 이메일 수
>
>  사용자-시스템 이메일의 기록은 채팅의 대화와 같습니다. Tencent Cloud IM은 사용자가 아직 메시지를 읽지 않았음을 사용자에게 상기시키는 읽지 않은 대화 개수 기능을 제공합니다. 사용자가 대화를 클릭하고 대화 목록으로 돌아가면 읽지 않은 메시지 수가 지워집니다. 다음은 Unity 예시 코드입니다.
>  ```javascript
>  // 읽지 않은 총 개수 가져오기
>  TIMResult res = TencentIMSDK.ConvGetTotalUnreadMessageCount((int code, string desc, GetTotalUnreadNumberResult unread, string user_data)=>{
>   // 비동기 로직 프로세스
>  });
>  
>  // 읽지 않은 개수 변경 알림
>  TencentIMSDK.SetConvTotalUnreadMessageCountChangedCallback((int total_unread_count, string user_data)=>{
>   // 콜백 로직 프로세스
>  });
>  
>  // 모든 대화의 읽지 않은 수 지우기
>  TIMResult res = TencentIMSDK.MsgMarkAllMessageAsRead((int code, string desc, string user_data)=>{
>   // 비동기 로직 프로세스
>  });
>  ```
>  자세한 내용은 [Unity - Total Unread Count of All the Conversations](https://intl.cloud.tencent.com/document/product/1047/48846)를 참고하십시오.
>
>  #### 모든 구성원에게 이메일 보내기
>  모든 구성원에게 이메일 보내기는 게임의 모든 플레이어에게 이메일 메시지를 보내는 것입니다. Tencent Cloud IM은 서버 측에서 `모든 구성원에게 푸시` 기능을 제공합니다. 다음은 예시 코드입니다.
>  ```
>  https://console.tim.qq.com/v4/all_member_push/im_push?usersig=xxx&identifier=admin&sdkappid=88888888&random=99999999&contenttype=json
>  ```
>  다음은 예시 요청입니다.
>  ```json
>  {
>      "From_Account": "admin",
>      "MsgRandom": 56512,
>      "MsgLifeTime": 120, // 120초(2분) 동안 오프라인 저장
>      "MsgBody": [
>          {
>          "MsgType": "TIMTextElem",
>          "MsgContent": {
>              "Text": "hi, beauty"
>              }
>          }
>      ]
>  }
>  ```
>
>  모든 구성원에게 메시지를 보내는 기능을 사용하면 일부 사용자가 온라인 상태가 아니더라도 지정된 오프라인 저장 기간 내에 메시지를 받을 수 있도록 오프라인 저장 기간을 설정할 수 있습니다. `MsgLifeTime`(단위: 초)을 구성하여 오프라인 저장 기간을 지정합니다. 최대 기간은 604800s(7일)입니다. 기본값은 0이며 메시지가 오프라인으로 저장되지 않음을 나타냅니다.
>
>  모든 사용자에게 푸시에 대한 자세한 내용은 [Pushing to All Users](https://intl.cloud.tencent.com/document/product/1047/37166)를 참고하십시오.
>
>  #### 이메일 유효 기간
>  기록 이메일의 저장 기간은 다음과 같습니다. 무료 버전 및 프로 버전의 경우 저장 기간은 7일입니다. 플래그십 버전의 경우 보관 기간은 30일입니다. 프로 버전 및 플래그십 버전을 사용하면 저장 기간을 연장할 수 있습니다. 기록 이메일 저장에 대한 자세한 내용은 [메시지 기록 저장 기간 설정](https://intl.cloud.tencent.com/document/product/1047/34419)을 참고하십시오.
>  또한 서버 측에서 메시지를 보낼 때 `MsgLifeTime`을 설정하여 메시지의 오프라인 저장 기간(최대 7일)을 지정할 수 있습니다. `MsgLifeTime`이 0이면 메시지가 온라인 사용자에게만 전송되고 오프라인에 저장되지 않음을 나타냅니다. 자세한 내용은 [서버 API](https://intl.cloud.tencent.com/document/product/1047/34919)를 참고하십시오.
>
>  ### 임시 팀 구성
>
>  일시적인 팀 구성은 온라인 멀티플레이어 게임에서 필수적입니다. 다음은 임시 팀 구성 시나리오와 배경 및 팀원이 팀 정보를 얻는 방법을 설명합니다.
>
>  [](id:Team_scene)
>  #### 팀 기반 시나리오
>
>  팀 기반 시나리오에는 팀 생성, 임시 팀 탈퇴, 팀 리더 되기, 다른 사람을 팀에 가입하도록 초대 및 팀 해산이 포함됩니다. 다음은 다양한 시나리오의 구현을 설명하는 몇 가지 코드 예시입니다.
>
>  - **게임 시작 전 팀 생성**: 첫 번째 플레이어가 게임에 입장하면 서버에서 자동으로 그룹을 생성하고 최대 그룹 구성원 수를 지정할 수 있습니다. 요청이 그룹 소유자 또는 그룹 구성원을 지정하는 경우 지정된 그룹 소유자 또는 그룹 구성원은 그룹이 생성될 때 그룹에 자동으로 추가됩니다. 다음은 예시 요청 URL입니다.
>  ```
>  https://console.tim.qq.com/v4/group_open_http_svc/create_group?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
>  ```
>  다음은 기본 요청 예시입니다.
>  ```json
>  {
>      "Owner_Account": "leckie", // 그룹 소유자의 UserId(선택 사항)
>      "Type": "Public", // 그룹 유형: Private/Public/ChatRoom/AVChatRoom/Community
>      "Name": "TestGroup", // 그룹 이름(필수)
>      "MaxMemberCount":5 // 최대 그룹 구성원 수(선택 사항)
>  }
>  ```
>  >? App은 최대 10만개의 그룹을 지원합니다. 추가 그룹의 경우 [요금 안내](https://intl.cloud.tencent.com/document/product/1047/34350)에 설명된 대로 특정 요금을 지불해야 합니다. 서버 측 그룹 생성에 대한 자세한 내용은 [Creating a Group](https://intl.cloud.tencent.com/document/product/1047/34895)을 참고하십시오.
>  - **그룹 구성원 추가**: 그룹 채팅이 생성된 후 새로운 플레이어가 게임에 입장하는 경우 기존 그룹에 새로운 플레이어를 추가해야 합니다. 다음은 예시 요청 URL입니다.
>  ```
>  https://console.tim.qq.com/v4/group_open_http_svc/add_group_member?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
>  ```
>  다음은 요청 샘플입니다.
>  ```json
>  {
>      "GroupId": "@TGS#2J4SZEAEL", // 구성원을 추가할 그룹(필수)
>      "MemberList": [ // 한 번에 최대 300명의 구성원 추가 가능
>          {
>              "Member_Account": "tommy" // 추가할 구성원의 ID(필수)
>          },
>          {
>              "Member_Account": "jared"
>      }]
>  }
>  ```
>  자세한 내용은 [Adding Group Members](https://intl.cloud.tencent.com/document/product/1047/34921)를 참고하십시오.
>  - **성공적인 팀업을 위한 콜백**: 그룹 생성 시 최대 그룹 구성원 수를 설정하면 그룹에 필요한 구성원 수가 모두 있어야 게임을 시작할 수 있습니다. `그룹이 가득 찬 후 콜백`을 수신하면 게임을 시작할 수 있습니다. 다음은 예시 요청 URL입니다.
>  ```
>  https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
>  ```
>  다음은 예시 요청입니다.
>  ```json
>  {
>      "CallbackCommand": "Group.CallbackAfterGroupFull", // 콜백 명령
>      "GroupId": "@TGS#2J4SZEAEL" // 그룹 ID
>  }
>  ```
>  자세한 내용은 [그룹 만원 후 콜백](https://intl.cloud.tencent.com/document/product/1047/34376)을 참고하십시오.
>  - **그룹 가입 신규 구성원 알림**: 신규 플레이어가 게임(그룹 채팅)에 입장하면 `사용자가 그룹에 가입한 후 콜백`를 시스템에서 전송하여 다른 그룹 회원에게 알립니다. 다음은 예시 요청 URL입니다.
>  ```
>  https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
>  ```
>  다음은 예시 요청입니다.
>  ```json
>  {
>      "CallbackCommand": "Group.CallbackAfterNewMemberJoin", // 콜백 명령
>      "GroupId" : "@TGS#2J4SZEAEL",
>      "Type": "Public", // 그룹 유형
>      "JoinType": "Apply", // 그룹 가입 방법: Apply(신청); Invited(초대)
>      "Operator_Account": "leckie", // 운영자
>      "NewMemberList": [ // 새 구성원 목록
>          {
>              "Member_Account": "jared"
>          },
>          {
>              "Member_Account": "tommy
>          }
>      ]
>  }
>  ```
>  >? 이 콜백을 활성화하려면 콜백 URL을 구성하고 해당 프로토콜을 토글해야 합니다. 구성 방법에 대한 자세한 내용은 [서드파티 콜백 설정](https://intl.cloud.tencent.com/document/product/1047/34520)을 참고하십시오. 자세한 내용은 [After a User Joins a Group](https://intl.cloud.tencent.com/document/product/1047/34372)을 참고하십시오.
>  >
>  - **게임 중 팀 탈퇴**: 플레이어가 자발적으로 게임을 떠나거나 네트워크 문제로 인해 게임을 떠나는 경우, 서버는 `사용자가 그룹을 탈퇴한 후 콜백`을 통해 누군가가 그룹 채팅에서 탈퇴했음을 그룹의 다른 플레이어에게 알릴 수 있으며, 네트워크 문제로 인해 게임을 탈퇴한 플레이어에게 메시지를 보낼 수도 있습니다. 다음은 [After a User Leaves a Group](https://intl.cloud.tencent.com/document/product/1047/34373)의 요청 URL 예시입니다.
>  ```
>  https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
>  ```
>  다음은 예시 요청입니다.
>  ```json
>  {
>      "CallbackCommand": "Group.CallbackAfterMemberExit", // 콜백 명령
>      "GroupId": "@TGS#2J4SZEAEL", // 그룹 ID
>      "Type": "Public", // 그룹 유형
>      "ExitType": "Kicked", // 구성원 이탈 유형: Kicked-퇴장 당함; Quit-자발적 퇴장
>      "Operator_Account": "leckie", // 운영자
>      "ExitMemberList": [ // 그룹을 탈퇴한 구성원 목록
>          {
>              "Member_Account": "jared"
>          },
>          {
>              "Member_Account": "tommy"
>          }
>      ]
>  }
>  ```
>  - **게임 종료 후 단체 채팅 해산**: 게임 종료 후 서버 측에서 직접 단체 대화를 해산할 수 있습니다. 다음은 [Disbanding a Group](https://intl.cloud.tencent.com/document/product/1047/34896)에 대한 요청 URL 예시입니다.
>  ```
>  https://console.tim.qq.com/v4/group_open_http_svc/destroy_group?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
>  ```
>  다음은 예시 요청입니다.
>  ```json
>  {
>      "GroupId": "@TGS#2J4SZEAEL"
>  }
>  ```
>  임시 팀의 오디오/비디오 채팅은 복잡하며 아래에서 자세히 설명합니다.
>
>  #### 백그라운드에서 팀 정보 가져오기
>
>  - **그룹 세부 정보 가져오기**: 서버 API `그룹 프로필 가져오기`를 호출하여 그룹의 구성원 수 및 그룹 구성원의 기본 정보와 같은 그룹 세부 정보를 가져올 수 있습니다. 요청에서 Filter 필드를 사용하여 가져올 정보를 필터링할 수 있습니다. 다음은 샘플 요청 URL입니다.
>  ```
>  https://console.tim.qq.com/v4/group_open_http_svc/get_group_info?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
>  ```
>  다음은 예시 요청입니다.
>  ```json
>  {
>      "GroupIdList": [ // 쿼리에 지정된 그룹 ID 목록(필수)
>          "@TGS#1NVTZEAE4",
>          "@TGS#1CXTZEAET"
>      ]
>  }
>  ```
>  자세한 내용은 [Getting Group Profiles](https://intl.cloud.tencent.com/document/product/1047/34961)를 참고하십시오.
>  - **그룹 구성원 세부 정보 가져오기**: `그룹 구성원 프로필 가져오기` API를 호출하여 그룹 구성원의 세부 정보(사용자 지정 필드 포함)를 가져올 수 있습니다. 다음은 샘플 요청 URL입니다.
>  ```
>  https://console.tim.qq.com/v4/group_open_http_svc/get_group_member_info?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
>  ```
>  다음은 예시 요청입니다.
>  ```json
>  {
>      "GroupId":"@TGS#1NVTZEAE4"  // 그룹 ID(필수)
>  }
>  ```
>  응답에서 `MemberNum` 필드는 그룹의 총 구성원 수를 나타내고 `AppMemberDefinedData`는 그룹 구성원의 사용자 지정 필드 정보를 나타냅니다.
>  >? 이 API는 오디오-비디오 그룹(AVChatRoom)을 지원하지 않습니다. 자세한 내용은 [Getting Group Member Profiles](https://intl.cloud.tencent.com/document/product/1047/34948)를 참고하십시오.
>
>
>  #### 팀 구성원의 팀 정보 가져오기
>
>  팀 구성원은 `그룹 구성원 프로필 가져오기` API를 호출하여 팀 내 다른 구성원의 역할 및 상태와 같은 자세한 정보를 얻을 수 있습니다.
>  ```java
>  GroupGetMemberInfoListParam param = new GroupGetMemberInfoListParam
>  {
>    group_get_members_info_list_param_group_id = "group_id",
>    group_get_members_info_list_param_identifier_array = new List<string>
>    {
>      "user_id"
>    }
>  };
>  TIMResult res = TencentIMSDK.GroupGetMemberInfoList(param, (int code, string desc, GroupGetMemberInfoListResult result, string user_data)=>{
>   // 비동기 로직 프로세스
>  });
>  ```
>  >?
>  >- 자세한 내용은 [Unity-Getting the Profile of a Group Member](https://intl.cloud.tencent.com/document/product/1047/50320)를 참고하십시오.
>  >- `그룹 만원 시 게임 시작`, `구성원의 팀 가입 또는 탈퇴` 등과 같은 기타 그룹 정보는 [팀 기반 시나리오](#Team_scene)를 참고하십시오. 이러한 정보는 콜백을 통해 그룹에 통보됩니다.
>  >- 그룹 선택 및 기타 그룹 관련 정보에 대한 자세한 내용은 [그룹 시스템](https://intl.cloud.tencent.com/document/product/1047/33529)을 참고하십시오. **그룹 관리**에 대한 자세한 내용은 [콘솔 가이드 - 그룹 관리](https://intl.cloud.tencent.com/document/product/1047/34578)를 참고하십시오.
>
>  ### 민감한 정보 필터링
>
>  민감한 콘텐츠를 필터링하는 것은 게임의 중요한 기능입니다. 구현 계획은 다음과 같습니다.
>  1. 그룹 메시지를 보내기 전에 웹후크를 바인딩합니다.
>  2. 웹후크 데이터를 기반으로 메시지 유형을 식별하고 메시지 데이터를 Tencent Cloud Security 또는 다른 타사 점검 서비스에 전달합니다.
>  3. 메시지가 일반 텍스트 메시지인 경우 Tencent Cloud Security의 점검 결과를 기다린 후 메시지를 IM 백엔드로 전달할지 여부를 나타내는 데이터 패킷을 반환합니다.
>
>  메시지를 보내기 전 웹후크의 샘플 데이터:
>
>  ```json
>  {
>      "CallbackCommand": "Group.CallbackBeforeSendMsg", // 콜백 명령
>      "GroupId": "@TGS#2J4SZEAEL", // 그룹 ID
>      "Type": "Public", // 그룹 유형
>      "From_Account": "jared", // 발신자
>      "Operator_Account":"admin", // 요청 개시자
>      "Random": 123456, // 랜덤 숫자
>      "OnlineOnlyFlag": 1, // 값은 온라인 메시지인 경우 1이고 그렇지 않은 경우 0(기본값)입니다. 오디오/비디오 그룹의 경우 값은 0입니다.
>      "MsgBody": [ // 메시지 본문, 자세한 내용은 TIMMessage 메시지 객체 참고
>          {
>              "MsgType": "TIMTextElem", // 텍스트
>              "MsgContent": {
>                  "Text": "red packet"
>              }
>          }
>      ],
>      "CloudCustomData": "your cloud custom data"
>  }
>  ```
>
>  >?MsgBody의 MsgType 필드를 기반으로 메시지 유형을 식별할 수 있습니다. 필드에 대한 자세한 내용은 [그룹 내 발언 전 콜백](https://intl.cloud.tencent.com/document/product/1047/34374)을 참고하십시오.
>
>  IM 백엔드로 반환된 웹후크의 데이터 패킷을 통해 구현될 수 있는 특정 방식으로 비준수 메시지를 처리하도록 선택할 수 있습니다.
>
>  ```json
>  {
>      "ActionStatus": "OK",
>      "ErrorInfo": "",
>      "ErrorCode": 0 // 다른 ErrorCode 값은 다른 의미를 갖습니다
>  }
>  ```
>
>  | ErrorCode | 설명                                                         |
>  | --------- | ------------------------------------------------------------ |
>  | 0         | 발언 허용, 메시지 전달 가능                                  |
>  | 1         | 발언 거부, 클라이언트 10016 반환                             |
>  | 2         | 자동 폐기가 활성화되고 클라이언트가 메시지를 정상적으로 반환 |
>
>  >?필요에 따라 사용할 수 있습니다.
>
>  ### 메시지 유형 사용자 지정(소품 선물 및 거래 메시지 등)
>
>  게임 채팅에는 텍스트, 이모티콘, 음성 메시지와 같은 단순 메시지 외에 사용자 지정 메시지가 필요합니다. 사용자 정의 메시지를 통해 개발자는 게임 소품 선물 및 거래와 같은 더 많은 대화방 기능을 구현하기 위해 메시지의 콘텐츠 형식을 사용자 정의할 수 있습니다.
>
>  Tencent Cloud IM은 텍스트, 이모티콘, 지리적 위치, 이미지, 음성, 파일, UGSV, 시스템 알림 및 사용자 지정 메시지의 9가지 기본 메시지 유형을 제공합니다. 사용자 지정 메시지를 제외한 모든 메시지의 형식은 고정되어 있으며 사용자는 해당 정보만 입력하면 됩니다. 메시지 유형에 대한 자세한 설명은 [메시지 유형](https://intl.cloud.tencent.com/document/product/1047/33523)을 참고하십시오. 메시지 형식에 대한 자세한 내용은 [메시지 형식](https://intl.cloud.tencent.com/document/product/1047/33527)을 참고하십시오.
>
>  서버 API [Sending One-to-One Messages to One User](https://intl.cloud.tencent.com/document/product/1047/34919), [Sending One-to-One Messages to Multiple Users](https://intl.cloud.tencent.com/document/product/1047/34920) 및 [Sending Ordinary Messages in a Group](https://intl.cloud.tencent.com/document/product/1047/34959)을 통해 사용자에게 사용자 지정 메시지를 보낼 수 있습니다. 다음은 그룹에서 일반 메시지를 보내기 위한 기본 요청 샘플입니다.
>
>  ```json
>  {
>      "GroupId": "@TGS#2C5SZEAEF",
>      "Random": 8912345, // 임의의 숫자. 두 메시지의 임의의 숫자가 5분 이내에 동일하면 동일한 메시지로 간주됩니다.
>      "MsgBody": [ // element 배열로 구성된 메시지 본문. 자세한 내용은 필드 설명 참고.
>          {
>              "MsgType": "TIMTextElem", // 텍스트
>              "MsgContent": {
>                  "Text": "red packet"
>              }
>          },
>          {
>              "MsgType": "TIMFaceElem", // 이모티콘
>              "MsgContent": {
>              "Index": 6,
>              "Data": "abc\u0000\u0001"
>              }
>          }
>      ],
>      "CloudCustomData": "your cloud custom data",
>      "SupportMessageExtension": 0,
>  }
>  ```
>
>  `CloudCustomData`를 수정하여 사용자 지정 메시지 데이터(클라우드에 저장됨)를 정의하고 보낼 사용자 지정 메시지를 `MsgBody`(메시지 본문)에 입력할 수 있습니다.
>
>  ### 팀 내 오디오/비디오 채팅
>
>  게임에서 오디오/비디오 채팅은 중요한 기능입니다. Tencent Cloud IM 앱은 [Tencent Real-Time Communication(TRTC)](https://www.tencentcloud.com/document/product/647) 및 TUICallKit을 사용하여 실시간 음성/영상 통화 기능을 갖추고 있습니다.
>
>  >? 
>  >- 각 SDKAppID에 대해 오디오/비디오 통화 기능의 7일 무료 평가판을 제공합니다. IM [콘솔](https://console.cloud.tencent.com/im)에서 각 SDKAppID에 대해 하나의 무료 평가판만 얻을 수 있습니다.
>  >-  TUICallKit에 대한 자세한 내용은 [Integration Solution (UI Included) - 음성/영상 통화](https://www.tencentcloud.com/document/product/1047/50025)를 참고하십시오.
>
>
>  ### 게임 채팅방 유형
>
>  게임 채팅방 유형은 다음과 같습니다.
>
>  | 유형               | 특성                                                         |
>  | ------------------ | ------------------------------------------------------------ |
>  | 채널               | 채널은 일반적으로 많은 수의 채팅 사용자를 참여시키며 고정 구성원 목록이 없습니다. 사용자는 언제든지 채널에 가입하고 채널에서 나갈 수 있습니다. 오프라인 메시지 푸시가 필요하지 않습니다. |
>  | 라이브 게임 로비   | 라이브 게임 로비에는 일반적으로 많은 채팅 사용자가 참여합니다. 사용자는 언제든지 라이브 룸에 참여하고 나갈 수 있습니다. 기록 메시지 쿼리가 지원됩니다. |
>  | 팀                 | 팀은 일반적으로 서로 친구가 될 필요가 없는 소수의 채팅 사용자와 관계를 맺습니다. 게임이 끝나면 팀이 종료됩니다. 오프라인 메시지 푸시가 필요하지 않습니다. |
>  | 친구               | C2C 채팅. 채팅 기록이 저장됩니다. 채팅 대상은 연락처 목록에 있는 친구만 될 수 있습니다. |
>  | 비공개 메시지      | C2C 채팅. 채팅 대상은 낯선 사람일 수 있습니다.               |
>  | 오디오-비디오 그룹 | 채팅 사용자 수에는 제한이 없습니다. 사용자는 언제든지 그룹에 가입하거나 탈퇴할 수 있습니다. |
>
>  IM은 다음 유형의 채팅방을 제공합니다.
>
>  | 유형                           | 특성                                                         |
>  | ------------------------------ | ------------------------------------------------------------ |
>  | 작업 그룹(work)                | 작업 그룹은 그룹 구성원인 친구의 초대를 통해 사용자가 그룹에 가입할 수 있도록 합니다. 초대는 초대받은 사람이 수락하거나 그룹 소유자가 승인할 필요가 없습니다. |
>  | 공개 그룹(Public)              | 공개 그룹을 사용하면 그룹 소유자가 그룹 관리자를 지정할 수 있습니다. 그룹에 가입하려면 사용자가 그룹 ID를 검색하여 요청을 보내고 그룹 소유자 또는 관리자가 요청을 승인해야 그룹에 가입할 수 있습니다. |
>  | 회의 그룹(Meeting)             | 회의 그룹을 사용하면 사용자가 자유롭게 참여하고 나갈 수 있으며 그룹에 참여하기 전에 전송된 기록 메시지를 볼 수 있습니다. 회의 그룹은 음성/화상 회의 및 온라인 교육과 같은 TRTC(Tencent Real-Time Communication)를 통합하는 시나리오에 이상적입니다. 이 그룹 유형은 이전 버전의 ChatRoom과 동일합니다. |
>  | 오디오-비디오 그룹(AVChatRoom) | 오디오-비디오 그룹은 사용자가 자유롭게 가입 및 탈퇴할 수 있고, 회원 수에 제한이 없으며, 메시지 기록을 저장하지 않습니다. 오디오-비디오 그룹은 Cloud Streaming Services(CSS)와 함께 사용하여 화면 댓글 채팅 시나리오를 지원할 수 있습니다. |
>  | 커뮤니티 그룹(Community)       | 커뮤니티 그룹은 사용자가 자유롭게 가입 및 탈퇴할 수 있으며 최대 10만명의 회원을 지원하고 메시지 기록을 저장합니다. 그룹에 가입하려면 사용자는 그룹 ID를 검색하고 신청서를 보내야 하며, 신청서는 관리자의 승인을 받지 않아도 그룹에 가입할 수 있습니다. |
>
>  다음은 필요에 따라 게임에 적용할 수 있는 IM 그룹 특성을 기반으로 하는 몇 가지 샘플 솔루션을 제공합니다.
>
>  | 유형                     | 솔루션                                                       | 특성                                                         |
>  | ------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
>  | 채널 및 라이브 게임 로비 | 커뮤니티 그룹(Community)                                     | 커뮤니티 그룹은 다수의 사용자를 지원하며 사용자가 승인 없이 자유롭게 가입 및 탈퇴할 수 있도록 합니다. |
>  | 친구                     | 1:1 채팅+권한 제어(친구끼리만 메시지보내기)                  | 친구끼리만 서로에게 메시지를 보낼 수 있습니다.               |
>  | 비공개 메시지            | 1:1 채팅+권한 제어(App 내 임의의 2명의 사용자가 서로 1:1 메시지를 보낼 수 있도록 허용) | 두 명의 낯선 사람이 서로에게 메시지를 보낼 수 있습니다.      |
>  | 팀업                     | 공개 그룹(Public) 및 회의 그룹(Meeting)                      | 게임 내 팀원만 그룹 채팅에 입장할 수 있습니다. 오디오-비디오 채팅이 지원됩니다. |
>  | 오디오-비디오 그룹       | 오디오-비디오 그룹(AVChatRoom)                               | 그룹 구성원 수에는 제한이 없으며 사용자는 언제든지 오디오-비디오 그룹에 가입하거나 탈퇴할 수 있습니다. |
>
>  >?
>  >- 친구 및 비공개 일대일 채팅 권한 제어에 대한 자세한 내용은 [1:1 채팅 메시지 권한 제어](https://intl.cloud.tencent.com/document/product/1047/33523#.E5.8D.95.E8.81.8A.E6.B6.88.E6.81.AF.E6.9D.83.E9.99.90.E6.8E.A7.E5.88.B6%EF%BC%89)를 참고하십시오.
>  >- 그룹 시스템에 대한 자세한 내용은 [그룹 시스템](https://intl.cloud.tencent.com/document/product/1047/33529)을 참고하십시오.
