UGSV SDK License는 UGSV SDK의 사용 권한 활성화에 사용됩니다. 콘솔에서 베타 버전 License를 신청, 연장 및 조회할 수 있습니다. UGSV SDK 기능에 대한 자세한 내용은 [UGSV](https://intl.cloud.tencent.com/document/product/1069/37914)를 참고하십시오.
## 베타 License 신청
베타 License를 신청하여 UGSV SDK 기본 버전에서 제공되는 다양한 기능을 무료로 사용해 볼 수 있습니다. License는 최초 신청 시 14일 동안 유효하며, 1회 무료 연장 시 최대 28일 동안 유효합니다. 신청 단계는 다음과 같습니다.

### 1단계: 베타 License 생성
1. [VOD 콘솔](https://console.cloud.tencent.com/vod/license)에 로그인하고 왼쪽 사이드바에서 [[UGSV SDK License](https://console.cloud.tencent.com/vod/license/video)]를 선택합니다.

2. [편집]을 클릭하여 License 설정 페이지로 이동하여 App Name, Package Name 및 Bundle ID를 입력합니다.

3. [확인]을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/5453b61401859a2599bab6ffcedbf808.png)

### 2단계: 베타 License 저장
무료 베타 License가 성공적으로 생성되면 생성된 License 정보가 페이지에 표시됩니다. 초기 SDK 구성 중에 Key 및 LicenseUrl 두 개의 매개변수를 전달해야 합니다. 다음 정보를 올바르게 저장하십시오.
![](https://qcloudimg.tencent-cloud.cn/raw/1500204df3029e9bbb23aa7161ad94bd.png)

## 베타 License 연장
베타 License의 유효기간은 VOD 콘솔에서 최대 28일까지 연장할 수 있습니다. 신청 후 14일 이내, 즉 베타 License가 만료되기 전에 다음 단계에 따라 License를 연장해야 합니다.
### 1단계: License 연장 신청
[[UGSV SDK License](https://console.cloud.tencent.com/vod/license/video)] 페이지로 이동하여 베타 License 섹션의 오른쪽 상단 모서리에 있는 [연장]을 클릭합니다.

### 2단계: License 연장 완료
연장 성공을 알리는 팝업 창이 표시된 후 오른쪽 상단 모서리에 있는 [연장] 버튼이 사라지고 베타 License가 14일 동안 연장되었음이 나타납니다.


## 베타 License 조회
License 설정 완료 후 잠시 기다리면(네트워크 환경에 따라 다름) 아래와 같은 방법으로 호출하여 License 정보를 확인할 수 있습니다.

- iOS:
```
NSLog(@"%@", [TXUGCBase getLicenceInfo]);
```
- Android:
```
TXUGCBase.getInstance().getLicenceInfo(context);
```

## License 사용 방법
SDK 관련 인터페이스를 호출하기 전에 아래와 같은 방법을 호출하여 License를 설정합니다.

- iOS는 `[AppDelegate application:didFinishLaunchingWithOptions:]`에 다음을 추가할 것을 권장합니다.
```
[TXUGCBase setLicenceURL:LicenceUrl key:Key];
```
- Android는 application에 다음을 추가할 것을 권장합니다.
```
TXUGCBase.getInstance().setLicence(context, LicenceUrl, Key);
```
