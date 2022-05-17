라이브 방송 푸시 스트리밍은 기본적으로 음란물 감지 화면 캡처 기능이 비활성화되어 있으며, 본 문서에서는 푸시 스트리밍 도메인을 음란물 감지 화면 캡처 템플릿에 연결하여 음란물 감지 화면 캡처 기능을 활성화하는 방법과 연결 완료 후 템플릿 바인딩을 해제해 음란물 감지 화면 캡처 기능을 비활성화하는 방법을 소개합니다.  

## 주의 사항
- 템플릿 설정을 완료하면 약 **5~10분** 후 적용됩니다.
- 음란물 감지 화면 캡처 설정을 완료하고 콜백 템플릿을 설정해야만 음란물 감지 화면 캡처 결과를 수신할 수 있습니다. 콜백 템플릿 설정은 [콜백 설정](https://intl.cloud.tencent.com/document/product/267/31065)을 참조하십시오.
- 도매인당 음란물 감지 화면 캡처 템플릿은 1개만 연결할 수 있으며, 연결 후 해당 도메인의 모든 스트리밍은 해당 템플릿에 따라 화면 캡처 및 음란물 감지가 진행됩니다.

## 전제 조건
 - [CSS 콘솔](https://console.cloud.tencent.com/live)에 로그인되어 있어야 하며 [푸시 스트리밍 도메인](https://intl.cloud.tencent.com/document/product/267/35970)이 추가되어 있어야 합니다. 
 - [음란물 감지 화면 캡처 템플릿](https://intl.cloud.tencent.com/document/product/267/31072)이 생성되어 있어야 합니다.


## 음란물 감지 화면 캡처 템플릿 연결

1. [Domain Management](https://console.cloud.tencent.com/live/domainmanage)로 이동하여 설정할푸시 스트리밍 도메인 또는 [Manage]를 클릭해 도메인 상세 페이지로 이동합니다.
2. [Template Configuration] 탭을 선택해 [Screencap&Porn Detection Configuration] 부분 오른쪽 상단의 [편집]을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/17f2d3e8f3fff6a1c3eeec09651caf37.png)
3. 설정할 음란물 감지 화면 캡처 템플릿을 선택하고 [Save]를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/39d729e20b7bb2b152d29eba3723f382.png)


## 음란물 감지 화면 캡처 템플릿 바인딩 해제
1. [Domain Management](https://console.cloud.tencent.com/live/domainmanage)로 이동하여 설정할푸시 스트리밍 도메인또는 [Manage]를 클릭해 도메인 상세 페이지로 이동합니다.
2. [Template Configuration] 탭을 선택해 [Screencap&Porn Detection Configuration] 부분 오른쪽 상단의 [Edit]를 클릭합니다.
3. 해당 템플릿의 선택을 해제하고 [Save]을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/f369adcf9c705a00024c50e8d6f94fea.png)
