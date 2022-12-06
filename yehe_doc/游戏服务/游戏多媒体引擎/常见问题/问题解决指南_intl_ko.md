이 문서는 개발 중에 발생하는 GME 문제를 해결하는 방법을 설명합니다.

## FAQ
개발 중에 발생하는 일반적인 문제의 경우 유형을 분석하고 다음과 같이 해결할 수 있습니다.

|문서|관련 문제|
|---|----|
|[기능](https://intl.cloud.tencent.com/document/product/607/39520)|플랫폼 호환성과 같은 GME 기능 문제.|
|[과금](https://intl.cloud.tencent.com/document/product/607/30255)|과금 방식 또는 과금 시간에 대한 문의사항.|
|[Demo](https://intl.cloud.tencent.com/document/product/607/39521)|GME의 SampleProject 또는 Demo를 사용할 때 발생하는 문제.|
|[인증](https://intl.cloud.tencent.com/document/product/607/39824)|GME 인증 중에 발생한 문제.|
|[방 입장 실패](https://intl.cloud.tencent.com/document/product/607/39523), [사운드 및 오디오](https://intl.cloud.tencent.com/document/product/607/39524) 및 [네트워크](https://intl.cloud.tencent.com/document/product/607/39519)|GME 음성 채팅 기능을 사용할 때 발생하는 문제.|
|[음성을 텍스트로 변환](https://intl.cloud.tencent.com/document/product/607/39716)|음성-텍스트 변환 기능을 사용할 때 발생하는 문제.|
| [프로그램 내보내기](https://intl.cloud.tencent.com/document/product/607/39522)|각 플랫폼에서 애플리케이션을 (실제 장치로) 내보낼 때 발생하는 문제.|


## 개발 문제

개발 중 기능 문제가 발생하면 먼저 반환되는 에러 코드를 기반으로 문제를 식별할 수 있습니다. 에러 코드를 기반으로 문제를 해결할 수 없는 경우 [티켓 제출](https://console.tencentcloud.com/workorder/category)을 통해 GME 개발자에게 연락하여 오류 분석 및 문제 해결에 도움을 받을 수 있습니다.


### 에러 코드

GME [에러 코드](https://intl.cloud.tencent.com/document/product/607/33223) 문서에서 에러 코드 값과 에러 코드별 원인 및 솔루션을 확인할 수 있습니다.


### 로그를 어떤 방식으로 획득하나요?

로그를 제공할 때 문제가 발생한 시점과 수신측(청취자)과 발신측(발언자)의 로그도 함께 명시해 주시기 바랍니다.

**로그 경로**
로그는 모두 `QAVSDK_` date `.log` 형식으로 이름이 지정되며 다음 디렉터리에서 찾을 수 있습니다.

| 플랫폼    | 경로                                                         |
| ------- | ------------------------------------------------------------ |
| Windows | `%appdata%\GMEGLOBAL\GME\processName`                            |
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


**로그 암호화**

현재 GME 로그는 기본적으로 암호화됩니다. 다음 API를 호출하여 로그 암호화를 비활성화할 수 있습니다. 개발 중에는 로그 암호화를 비활성화하고 애플리케이션 출시 전에 활성화하는 것이 좋습니다. 이 API는 init 전에 호출해야 합니다.

```
SetAdvanceParams("DisableEncryptLog", "1");
```

|매개변수|의미|
|--|--|
| 매개변수1 | "DisableEncryptLog" 입력, 암호화 관련 기능 비활성화 |
| 매개변수2 | "1": 로그 암호화 비활성화, “0”: 로그 암호화 활성화 |


## 크래쉬 문제


크래쉬가 발생하면 먼저 [프로그램 내보내기](https://intl.cloud.tencent.com/document/product/607/39522)의 지침에 따라 문제를 해결하십시오. 문제가 지속되면 스택을 GME 개발자에게 제공하여 도움을 받으십시오.
- 타사 예외 리포트 플러그인을 연결한 경우 GME 개발자에게 연락하여 크래쉬된 스택에 대한 링크를 공유할 수 있습니다.
- iOS 또는 Android의 경우 장치를 PC에 연결하고 AndroidStudio에서 Xcode 또는 LogCat을 사용하여 크래쉬된 스택을 가져와 복제하고 GME 개발자에게 제공할 수 있습니다.
- Windows의 경우 DUMP 파일을 제공합니다.
