- # [Chat UIKit React](https://www.tencentcloud.com/document/product/1047/34279/)
  >Chat UIKit은 Tencent Cloud IM SDK를 기반으로 하는 UI 컴포넌트 라이브러리로, 세션, 채팅, 관계 체인, 그룹, 음성/영상 통화 등의 기능을 포함한 일부 범용 UI 컴포넌트를 제공합니다.
  >UI 컴포넌트를 기반으로 블록을 쌓는 것처럼 자신의 비즈니스 로직을 빠르게 구축할 수 있습니다.
  >Chat UIKit의 컴포넌트는 UI 기능을 구현하는 동시에 IM SDK에 해당하는 인터페이스를 호출하여 IM 관련 로직과 데이터를 처리하므로 개발자는 Chat UIKit을 사용할 때 자신의 업무에만 집중하거나 필요에 따라 확장할 수 있습니다.


  ## Example App
  당사는 채팅 기능을 보여주는 작동하는 데모를 만들었습니다. 당사 웹사이트에서 이러한 [demo](https://web.sdk.qcloud.com/im/demo/intl/index.html)와 GitHub의 관련 [오픈 소스 코드](https://github.com/TencentCloud/chat-uikit-react)를 미리 볼 수 있습니다.

  ![img.png](https://web.sdk.qcloud.com/im/demo/TUIkit/react-static/images/home.png)

  ## 데모 실행

  ### 1단계: 소스 코드 다운로드
  ```
  # Run the code in CLI
  $ git clone https://github.com/TencentCloud/chat-uikit-react
  # Go to the project  
  $ cd chat-uikit-react
  # Install dependencies of the demo
  $ npm install && cd examples/sample-chat && npm install
  ```
  ### 2단계: demo 설정
  1. `examples/sample-chat` 프로젝트를 열고 `./examples/sample-chat/src/debug/GenerateTestUserSig.js` 경로를 통해 `GenerateTestUserSig.js` 파일을 찾습니다.
  2. `GenerateTestUserSig.js` 파일에 `SDKAPPID`와 `SECRETKEY`를 설정하고 [IM 콘솔](https://console.tencentcloud.com/im)에서 해당 값을 얻을 수 있습니다. 대상 애플리케이션 카드를 클릭하여 설정 페이지로 이동합니다.
     ![](https://qcloudimg.tencent-cloud.cn/raw/8d469e975f1ca5a2f3dbc9c6fe8774f5.png)
  3. **Basic Information** 영역에서 **Display key**를 클릭하여 키 정보를 복사하고 GenerateTestUserSig 파일에 저장합니다.
  >!
  >- 본 문서의 UserSig 생성 방법은 클라이언트 코드에서 SECRETKEY를 설정하는 것입니다. 이 방법에서 SECRETKEY는 디컴파일로 크래킹되기 쉬우므로, 키가 유출되면 해커가 귀하의 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 Demo 실행 및 기능 디버깅용으로만 적합합니다.**
  >- UserSig의 계산 코드를 서버에 통합하고 App 지향 API를 제공하는 것이 가장 좋습니다. UserSig가 필요할 때 App은 동적 UserSig에 대한 요청을 서버에 보낼 수 있습니다. 자세한 내용은 [서버에서 UserSig 생성](https://www.tencentcloud.com/document/product/1047/34385)을 참고하십시오.

  ### 3단계: 프로젝트 실행
  ```
  # Launch the project
  $ cd examples/sample-chat
  $ npm run start
  ```

  ### 4단계: 첫 번째 메시지 전송
  1. 프로젝트가 성공적으로 실행된 후 ‘+’ 아이콘을 클릭하여 세션을 생성합니다.
  2. 입력란에 다른 사용자의 userID를 검색합니다.
  3. 사용자 프로필 사진을 클릭하여 세션을 시작합니다.
  4. 입력란에 메시지를 입력하고 "Enter"키를 누르면 전송됩니다.
     ![](https://web.sdk.qcloud.com/im/demo/TUIkit/react-static/images/chat-English.gif)


  ### Quick Links
  - [Demo App](https://web.sdk.qcloud.com/im/demo/intl/index.html)
  - [Client API](https://www.tencentcloud.com/document/product/1047/33999)
  - [Free Demos](https://www.tencentcloud.com/document/product/1047/34279)
  - [FAQ](https://www.tencentcloud.com/document/product/1047/34455)
  - [GitHub Source](https://github.com/TencentCloud/chat-uikit-react)
  - [Generating UserSig](https://www.tencentcloud.com/document/product/1047/34385)
