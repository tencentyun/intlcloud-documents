## 기능 설명
IM SDK를 초기화한 후 SDK 로그인 API를 호출하여 계정을 인증해야 메시지, 대화 및 기타 기능을 사용할 수 있습니다.

<dx-alert infotype="notice" title="">
대화 가져오기 API만 로그인 API 호출 직후 호출이 가능하며, 그 외 API는 SDK에 성공적으로 로그인한 이후에만 호출이 가능합니다. 따라서 다른 기능을 사용하기 전에 **성공적으로 로그인했는지 확인하십시오**. 그렇지 않으면 이러한 기능이 비정상이 되거나 사용할 수 없게 될 수 있습니다!
</dx-alert>


## 로그인
로그인에 성공하면 자동으로 가입되므로 처음 로그인할 때 가입할 필요가 없습니다.
`login`([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/login.html)) API를 호출하여 로그인합니다.

`login` API의 주요 매개변수는 다음과 같습니다.

| 매개변수 | 의미             | 설명                                                         |
| -------- | ---------------- | ------------------------------------------------------------ |
| UserID   | 고유한 사용자 ID | 최대 32바이트의 영어(a-z 및 A-Z), 숫자(0-9), 언더바(_) 및 하이픈(-)을 포함할 수 있습니다. |
| UserSig  | 로그인 티켓      | 보안을 위해 비즈니스 서버에서 계산합니다. 자세한 내용은 [UserSig 생성하기](https://intl.cloud.tencent.com/document/product/1047/34385)를 참고하십시오. |

다음 시나리오에서 `login` API를 호출할 수 있습니다.
* App이 시작된 후 처음으로 IM SDK의 기능을 사용합니다.
* 로그인 시 티켓 만료: `login` API의 콜백은 `ERR_USER_SIG_EXPIRED(6206)` 또는 `ERR_SVR_ACCOUNT_USERSIG_EXPIRED(70001)` 에러 코드를 반환합니다. 이 경우 다시 로그인하려면 새 userSig를 생성해야 합니다.
* 사용자가 온라인 상태일 때 티켓이 만료됩니다. 사용자가 온라인 상태일 때 `onUserSigExpired`([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Class/Listener/V2TimSDKListener.html?h=onUserSigExpired)) 콜백을 수신할 수 있습니다. 이 경우 다시 로그인하려면 새 userSig를 생성해야 합니다.
* 사용자가 강제 오프라인 됨: 사용자가 강제 오프라인되면 IM SDK는 `onKickedOffline`([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Class/Listener/V2TimSDKListener.html?h=onKickedOffline)) 콜백을 통해 알려줍니다. 이 경우 사용자에게 메시지를 표시하고 `login`을 호출하여 다시 로그인할 수 있습니다.

다음 시나리오에서는 `login` API를 호출할 필요가 없습니다.
* 사용자 네트워크가 연결 해제되었다가 다시 연결되면 IM SDK가 자동으로 온라인 상태가 되므로 `login` 함수를 호출할 필요가 없습니다.
* 로그인 프로세스가 실행 중입니다.

>?
>1. IM SDK API를 호출하고 성공적으로 로그인하면 DAU 계산이 시작됩니다. 따라서 높은 DAU를 피하기 위해 필요에 따라 로그인 API를 호출하십시오.
>2. 동일한 App의 여러 IM SDK 계정에 동시에 로그인할 수 없습니다. 그렇지 않으면 마지막으로 로그인한 계정만 온라인 상태가 됩니다.

예시 코드는 다음과 같습니다.[](id:login_code)


```dart
String userID = "your user id";
String userSig = "userSig from your server";
V2TimCallback res = await TencentImSDKPlugin.v2TIMManager.login(userID: userID, userSig: userSig);
if(res.code == 0){
	// 로그인 성공 로직
}else{
 	// 로그인 실패 로직
}
```


### 사용자 ID 가져오기

성공적으로 로그인한 후 `getLoginUser`([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/getLoginUser.html))를 호출하여 UserID를 가져옵니다.
로그인에 실패하면 UserID는 비어 있습니다.

예시 코드는 다음과 같습니다.


```dart
    // 사용자 로그인 성공 후 호출 가능
    // getLoginUser 호출하여 로그인에 성공한 UserID 가져오기
    V2TimValueCallback<String> getLoginUserRes =
        await TencentImSDKPlugin.v2TIMManager.getLoginUser();
    if (getLoginUserRes.code == 0) {
      //가져오기 성공
      getLoginUserRes.data; // getLoginUserRes.data는 쿼리된 로그인 UserID
    }
```



### 로그인 상태 가져오기

`getLoginStatus`([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/getLoginStatus.html))를 호출하여 로그인 상태를 가져옵니다. 사용자가 로그인되었거나 로그인 중인 경우 로그인 API를 자주 호출하지 마십시오. IM SDK는 다음 로그인 상태를 지원합니다.

| 로그인 상태               | 설명            |
| ------------------------- | --------------- |
| V2TIM_STATUS_LOGINED (1)  | 로그인 됨       |
| V2TIM_STATUS_LOGINING (2) | 로그인 중       |
| V2TIM_STATUS_LOGOUT (3)   | 로그인하지 않음 |

예시 코드는 다음과 같습니다.


```dart
    // 사용자 로그인 성공 후 호출 가능
    // getLoginStatus 호출하여 로그인에 성공한 사용자 상태 가져오기
    V2TimValueCallback<int> getLoginStatusRes =
        await TencentImSDKPlugin.v2TIMManager.getLoginStatus();
    if (getLoginStatusRes.code == 0) {
      int? status = getLoginStatusRes.data; // getLoginStatusRes.data는 사용자 로그인 상태 값
      if (status == 1) {
        // 로그인 됨
      } else if (status == 2) {
        // 로그인 중
      } else if (status == 3) {
        // 로그인하지 않음
      }
    }
```



## 멀티 클라이언트 로그인 및 킥아웃
Tencent Cloud 콘솔에서 IM SDK에 대한 멀티 클라이언트 로그인 정책을 구성할 수 있습니다.
사용자가 ‘모바일 또는 데스크톱 플랫폼+Web 플랫폼에서 동시에 온라인 상태’일 수 있거나 사용자가 ‘모든 플랫폼에서 동시에 온라인 상태’일 수 있는 것과 같은 여러 멀티 클라이언트 로그인 정책이 있습니다.
구성에 대한 자세한 내용은 [기능 구성](https://intl.cloud.tencent.com/document/product/1047/34419)을 참고하십시오.

Tencent Cloud 콘솔에서 IM SDK에 대한 사용자당 플랫폼별 최대 로그인 인스턴스 수, 즉 동시에 온라인 상태가 될 수 있는 동일한 플랫폼의 최대 인스턴스 수를 구성할 수 있습니다.
이 기능은 Ultimate 버전에서만 사용할 수 있습니다. 사용자는 Web 플랫폼에서 최대 10개의 클라이언트 또는 Android, iPhone, iPad, Windows 또는 Mac 플랫폼에서 최대 3개의 클라이언트에서 동시에 온라인 상태일 수 있습니다(Flutter에서 동시에 온라인 상태가 될 수 있는 최대 클라이언트 수는 실제 컴파일 결과에 따라 달라짐).
구성에 대한 자세한 내용은 [기능 구성](https://intl.cloud.tencent.com/document/product/1047/34419)을 참고하십시오.

`login`([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/login.html)) API를 호출하여 로그인할 때 계정에 대한 멀티 클라이언트 로그인 정책에 지정된 제한을 초과하면 새로 로그인한 인스턴스가 이전 인스턴스를 킥아웃합니다.
킥아웃된 측은 `onKickedOffline`([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Class/Listener/V2TimSDKListener.html?h=onKickedOffline)) 콜백을 받게 됩니다.


## 로그아웃
일반적으로 애플리케이션의 라이프사이클이 IM SDK의 라이프사이클과 동일한 경우 애플리케이션을 종료하기 전에 로그아웃할 필요가 없습니다.
특별한 경우, 예를 들어 특정 UI 진입 후 IM SDK를 사용하고 UI 종료 후 더 이상 사용하지 않는 경우 `logout`([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/logout.html)) API를 호출하여 SDK에서 로그아웃하면 더 이상 새 메시지를 받을 수 없습니다. 이 경우 SDK를 초기화 취소하려면 로그아웃 후 `unInitSDK`([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/unInitSDK.html))도 호출해야 합니다.

예시 코드는 다음과 같습니다.


```dart
V2TimCallback logoutRes = await TencentImSDKPlugin.v2TIMManager.logout();
if(logoutRes.code == 0){

}
```


## 계정 전환
애플리케이션에서 계정 간에 전환하려면 `login`([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/login.html))을 호출합니다.

예를 들어 로그인한 사용자를 alice에서 bob으로 전환하려면 login bob 하기만 하면 됩니다. [login](#login_code) bob 전에 logout alice를 명시적으로 호출할 필요가 없습니다. 이 작업은 IM SDK 내에서 자동으로 처리되기 때문입니다.
