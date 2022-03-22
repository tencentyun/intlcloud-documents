[](id:que1)
### Android release 패키지가 일부 메소드를 찾을 수 없다는 오류를 보고하면 어떻게 해야 하나요?
- release 패키지를 인쇄할 때 컴파일 최적화를 활성화한 경우(minifyEnabled를 true로 설정) `no xxx method` 예외입니다.
- 이러한 컴파일 최적화를 활성화한 경우 xmagic 코드가 잘리지 않도록 다음 keep 규칙을 추가합니다.
```java
-keep class com.tencent.xmagic.** { *;}
-keep class org.light.** { *;}
-keep class org.libpag.** { *;}
-keep class org.extra.** { *;}
-keep class org.gyailib.** { *;}
-keep class com.tencent.cloud.iai.lib.** { *;}
```

[](id:que2)
### 호스트 프로젝트에 통합된 Android SDK가 gson 라이브러리 충돌을 보고하면 어떻게 해야 하나요?
호스트 프로젝트의 `build.gradle` 파일에 다음 코드를 추가합니다.

```
Android{
  configurations {
    all*.exclude group: 'com.google.code.gson'
  }
}
```

[](id:que3)
### iOS에서 리소스를 가져온 후 Xcode 12.X에서 컴파일하는 동안 "Building for iOS Simulator, but the linked and embedded framework '.framework'..."가 보고되면 어떻게 해야 하나요?

**Build Settings** > **Build Options**로 이동하여 **Validate Workspace**를 Yes로 변경하고 **실행**을 클릭합니다.
> ? 컴파일이 완료된 후 Yes에서 No로 Validate Workspace를 변경해도 정상적으로 실행됩니다.

[](id:que4)
### 필터 설정이 적용되지 않으면 어떻게 해야 하나요?
값이 올바르게 설정되었는지 확인합니다(값 범위: 0–100). 값을 너무 작게 설정하여 효과가 명확하지 않을 수 있습니다.

[](id:que5)
### iOS Demo 컴파일 중 dSYM이 생성될 때 오류가 보고되면 어떻게 해야 하나요?
- **오류 정보:**
```
PhaseScriptExecution CMake\ PostBuild\ Rules build/XMagicDemo.build/Debug-iphoneos/XMagicDemo.build/Script-81731F743E244CF2B089C1BF.sh
    cd /Users/zhenli/Downloads/xmagic_s106
    /bin/sh -c /Users/zhenli/Downloads/xmagic_s106/build/XMagicDemo.build/Debug-iphoneos/XMagicDemo.build/Script-81731F743E244CF2B089C1BF.sh

Command /bin/sh failed with exit code 1
```
- **문제 분석**: 원인은 `libpag.framework` 및 `Masonary.framework` 재서명 실패입니다.
- **솔루션**:
	1. **demo/copy_framework.sh**를 엽니다.
	2. `$(what cmake)`를 로컬 cmake의 절대 경로로 변경합니다.
	3. 'Apple Development: ......'를 자신의 계정 서명으로 바꿉니다.

[](id:que6)
### iOS Demo에서 홈페이지 인증 오류가 표시되면 어떻게 해야 하나요?
로그에 인쇄된 라이선스 실패 오류 코드를 확인합니다. 로컬 License 파일을 사용 중이라면 해당 파일이 프로젝트에 추가되었는지 확인하세요.

[](id:que7)
### iOS Demo  에서 컴파일 오류가 보고되면 어떻게 해야 하나요?
- **오류 정보:**
```
unexpected service error: build aborted due to an internal error: unable to write manifest to-xxxx-manifest.xcbuild': mkdir(/data, S_IRWXU | S_IRWXG | S_IRWXO): Read-only file system (30):
```
- **솔루션**:
	1. **File** > **Project settings** > **Build System**으로 이동하고 **Legacy Build System**을 선택합니다.
	2. Xcode 13.0++의 경우 **File** > **Workspace Settings**에서 **Do not show a diagnostic issue about build system deprecation**을 선택해야 합니다.


