라이브 방송 푸시 스트리밍은 기본적으로 녹화 기능이 비활성화되어 있으며, 본 문서에서는 푸시 스트리밍 도메인을 녹화 템플릿에 연결하여 녹화 기능을 활성화하는 방법과 연결 완료 후 템플릿 바인딩을 해제해 도메인 녹화 기능을 비활성화하는 방법을 소개합니다.  

[](id:limit)
## 사용 제한
- 녹화한 비디오 파일은 기본적으로 [VOD](https://console.cloud.tencent.com/vod/overview) 콘솔에 저장되며, 먼저 VOD 서비스를 활성화하고 VOD 서비스가 연체되어 중단되지 않도록 사전에 VOD 관련 리소스 패키지를 선택하시기 바랍니다. 자세한 내용은 [VOD 시작하기](https://intl.cloud.tencent.com/document/product/266/8757)를 참조하십시오.
- 녹화 기능을 활성화한 후에는 VOD 서비스의 정상 사용 상태를 유지해야 합니다. VOD 서비스를 활성화하지 않거나 계정이 연체되어 VOD 서비스가 중단되는 경우 라이브 방송을 녹화할 수 없으며, 해당 기간 동안에는 녹화 파일 및 녹화 비용이 발생하지 않습니다.
- 템플릿 설정을 완료하면 약 5~10분 후 적용됩니다. 
- 템플릿 연결 완료 후 지정한 푸시 스트리밍 도메인의 푸시 스트리밍 주소에 녹화 기능을 활성화할 수 있습니다.
- 도매인당 녹화 템플릿은 1개만 연결할 수 있으며, 연결 후 해당 도메인의 모든 스트리밍은 해당 템플릿에 따라 녹화됩니다.
- 혼합 스트리밍 녹화는 중국대륙 및 글로벌/홍콩, 마카오, 대만의 라이브 방송 혼합 스트리밍은 지원하지 않아 녹화 파일에 오류가 발생할 수 있으며 정상적인 재생에 영향을 미칠 수 있습니다.

## 전제 조건
- [CSS 콘솔](https://console.cloud.tencent.com/live)에 로그인되어 있어야 하며 [푸시 스트리밍 도메인](https://intl.cloud.tencent.com/document/product/267/35970)이 추가되어 있어야 합니다.
- [녹화 템플릿 생성](https://intl.cloud.tencent.com/document/product/267/34223)이 완료되었어야 합니다.


[](id:conect)
## 녹화 템플릿 연결
1.	[Domain Management](https://console.cloud.tencent.com/live/domainmanage)로 이동하여 설정할 **푸시 스트리밍 도메인** 또는 [Manage]를 클릭해 도메인 상세 페이지로 이동합니다.
2.	[Template Configuration] 탭을 선택해 [Recording Configuration] 부분 오른쪽 상단의 [Edit]를 클릭합니다.
![](https://main.qcloudimg.com/raw/29bf30fa3b4ce940a9903c0331fc608e.png)
3. 설정할 녹화 템플릿을 선택하고 [OK]를 클릭합니다.
![](https://main.qcloudimg.com/raw/8ecacaebb47ab9ae476d9286c1796b46.png)


[](id:unite)
## 녹화 템플릿 바인딩 해제
1. [Domain Management](https://console.cloud.tencent.com/live/domainmanage)로 이동하여 설정할 **푸시 스트리밍 도메인** 또는 [Manage]를 클릭해 도메인 상세 페이지로 이동합니다.
2. [Template Configuration] 탭을 선택해 [Recording Configuration] 부분 오른쪽 상단의 [Edit]를 클릭합니다.
3. 해당 템플릿의 선택을 해제하고 [OK]을 클릭합니다.
![](https://main.qcloudimg.com/raw/f2c5f091437cd8b873ed6447562fb697.png)

>? 
>- 녹화 템플릿 바인딩을 해제해도 현재 라이브 방송 중인 스트리밍에는 영향을 주지 않습니다.
>- 바인딩 해제 적용이 필요한 경우, 해제 후 스트리밍을 중단하고 다시 푸시 스트리밍 라이브 방송을 시작하면 새로운 라이브 방송부터는 녹화 파일이 생성되지 않습니다.


[](id:get_record)
## 녹화 파일 획득
녹화 파일이 생성되면 자동으로 VOD 시스템에 저장되며, 녹화 파일은 다음 방법으로 획득할 수 있습니다.

### VOD 콘솔
VOD 콘솔에 로그인하여 서브 애플리케이션을 선택해 이동한 후 왼쪽에 있는 [Media Asset Management](https://console.cloud.tencent.com/vod/media)를 클릭하면 녹화된 모든 파일을 확인할 수 있습니다.
![](https://main.qcloudimg.com/raw/b41dc459807ac1986d1db04032ea7942.png)
 
### 녹화 이벤트 알림
콘솔 또는 API 호출을 통해 녹화 콜백 주소를 설정할 수 있으며, 녹화 파일이 생성되면 메시지 방식으로 해당 콜백 주소로 알림을 전송합니다. 메시지를 수신한 후 녹화 [콜백 프로토콜 내용](https://intl.cloud.tencent.com/document/product/267/31566)에 따라 작업을 진행합니다.
>?이벤트 알림 메커니즘은 효율성과 신뢰도가 높고 실시간으로 전달됩니다. 녹화 파일 획득 시 콜백 방식 사용을 권장합니다.

### VOD API 조회
자세한 사용 방법은 VOD API [SearchMedia](https://intl.cloud.tencent.com/document/product/266/34179) 인터페이스를 참조하여 녹화 파일을 필터링해 조회하십시오.
