- 본문은 Tencent Cloud IM Demo(iOS)를 빠르게 실행하는 방법을 소개합니다.

  

  ## 작업 단계
  [](id:step1)

  ### 1단계: 애플리케이션 생성
  1. [IM 콘솔](https://console.cloud.tencent.com/im)에 로그인합니다.
  >?이미 애플리케이션이 있는 경우 SDKAppID를 기록하고 [키 정보 가져오기](#step2)를 합니다.
  >동일한 Tencent Cloud 계정으로 최대 300개의 IM 애플리케이션을 만들 수 있습니다. 이미 300개의 애플리케이션이 있는 경우 신규 애플리케이션 생성 전에 사용하지 않는 애플리케이션을 [비활성화 및 삭제](https://intl.cloud.tencent.com/document/product/1047/34540)합니다. **애플리케이션 삭제 후에는 SDKAppID에 해당하는 모든 데이터 및 서비스를 복구할 수 없으므로 주의하시기 바랍니다.**
  >
  2. **애플리케이션 생성**을 클릭하고 **애플리케이션 생성** 대화 상자에 애플리케이션 이름을 입력한 후 **확인**을 클릭합니다.
  ![](https://main.qcloudimg.com/raw/15e61a874a0640d517eeb67e922a14bc.png)
  3. 애플리케이션 생성 후, 콘솔 전체보기 페이지에서 새로 생성된 애플리케이션의 상태, 서비스 버전, SDKAppID, 생성 시간, 태그 및 만료 시간을 확인할 수 있습니다. SDKAppID 정보를 저장하십시오.
  ![](https://main.qcloudimg.com/raw/7954cc2882d050f68cd5d1df2ee776a6.png)


  [](id:step2)
  ### 2단계: 키 정보 가져오기
  1. 대상 애플리케이션 카드를 클릭하여 애플리케이션의 기본 구성 페이지로 이동합니다.
  ![](https://qcloudimg.tencent-cloud.cn/raw/8d469e975f1ca5a2f3dbc9c6fe8774f5.png)
  2. **기본 정보** 섹션에서 **키 표시**를 클릭하고 키 정보를 복사 및 저장합니다.
  >!키 정보가 유출되지 않도록 잘 보관하십시오.

  [](id:step3)
  ### 3단계: Demo 소스 다운로드 및 설정

  1. IM Demo 프로젝트를 다운로드합니다. 다운로드 주소는 [SDK 다운로드](https://intl.cloud.tencent.com/document/product/1047/33996)를 참고하십시오.
  >?이모티콘 디자인의 저작권 존중을 위해, 다운로드한 Demo 프로젝트에는 주요 이모티콘 요소의 슬라이스 이미지가 포함되어 있지 않습니다. 로컬 이모티콘 패키지를 사용하여 코드를 구성할 수 있습니다. IM Demo에서의 이모티콘 무단 사용 행위는 디자인 저작권 침해에 해당될 수 있습니다.
  2. 단말 디렉터리의 프로젝트를 열고, 해당 'GenerateTestUserSig' 파일을 찾습니다.
   iOS 경로: iOS/Demo/TUIKitDemo/Private/GenerateTestUserSig.h
    Mac 경로: Mac/Demo/TUIKitDemo/Debug/GenerateTestUserSig.h
  3. `GenerateTestUserSig` 파일에서 관련 매개변수를 설정합니다.
   - SDKAPPID: [1단계](#step1)에서 획득한 실제 애플리케이션 SDKAppID로 설정합니다.
   - SECRETKEY: [2단계](#step2)에서 획득한 실제 키 정보로 설정합니다.
   ![](https://qcloudimg.tencent-cloud.cn/raw/57ba967d9f8222bf89b748f32994ce9c.png)


  >!본문의 UserSig 획득 방법은 클라이언트 코드에서 SECRETKEY를 설정하는 것입니다. 해당 방법 중 SECRETKEY는 디컴파일로 크래킹되기 쉬우므로, 키가 유출되면 해커가 사용자의 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 Demo 실행 및 기능 디버깅에만 적합합니다**.
  >올바른 UserSig 배포 방식은 UserSig 컴퓨팅 코드를 귀하의 서버에 통합하고, App 지향 인터페이스를 제공하는 것입니다. UserSig가 필요할 때, App은 비즈니스 서버에 동적 UserSig 가져오기 요청을 발송합니다. 자세한 내용은 [서버에서 UserSig 생성](https://intl.cloud.tencent.com/document/product/1047/34385)을 참고하십시오.

  [](id:step4)
  ### 4단계: 컴파일 실행
  [3단계](#step3)에서 복제된 Demo 프로젝트의 해당 디렉터리에 있는 `README.md` 파일을 참고하십시오.

  1. 단말에서 다음 명령어를 실행하여 Pod 버전을 확인합니다.
  ```
  pod --version
  ```
  pod가 존재하지 않거나 pod 버전이 1.7.5 이전 버전이라는 메시지가 표시되면 다음 명령을 실행하여 최신 pod를 설치합니다.
  ```
  //gem 소스 교체
  gem sources --remove https://rubygems.org/
  gem sources --add https://gems.ruby-china.com/
  //pod 설치
  sudo gem install cocoapods -n /usr/local/bin
  //여러 Xcode가 설치된 경우 다음 명령을 사용하여 Xcode 버전을 선택하십시오(일반적으로 최신 Xcode 버전 선택).
  sudo xcode-select -switch /Applications/Xcode.app/Contents/Developer
  //로컬 pod 라이브러리 업데이트
  pod setup
  ```
  2. 단말에서 다음 명령을 실행하여 종속 라이브러리를 설치합니다.
  ```
  //iOS
  cd iOS/TUIKitDemo
  pod install
  //Mac
  cd Mac/TUIKitDemo
  pod install
  ```
   설치에 실패하면 다음 명령을 실행하여 로컬 CocoaPods 리포지토리 목록을 업데이트합니다.
   ```bash
   pod repo update
   ```
  3. 컴파일 및 실행
   - iOS: iOS/TUIKitDemo 폴더로 이동하여 `TUIKitDemo.xcworkspace`를 열어 컴파일 및 실행합니다.
   - Mac: Mac/TUIKitDemo 폴더로 이동하여 `TUIKitDemo.xcworkspace`를 열어 컴파일 및 실행합니다.

  >!Demo는 기본적으로 음성/영상 통화 기능과 통합되어 있습니다. 그러나 음성/영상 통화 기능이 의존하는 TRTC SDK는 현재 시뮬레이터를 지원하지 않습니다. Demo 실행 또는 디버깅을 위해 실제 장치를 사용하십시오.

  ## 고급 기능
  - [UI 인터페이스 라이브러리](https://intl.cloud.tencent.com/document/product/1047/50062)
  - [영상 통화 활성화](https://www.tencentcloud.com/document/product/1047/50024)

  ## 관련 문서
  - [요금 안내](https://intl.cloud.tencent.com/document/product/1047/34350)
