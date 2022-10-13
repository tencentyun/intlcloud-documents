본문은 StreamPackage를 구성하는 방법을 보여줍니다.

1. [StreamPackage 콘솔](https://console.tencentcloud.com/mdp/channel)에 로그인하고 가까운 리전을 선택합니다. ![](https://qcloudimg.tencent-cloud.cn/raw/9e2a246d5681ee392a1c8c70cd342de3.png)
2. **Create Channel**을 클릭하고 팝업 창에 필요한 정보를 입력합니다. ![](https://qcloudimg.tencent-cloud.cn/raw/beef79acbc0bb01fdc795adabd23cf83.png)
- **Input Protocol**: HLS 또는 DASH. 이 예시에서는 HLS를 선택합니다.
- **Max Segment Duration**: 이 채널에 푸시된 TS 세그먼트의 최대 지속 시간입니다. 4초로 설정하는 것이 좋습니다.
- **Max Playlist Duration**: 이 채널에 푸시된 m3u8 재생 목록 파일의 최대 지속 시간입니다. 12초로 설정하는 것이 좋습니다(즉, m3u8 재생 목록에 3개의 TS 세그먼트).

3. 생성을 클릭합니다. 고급 구성 페이지로 들어갑니다. **Information** 탭에서 기존 구성 정보를 보거나 **Input**, **Endpoints** 및 **CDN** 탭에서 푸시 URL, 재생 URL 및 CDN 가속을 구성할 수 있습니다.

4. **Input**: 시스템은 고가용성을 보장하기 위해 장애 조치에 사용할 수 있는 두 개의 Input URL을 채널에 자동으로 할당합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/48526b3405cd4373f41f95aa254c4a37.png)
- 각 Input에 대해 독립적인 인증 정보를 구성할 수 있습니다. **Input Authentication**을 활성화하면 시스템에서 입력에 대한 **Username / Password**를 자동으로 생성합니다. ![](https://qcloudimg.tencent-cloud.cn/raw/c32de384eda1fa084d50b13f243a9021.png)
- **Rotate credentials**를 클릭하여 새 인증 정보를 생성할 수 있습니다. 원본 정보는 복구할 수 없습니다.
- 타사 서비스에서 입력 URL로 콘텐츠를 푸시하려면 **Input Url** 및 **Authentication** 정보를 기록해 두십시오.

5. **Endpoint**: **Endpoint** 탭을 선택하고 **Create Endpoint**를 클릭하여 재생 URL을 만듭니다. IP 제한(IP Restriction) 및 인증 키(AuthKey)의 두 가지 액세스 제어 방법이 지원됩니다. HLS가 입력 프로토콜로 선택되었기 때문에 HLS URL이 생성됩니다. URL은 main.m3u8 파일의 전체 경로입니다.
![](https://qcloudimg.tencent-cloud.cn/raw/43f73db0ecaba6c72d7eb4677397caad.png)

6. 이제 StreamPackage에 대한 구성을 완료했습니다. **Channel Management**로 돌아가서 목록에서 만든 채널을 찾은 다음 나중에 사용할 수 있도록 **ID**와 **Endpoint Url**을 기록해 둡니다.
![](https://qcloudimg.tencent-cloud.cn/raw/5eb1b481f758f89ec7a1279d7bd4d873.png)
![](https://qcloudimg.tencent-cloud.cn/raw/3f7c30d33e17425a44dca05a701e8ad7.png)