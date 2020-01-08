### Game Multimedia Engine(GME) Demo와 SDK는 어디서 다운로드하나요?

[다운로드 매뉴얼](https://intl.cloud.tencent.com/document/product/607/18521)에서 관련 Demo와 SDK를 다운로드할 수 있습니다. 현재 홈페이지에 Unity 엔진 Demo, Cocos2D 엔진 Demo, Android 오리지널 개발 Demo 및 iOS 오리지널 개발 Demo가 있습니다.

### GME DEMO를 다운로드 후, 내가 신청한 계정으로 변경할 수 있나요?
- 네. 콘솔에서 sdkappid, 권한 보안키 등 2종 계정을 획득하시면 됩니다.
- 클라이언트가 스스로 신청한 appid를 적용하려면 AVChatViewController의 GetAuthBuffer에서 실시간 음성 Key를 수정해야 합니다. 

### Demo를 사용 시에 errinfo=priv map info error 에러가 뜹니다. 어떡해야 할까요?
방에 입장하는 파라미터에 오류가 존재합니다. sdkappid, 권한 보안키를 교체하였는지 체크하시기 바랍니다.



### 로그를 어떤 방식으로 획득하나요?
QAVSDK_일자 적용.log, 이 파일은 로그 파일입니다. 목록은 다음과 같습니다: 

| 플랫폼    | 경로                                                         |
| ------- | ------------------------------------------------------------ |
| Windows | %appdata%\Tencent\GME\ProcessName                            |
| iOS     | Application/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/Documents   |
| Android | /sdcard/Android/data/xxx.xxx.xxx/files                       |
| Mac     | /Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents |

### 사운드 랙의 주요 원인은 무엇인가요?
-  **뮤직 랙: **BJ가 뮤직을 파워 앰프리파이어하고 다른 모바일을 통해 수집 및 방송(이때 무조건 랙이 나타나며, BJ가 이어폰을 착용할것을 권장드립니다)하는 경우에 나타납니다. 
-  **네트워크 랙: **업스트림 패킷 손실률이 지나치게 높거나 업스트림 딜레이 파동이 클 경우 관중들은 랙을 듣게 됩니다. 


### iOS Demo를 다운로드 후 작동 불가
공식 iOS Demo를 다운로드하면, Xcode(10이상 버전)를 컴파일할 경우 “ld: warning: directory not found for option” 에러가 나타납니다. 수동으로 Demo 동급 디렉터리의 “GME_SDK” 파일 폴더에 위치한 “GMESDK.framework” 파일을 프로그램의 Framework 리스트에 추가해야 합니다. 


### Unity Demo를 다운로드하여 실행가능한 파일을 출력 시에 에러가 뜹니다
사용 과정에 Found plugins with same names and architectures 과 유사한 에러가 뜨는 것은, GME SDK는 기본적으로 x86 아키키텍처의 SDK버전과 x86_64 아키텍처의 SDK 버전을 제공하기 때문입니다. plugins 폴더에서 1종을 삭제하십시오.