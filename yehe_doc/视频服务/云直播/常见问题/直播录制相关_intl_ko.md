<span id="que1"></span>
### 라이브 방송 녹화는 어떤 원리인가요?
![img](https://main.qcloudimg.com/raw/9c9d31c6ffec97d2b8b4042b7a673cbc.jpg)

라이브 방송 스트리밍에 대해 일단 녹화를 시작하면 멀티미디어 데이터가 녹화 시스템에 녹화됩니다. 호스트의 모바일에서 업푸시되는 모든 프레임 데이터가 녹화 시스템에 의해 녹화 파일에 추가 기록됩니다.

라이브 방송 스트리밍이 중단되면 액세스 레이어가 녹화 서버에 즉각 통보하여 현재 기록하고 있는 파일을 VOD 시스템으로 전환하여 저장하며, 색인을 생성해 VOD 시스템에서 새로 생성된 녹화 파일을 확인할 수 있습니다. 또한 녹화 이벤트 알림을 설정한 경우 녹화 시스템이 해당 문서의 **색인 ID**와 **온라인 재생 주소** 등의 정보를 이전에 설정한 서버로 통보합니다.

그러나 파일이 너무 큰 경우 클라우드 단의 전송 및 처리 과정에서 쉽게 에러가 발생할 수 있습니다. 따라서 성공률 확보를 위해 녹화 파일 1개 길이는 최장 120분으로 제한하며, RecordInterval 매개 변수를 통해 더 짧게 설정할 수 있습니다.

<span id="que2"></span>
### 라이브 방송은 왜 비디오 녹화를 할 수 없나요? 
라이브 방송 녹화 다시보기 기능은 Tencent Cloud의 **VOD 서비스**에 따라 지원하며, 녹화 기능을 사용하고 싶은 경우 먼저 Tencent Cloud의 관리 콘솔에서 [VOD 서비스 활성화](https://console.cloud.tencent.com/vod)를 진행하십시오.

<span id="que3"></span>
### 라이브 방송 종료 후 얼마 후에 녹화 파일을 볼 수 있나요? 
라이브 방송 종료 후 약 5분 후 녹화 파일이 생성되며, 녹화 완료 후 이벤트가 콜백 됩니다. 구체 내용은 전달 받은 콜백 시간을 기준으로 하며, 더 자세한 사항은 [콜백 설정](https://intl.cloud.tencent.com/document/product/267/31074)을 참조하십시오.

<span id="que4"></span>
### 라이브 방송 녹화 후, 녹화 파일은 어떻게 받을 수 있나요?
녹화 파일 생성 후 자동으로 VOD 시스템에 저장되며 클라이언트가 VOD 서비스를 활성화해야만 저장됩니다. 다음과 같이 녹화 파일을 받을 수 있습니다.
- [VOD 콘솔](https://intl.cloud.tencent.com/document/product/267/31563#vod-console)
- [녹화 이벤트 알림](https://intl.cloud.tencent.com/document/product/267/31563#recording-event-notification)
- [VOD API 조회](https://intl.cloud.tencent.com/document/product/267/31563#vod-api-query)

<span id="que5"></span>
### 라이브 방송 비디오를 마이그레이션할 수 있나요?
현재는 비디오 다운로드 주소를 획득한 후 자체적으로 마이그레이션할 수 있습니다. 

<span id="que6"></span>
### 비디오 저장 시간은 어떻게 설정하나요?
현재 LVB 비디오 저장은 시간 제한이 없습니다. 콘솔과 RSET API 인터페이스를 통해 비디오 파일을 관리할 수 있습니다. 

<span id="que7"></span>
### 라이브 방송 1회 녹화 시 몇 개의 녹화 파일이 생성되나요?

- **MP4, FLV 또는 AAC 포맷 녹화**: 파일 1개 시간은 5분 ~ 120분으로 제한됩니다. [녹화 템플릿 생성](https://intl.cloud.tencent.com/document/product/267/30845) 인터페이스의 RecordInterval 매개변수를 통해 더 짧게 설정할 수 있습니다.
	- 라이브 방송이 매우 짧아 녹화 템플릿이 활성화되지 않고 푸시 스트리밍이 종료된 경우 시스템은 녹화 파일을 생성하지 않습니다.
	- 라이브 방송 시간이 많이 길지 않고(RecordInterval 시간보다 짧은 경우) 중도에 푸시 스트리밍 중단 이벤트가 발생하지 않은 경우 통상적으로 1개의 파일이 생성됩니다.
	- 라이브 방송 시간이 너무 긴 경우(RecordInterval 시간 보다 긴 경우) RecordInterval 지정 시간에 따라 파일을 분할합니다. 이는 시간이 너무 긴 파일의 경우 분산형 시스템에서 스트리밍 전송 시간의 불확실성이 존재하기 때문입니다.
	- 라이브 방송 과정에서 푸시 스트리밍을 중단(이후 SDK가 다시 푸시 스트리밍 시도)하는 경우 모든 중단 지점에서 1개의 새로운 분할 파일이 생성됩니다.

- **HLS 포맷 녹화**: 파일 1개의 최장 길이에 제한이 없으며, 계속 녹화 시간 제한을 초과한 경우 새로운 파일이 생성되고 계속 녹화가 이루어집니다. 계속 녹화 시간 제한은 0초 ~ 1800초까지 설정할 수 있습니다.

<span id="que9"></span>
### 조각 파일 스플라이싱은 어떻게 하나요?
현재 Tencent Cloud는 클라우드 단의 API 인터페이스를 사용해 비디오 조각 파일 스플라이싱을 지원합니다. 

<span id="que10"></span>
### 녹화 템플릿 1개만 설정했는데 라이브 방송이 2개 채널로 녹화되었습니다. 어떻게 해결해야 하나요? 
대부분의 경우 현재 푸시 스트리밍 도메인에서 동시에 2개 채널 녹화 작업을 전송한 것일 수 있습니다. 다음 방식에 따라 순서대로 진단해 보길 권장합니다.

1. 콘솔의 녹화 설정 정보를 조회하여 녹화 파일 유형이 1개 포맷만 선택되어 있는지 확인합니다.
   -콘솔이 **신규 버전 콘솔**인 경우, [도메인 관리](https://console.cloud.tencent.com/live/domainmanage)를 방문하여 푸시 스트리밍 도메인 오른쪽의 [Manage]를 클릭하고 [Configure Template]의 [Recording Configuration]에서 템플릿 관련 "녹화 포맷" 정보를 확인하십시오.
  
2. [녹화 작업 생성](https://intl.cloud.tencent.com/document/product/267/30847)과 [녹화 템플릿 생성](https://intl.cloud.tencent.com/document/product/267/34223)은 2가지의 녹화 요청 방식입니다. 실제 사용 시 필요에 따라 1가지만 선택하면 됩니다. 동일한 라이브 방송 스트리밍에서 녹화 템플릿을 설정한 동시에 녹화 작업을 생성한 경우 중복 녹화될 수 있습니다. 콘솔에서 녹화 작업을 시작하고 동시에 API 3.0의 [CreateLiveRecord](https://intl.cloud.tencent.com/document/product/267/30847) 인터페이스 또는 API 2.0의 [Live_Tape_Start](https://intl.cloud.tencent.com/document/product/267/9567)  인터페이스를 호출하여 녹화 작업을 활성화했는지 확인하십시오.

>!위의 방법으로 문제를 해결할 수 없을 경우 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 해결하십시오. 전문가가 상담해 드립니다.






