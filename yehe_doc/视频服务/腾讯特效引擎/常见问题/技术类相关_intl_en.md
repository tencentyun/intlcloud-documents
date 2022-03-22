[](id:que1)
### What should I do if the `release` package on Android reports an error that some methods are not found?
- If you have enabled compilation optimization (by setting `minifyEnabled` to `true`) when printing the `release` package, some code that is not called at the Java layer will be trimmed out and may be called at the native layer, causing a `no xxx method` exception.
- If you have enabled such compilation optimization, add the following `keep` rules to prevent xMagic code from being trimmed out:
```java
-keep class com.tencent.xmagic.** { *;}
-keep class org.light.** { *;}
-keep class org.libpag.** { *;}
-keep class org.extra.** { *;}
-keep class org.gyailib.** { *;}
-keep class com.tencent.cloud.iai.lib.** { *;}
```

[](id:que2)
### What should I do if the SDK for Android integrated to the host project reports a `gson` library conflict?
Add the following code to the `build.gradle` file of the host project:

```
Android{
  configurations {
    all*.exclude group: 'com.google.code.gson'
  }
}
```

[](id:que3)
### What should I do if "Building for iOS Simulator, but the linked and embedded framework '.framework'..." is reported during compilation by Xcode 12.X after resources are imported on iOS?

Go to **Build Settings** > **Build Options**, change **Validate Workspace** to **Yes**, and click **Run**.
> ? Note that the execution will also be normal if you change **Validate Workspace** from **Yes** to **No** after the compilation is completed.

[](id:que4)
### What should I do if the filter settings don't take effect?
Check whether the value is set properly (value range: 0–100). You may have set too small a value so the effect is not obvious.

[](id:que5)
### What should I do if an error is reported when `dSYM` is generated during demo compilation on iOS?
- **Error information:**
```
PhaseScriptExecution CMake\ PostBuild\ Rules build/XMagicDemo.build/Debug-iphoneos/XMagicDemo.build/Script-81731F743E244CF2B089C1BF.sh
    cd /Users/zhenli/Downloads/xmagic_s106
    /bin/sh -c /Users/zhenli/Downloads/xmagic_s106/build/XMagicDemo.build/Debug-iphoneos/XMagicDemo.build/Script-81731F743E244CF2B089C1BF.sh

Command /bin/sh failed with exit code 1
```
- **Problem analysis**: the cause is the failure to sign `libpag.framework` and `Masonary.framework` again.
- **Solution**:
	1. Open **demo/copy_framework.sh**.
	2. Change `$(which cmake)` to the absolute path of the local `cmake`.
	3. Replace `Apple Development: ......` with your own account signature.

[](id:que6)
### What should I do if the homepage shows an authorization error in the demo for iOS?
Check the license failure error code printed in the log. If you are using a local license file, check whether the file has been added to the project.

[](id:que7)
### What should I do if the demo for iOS reports a compilation error?
- **Error information:**
```
unexpected service error: build aborted due to an internal error: unable to write manifest to-xxxx-manifest.xcbuild': mkdir(/data, S_IRWXU | S_IRWXG | S_IRWXO): Read-only file system (30):
```
- **Solution**:
	1. Go to **File** > **Project settings** > **Build System** and select **Legacy Build System**.
	2. For Xcode 13.0++, you need to select **File** > **Workspace Settings** > **Do not show a diagnostic issue about build system deprecation**.


