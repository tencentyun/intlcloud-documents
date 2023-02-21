본문은 Unity용 Tencent Cloud Game Multimedia Enginec(GME) API에 대한 Unity 프로젝트 내보내기를 구성하는 방법을 설명합니다.

## iOS용으로 내보내기

Unity 프로젝트에서 Xcode 프로젝트로 내보낼 때 GME 동적 라이브러리를 처리해야 하며 처리 방법은 Unity 버전에 따라 다릅니다.

### 1. 동적 라이브러리 처리(Unity 2019 이상 버전)

#### 구성 원리

Editor OnPostprocessBuild 스크립트를 생성하고 UnityEditor.iOS.Xcode.Extensions.PBXProjectExtensions.AddFileToEmbedFrameworks를 사용하면 이 API가 자동으로 동적 라이브러리를 최종 패키지 번들의 프레임워크 디렉터리에 복사하고 서명합니다.

비즈니스 레이어는 필요한 기능에 따라 동적 라이브러리를 삭제할 수 있으며 동적 라이브러리 목록에 따라 예시 코드에서 가져온 프레임워크 목록을 결정할 수 있습니다. 동적 라이브러리 기능은 [동적 라이브러리 디렉터리](https://intl.cloud.tencent.com/document/product/607/32363)를 참고하십시오.

```
string[] framework_names = {
	"libgme_fdkaac.framework",
	"libgme_lamemp3.framework",
	"libgme_ogg.framework",
	"libgme_soundtouch.framework"
};
```


#### 예시 코드

Demo 프로젝트의 add_dylib.cs 스크립트 파일을 참고하여 자신의 프로젝트 요구 사항에 따라 이 부분의 코드를 프로젝트의 Editor 폴더 아래에 넣을 수 있습니다.

```c#
[UnityEditor.Callbacks.PostProcessBuild(1002)]
public  static void OnPostprocessBuild (UnityEditor.BuildTarget BuildTarget, string path){  
	if (BuildTarget == UnityEditor.BuildTarget.iOS) {
		UnityEngine.Debug.Log ("OnPostprocessBuild add_dylib:" + path);
#if UNITY_EDITOR_OSX || UNITY_STANDALONE_OSX
		{
			string projPath = UnityEditor.iOS.Xcode.PBXProject.GetPBXProjectPath (path);  
			UnityEditor.iOS.Xcode.PBXProject proj = new UnityEditor.iOS.Xcode.PBXProject ();  

			proj.ReadFromString (System.IO.File.ReadAllText (projPath));  
			// string targetGuid = proj.TargetGuidByName (UnityEditor.iOS.Xcode.PBXProject.GetUnityTargetName ()); // 2018
			string targetGuid = proj.GetUnityMainTargetGuid();	// 2019
				
			// 가져오기한 framework에 따라 삭제
			string[] framework_names = {
				"libgme_fdkaac.framework",
				"libgme_lamemp3.framework",
				"libgme_ogg.framework",
				"libgme_soundtouch.framework"
			};

			for (int i = 0; i < framework_names.Length; i++)
			{
				string framework_name = framework_names[i];
				string dylibGuid = null;
				dylibGuid = proj.FindFileGuidByProjectPath("Frameworks/Plugins/iOS/" + framework_name);

				if (dylibGuid == null) {
					UnityEngine.Debug.LogWarning (framework_name + " guid not found");
				} else {
					UnityEngine.Debug.LogWarning (framework_name + " guid:" + dylibGuid);
					// proj.AddDynamicFramework (targetGuid, dylibGuid);
					UnityEditor.iOS.Xcode.Extensions.PBXProjectExtensions.AddFileToEmbedFrameworks(proj, targetGuid, dylibGuid);

					proj.AddBuildProperty(targetGuid, "LD_RUNPATH_SEARCH_PATHS", "@executable_path/Frameworks");
					System.IO.File.WriteAllText (projPath, proj.WriteToString ());
				}
			}
		}
#endif
	}
}
```

### 2. 동적 라이브러리 처리(Unity 2019 이하 버전)

현재 Unity 2019 이상 버전에서만 UnityEditor.iOS.Xcode.Extensions를 사용할 수 있으며, Unity 이전 버전인 경우 Unity 상위 버전에서 하위 버전 Unity로 UnityEditor.iOS.Xcode 패키지를 내보내거나 [UnityEditorAV.iOS.XCode.zip](http://dldir1.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.0/Other/UnityEditorAV.iOS.XCode.zip) 첨부 파일을 직접 참고하여 이 파일의 압축을 풀어 프로젝트 디렉터리의 Editor 폴더 아래에 넣습니다.

<img src="https://qcloudimg.tencent-cloud.cn/raw/a141d2c41dc4494148e9451d3d63cd38.png"  width="60%" /></img>

### 3. Xcode 프로젝트 내보내기

Xcode 버전이 10.0 이상인지 확인하고 Unity 에디터에서 Xcode 프로젝트를 내보냅니다.

### 4. BitCode 비활성화

컴파일 중에 다음 오류가 발생하면 Bitcode를 비활성화하십시오. **Targets**>**Build Settings**에서 Bitcode를 검색하고 해당 옵션을 NO로 설정합니다.
<img src="https://main.qcloudimg.com/raw/bcc77d7574e2d1861ca408cdd77dff00.png"  width="60%" /></img>

### 5. iOS에 대한 액세스 추가

- Required background modes: 백그라운드에서 실행을 허용합니다(선택 사항).
- Microphone Usage Description: 마이크에 대한 액세스를 허용합니다.

### 6. 라이브러리 파일 추가

컴파일 중 아래와 같은 오류가 발생하면 라이브러리 파일을 완성하십시오.
<img src="https://main.qcloudimg.com/raw/335c9d806cd2d5fe11b5f6a04a6fad80.png"  width="25%" /></img>
라이브러리 파일 목록은 다음과 같습니다.
```
libc++.tbd
CoreMedia.framework
libresolv.tbd
AVFoundation.framework
Security.framework
CoreAudio.framework
AudioToolbox.framework
libiconv.tbd
libz.tbd
SystemConfiguration.framework
OpenAL.framework
```

### 7. libresolv9.tbd 추가

다음 오류가 발생하는 경우:

<img src="https://main.qcloudimg.com/raw/b8e40f601d9e8c1a62cf88bd10bdd241.png"  width="60%" /></img>

**UnityFramework**에 libresolv9.tbd를 추가합니다.

<img src="https://main.qcloudimg.com/raw/ee0a20a0b0ad99f30fa87855d1b17f0f.jpg"  width="60%" /></img>

### 8. 내보내기 관련 FAQ
내보내기 관련 문제는 [iOS용으로 내보내기](https://intl.cloud.tencent.com/document/product/607/39522)를 참고하십시오.



## Android용으로 내보내기

### 1. 불필요한 lib 파일 삭제

Unity용 GME SDK는 기본적으로 arm64-v8a, armeabi-v7a 및 x86용 lib 파일을 제공합니다. 필요에 따라 불필요한 파일을 삭제하십시오.
<dx-alert infotype="alarm" title="아키텍처 손실">
내보낸 Android 실행 파일에 지정된 아키텍처가 없으면 Crash가 발생합니다.
</dx-alert>
실행 가능한 apk 파일을 내보낸 후 열 때 검은 화면이나 충돌이 발생하는 원인은 일반적으로 해당 아키텍처 lib 파일이 없기 때문입니다. 프로젝트에 따라 해당 아키텍처 lib 파일을 추가하거나 삭제하십시오.

### 2. 권한 구성
**2.1 필수 권한**
프로젝트의 AndroidManifest.xml 파일에 다음 권한을 추가합니다:

```
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
```

**2.2 필요에 따라 권한 추가**
필요에 따라 프로젝트의 AndroidManifest.xml 파일에 다음 권한을 추가합니다:
<dx-tabs>
::: 읽기/쓰기 권한
읽기/쓰기 권한이 필요하지 않습니다. 다음 규칙에 따라 추가 여부를 결정합니다.

- 기본 로그 경로(/sdcard/Android/data/xxx.xxx.xxx/files)를 사용하는 경우 SetLogPath를 호출하지 않으며 WRITE_EXTERNAL_STORAGE 권한이 필요하지 않음을 의미합니다.
- setLogPath API를 호출하여 로그 경로를 외부 저장 장치로 설정하고 음성 메시지 녹음의 저장 경로가 외부 저장 장치인 경우 사용자에게 WRITE_EXTERNAL_STORAGE 권한을 신청하고 사용자의 승인을 받아야 합니다.

```
 <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
```
:::
::: 블루투스 권한
다음 규칙에 따라 블루투스 권한을 추가하십시오.

- 프로젝트의 targetSDKVersion이 v30 이하인 경우:
```
<uses-permission android:name="android.permission.BLUETOOTH"/>
```

- 프로젝트의 targetSDKVersion이 v31 이상인 경우:
```
<uses-permission android:name="android.permission.BLUETOOTH" android:maxSdkVersion="30" />
<uses-permission android:name="android.permission.BLUETOOTH_CONNECT" />
```
:::
</dx-tabs>


### 3. 내보내기 관련 FAQ
내보내기 관련 문제는 [Android용으로 내보내기](https://intl.cloud.tencent.com/document/product/607/39522)를 참고하십시오.


## Windows용으로 내보내기

내보내기 관련 문제는 [Windows용으로 내보내기](https://intl.cloud.tencent.com/document/product/607/39522)를 참고하십시오.


## WebGL용으로 내보내기

### 1. WebGL에서 plugins 구성
WebGL 플랫폼에서 gmesdk와의 충돌을 피하기 위해 Windows 플랫폼에서 gmesdk.dll의 적용 범위를 설정합니다.

<img src="https://qcloudimg.tencent-cloud.cn/raw/18870d8c1a15a496da1dc3fe3e579d45.png"  width="60%" /></img>

<img src="https://qcloudimg.tencent-cloud.cn/raw/4b697ba47fb49484989a1e201f2d7ee6.jpg"  width="60%" /></img>


### 2. Flare Layer 취소(Unity 2018 이상 버전)

<img src="https://qcloudimg.tencent-cloud.cn/raw/894943f084fc5aefc94c709e35d65d0e.png"  width="60%" /></img>

일부 Unity 버전은 MainCamera의 Flare Layer 모드를 더 이상 지원하지 않으므로 패키징할 Scene에서 Flare Layer를 선택 취소해야 합니다. 그렇지 않으면 다음 오류가 보고됩니다.

<img src="https://qcloudimg.tencent-cloud.cn/raw/67506d24d1fef748b9ffbf6654ea27bc.png"  width="60%" /></img>


### 3. 템플릿 선택
WebGL용으로 내보내기 할 때 GME WebGL 템플릿을 선택해야 패키징된 아티팩트가 관련 종속 라이브러리를 올바르게 가져옵니다. 기본적으로 프로젝트는 Unity2018 및 Unity2019 버전을 지원하는 GMEWebGLTemplatesUnity2018 템플릿을 사용합니다. Unity2020 및 Unity2021 버전의 경우 패키징할 때 사용하는 템플릿을 변경하고 패키징에 GMEWebGLTemplatesUnity2021을 사용해야 합니다.
 
<img src="https://qcloudimg.tencent-cloud.cn/raw/def41a1210c286b47ddbe7dbeef1dd19.png"  width="60%" /></img>

### 4. 프런트엔드 라이브러리 가져오기
 
GME-WebGL을 자신의 프로젝트로 가져오고 Unity를 사용하여 해당 웹 페이지를 생성할 때 프런트 엔드 라이브러리를 수동으로 가져와 프런트 엔드 라이브러리 파일을 해당 참조 위치에 배치하고 오디오 태그를 추가해야 합니다(아래 이미지 참고). Unity 아티팩트를 패키징할 때마다 상기 작업을 자동으로 완료하려면 GME-WebGL demo를 참고하여 프로젝트에 해당하는 템플릿을 추가하면 됩니다.

<img src="https://qcloudimg.tencent-cloud.cn/raw/b939e1cd5e331579440c16672a59c2e1.png"  width="60%" /></img>


### 5. 내보내기 관련 FAQ
내보내기 관련 문제는 [Unity-WebGL용으로 내보내기](https://intl.cloud.tencent.com/document/product/607/39522)를 참고하십시오.
