
## iOS용으로 내보내기
### `GMESDK.framework` 라이브러리를 추가한 후 Xcode에서 실행 파일을 내보내려고 할 때 컴파일 중에 오류가 발생하면 어떻게 해야 합니까?

프로그램 파일에서 Build Setting을 선택하고 "Other Linker Flags"에서 ‘-all_load’ 플래그가 사용되는지 확인하십시오. 그렇다면 삭제하고 프로그램을 다시 컴파일하십시오.


### Unity를 사용하여 Xcode 프로그램을 내보낸 후 `framework not found GMESDK` 오류 프레임워크가 나타납니다.

Unity 엔진을 사용하려면 GME Unity SDK를 통합하고 framework 파일 대신 `libGMESDK.a` 라이브러리를 사용하십시오.

### Unity용 SDK에서 iOS 실행 파일을 내보내려고 하면 armv7 관련 오류가 발생했지만 armv7을 삭제한 후 내보내기가 제대로 작동했습니다.

- Unity를 업그레이드하는 것이 좋습니다. 자세한 내용은 [Unity 포럼](https://forum.unity.com/threads/undefined-symbols-for-architecture-armv7-query_call_back-callback_func_type.830544/#post-5590516)을 참고하십시오.
- 업그레이드가 필요하지 않은 경우 armv7 아키텍처를 패키징할 필요가 없습니다.

### 다운로드한 iOS용 Demo를 실행할 수 없으면 어떻게 해야 합니까?

iOS용 공식 Demo를 다운로드한 후 Xcode(v10 이상)를 통해 컴파일하는 동안 `ld: warning: directory not found for option`과 유사한 오류가 발생할 경우, 수동으로 Demo 폴더와 동일한 수준의 ‘GME_SDK’ 폴더에 있는 ‘GMESDK.framework’ 파일을 프로그램의 Framework 목록에 추가해야 합니다.


### iOS용 SDK는 시뮬레이터에서 디버깅을 지원합니까?

지원합니다. [최신 버전](https://intl.cloud.tencent.com/document/product/607/18521)을 사용하십시오.

### Demo 내보내기 중 발생한 인증서 오류를 수정하는 방법은 무엇입니까?
에러 메시지:
```
Showing Recent Messages:-1: Unity-iPhone has conflicting provisioning settings. Unity-iPhone is automatically signed, but code signing identity iPhone Distribution: Tencent Technology (Shenzhen) Co., Ltd has been manually specified. Set the code signing identity value to "iPhone Developer" in the build settings editor, or switch to manual signing in the project editor. (in target 'Unity-iPhone')
```
솔루션:
Tencent Cloud 엔터프라이즈 인증서를 개발자 인증서로 교체하십시오.


### 데모를 장치로 내보낼 때 아래 오류가 발생합니다.
에러 메시지:
```
dyld: Library not loaded: @rpath/libLamemp3.framework/libLamemp3
Referenced from: /private/var/containers/Bundle/Application/XXXX
Reason: image not found
dyld: launch, loading dependent libraries
DYLD_LIBRARY_PATH=/usr/lib/system/introspection
DYLD_INSERT_LIBRARIES=/Developer/usr/lib/libBacktraceRecording.dylib:/Developer/usr/lib/libMainThreadChecker.dylib:/Developer/Library/PrivateFrameworks/DTDDISupport.framework/libViewDebuggerSupport.dylib
```
솔루션:
- 동적 라이브러리를 사용하는 경우 로딩된 동적 라이브러리는 기본적으로 정적 라이브러리 `Linked Frameworks and Libraries` 아래에 있습니다. 선택하고 `-` 아이콘을 클릭하여 삭제한 다음 `Embedded Binaries` 아래의 `+`를 클릭하여 동적 라이브러리를 추가해야 합니다.
- framework를 아래와 같이 수정할 수도 있습니다.
![](https://main.qcloudimg.com/raw/fe01a75aba37436d4cae1dd68b3b9640.jpg)


## Windows용 내보내기

### Unity용 Demo를 다운로드하고 PC용 실행 파일을 내보낼 때 오류가 발생합니다.

`Found plugins with same names and architectures`와 유사한 오류가 발생하는 경우 기본적으로 GME SDK를 x86 및 x86_64 아키텍처 모두에서 사용할 수 있기 때문입니다. plugins 폴더에서 두 SDK 중 하나를 삭제하십시오.


### Unreal용 Demo를 다운로드하고 PC용 실행 파일을 내보낼 때 dll 파일을 찾을 수 없으면 어떻게 해야 합니까?

Windows x64를 예로 들어 보겠습니다. 실행 파일을 내보낸 후 `UEDemo1\Plugins\GMESDK\Source\ThirdParty\GMESDKLibrary\x64` 디렉터리의 모든 dll 파일을 실행 파일(.exe)과 동일한 디렉터리에 복사해야 합니다.

## Android용으로 내보내기

### GME SDK를 통합하고 Apk 파일을 내보낸 후 애플리케이션을 열려고 하면 화면이 검게 변하는 경우 어떻게 해야 하나요?

일부 lib 파일이 누락되었을 수 있습니다. Apk 파일의 압축을 풀고 lib 아래의 각 폴더에 모든 라이브러리 파일이 있는지 확인하십시오.

### Apk를 Android 휴대폰으로 내보낸 후 App을 열면 해당 앱이 기기에서 지원되지 않는다는 오류 메시지가 나타납니다.

오류는 패키지된 실행 파일에 포함된 아키텍처와 관련이 있습니다. v8a 아키텍처가 필요하지 않은 경우 Unity 프로그램 구성의 내보내기 표시줄에서 선택을 ‘취소’할 수 있습니다.

### 내보낸 Apk가 시뮬레이터를 지원하지 않습니다.

내보내기한 Apk에 x86 아키텍처 SDK가 포함된 라이브러리 파일이 있는지 확인하십시오. 그렇지 않은 경우 SDK를 다시 다운로드하고 x86 아키텍처 SDK를 가져온 다음 마지막으로 실행 파일을 다시 내보내십시오.




## Unity-WebGL 내보내기 문제

### Unity-WebGL 플랫폼은 https 프로토콜과 http 프로토콜 중 어떤 것을 사용합니까?
패키징된 제품은 **https 프로토콜**을 통해 배포해야 하며 http 프로토콜을 사용하여 서버에 배포하면 기능이 비정상적으로 작동합니다.

### Unity-WebGL 플랫폼 패키징 후 방 입장 시 1004 오류가 발생합니다.
방 입장 시 1004(Invalid Argument) 오류가 발생하면 이는 입력한 Openid가 10000보다 작기 때문입니다. 여기에는 **Openid가 10000보다 큰 값**을 입력해야 합니다.

### Unity-WebGL 플랫폼을 패키징한 후 휴대폰에서 사용할 수 있나요?
Unity의 공식 웹 사이트에 따르면 Unity-WebGL로 패키징된 제품은 당분간 휴대폰 실행을 지원하지 않습니다. 자세한 내용은 [Unity - Manual: WebGL Browser Compatibility (unity3d.com)](https://docs.unity3d.com/2020.1/Documentation/Manual/webgl-browsercompatibility.html)를 참고하십시오.

### Unity-WebGL 플랫폼 패키징 후 GME의 레인지 보이스 기능을 사용할 수 있나요?
현재 WebGL 플랫폼에서는 방 입퇴장 및 마이크 on/off와 같은 가장 기본적인 실시간 음성 통화 기능만 지원됩니다. 지원되지 않는 기능에 대한 API를 호출하면 오류 코드 1006이 반환됩니다. 레인지 보이스 기능은 현재 WebGL 플랫폼에 맞게 조정되고 있습니다.
