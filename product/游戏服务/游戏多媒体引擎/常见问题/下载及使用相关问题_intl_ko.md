### GME Demo 및 SDK는 어디서 다운로드하나요?

[다운로드 가이드](https://cloud.tencent.com/document/product/607/18521)에서 관련 Demo 및 SDK를 다운로드합니다. 현재 공식 웹사이트에는 Unity 엔진 Demo, Cocos2D 엔진 Demo, Android 원본 개발 Demo 및 iOS 원본 개발 Demo 등이 있습니다.

### GME Demo를 다운로드한 후 자신이 신청한 계정으로 바꾸는 것이 가능한가요?
- 가능합니다. 콘솔에서 두 개의 번호, 즉 SDKAppID와 권한 키를 각각 얻어야 합니다.
- 사용자가 자신이 신청한 AppID를 사용하는 경우 AVChatViewController의 GetAuthBuffer에서 음성 채팅 키를 수정해야 합니다.

### Demo를 사용할 때 errinfo=priv map info error라는 오류가 난 경우 어떻게 해야 하나요?
방 입장 관련 매개변수에 오류가 있습니다. SDKAppID, 권한 키를 바꾸었는지 확인하십시오.



### 어떻게 로그 파일을 얻을 수 있나요?
QAVSDK_날짜 포함.log 파일이 로그 파일입니다. 디렉터리는 아래와 같습니다.

| 플랫폼    | 경로                                                         |
| ------- | ------------------------------------------------------------ |
| Windows | %appdata%\Tencent\GME\ProcessName                            |
| iOS     | Application/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/Documents   |
| Android | /sdcard/Android/data/xxx.xxx.xxx/files                       |
| Mac     | /Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents |

### 사운드 렉걸림의 주요 원인은 무엇인가요?
-  **사운드 렉걸림: ** VJ 호스트는 외부 장치를 사용하여 음악을 재생한 다음, 다른 휴대폰을 통해 캡처하고 방송합니다(여기서 렉걸림이 발생하므로 VJ 호스트는 헤드폰 착용을 추천함).
-  **네트워크 렉걸림: **업링크 패킷 손실률이 너무 높거나 업링크 지연 변동이 큰 경우 관중에게 렉걸림이 들립니다.
