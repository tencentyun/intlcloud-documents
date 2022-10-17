>?‘월간’ 구독 인스턴스는 삭제할 수 없지만 만료 시 갱신을 중지할 수 있습니다.

CLB 인스턴스에 트래픽이 없고 더 이상 필요하지 않은 경우 CLB 콘솔 또는 API를 통해 삭제할 수 있습니다.
삭제된 CLB 인스턴스는 완전히 종료되어 복구할 수 없습니다. 모든 실제 서버의 바인딩을 해제하고 인스턴스를 삭제하기 전에 잠시 관찰하는 것이 좋습니다.

## 콘솔을 통해 CLB 인스턴스 삭제
1. [CLB 콘솔](https://console.cloud.tencent.com/loadbalance)에 로그인합니다.
2. 삭제하려는 CLB 인스턴스를 찾아 우측 작업 열에서 [더 보기]>[삭제]를 클릭합니다.
 ![](https://main.qcloudimg.com/raw/693acd714a4335920aea91b3ec4888f9.png)
3. 확인 창이 팝업되면, 작업 보안 프롬프트를 읽은 후 [확인]을 클릭하여 삭제합니다.
대화 상자는 아래와 같습니다. 바인딩된 규칙이 **‘0’**개 있고 바인딩된 CVM 인스턴스가 **‘없음’**이며 작업 보안에 대한 참고 사항 열 아래에 **‘녹색’** 체크 표시가 나타났을 때 삭제하는 것이 좋습니다.                                                               ![](https://main.qcloudimg.com/raw/e3f3e2f08b4b9c4f61c478762de4b33a.png)

## API를 통해 CLB 인스턴스 삭제
자세한 내용은 [DeleteLoadBalancers](https://intl.cloud.tencent.com/document/api/214/1257)를 참고하십시오.
