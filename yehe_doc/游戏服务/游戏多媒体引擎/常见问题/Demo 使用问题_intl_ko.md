
### GME Demo 및 SDK는 어디에서 다운로드할 수 있습니까?

[SDK Download Guide](https://intl.cloud.tencent.com/document/product/607/18521)를 참고하십시오. GME는 Unity, Cocos2d, Android(네이티브) 및 iOS(네이티브)에 대한 Demo를 제공합니다.

### GME의 Windows Demo에서 지원되는 VS 버전은 무엇입니까?
VS2015를 권장합니다. VS2010을 사용하려면 프로젝트를 직접 다운그레이드해야 합니다.

### GME Demo에서 본인 계정을 사용하려면 어떻게 해야 합니까?

- [GME 콘솔](https://console.cloud.tencent.com/gamegme/detail/1400391524)로 이동하여 서비스 관리에서 AppID와 키를 가져옵니다.
- AVChatViewController의 GetAuthBuffer에서 음성 채팅용  Key를 수정합니다.

### GME는 여러 장치에서 하나의 OpenId만 사용할 수 있습니까?

OpenId는 사용자의 고유 ID입니다. 여러 장치 로그인과 같이 여러 장치에서 동일한 OpenId를 사용하는 경우 로그인 실패의 원인이 될 수 있습니다.

### 방에 혼자 있는 경우 효과를 어떻게 경험할 수 있나요?

다른 장치에서 demo를 사용하여 같은 방에 입장하십시오.

### Demo를 사용할 때 errinfo=priv map info error 오류 메시지가 표시되면 어떻게 해야 합니까?

방 액세스 매개변수에 오류가 발생하면 SDKAppID와 액세스 키가 지시에 따라 교체되었는지 확인하십시오.

### 다운로드한 Demo는 어떻게 사용합니까?

- Demo 사용 설명서를 참고하십시오.
- Unity Demo 사용자의 경우 [Unity Demo 사용](https://intl.cloud.tencent.com/document/product/607/38535)을 참고하십시오.

### Unity에서 내보낸 Demo가 사용될 때 종종 음소거되는 이유는 무엇입니까?
OnApplicationFocus는 Unity Demo에서 구성됩니다. 프로그램이 포커스를 잃으면 사운드가 Pause됩니다. 백그라운드에서 사운드를 재생해야 하는 경우 Pause API를 호출하는 코드를 제거하십시오.

### 로그를 어떤 방식으로 획득하나요?

**문제 해결을 위해 로그 및 발생 시간도 함께 제공하십시오**
로그는 모두 `QAVSDK_` date `.log` 형식으로 이름이 지정되며 다음 디렉터리에서 찾을 수 있습니다.

| 플랫폼    | 경로                                                         |
| ------- | ------------------------------------------------------------ |
| Windows | `%appdata%\Tencent\GMEGLOBAL\ProcessName`                            |
| iOS     | `Application/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/Documents`   |
| Android | `/sdcard/Android/data/xxx.xxx.xxx/files`                       |
| Mac     | `/Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents` |

Unity 엔진을 사용하고 PC에서 개발 중인 경우 `%appdata%\Tencent\GME\Unity.exe`에서 로그를 찾아보십시오.

iOS 기기에서는 다음과 같이 파일 공유를 지원하는 애플리케이션을 통해 로그를 얻을 수 있습니다.
1. UIFileSharingEnabled 키를 애플리케이션의 `Info.plist` 파일에 추가하고 키 값을 ‘YES’로 설정합니다.
2. 애플리케이션의 Documents 디렉터리에 공유할 파일을 배치합니다.
3. 장치가 사용자의 컴퓨터에 연결되면 iTunes는 선택한 장치의 Apps 탭에 File Sharing 영역을 표시합니다.
4. 사용자는 디렉터리에 파일을 추가하거나 데스크탑 컴퓨터로 파일을 드래그할 수 있습니다.

>?GME SDK 2.8.4 및 이전 버전의 경우 Windows 장치의 로그는 `%appdata%\Tencent\GME\ProcessName`에 저장됩니다.

**로그 출력 레벨**

로그 제공 시 SetLogLevel을 호출한 경우 기본 로그 출력 레벨을 복구하는 것이 좋습니다.
