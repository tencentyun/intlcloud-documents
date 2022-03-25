This document describes how to access and debug the GME APIs for Unity HD voice chat room.


## Prerequisites

Starting from GME SDK v2.9, GME SDK for Unity does not support the use of HD voice chat room by default. If your SDK is not on v2.9 or higher, the following operations are not required.

## Involved Features
Without adaptation, the SDK for Unity lacks the following features:

HD voice chat room. For more information, see [Sound Quality Selection](https://intl.cloud.tencent.com/zh/document/product/607/18522).
Accompaniment playback. For more information, see [Accompaniment in Voice Chat](https://intl.cloud.tencent.com/zh/document/product/607/31504).
Voice changing for voice chat and voice message. For more information, see [Voice Changing Effect](https://intl.cloud.tencent.com/zh/document/product/607/31503#.E5.8F.98.E5.A3.B0.E7.89.B9.E6.95.88).

## SDK Update

### Download link
If you have downloaded the standard version of the SDK for Unity in the [Download Guide](https://intl.cloud.tencent.com/zh/document/product/607/18521), you need to download other library files by [submitting a ticket](https://console.intl.cloud.tencent.com/workorder/category).


### Library file replacement
Delete the original GME library files and use the downloaded ones. The added library files are as shown below:

![](https://qcloudimg.tencent-cloud.cn/raw/5d218010fd171e5d098e49a609f7390d.png)


### Library files' corresponding features

You may import only required library files according to your own needs. For example, if you only need the voice changing feature, you only need to import `libgme_soundtouch`.

| Library File | Feature |
|----|-----|
|libgme_fdkaac| 1. Used to enter an SD or HD voice room. 2. Used to play back accompaniment files in ACC format |
|libgme_faad2| Used to play back accompaniment files in MP4 format |
|libgme_ogg| Used to play back accompaniment files in OGG format |
|libgme_lamemp3| Used to play back accompaniment files in MP3 format |
|libgme_soundtouch| Used for voice changing and pitch changing |


## Configuration Export
After configuring the required library files, you need to configure the iOS dynamic library package when exporting it. For other platforms, simply export them by default.

### Unity 2019 and higher

#### Configuration principle

Create an `Editor OnPostprocessBuild` script and use the `UnityEditor.iOS.Xcode.PBXProject.AddDynamicFramework` API, which will automatically copy the dynamic library to the `framework` directory of the final output Bundle and sign it.

#### Sample code
You can refer to the `add_dylib.cs` script file in the demo project and put this part of code in the `Editor` folder of the project as needed.

```
[UnityEditor.Callbacks.PostProcessBuild(1002)]
	public  static void OnPostprocessBuild (UnityEditor.BuildTarget BuildTarget, string path){  
		if (BuildTarget == UnityEditor.BuildTarget.iOS) {
			UnityEngine.Debug.Log ("OnPostprocessBuild add_dylib:" + path);
			{
				string projPath = UnityEditor.iOS.Xcode.PBXProject.GetPBXProjectPath (path);  
				UnityEditor.iOS.Xcode.PBXProject proj = new UnityEditor.iOS.Xcode.PBXProject ();  

				proj.ReadFromString (System.IO.File.ReadAllText (projPath));  
				string targetGuid = proj.TargetGuidByName (UnityEditor.iOS.Xcode.PBXProject.GetUnityTargetName ()); 
				
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
						proj.AddDynamicFramework (targetGuid, dylibGuid);
						System.IO.File.WriteAllText (projPath, proj.WriteToString ());
					}
				}
			}
		}
	}
```


### Unity below 2019

Currently, only Unity 2019 and higher can use `UnityEditor.iOS.Xcode`. You can export the `UnityEditor.iOS.Xcode` package from a higher version for use in a lower version, or directly decompress the attachment [UnityEditorAV.iOS.XCode.zip](http://dldir1.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.0/Other/UnityEditorAV.iOS.XCode.zip) and place it in the `Editor` folder of the project directory.

![](https://qcloudimg.tencent-cloud.cn/raw/a141d2c41dc4494148e9451d3d63cd38.png)

