## 작업 시나리오
도메인이 추가 및 확인되면 이를 통해 비디오 리소스에 액세스할 수 있습니다. 그러나 API 또는 콘솔을 통해 얻은 비디오 URL의 호스트는 기존 도메인 이름의 Host로 유지됩니다. 따라서 콘솔에 로그인하여 기본 배포 구성에서 URL의 Host 정보를 업데이트해야 합니다.
## 작업 단계
1. [VOD 콘솔](https://console.cloud.tencent.com/vod/overview)로그인하고 왼쪽 사이드바에서 [배포 및 재생]>[기본 배포 구성]을 클릭하여 ‘기본 배포 구성’ 페이지로 들어갑니다.
2. 오른쪽 상단 모서리에 있는 [편집]을 클릭하고 해당 매개변수를 설정합니다:
 - 기본 배포 프로토콜: HTTP 및 HTTPS가 지원됩니다.
 - 기본 배포 도메인 이름: 기본적으로 시스템이 할당한 `xxx.vod2.myqcloud.com`이 사용됩니다. 사용자 정의 도메인 이름을 기본 배포 도메인 이름으로 [추가](https://intl.cloud.tencent.com/document/product/266/35572)하고 [리졸브](https://intl.cloud.tencent.com/document/product/266/35572)할 수도 있습니다.
 
![](https://qcloudimg.tencent-cloud.cn/raw/63d948da67e7b1d9c48b7bcfae3567c9.png)
