StreamLive는 Tencent Cloud StreamPackage와 함께 사용하여 HLS/DASH 포맷의 라이브 방송 스트림을 그대로 동일 계정의 StreamPackage에서 출력할 수 있도록 지원함으로써, 사용자가 손쉽게 자체 원본 서버를 구축하고 비디오 배포 및 재생할 수 있도록 해줍니다.

### StreamPackage 활성화

StreamPackage로 출력하기 전에 먼저 [StreamPackage 서비스를 활성화](https://console.cloud.tencent.com/mdp/channel)하고 Channel을 생성하십시오.

### StreamPackage의 Channel 생성

좌측 상단의 [Create Channel]을 클릭하여 채널을 생성하고 채널 이름과 StreamLive 출력 유형과 동일한 프로토콜을 입력합니다. 예시: StreamLive의 출력 유형을 HLS_StreamPackage로 선택한 경우, 여기에서도 HLS를 선택합니다.

>! StreamLive과 StreamPackage은 같은 Region에 있어야 합니다.

![img](https://main.qcloudimg.com/raw/ca0ae9e483499e4489a8db47b7bb290b.png)

### Endpoint 생성

Channel이 생성되면 Channel의 상세 내용 페이지로 들어가 Endpoint 노드를 생성할 수 있으며, 실제 비즈니스 니즈에 따라 IP 블록리스트/얼로우리스트 또는 인증 기능 활성화 여부도 선택할 수 있습니다.

![img](https://main.qcloudimg.com/raw/da2c4f2cefcbb73aa5ba68f75579937c.png)

### Endpoint 주소 및 Channel ID 획득

생성된 Endpoint의 URL이 재생/원본 서버 주소가 됩니다.

![img](https://main.qcloudimg.com/raw/30594049a37593a5d8827990bd9a13a1.png)

>? Channel ID는 StreamLive 출력을 입력하는 데 사용됩니다.

![img](https://main.qcloudimg.com/raw/c66b1bb5f1c9f570225310e66f8e0a66.png)

### 출력 유형 선택

StreamLive 콘솔로 돌아가 출력 설정 시, 출력 유형을 HLS_STREAMPACKAGE 또는 DASH_STREAMPACKAGE(사용자의 실제 비즈니스 니즈 및 방금 생성한 StreamPackage의 Channel 유형에 따라 결정)로 선택합니다. StreamPackage의 Channel ID를 입력합니다.

![img](https://main.qcloudimg.com/raw/486e54380f8bbecd2430c01ad8265c86.png)

### 설정 저장 및 제출

설정을 저장하고 제출합니다. 이어서 [StreamLive 채널 관리](https://intl.cloud.tencent.com/document/product/1048/45214) 챕터의 나머지 Channel 설정을 완료하고 저장합니다.
