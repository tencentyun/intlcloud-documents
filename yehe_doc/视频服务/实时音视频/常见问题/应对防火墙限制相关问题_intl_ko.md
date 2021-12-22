### 클라이언트 Native SDK에서 어떤 포트 또는 도메인을 화이트리스트로 설정해야 합니까?

방화벽 포트는 다음과 같습니다.

| TRTC SDK(Native) | 화이트리스트 항목 |
|---------|---------|
| TCP 포트 | 443, 20166 |
| UDP 포트 | 8000, 8080, 16285, 9000 |

도메인 화이트리스트:

```
cloud.tim.qq.com
gz.file.myqcloud.com
avc.qcloud.com
yun.tim.qq.com
dldir1.qq.com
mlvbdc.live.qcloud.com
query.tencent-cloud.com
```


### WebRTC에서 어떤 포트 또는 도메인을 화이트리스트로 설정해야 합니까?

방화벽 포트는 다음과 같습니다.

| WebRTC(H5) | 화이트리스트 항목 |
|---------|---------|
| TCP 포트 | 8687 |
| UDP 포트 | 8000; 8080; 8800; 843; 443; 16285 |

도메인 화이트리스트:

```
*.rtc.qq.com
yun.tim.qq.com
```

### TRTC web 내부 네트워크 환경에서 프록시를 어떻게 설정합니까?
Nginx+coturn 프록시 솔루션을 사용할 수 있습니다.

| 솔루션 이름 | 적용 시나리오                             | 네트워크 요구 사항                          |
| :----- | :----------------------------------- | :-------------------------------- |
| 솔루션 1 | 클라이언트가 특정 외부 네트워크 프록시 서버에 액세스하도록 허용   | 클라이언트가 외부 네트워크의 proxy server에 액세스하도록 허용 |
| 솔루션 2 | 클라이언트가 내부 네트워크 프록시 서버를 통해 외부 네트워크에 액세스하도록 허용 | proxy server가 외부 네트워크에 액세스하도록 허용        |




### WeChat 미니프로그램에서 어떤 도메인을 화이트리스트로 설정해야 합니까?

&lt;trtc-room&gt; 도메인 화이트리스트:

```
https://official.opensso.tencent-cloud.com
https://yun.tim.qq.com
https://cloud.tencent.com
https://webim.tim.qq.com
https://query.tencent-cloud.com
```


>!Tencent Cloud 서버 IP 주소는 동적 업데이트되며 고정 IP 주소가 아닙니다. 따라서 고정 IP 리스트는 제공되지 않습니다.
