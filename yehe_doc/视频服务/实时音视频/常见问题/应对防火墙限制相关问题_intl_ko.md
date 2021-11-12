### 클라이언트 Native SDK에서 어떤 포트 또는 도메인을 화이트리스트로 설정해야 합니까?

방화벽 포트는 다음과 같습니다.

| TRTC SDK(Native) | 화이트리스트 항목 |
|---------|---------|
| TCP 포트 | 443, 20166 |
| UDP 포트 | 8000、8080、16285、9000 |

도메인 화이트리스트:

<pre>
cloud.tim.qq.com
gz.file.myqcloud.com
avc.qcloud.com
yun.tim.qq.com
dldir1.qq.com
mlvbdc.live.qcloud.com
query.tencent-cloud.com
</pre>

 
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


### WeChat 미니프로그램에서 어떤 도메인을 화이트리스트로 설정해야 합니까?

&lt;trtc-room&gt; 도메인 화이트리스트:

<pre>
https://official.opensso.tencent-cloud.com
https://yun.tim.qq.com
https://cloud.tencent.com
https://webim.tim.qq.com
https://query.tencent-cloud.com
</pre>


>!Tencent Cloud 서버 IP 주소는 동적 업데이트되며 고정 IP 주소가 아닙니다. 따라서 본사는 고정 IP 리스트를 제공하지 않습니다.
