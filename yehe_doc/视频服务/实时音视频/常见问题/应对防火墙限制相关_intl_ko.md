### 클라이언트 Native SDK에서 어떤 포트 또는 도메인을 얼로우리스트로 설정해야 합니까?

방화벽 포트는 다음과 같습니다.

| TRTC SDK(Native) | 얼로우리스트 항목 |
|---------|---------|
| TCP 포트 | 443, 20166, 10443, 10444, 10445, 10446, 10447, 10448, 10449, 10450, 10451, 13275, 23275, 33000, 37528 |
| UDP 포트 | 8000, 8080, 8001, 8002, 8003, 8004, 8005, 8006, 8007, 8008, 8009, 16285, 9000 |

도메인 얼로우리스트:

```
intl-query.trtc.tencent-cloud.com
intl-accelerate.trtc.tencent-cloud.com
trtc-client-log-overseas-1258344699.cos.ap-singapore.myqcloud.com
intl-sdklog.trtc.tencent-cloud.com
sdkdc.live.qcloud.com
speedtestint.trtc.tencent-cloud.com
intl-query.trtc.tencent-cloud.com
hwapi.im.qcloud.com
videoapi-sgp.im.qcloud.com
trtc-sdk-config-1258344699.file.myqcloud.com          
```

 
### WebRTC에서 어떤 포트 또는 도메인을 얼로우리스트로 설정해야 합니까?

방화벽 포트는 다음과 같습니다.

| WebRTC(H5) | 얼로우리스트 항목 |
|---------|---------|
| TCP 포트 | 8687 |
| UDP 포트 | 8000; 8080; 8800; 843; 443; 16285 |

도메인 얼로우리스트:

```
intl-signaling.rtc.qq.com
intl-signaling.rtc.qcloud.com
intl-schedule.rtc.qq.com
intl-schedule.rtc.qcloud.com
videoapi-sgp.im.qcloud.com
```

### 클라이언트가 프라이빗 네트워크에서 web용 TRTC SDK에 액세스하도록 프록시를 구성하려면 어떻게 해야 합니까?
Nginx+coturn 솔루션을 사용할 수 있습니다. 자세한 내용은 [엔터프라이즈 프라이빗 네트워크 프록시 솔루션](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-34-advanced-proxy.html)을 참고하십시오.

| 솔루션 | 적용 시나리오                             | 네트워크 요구 사항                          |
| :----- | :----------------------------------- | :-------------------------------- |
| 솔루션1 | 클라이언트가 공용 네트워크의 특정 프록시 서버에 액세스할 수 있도록 허용   | 클라이언트가 공용 네트워크의 proxy server에 액세스할 수 있도록 허용 |
| 솔루션2 | 클라이언트가 프라이빗 네트워크의 프록시 서버를 통해 공용 네트워크에 액세스할 수 있도록 허용 | proxy server가 공용 네트워크에 액세스하도록 허용        |


