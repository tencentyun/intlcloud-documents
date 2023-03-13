
### GME Sample Project 및 SDK는 어디에서 다운로드할 수 있습니까?

GME 관련 Sample Project 및 SDK 다운로드에 대한 자세한 내용은 [다운로드 가이드](https://intl.cloud.tencent.com/document/product/607/18521)를 참고하십시오. GME는 Unity, Unreal, Cocos2d, Android, iOS, Windows, macOS(네이티브), web(네이티브)용 Sample Project를 제공합니다.

### GME의 Windows Sample Project에서 지원되는 VS 버전은 무엇입니까?
VS2015를 권장합니다. VS2010을 사용하려면 프로젝트를 직접 다운그레이드해야 합니다.

### GME Sample Project에서 내 계정을 어떻게 사용할 수 있습니까?

- 콘솔 [서비스 관리-애플리케이션 설정](https://console.cloud.tencent.com/gamegme)에서 AppID 및 권한 키를 가져옵니다.
- AVChatViewController의 GetAuthBuffer에서 음성 채팅용  Key를 수정합니다.


### GME에서 여러 사용자가 동일한 OpenID를 사용하면 영향이 있을까요?
GME 엔진을 초기화할 때 OpenID를 사용하며, OpenID는 애플리케이션 내에서 사용자의 고유 식별자입니다. 여러 기기에서 동시에 하나의 OpenID를 사용하는 경우, 예를 들어 지역이 다른 여러 기기에서 로그인하는 경우 계정 비정상적인 작동이나 GME 기능을 정상적으로 사용할 수 없는 문제가 발생할 수 있습니다.

### 방에 한 사람만 있을 때, 로컬에서 경험할 수 있는 방법은 무엇인가요?

다른 단말기에서 Sample Project를 사용하여 동일한 방에 입장하면 됩니다.

### Sample Project를 사용할 때 errinfo=priv map info error 오류가 발생하는 경우 어떻게 해야 하나요?

방 액세스 매개변수에 오류가 발생하면 SDKAppID와 액세스 키가 지시에 따라 교체되었는지 확인하십시오.

### 다운로드한 Sample Project 또는 Demo를 어떻게 사용하나요?

- [Demo 사용 문서](https://www.tencentcloud.com/document/product/607/39154)를 참고하십시오.
- Unity Demo 사용자의 경우 [Unity Demo 사용](https://intl.cloud.tencent.com/document/product/607/50219)을 참고하십시오.

### Unity로 내보낸 Sample Project를 사용할 때 왜 종종 소리가 안나오나요?
OnApplicationFocus는 Unity Sample Projec에서 구성됩니다. 프로그램이 포커스를 잃으면 사운드가 Pause됩니다. 백그라운드에서 사운드를 재생해야 하는 경우 Pause API를 호출하는 코드를 제거하십시오.

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
4. 사용자는 디렉터리에 파일을 추가하거나 데스크톱 컴퓨터로 파일을 드래그할 수 있습니다.

>?GME SDK 2.8.4 및 이전 버전의 경우 Windows 장치의 로그는 `%appdata%\Tencent\GME\ProcessName`에 저장됩니다.

**로그 출력 레벨**

로그 제공 시 SetLogLevel을 호출한 경우 기본 로그 출력 레벨을 복구하는 것이 좋습니다.


### GME Unity SDK는 어떤 Unity 버전을 지원하나요?
GME Unity SDK에서 지원하는 Unity에는 버전 제한이 없습니다.



### GME Android의 so 데이터베이스에 armv8가 있습니까?
있습니다. 2.3.5버전에서 지원됩니다.


### Android용 so 라이브러리는 x86_64 버전을 제공합니까?
제공하지 않습니다.
