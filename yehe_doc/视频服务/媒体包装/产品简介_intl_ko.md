## 개요

Tencent Cloud StreamPackage는 Tencent Cloud가 새롭게 출시한 고품질의 비디오 캡슐화 및 원본 서버 플랫폼입니다. 전세계 사용자들에게 전문적이고 안정적이며 안전한 비디오 캡슐화 및 딜리버리 서비스 제공에 주력하고 있습니다. StreamPackage는 전 세계 수많은 Tencent Cloud 가용존에 배포된 컴퓨팅 리소스와, Tencent의 애플리케이션 자체 개발 과정에서 다년간 연구한 멀티미디어 기술을 통해, 비디오 패키지 전송의 난이도를 낮추고 원본의 엘라스틱(Origin Resiliency) 성능을 강화하였습니다. 이에 따라 비디오 공급자는 대용량 비디오 스트림 미디어를 안전하고 안정적으로 배포할 수 있습니다. 또한 7 * 24시간의 가용성을 보장합니다.

![img](https://main.qcloudimg.com/raw/4a892b3997e8b86ff17ca6fe26f223ba.png)

## 특징

**멀티프로토콜 기본****/****보조 스트림 입력**

StreamPackage는 HLS, DASH 두 가지 프로토콜의 스트림 입력 모드를 지원하며, 각 Channel에 기본/보조 스트림 입력 주소(이중 채널 구성)를 생성하여 기본/보조 두 스트림 input을 동시에 푸시 스트림함으로써, 사용자의 비디오 자산을 안정적이고 신뢰도 높게 보호할 수 있습니다.

**유연하고 안정적인 재해 복구 메커니즘**

Channel의 기본/보조 채널 동시 입력 시, 기본 input에서 네트워크 불안정 등의 비정상적인 푸시 스트림 상황이 발생할 수 있으나, 보조 input의 푸시 스트림이 정상인 경우, 매끄럽게 보조 input으로 전환하여 출력할 수 있습니다. 전환 시간 등의 매개변수는 사용자 정의 설정이 가능합니다.

**높은 보안성**

StreamPackage는 입력부터 출력까지 각종 보안 인증 모드를 지원합니다. 입력에서는 http-authentication 모드를 지원하여 username, password로 푸시 스트림을 인증합니다. 출력에서는 IP 블랙리스트/화이트리스트 구성, Authkey 구성, X-TENCENT-PACKAGE를 통한 http-header의 인증, CIDR 수준의 보안 정책을 지원합니다.

**CDN** **배포 원클릭 연결**

StreamPackage는 라이브 방송 CDN의 원클릭 구성을 지원합니다. 자체 재생 도메인을 추가하여 배포하며, 전세계 각지에 분포되어 있는 엣지 노드를 통해 비디오를 안정적이고 효율적으로 배포합니다.

**가용성 높은 캐시 보호 메커니즘**

StreamPackage는 여러 단계의 캐시 보호 메커니즘을 제공합니다. 한 노드 서버에 이상이 발생할 경우, 내부 모니터링을 통해 노드를 자동으로 제거하여, 리전 리소스의 높은 가용성을 보장합니다. 또한 푸시 스트림에 기본/보조 스트림 input 모드를 지원함에 따라, 기본/보조 간의 스트림 입력을 매끄럽게 전환할 수 있으며, 푸시 스트림의 높은 안정성과 가용성을 보장합니다.

**아키텍처 및 장애 전환**

StreamPackage는 이중 채널 구성을 지원하여 pipeline A와 pipeline B가 동시에 라이브 방송 스트림을 입력할 수 있습니다. 또한 StreamPackage는 장애 자동 전환을 지원하여 StreamPackage의 기본 채널(pipeline A)에서 라이브 방송 스트림이 일정 시간동안 중단되었음이 감지되면(Max segment duration을 통해 설정 가능) 자동으로 보조 채널(pipeline B)로 전환하여 출력합니다.

StreamPackage의 Channel은 멀티 노드 풀 스트림 구성을 지원하여, 한 개의 Channel에서 여러 endpoint의 풀 스트림 및 출력을 지원합니다.

![img](https://main.qcloudimg.com/raw/b8d01ade821b7ed659ab65a4617ed6e1.png)