본문은 OBS를 사용하여 스트림을 푸시하고 VLC를 사용하여 스트림을 재생하는 방법을 보여줍니다. OBS를 열고 설정에서 스트림으로 이동하여 서버에 Input URL을, 스트림 키에 스트림 이름을 입력합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/d19308151baf27053d3ef774f416274c.png)

VLC를 열고(이 예시에서는 macOS용 VLC가 사용됨) File에서 Open Network를 클릭하고 네트워크 탭을 선택한 다음 StreamPackage Endpoint URL을 입력합니다(도메인 부분을 CSS에 구성된 재생 도메인으로 교체).
![](https://qcloudimg.tencent-cloud.cn/raw/e5d6e5f9c304f6b38fffafca19c0b456.png)

이제 StreamLive+StreamPackage+CSS를 기반으로 하는 신뢰성 높은 라이브 스트리밍 서비스를 구현했습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/3096992f56506043045b681624e12770.png)