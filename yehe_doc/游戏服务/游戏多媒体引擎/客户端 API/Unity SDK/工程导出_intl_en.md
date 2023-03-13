This document describes how to configure a Unity project export for the GME APIs for Unity.

## Export for iOS

When exporting a Unity project as an Xcode project, you need to process GME dynamic libraries. The processing steps vary by Unity version.

### 1. Process dynamic libraries (for Unity 2019 or later)

#### Configuration principle

Create an `Editor OnPostprocessBuild` script and use the `UnityEditor.iOS.Xcode.Extensions.PBXProjectExtensions.AddFileToEmbedFrameworks` API, which will automatically copy the dynamic libraries to the `framework` directory of the final output bundle and sign them.

You can add or remove dynamic libraries based on the required features and determine the list of imported frameworks in the sample code based on the dynamic library list. For more information on dynamic library features, see [SDK Version Upgrade Guide](https://intl.cloud.tencent.com/document/product/607/32363).

```
string[] framework_names = {
	"libgme_fdkaac.framework",
	"libgme_lamemp3.framework",
	"libgme_ogg.framework",
	"libgme_soundtouch.framework"
};
```


#### Sample code

You can refer to the `add_dylib.cs` script file in the demo project and put this part of code in the `Editor` folder of the project as needed.

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
				
			// Delete according to the imported frameworks
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

### 2. Process dynamic libraries (for Unity versions earlier than 2019)

Currently, only Unity 2019 or later can use `UnityEditor.iOS.Xcode.Extensions`. You can export the `UnityEditor.iOS.Xcode` package from a later version for use in an earlier version, or directly decompress the attachment [UnityEditorAV.iOS.XCode.zip](http://dldir1.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.0/Other/UnityEditorAV.iOS.XCode.zip) and place it in the `Editor` folder of the project directory.

<img src="https://qcloudimg.tencent-cloud.cn/raw/a141d2c41dc4494148e9451d3d63cd38.png"  width="60%" /></img>

### 3. Export the Xcode project

Make sure that the Xcode version is 10.0 or later. Export the Xcode project from the Unity Editor.

### 4. Disable Bitcode

If the following error occurs during the compilation, disable Bitcode. Search for Bitcode in **Targets** > **Build Settings** and set the corresponding option to `NO`.
<img src="https://main.qcloudimg.com/raw/bcc77d7574e2d1861ca408cdd77dff00.png"  width="60%" /></img>

### 5. Add access to iOS

- Required background modes: Allows running in the background (optional).
- Microphone Usage Description: Allows access to microphone.

### 6. Add library files

If the following error occurs during compilation, please complete the library files.
<img src="https://main.qcloudimg.com/raw/335c9d806cd2d5fe11b5f6a04a6fad80.png"  width="25%" /></img>
The list of library files is as follows:
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

### 7. Add `libresolv9.tbd`

If the following error occurs:

<img src="https://main.qcloudimg.com/raw/b8e40f601d9e8c1a62cf88bd10bdd241.png"  width="60%" /></img>

Add `libresolv9.tbd` to **UnityFramework**.

<img src="https://main.qcloudimg.com/raw/ee0a20a0b0ad99f30fa87855d1b17f0f.jpg"  width="60%" /></img>

### 8. FAQs about export
If you have any questions during exporting, see [Exporting for iOS](https://intl.cloud.tencent.com/document/product/607/39522).



## Export for Android

### 1. Delete unnecessary .lib files

The GME SDK for Unity provides lib files for arm64-v8a, armeabi-v7a, and x86 by default. Please delete unnecessary files as needed.
<dx-alert infotype="alarm" title="Architecture loss">
A crash will occur if the exported Android executable file lacks the specified architecture.
</dx-alert>
After the executable `apk` file is exported, if a black screen or crash occurs when you open it, it is generally caused by the lack of corresponding architecture `lib` file. Please add or delete the corresponding architecture `lib` file according to the project.

### 2. Configure permissions
**2.1 Required permissions**
Add the following permissions in the `AndroidManifest.xml` file of the project:

```
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
```

**2.2 Adding permissions as needed**
Add the following permissions in the `AndroidManifest.xml` file of the project as needed:
<dx-tabs>
::: Read/Write permission
The read/write permission is not required. Determine whether to add it according to the following rules:

- If you use the default log path (/SDCARD/Android/Data/files), it means that you do not call SetLogPath, and do not need Write_External_Storage permission.
- If you call the setLogPath API to set the log path to an external storage device, and the storage path of the voice message recording is an external storage device, you need to apply for the Write_External_Storage permission to the user and get the user's approval.

```
 <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
```
:::
::: Bluetooth permission
Add the Bluetooth permission according to the following rules:

- If `targetSDKVersion` in the project is v30 or earlier:
```
<uses-permission android:name="android.permission.BLUETOOTH"/>
```

- If `targetSDKVersion` in the project is v31 or later:
```
<uses-permission android:name="android.permission.BLUETOOTH" android:maxSdkVersion="30" />
<uses-permission android:name="android.permission.BLUETOOTH_CONNECT" />
```
:::
</dx-tabs>


### 3. FAQs about export
If you have any questions during exporting, see [Exporting for Android](https://intl.cloud.tencent.com/document/product/607/39522).


## Export for Windows

If you have any questions during exporting, see [Exporting for Windows](https://intl.cloud.tencent.com/document/product/607/39522).


## Export for WebGL

### 1. Configure WebGL plugins
Set the scope of `gmesdk.dll` on Windows to prevent it from conflicting with `gmesdk` on WebGL.

<img src="https://qcloudimg.tencent-cloud.cn/raw/18870d8c1a15a496da1dc3fe3e579d45.png"  width="60%" /></img>

<img src="https://qcloudimg.tencent-cloud.cn/raw/4b697ba47fb49484989a1e201f2d7ee6.jpg"  width="60%" /></img>


### 2. Disable Flare Layer (on Unity 2018 or later)

<img src="https://qcloudimg.tencent-cloud.cn/raw/894943f084fc5aefc94c709e35d65d0e.png"  width="60%" /></img>

As certain Unity versions no longer support the Flare Layer mode in `MainCamera`, you need to deselect Flare Layer in the scene to be built; otherwise, the following error will be reported:

<img src="https://qcloudimg.tencent-cloud.cn/raw/67506d24d1fef748b9ffbf6654ea27bc.png"  width="60%" /></img>


### 3. Select a template
When exporting to WebGL, select a WebGL template of GME to ensure that the relevant dependent libraries are imported to the build. The project will use the `GMEWebGLTemplatesUnity2018` template by default, which supports Unity 2018 and 2019. For Unity 2020 and 2021, you need to use `GMEWebGLTemplatesUnity2021` to create the build.
 
<img src="https://qcloudimg.tencent-cloud.cn/raw/def41a1210c286b47ddbe7dbeef1dd19.png"  width="60%" /></img>

### 4. Import frontend libraries
 
Before importing GME for WebGL to your project, you need to manually import frontend libraries, place the library files in the corresponding import locations, and add the audio tag as shown below. If you want the above operations to be automatically completed every time you build a Unity project, you can add the corresponding template to your project by referring to the GME demo for WebGL.

<img src="https://qcloudimg.tencent-cloud.cn/raw/b939e1cd5e331579440c16672a59c2e1.png"  width="60%" /></img>


### 5. FAQs about export
If you have any questions during export, see [Program Export](https://intl.cloud.tencent.com/document/product/607/39522).
