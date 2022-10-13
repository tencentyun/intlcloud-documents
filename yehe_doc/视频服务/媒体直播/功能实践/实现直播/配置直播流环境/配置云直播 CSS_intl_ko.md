CSS는 최종 사용자에게 더 나은 보기 경험을 보장합니다. 이 문서는 CSS를 구성하는 방법을 보여줍니다.

1. [StreamPackage](https://www.tencentcloud.com/products/mdp)에서 다음 구성을 완료하면 Tencent Cloud가 [CSS](https://www.tencentcloud.com/products/css)의 해당 재생 도메인에 대한 원본 서버 설정을 자동으로 추가합니다. StreamPackage 콘솔에서 생성한 StreamPackage Channel을 클릭하고 **CDN** 탭을 선택한 다음 **Edit Configuration**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/91fdb17fa19c8c2cc98a230017b9e2f8.png)

2. 팝업 창에서 사용하려는 재생 도메인을 입력하고 확인을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/3d9b5fc8f4fbffb56fb9a14d17726be5.png)

3. CSS 원본 서버 구성이 완료되면 현재 페이지에 재생 도메인 이름(**Playback Domain Name**), **CNAME**, 가속 리전(**Acceleration Region**) 및 상태(**Status**)를 포함한 정보가 표시됩니다. 기본 가속 영역은 중국대륙 외부입니다.
![](https://qcloudimg.tencent-cloud.cn/raw/0d0f202a0394c67926da815e460b7ca4.png)

4. 재생 도메인에 대한 액세스 제어, Referer 얼로우리스트/블록리스트 및 HTTPS도 구성하려면 **Go to the CSS CDN Console to Perform More Actions**를 클릭합니다.

5. 추가 구성을 수행할 필요가 없는 경우 시스템에서 할당한 **CNAME**을 기록하고 DNS 플랫폼에 추가합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/2696cd0cda9bb9412c4d799457b9698e.png)

6. 재생을 위한 최종 URL을 얻으려면 CSS 재생 도메인과 StreamPackage Endpoint 경로를 연결합니다.
