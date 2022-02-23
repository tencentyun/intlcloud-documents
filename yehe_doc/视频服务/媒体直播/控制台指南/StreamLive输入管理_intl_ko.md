입력 채널은 StreamLive의 미디어 스트림 입력 채널로, 일반적으로 1개의 보안 그룹 및 1개의 StreamLive 채널과 연결됩니다.

### 입력 생성

[Input Management] 메뉴를 선택하고 [Create Input]을 클릭하여 입력 채널을 생성합니다. 입력 채널은 현재 RTP, RTP-FEC, RTMP, UDP, HLS, HTTP-MP4 등 기타 프로토콜 입력을 지원하며, PULL 및 PUSH 입력 메소드를 제공합니다.

모든 채널은 하나의 보안 그룹 및 하나의 채널에 연결할 수 있으며, 채널과 연결된 입력 상태는 attached로 표시됩니다.
![img](https://main.qcloudimg.com/raw/eed9a73cc25fc646b1f601ac545ccc0e.png)

>?
> - 콘솔은 기본적으로 최대 5개의 input를 지원합니다.
> - input의 미디어 소스는 현재 최소 1개의 비디오 데이터 채널을 포함해야 합니다.
> - MPEG-TS 멀티 채널을 사용하면 최대 8개 채널의 동시 전송이 가능합니다.
