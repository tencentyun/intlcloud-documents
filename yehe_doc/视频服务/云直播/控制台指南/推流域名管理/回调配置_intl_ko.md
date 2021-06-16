라이브 방송 푸시 스트리밍은 기본적으로 콜백 기능이 비활성화되어 있습니다. 푸시 스트리밍 도메인에 콜백 설정을 연결한 후에는 해당 도메인의 모든 푸시 스트리밍 주소는 콜백 기능이 활성화됩니다. 라이브 방송 시 설정한 템플릿 이벤트에 따라 콜백 이벤트가 트리거되며, Tencent Cloud에서 직접 클라이언트 서버에 요청을 발송하고 클라이언트 서버에서 요청에 응답합니다. 인증을 통과하면 음란물 감지 콜백 정보가 포함된 JSON 데이터 패킷을 획득하게 됩니다.
본 문서에서는 푸시 스트리밍 도메인을 콜백 템플릿에 연결하여 콜백 기능을 활성화하는 방법과 연결 완료 후 템플릿 바인딩을 해제해 도메인 콜백 기능을 비활성화하는 방법을 소개합니다.  



 
## 주의 사항
- 템플릿 설정을 완료하면 약 5~10분 후 적용됩니다.
- 콜백 설정 완료 후, 라이브 방송 중 이벤트가 트리거되면 이벤트 정보 알림을 통해 자세한 라이브 방송 이벤트 정보를 획득할 수 있습니다. 자세한 내용은 [이벤트 정보 알림](https://intl.cloud.tencent.com/document/product/267/38080)을 참조하십시오.
- 콘솔의 콜백 템플릿 관리에서는 현재 도메인 차원에서 연결 인터페이스 생성 취소 규칙을 취소할 수 없습니다. 라이브 방송 콜백 관련 인터페이스를 통해 지정한 스트림과 연결하고 있는 경우, [콜백 템플릿 삭제](https://intl.cloud.tencent.com/zh/document/product/267/30813)를 참조하여 연결을 해제해야 합니다.
- 도매인당 콜백 템플릿은 1개만 연결할 수 있으며, 연결 후 해당 도메인의 모든 스트리밍은 해당 템플릿에 따라 콜백됩니다.

## 전제 조건
- [CSS 콘솔](https://console.cloud.tencent.com/live)에 로그인되어 있어야 하며 [푸시 스트리밍 도메인](https://intl.cloud.tencent.com/document/product/267/35970)이 추가되어 있어야 합니다.
- [콜백 템플릿](https://intl.cloud.tencent.com/document/product/267/31074)이 생성되어 있어야 합니다.

<span id="related"></span>
## 콜백 템플릿 연결
1.	[Domain Management](https://console.cloud.tencent.com/live/domainmanage)로 이동하여 설정할 **푸시 스트리밍 도메인** 또는 [Manage]를 클릭해 도메인 상세 페이지로 이동합니다.
2. [Template Configuration] 탭을 선택해 [Callback Configuration] 부분 오른쪽 상단의 [Edit]를 클릭합니다.
![](https://main.qcloudimg.com/raw/d3e31f428ab1463335e234007c663311.png)
3.	해당 콜백 템플릿을 선택하고 [Save]를 클릭합니다.
![](https://main.qcloudimg.com/raw/27f9da682e20283e25cc2478e1a53a0b.png)

<span id="untie"></span>
## 콜백 템플릿 바인딩 해제

1. [Domain Management](https://console.cloud.tencent.com/live/domainmanage)로 이동하여 설정할 **푸시 스트리밍 도메인** 또는 [Manage]를 클릭해 도메인 상세 페이지로 이동합니다.
2. [Template Configuration] 탭을 선택해 [Callback Configuration] 부분 오른쪽 상단의 [Edit]를 클릭합니다.
3. 연결 취소할 템플릿의 선택을 해제하고 [확인]를 클릭합니다.
![](https://main.qcloudimg.com/raw/0f8ec4ae49d2f1c5329bdb509f056366.png)
