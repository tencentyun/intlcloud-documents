
[모범 사례-라이브 방송 푸시 스트리밍](https://intl.cloud.tencent.com/document/product/267/31558)의 모범 사례대로 진행했음에도 푸시 스트리밍에 실패하는 경우가 있습니다. 이런 경우 본 문서에 나열되어 있는 영상 푸시 스트리밍 과정에서 자주 발생하는 문제를 참고하여 지침에 따라 해결할 수 있습니다.

### 1. 도메인의 CNAME 레코드가 Tencent Cloud 주소에 연결되었나요?
푸시 도메인의 CNAME이 Tencent Cloud 주소에 연결되어야만 스트림 푸시가 가능하며, [도메인 관리](https://console.cloud.tencent.com/live/domainmanage)에서 이미 생성된 푸시 도메인에 CNAME 레코드가 있는지 여부를 확인할 수 있습니다. CNAME 제목 표시줄의 해당 항목 상태에 따라 푸시 도메인에 CNAME 레코드가 있는지 여부를 확인할 수 있습니다. CNAME의 상태는 다음과 같습니다:
![](https://main.qcloudimg.com/raw/ebb055071447bc55c2f17e60ab8d0b75.png)
아직 CNAME이 없는 경우 [CNAME 설정](https://intl.cloud.tencent.com/zh/document/product/267/31057)에 따라 설정할 수 있습니다.
	

### 2. 네트워크가 정상인가요?
RTMP 푸시 스트리밍에 사용되는 기본 포트 번호는 **1935**입니다. 테스트 진행 중인 네트워크의 방화벽이 1935 포트 통과를 허용하지 않을 경우에는 서버에 연결할 수 없습니다. 이때 네트워크를 변경(4G로 전환 등)하여 네트워크가 문제의 원인인지를 파악할 수 있습니다.

### 3. txTime이 만료되었나요?
일부 고객은 자신의 라이브 방송 트래픽을 타인이 도용하는 것을 우려해 txTime을 시작 시간부터 5분 뒤로 설정하는 등 굉장히 보수적으로 설정하는 경우가 있습니다. 그러나 txSercet 서명이 있기 때문에 txTime의 유효기한을 지나치게 짧게 설정할 필요는 없습니다. 오히려 시간이 너무 짧은 경우, 호스트가 라이브 방송 시 네트워크가 몇 초간 끊기는 상황이 발생할 때 푸시 스트리밍 URL이 만료되어 푸시 스트리밍을 복구하지 못할 수 있습니다.
txTime은 현재 시간으로부터 12시간 또는 24시간 뒤로, 즉 일반적인 라이브 방송의 방송 시간보다 길게 설정하는 것이 좋습니다.

### 4. txSecret이 정확한가요？
Tencent Cloud는 보안을 위해 현재 푸시 스트리밍 주소가 링크 도용 방지가 되도록 하고 있습니다. 잘못 계산된 링크 도용 방지 또는 유효기한이 만료된 푸시 스트리밍 URL은 Tencent Cloud에서 **거부**되며, 이 경우 라이브 방송 SDK는 **PUSH_WARNING_SERVER_DISCONNECT** 이벤트를 발생시킵니다.
![](https://main.qcloudimg.com/raw/00c846dda473ee0dd241ffe89554849b.jpg)
신뢰할 수 있는 푸시 스트리밍 URL을 얻는 방법은 [모범 사례-라이브 방송 푸시 스트리밍](https://intl.cloud.tencent.com/document/product/267/31558)을 참조 바랍니다.

### 5. 푸시 스트리밍 URL이 사용 중인가요?
한 개의 푸시 스트리밍 URL은 한 번에 하나의 푸시 스트림만 가질 수 있으며, URL로 푸시 스트리밍을 시도하는 두 번째 클라이언트는 Tencent Cloud에서 거부될 수 있습니다. 이 경우, 라이브 방송 콘솔에 로그인한 뒤 [스트림 관리](https://console.cloud.tencent.com/live/streammanage)의 [온라인 스트림]에서 해당 스트림이 이미 푸시되었는지 확인 가능하며, [스트림 푸시 금지]에서도 해당 스트림의 푸시 금지 여부를 확인할 수 있습니다.

 
