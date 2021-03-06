[](id:que1)

### 라이브 방송 녹화는 어떤 원리인가요?
![img](https://main.qcloudimg.com/raw/9c9d31c6ffec97d2b8b4042b7a673cbc.jpg)

라이브 방송 스트리밍에서는 일단 녹화를 시작하면 멀티미디어 데이터가 녹화 시스템에 녹화됩니다. 녹화 시스템이 호스트의 모바일에서 푸시되는 모든 프레임 데이터를 녹화 파일에 추가 기록합니다.

라이브 방송 스트리밍이 중단되면 액세스 레이어는 녹화 서버에 즉시 공지하여 현재 기록하고 있는 파일을 VOD 시스템으로 옮겨 저장하며, 인덱스를 생성해 사용자가 VOD 시스템에서 새로 생성된 녹화 파일을 확인할 수 있습니다. 또한 녹화 이벤트 공지를 설정한 경우 녹화 시스템이 해당 문서의 **인덱스 ID**와 **온라인 재생 주소** 등의 정보를 이전에 설정한 서버로 공지합니다.

그러나 파일이 너무 큰 경우 클라우드에서 전송 및 처리하는 과정에서 오류가 발생하기 쉽습니다. 따라서 성공률을 높이기 위해 개별 녹화 파일의 길이는 최대 120분으로 제한하며, RecordInterval 매개변수를 통해 멀티 파트를 더 짧게 지정할 수 있습니다.

[](id:que2)
### 라이브 방송은 왜 비디오 녹화를 할 수 없나요? 
라이브 방송 녹화 다시보기 기능은 Tencent Cloud의 **VOD 서비스**에 따라 지원하며, 녹화 기능을 사용하고 싶은 경우 먼저 Tencent Cloud의 관리 콘솔에서 [VOD 서비스 활성화](https://console.cloud.tencent.com/vod)를 진행하십시오.

[](id:que3)
### 라이브 방송 종료 후 얼마 후에 녹화 파일을 볼 수 있나요? 
라이브 방송 종료 약 5분 후 녹화 파일을 가져올 수 있으며, 녹화 완료 후 이벤트가 콜백됩니다. 상세 내용은 전달받은 콜백 시간을 기준으로 하며, 더 자세한 사항은 [콜백 설정](https://intl.cloud.tencent.com/document/product/267/31074)을 참조하십시오.

[](id:que4)
### 라이브 방송 녹화 후, 녹화 파일은 어떻게 받을 수 있나요?
녹화 파일 생성 후 자동으로 VOD 시스템에 저장되며 클라이언트가 VOD 서비스를 활성화해야만 저장됩니다. 다음과 같은 방식으로 녹화 파일을 받을 수 있습니다.
- [VOD 콘솔](https://intl.cloud.tencent.com/document/product/267/31563)
- [녹화 이벤트 알림](https://intl.cloud.tencent.com/document/product/267/31563)
- [VOD API 조회](https://intl.cloud.tencent.com/document/product/267/31563)

[](id:que5)
### 라이브 방송 비디오를 마이그레이션할 수 있나요?
현재는 비디오 다운로드 주소를 획득한 후 자체적으로 마이그레이션해야 합니다.. 

[](id:que6)
### 비디오 저장 시간은 어떻게 설정하나요?
현재 CSS 비디오 저장은 시간 제한이 없습니다. 콘솔과 RSET API 인터페이스를 통해 비디오 파일을 관리할 수 있습니다. 

[](id:que7)
### 라이브 방송 1회 녹화 시 몇 개의 녹화 파일이 생성되나요?

- **MP4, FLV 또는 AAC 포맷 녹화**: 개별 파일의 녹화 시간은 5분 ~ 120분으로 제한됩니다. [녹화 템플릿 생성](https://intl.cloud.tencent.com/document/product/267/30845) 인터페이스의 RecordInterval 매개변수를 통해 멀티 파트를 더 짧게 지정할 수 있습니다.
    - 라이브 방송이 너무 짧아 녹화 템플릿이 활성화되지 않고 푸시 스트림이 종료된 경우 시스템은 녹화 파일을 생성할 수 없습니다.
    - 라이브 방송 시간이 길지 않고(RecordInterval 시간보다 짧은 경우) 중도에 푸시 스트림 중단 이벤트가 발생하지 않은 경우 통상적으로 1개의 파일이 생성됩니다.
    - 라이브 방송 시간이 매우 긴 경우(RecordInterval 시간 보다 긴 경우) RecordInterval 지정 시간에 따라 멀티 파트를 진행합니다. 이는 파일의 시간이 너무 긴 경우 분산형 시스템에서 스트리밍 전송 시 시간의 불확실성이 발생하는 것을 방지하기 위함입니다.
    - 라이브 방송 도중에 푸시 스트림이 중단된 경우(이후 SDK가 다시 푸시 스트림 시도), 모든 중단 지점마다 1개의 새로운 파트가 생성됩니다.

- **녹화 HLS 포맷**: 단일 파일의 최장 길이는 제한이 없습니다. 연장 녹화 시간 초과 시 새 파일이 생성돼 녹화가 계속됩니다. 연장 녹화 초과 시간은 0s~1800s로 설정할 수 있습니다.

[](id:que8)
### 어느 파일이 1회 라이브 방송에 포함되는지 어떻게 알 수 있나요?

정확히 말하자면 PAAS의 Tencent Cloud는 고객님이 라이브 방송을 어떻게 정의했는지 알지 못합니다. 만약 라이브 방송이 20분 동안 지속되었는데 중간에 한 번은 네트워크 전환으로 스트리밍이 중단되고 한 번은 수동으로 정지 및 재시작했다면 이는 1회의 라이브 방송으로 간주할까요, 3회로 간주할까요?

일반 모바일 라이브 방송 시나리오에 대해 우리는 아래와 같이 인터페이스 사이의 시간을 1회 라이브 방송으로 정의합니다.

따라서 App 클라이언트에서 보내는 시간 정보가 중요합니다. 만약 이 시간에 녹화한 파일이 1회 라이브 방송에 들어가도록 정의하고 싶다면 라이브 방송 코드와 시간 정보를 이용해 받은 녹화 공지를 검색하면 됩니다(각 녹화 공지 이벤트마다 **스트림 ID**, **시작 시간** 및 **종료 시간**등의 정보를 가집니다).

[](id:que9)
### 조각 파일 연결은 어떻게 하나요?
현재 Tencent Cloud는 클라우드의 API 인터페이스를 사용해 비디오 멀티 파트 연결을 지원합니다. 

[](id:que10)
###  녹화 템플릿을 1개만 설정했는데 라이브 방송이 2개 채널로 녹화되었습니다. 어떻게 해결해야 하나요? 
이 경우 일반적으로 현재 푸시 도메인에서 동시에 2개의 녹화 작업을 전송한 것일 수 있습니다. 다음 방식에 따라 순서대로 진단해 보시기를 권장합니다.

1. 콘솔의 녹화 설정 정보를 조회하여 녹화 파일 유형이 1개 포맷만 선택되어 있는지 확인합니다.
   -콘솔이 **신규 버전 콘솔**인 경우, [[도메인 관리]](https://console.cloud.tencent.com/live/domainmanage)에서 푸시 도메인 우측의 [관리]를 클릭하고 [템플릿 설정]의 [녹화 설정]에서 관련 템플릿의 '녹화 포맷' 정보를 확인하십시오.
   -콘솔이 **구 버전 콘솔**인 경우, [[라이브 방송 코드 액세스]](https://console.cloud.tencent.com/live/livecodemanage)>[액세스 설정]에서 라이브 방송 녹화 설정 정보를 확인하십시오.  
2. [녹화 작업 생성](https://intl.cloud.tencent.com/document/product/267/30847)과 [녹화 템플릿 생성](https://intl.cloud.tencent.com/document/product/267/34223)의 2가지 녹화 작업 시작 방식 중 실제 요구사항에 따라 1가지만 선택하면 됩니다. 만약 동일한 라이브 방송 스트리밍에서 녹화 템플릿을 설정함과 동시에 녹화 작업을 생성한 경우 중복 녹화될 수 있습니다. 콘솔에서 녹화 작업을 시작하고 동시에 API 3.0의 [CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/30847) 인터페이스 또는 API 2.0의 Live_Tape_Start 인터페이스를 호출하여 녹화 작업을 활성화했는지 확인하십시오.

> ! 
> - 만약 라이브 방송 녹화가 구 버전의 콘솔에서 활성화 되었고 신규 버전 콘솔은 비활성화해야 한다면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 관련 직원을 찾아 해결할 수 있습니다. 
> - 위의 방법으로 문제를 해결할 수 없을 경우 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 해결하십시오. 전문가 상담으로 연결해드립니다.






