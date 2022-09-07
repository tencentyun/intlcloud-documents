
### GME(Game Multimedia Engine) 음성 채팅은 얼마나 많은 트래픽을 소비합니까?
유창한 음질의 경우 비트 레이트는 30Kbps이고 표준 및 고음질의 경우 64Kbps입니다. 트래픽은 비트 레이트 및 음성 채팅을 통해 통신하는 방 구성원 수와 관련이 있습니다. 공식은 비트 레이트 x 구성원 수 / 8 = 바이트입니다.

### 방에 들어갈 때 네트워크 오류를 나타내는 오류 코드 7004가 반환됩니다. 어떻게 해결해야 합니까?
문제 해결을 위해 다음을 확인하십시오.
1. AppId, UIN 및 AuthBuffer와 같은 EnterRoom API의 매개변수가 유효한지 여부입니다. 자세한 내용은 [API 문서](https://intl.cloud.tencent.com/zh/document/product/607/18522)를 참고하십시오.
2. 테스트 장치가 사설망 또는 공중망에 있는지 여부입니다. 사설망에 있는 경우 [How to deal with the restrictions of corporate firewall](https://intl.cloud.tencent.com/document/product/607/35232)의 지침에 따라 문제를 해결하십시오.
3. 기타 네트워크 문제는 다음과 같습니다.

### 네트워크 문제는 어떻게 해결합니까?

- **네트워크 진단**
	- [도메인 이름 tcloud.tim.qq.com의 상태 확인](https://ping.huatuo.qq.com/tcloud.tim.qq.com)을 클릭합니다
	- [도메인 이름 gmeconf.qcloud.com의 상태 확인](https://ping.huatuo.qq.com/gmeconf.qcloud.com)을 클릭합니다
	- [도메인 이름 yun.tim.qq.com의 상태 확인](https://ping.huatuo.qq.com/yun.tim.qq.com )을 클릭합니다

네트워크 문제가 있는 장치를 사용하여 브라우저에서 위의 3개 URL을 열고 결과를 기다리십시오(확인을 완료하는 데 약 5 - 10초 소요). **결과 URL 복사 및 공유**를 클릭한 다음 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 클릭하여 도움을 받으십시오.
![](https://main.qcloudimg.com/raw/0b540f4bf6222c6b9548b148496a15bb.png)

- **SSO 진단**
네트워크 문제가 있는 장치를 사용하여 [도메인 이름 tcloud.tim.qq.com의 상태 확인](https://tcloud.tim.qq.com)을 엽니다. 스크린샷을 캡처하거나 결과를 복사한 다음 [티켓 제출](https://console.cloud.tencent.com/workorder/category)하여 도움을 받으십시오.
예시 코드는 다음과 같습니다.
```
{"ActionStatus":"FAIL","ErrorCode":60002,"ErrorInfo":"HTTP parse Error"}
```
