본 문서에서는 [LVB 콘솔](https://console.cloud.tencent.com/live)을 통해 콜백 설정을 생성하는 방법을 소개합니다. 생성 완료 후 해당 푸시 스트리밍 도메인에서의 [콜백 설정](https://intl.cloud.tencent.com/document/product/267/31065)을 연결해야 하며, 연결하고 약 5~10분 후 적용됩니다. API를 통해서도 라이브 방송 채널에 콜백 템플릿을 생성할 수 있으며, 자세한 내용은 [콜백 템플릿 생성](https://cloud.tencent.com/document/api/267/32637)을 참조하십시오.


## 콜백 템플릿 생성
LVB 콘솔에 로그인하여 왼쪽 메뉴바에서 [기능 템플릿]>[Callback Configuration](https://console.cloud.tencent.com/live/config/callback)을 선택한 후, [+] 버튼을 클릭해 콜백 템플릿을 생성합니다. 팝업되는 콜백 설정창에서 콜백 정보를 작성하고 [Save]을 클릭합니다.
![](https://main.qcloudimg.com/raw/870c6dd664a4eb618bdc1a7fcdf922dc.png)
>
>- **콜백 키**는 사용자 정의 문자열로, 영문 대소문자와 숫자로 구성되며 최대 32자까지 입력할 수 있습니다.
>- 콜백 키 사용에 대한 자세한 내용은 [이벤트 정보 알림 매개변수 설명](https://intl.cloud.tencent.com/document/product/267/31566)을 참조하십시오.
>- 콜백 프로토콜에 대한 정보는 [이벤트 정보 알림 프로토콜](https://intl.cloud.tencent.com/document/product/267/31566)을 참조하십시오.

## 도메인 연결
콜백 템플릿 생성 후 [Domain Management](https://console.cloud.tencent.com/live/domainmanage)에서 해당 푸시 스트리밍 도메인 또는 [Manage]를 클릭해 도메인 상세 페이지로 이동합니다. [Template Configuration]으로 이동하여 해당 도메인에 콜백 템플릿을 지정해 줍니다.
![](https://main.qcloudimg.com/raw/e18e4c7f58950bd2dbe74f038c455cd9.png)
>
>- 콜백 설정 바인딩 해제가 필요한 경우, [Template Configuration]에서 [Edit]를 클릭하여 해당 템플릿 선택을 해제한 후 [Save]를 클릭하면 해당 템플릿과 도메인 연결이 해제됩니다.
>- 콘솔의 콜백 템플릿 관리에서는 현재 도메인 차원에서 연결 인터페이스 생성 취소 규칙을 취소할 수 없습니다. 라이브 방송 콜백 관련 인터페이스를 통해 지정한 스트림과 연결하고 있는 경우, [콜백 템플릿 삭제](https://intl.cloud.tencent.com/document/product/267/30813)를 참조하여 연결을 해제해야 합니다.
