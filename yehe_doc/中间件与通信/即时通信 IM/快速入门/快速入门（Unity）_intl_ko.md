- [](id:toc)
  본문은 Unity SDK를 프로젝트에 통합하는 전체 프로세스를 소개합니다.

  ## 환경 요건

  | 플랫폼  | 버전                                                         |
  | ------- | ------------------------------------------------------------ |
  | Unity   | 2019.4.15f1 이후 버전.                                       |
  | Android | Android Studio 3.5 이후 버전. App은 Android 4.1 이후 버전 디바이스가 필요합니다. |
  | iOS     | Xcode 11.0 이후 버전. 프로젝트에 유효한 개발자 서명이 설정되어 있는지 확인십시오. |

  ## 플랫폼 지원

  당사는 Unity에서 전체 플랫폼을 커버하는 Tencent Cloud IM SDK 개발에 주력하여 하나의 코드 세트로 모든 플랫폼에서 실행할 수 있도록 지원합니다.

  | 플랫폼      | IM SDK               |
  | ----------- | -------------------- |
  | iOS         | 지원                 |
  | Android     | 지원                 |
  | macOS       | 지원                 |
  | Windows     | 지원                 |
  | [Web](#web) | 1.8.1+ 버전부터 지원 |

  >? Web 빌드에는 간단한 추가 단계가 필요합니다. [파트5](#web)를 확인하십시오.

  ## 전제 조건

  1. [Signing Up](https://intl.cloud.tencent.com/document/product/378/17985)된 계정이 있고 [Identity Verification](https://intl.cloud.tencent.com/document/product/378/3629)이 완료되어야 합니다.
  2. [애플리케이션 생성 및 업그레이드](https://intl.cloud.tencent.com/document/product/1047/34577)를 참고하여 애플리케이션을 생성하고 'SDKAppID'를 기록합니다.

  [](id:part1)

  ## 파트1: 테스트 사용자 생성

  [IM 콘솔](https://console.cloud.tencent.com/im)에서 애플리케이션을 선택하고 왼쪽 사이드바에서 **보조 툴** > **UserSig Generation & Verification**을 클릭하여 두 개의 UserID와 해당 UserSig를 생성하고 `UserID`, `서명(Key)`, `UserSig`를 복사하여 이후 로그인에 사용합니다.

  >? 이 계정은 개발 및 테스트 전용입니다. 애플리케이션 런칭 전에 올바른 `UserSig` 배포 방식은 서버에서 생성하여, App 지향 인터페이스를 제공하는 것입니다. `UserSig`가 필요할 때, App은 비즈니스 서버에 동적 `UserSig` 가져오기 요청을 발송합니다. 자세한 내용은 [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385)를 참고하십시오.

  ![](https://main.qcloudimg.com/raw/8315da2551bf35ec85ce10fd31fe2f52.png)

  [](id:part2)

  ## 파트2: Tencent Cloud IM SDK를 Unity 프로젝트에 통합

  1. Unity를 사용하여 프로젝트를 생성하고 프로젝트 디렉터리를 기록합니다.
  ![](https://qcloudimg.tencent-cloud.cn/raw/f07ae1bb4db4ca5f43f6acc563aafa8c.png)
  또는 기존 Unity 프로젝트를 엽니다.
  2. IDE(예시: Visual Studio Code)를 통해 프로젝트를 엽니다.
  ![](https://qcloudimg.tencent-cloud.cn/raw/881d625bf3ee2e736db22762e8763c18.png)
  3. 디렉터리에 따라 Packages/manifest.json을 찾아 종속성을 다음과 같이 수정합니다.
  ```json
     {
       "dependencies":{
         "com.tencent.imsdk.unity":"https://github.com/TencentCloud/chat-sdk-unity.git#unity"
       }
     }
  ```

  Tencent Cloud IM SDK 내의 모든 API를 더 잘 이해할 수 있도록 개발 초기 단계에서 SDK API를 테스트하고 특정 API를 호출하기 위한 [API Example](https://github.com/TencentCloud/tc-chat-sdk-unity/tree/main/Assets/IM_Api_Example)을 제공합니다.

  [](id:part3)

  ## 파트3: 로딩 종속성

  Unity Editor에서 프로젝트를 열고 종속성 로딩이 완료되기를 기다렸다가 Tencent Cloud IM이 로딩되었는지 확인합니다.
  ![](https://qcloudimg.tencent-cloud.cn/raw/d98dfb17bbee6c0319e370de6f2ba9dd.jpg)

  [](id:part4)

  ## 파트4: 자체 UI와 통합

  ### 전제 조건

  Unity 프로젝트를 생성하고 Tencent Cloud IM SDK를 로딩했습니다.

  ### SDK 초기화

  [본 섹션의 상세 문서](https://intl.cloud.tencent.com/document/product/1047/48570)

  `TencentIMSDK.Init`를 호출하여 SDK를 초기화합니다.

  `SDKAppID`를 전달합니다.

  ```c#
  public static void Init() {
    int SDKAppID = 0; // IM 콘솔에서 SDKAppID를 가져옵니다.
    SdkConfig sdkConfig = new SdkConfig();
  
    sdkConfig.sdk_config_config_file_path = Application.persistentDataPath + "/TIM-Config";
  
    sdkConfig.sdk_config_log_file_path = Application.persistentDataPath + "/TIM-Log";
  
    TIMResult res = TencentIMSDK.Init(long.Parse(SDKAppID), sdkConfig);
  }
  ```

  `Init` 후에는 주로 네트워크 상태 및 사용자 정보 변경에 대한 리스너를 포함하여 일부 리스너를 IM SDK에 마운트할 수 있습니다. 자세한 내용은 [여기](https://intl.cloud.tencent.com/document/product/1047/48570)에서 확인하십시오.

  ### 테스트 계정으로 로그인

  [본 섹션의 상세 문서](https://intl.cloud.tencent.com/document/product/1047/48571)

  콘솔에서 처음 생성된 테스트 계정을 사용하여 로그인 인증을 완료할 수 있습니다.

  `TencentIMSDK.Login`을 호출하여 계정에 로그인하십시오.

  반환값 'res.code'가 0이면 로그인이 성공한 것입니다.

  ```c#
  public static void Login() {
    if (userid == "" || user_sig == "")
    {
        return;
    }
    TIMResult res = TencentIMSDK.Login(userid, user_sig, (int code, string desc, string json_param, string user_data)=>{
      // 로그인 콜백 로직 프로세스
    });
  }
  ```

  >? 이 계정은 개발 테스트 전용입니다. 애플리케이션이 런칭되기 전에 정확한 `UserSig` 발급 방식은 다음과 같습니다. `UserSig` 계산 코드를 귀하의 서버에 통합하고 App 방향의 인터페이스를 제공합니다. `UserSig`가 필요할 때 귀하의 App이 비즈니스 서버로 동적 `UserSig`를 요청합니다. 자세한 내용은 [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385)를 참고하십시오.

  ### 메시지 발송

  [본 섹션의 상세 문서](https://intl.cloud.tencent.com/document/product/1047/48572)

  다음은 문자 메시지를 보내는 예시 코드입니다

  코드 예시:

  ```c#
  public static void MsgSendMessage() {
          string conv_id = ""; // c2c 메시지의 대화 ID는 userID, 그룹 메시지의 대화 ID는 groupID
          Message message = new Message
          {
            message_conv_id = conv_id,
            message_conv_type = TIMConvType.kTIMConv_C2C, // 그룹 메시지는 TIMConvType.kTIMConv_Group
            message_elem_array = new List<Elem>
            {
              new Elem
              {
                elem_type = TIMElemType.kTIMElem_Text,
                text_elem_content =  "일반 문자 메시지입니다"
              }
            }
          };
          StringBuilder messageId = new StringBuilder(128);
  
          TIMResult res = TencentIMSDK.MsgSendMessage(conv_id, TIMConvType.kTIMConv_C2C, message, messageId, (int code, string desc,                         string json_param, string user_data)=>{
            // 비동기 메시지 전송 결과
          });
                // 메시지가 전송될 때 반환되는 메시지 ID messageId
  }
  ```

  >?만약 SDKAppID가 낯선 사람에게 메시지를 보낼 수 없기 때문에 전송에 실패한다면, 테스트용으로 콘솔에서 활성화할 수 있습니다.
  >
  >[이 링크를 클릭](https://console.cloud.tencent.com/im/login-message)하여, 친구 관계망 확인을 비활성화하십시오.

  ### 대화 목록 가져오기

  [본 섹션의 상세 문서](https://intl.cloud.tencent.com/document/product/1047/50020)

  이전 단계에서 테스트 메시지를 보내면 다른 테스트 계정에 로그인하여 대화 목록을 가져올 수 있습니다.

  대화 목록을 가져오는 방법은 두 가지입니다.

  1. 장기간 연결 콜백을 수신하여 대화 목록을 실시간으로 업데이트합니다.
  2. API를 요청하여 페이징에 따라 대화 목록을 한번에 가져옵니다.

  일반 응용 시나리오는 다음과 같습니다.

  응용 프로그램을 실행한 후 바로 대화 목록을 가져온 다음 장기간 연결을 수신하여 대화 목록의 변경 사항을 실시간으로 업데이트합니다.

  #### 일회성 요청 대화 목록

  ```c#
  TIMResult res = TencentIMSDK.ConvGetConvList((int code, string desc, List<ConvInfo> info_list, string user_data)=>{
   // 비동기 로직 프로세스
  });
  ```

  이 때 이전 단계에서 다른 테스트 계정에서 보낸 메시지를 볼 수 있습니다.

  #### 긴 링크에서 실시간으로 대화 목록 가져오기

  이 단계에서는 SDK에 리스너를 마운트한 다음 콜백 이벤트를 처리하고 UI를 업데이트해야 합니다.

  1. 리스너 마운트.
  ```c#
  TencentIMSDK.SetConvEventCallback((TIMConvEvent conv_event, List<ConvInfo> conv_list, string user_data)=>{
   // 콜백 로직 프로세스
  });
  ```
  2. 콜백 이벤트를 처리하고 UI에 최신 대화 목록을 표시합니다.

  ### 메시지 수신

  [본 섹션의 상세 문서](https://intl.cloud.tencent.com/document/product/1047/48573)

  Tencent Cloud IM SDK를 통해 메시지를 수신하는 두 가지 방법:

  1. 장기간 연결 콜백을 수신하고, 실시간으로 메시지 변경 사항을 가져오고, 렌더링 메시지 기록 목록을 업데이트합니다.
  2. API를 요청하여 페이징에 따라 메시지 기록를 한번에 가져옵니다.

  일반 응용 시나리오는 다음과 같습니다.

  1. 인터페이스는 새로운 대화가 시작되면 먼저 일정량의 메시지 기록을 한꺼번에 요청하여 메시지 기록 목록을 보여 줍니다.
  2. 긴 링크를 수신하여 실시간으로 새로운 메시지를 수신하여 메시지 기록 목록에 추가합니다.

  #### 일회성 요청 메시지 기록 리스트

  페이지당 풀링하는 메시지의 수는 너무 크면 안 됩니다. 그렇지 않으면 풀링 속도에 영향을 줄 수 있습니다. 약 20으로 설정하는 것이 좋습니다.

  다음 요청 시 현재 페이지 수를 동적으로 기록해야 합니다.

  예시 코드는 다음과 같습니다.

  ```c#
  // 일대일 메시지 기록 풀링
  // 첫 번째 풀링에 대해 msg_getmsglist_param_last_msg를 null로 설정
  // msg_getmsglist_param_last_msg는 두 번째 풀링에 대해 반환된 메시지 목록의 마지막 메시지일 수 있습니다
  var get_message_list_param = new MsgGetMsgListParam
      {
        msg_getmsglist_param_last_msg = LastMessage
      };
  TIMResult res = TencentIMSDK.MsgGetMsgList(conv_id, TIMConvType.kTIMConv_C2C, get_message_list_param, (int code, string desc, string user_data) => {
    // 콜백 로직 프로세스
  });
  ```

  ```c#
  // 그룹 메시지 기록 풀링
  // 첫 번째 풀링에 대해 msg_getmsglist_param_last_msg를 null로 설정
  // msg_getmsglist_param_last_msg는 두 번째 풀링에 대해 반환된 메시지 목록의 마지막 메시지일 수 있습니다
  var get_message_list_param = new MsgGetMsgListParam
      {
        msg_getmsglist_param_last_msg = LastMessage
      };
  TIMResult res = TencentIMSDK.MsgGetMsgList(conv_id, TIMConvType.kTIMConv_Group, get_message_list_param, (int code, string desc, string user_data) => {
    // 콜백 로직 프로세스
  });
  ```

  #### 긴 링크를 통해 실시간으로 새 메시지 가져오기

  메시지 기록 목록이 초기화된 후 새 메시지는 긴 링크 `TencentIMSDK.AddRecvNewMsgCallback`에서 나옵니다.

  `AddRecvNewMsgCallback` 콜백이 트리거된 후 필요에 따라 메시지 기록 목록에 새 메시지를 추가할 수 있습니다.

  바인딩 리스너의 예시 코드는 다음과 같습니다.

  ```c#
  TencentIMSDK.AddRecvNewMsgCallback((List<Message> message, string user_data) => {
    // 새 메시지 프로세스
  });
  ```

  이제 IM 모듈 개발을 완료했으며, 메시지를 주고받거나 다른 대화에 들어갈 수 있습니다.

  귀하는 계속해서 [그룹](https://intl.cloud.tencent.com/document/product/1047/48169), [사용자 프로필](https://intl.cloud.tencent.com/document/product/1047/48859), [친구 관리](https://intl.cloud.tencent.com/document/product/1047/49563), [로컬 검색](https://intl.cloud.tencent.com/document/product/1047/50066) 등 관련 기능을 개발할 수 있습니다.

  자세한 내용은 [통합 솔루션(UI 없음)](https://www.tencentcloud.com/document/product/1047/34299)을 참고하십시오.

  [](id:part5)

  ## 파트5: #Unity for WebGL[](id:web)

  Tencent Cloud IM SDK (Unity 버전)는 `1.8.1` 버전부터 WebGL용 빌드를 지원합니다.

  Web 지원을 활성화하려면 Android 및 iOS 지원을 활성화하는 단계와 비교하여 다음과 같은 추가 단계를 수행해야 합니다.

  ### JS 가져오기

  GitHub에서 다음 3개의 JS 파일을 다운로드하여 프로젝트 빌드 WebGL 제품 폴더에 배치합니다.

  - [tim-js](https://github.com/TencentCloud/TIMSDK/blob/master/Web/IMSDK/tim-js.js)
  - [tim-js-friendship.js](https://github.com/TencentCloud/TIMSDK/blob/master/Web/IMSDK/tim-js-friendship.js)
  - [이 파일의 이름을 tim-upload-plugin.js로 변경](https://github.com/TencentCloud/TIMSDK/blob/master/Web/IMSDK/tim-upload-plugin/index.js)
  `index.html`을 열고 이 세 개의 JS 파일을 가져옵니다. 다음과 같습니다.

  ```html
  <script src="./tim-js.js"></script>
  <script src="./tim-js-friendship.js"></script>
  <script src="./tim-upload-plugin.js"></script>
  ```

  ## FAQ

  #### 어떤 플랫폼이 지원됩니까?

  현재 iOS, Android, Windows, Mac 및 WebGL이 지원됩니다.

  #### Android에서 Build And Run 클릭 후, 사용 가능한 디바이스를 찾을 수 없다는 오류가 보고되면 어떻게 해야 합니까?

  디바이스가 다른 리소스에 의해 점유되어 있지 않은지 확인하거나, Build를 클릭하여 apk 패키지를 생성한 다음 시뮬레이터로 드래그하여 실행합니다.

  #### iOS 최초 실행 시 오류가 보고되면 어떻게 합니까?

  상기 내용에 따라 설정된 Demo 실행 시 오류가 보고되면, **Product**>**Clean**을 클릭하여 지우고 다시 Build하거나, Xcode를 닫고 재실행 후 다시 Build합니다.

  #### Unity 2019.04 버전이 iOS 플랫폼에서 오류가 보고되면 어떻게 합니까?

  Library/PackageCache/com.unity.collab-proxy@1.3.9/Editor/UserInterface/Bootstrap.cs(23,20): error CS0117: 'Collab' does not contain a definition for 'ShowChangesWindow'
  Editor 툴바에서 **Window**>**Package Manager**를 클릭하여 Unity Collaborate를 1.2.16으로 다운그레이드합니다.

  #### Unity 2019.04 버전이 iOS 플랫폼에서 오류가 보고되면 어떻게 합니까?

  Library/PackageCache/com.unity.textmeshpro@3.0.1/Scripts/Editor/TMP_PackageUtilities.cs(453,84): error CS0103: The name 'VersionControlSettings' does not exist in the current context
  소스 코드를 열고 `|| VersionControlSettings.mode != "Visible Meta Files"` 코드를 삭제합니다.

  #### 에러 코드를 쿼리하는 방법은 무엇입니까?

  - IM SDK의 API 레이어 에러 코드는 [에러 코드](https://intl.cloud.tencent.com/document/product/1047/34348)를 참고하십시오.
