## 개요
StreamLink는 비디오 콘텐츠 공급자에게 안정적이고 안전하며 빠르며 대기 시간이 짧은 미디어 전송 기능을 제공합니다. StreamLink 서비스는 플로우 레벨에서 관리됩니다. 각 플로우는 전송 연결에 해당합니다. StreamLink를 사용하면 스트리밍 미디어를 빠르고 안정적으로 전송하고 전송 프로세스 전반에 걸쳐 스트리밍 품질의 다양한 측면을 모니터링할 수 있습니다.

## Flow 리스트
StreamLink 서비스는 Flow 레벨에서 관리됩니다. Flow는 라이브 스트림을 하나 이상의 대상으로 전송하고 재생 URL을 생성합니다. StreamLink 콘솔의 [Flow Management](https://console.tencentcloud.com/mdc/flow)에서 모든 Flow를 관리할 수 있습니다. 이 페이지에서 Flow를 추가, 보기, 편집, 삭제, 시작 또는 중지할 수도 있습니다.

![](https://qcloudimg.tencent-cloud.cn/raw/afd0fc995dafc79a23feb9ba2df91dae.jpg)

**Flow** 관리 페이지에는 다음 정보가 표시됩니다.
- **Status**: IDLE은 Flow가 시작되지 않았음을 나타냅니다. RUNNING은 Flow가 시작되었음을 나타냅니다.
- **Source Protocol**: Input 프로토콜입니다.
- **Input Address**: Input 주소입니다.
Flow가 실행 중인 경우 얼로우 리스트를 편집하거나 기존 Output을 삭제하거나 새 Output을 생성할 수 있습니다. 그러나 다른 작업을 수행하려면 먼저 Flow를 중지해야 합니다.