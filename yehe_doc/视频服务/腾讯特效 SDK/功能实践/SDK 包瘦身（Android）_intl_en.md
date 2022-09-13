To downsize the package, you can download the `assets` resources, `so` libraries, and animated effect resources `MotionRes` (unavailable in some basic SDKs) required by the SDK online. After successful download, set the paths of the above files in the SDK.

We recommend you reuse the download logic of the demo. You can also use your existing download service.

If you reuse the demo download logic, note that the checkpoint restart feature is enabled by default in the demo, so that a download can be resumed later if it is interrupted. To use this feature, make sure that your download server supports the checkpoint restart capabilities. 

**Check method**

```java
Check whether the web server supports range requests. If range requests are supported, then the server supports checkpoint restart. Run the following `curl` command on the command line:
curl -i --range 0-9 https://your server address/name of the file to be download
For example:
curl -i --range 0-9 https://mediacloud-76607.gzc.vod.tencent-cloud.com/TencentEffect/Android/2.4.1.119/xmagic_S1-04_android_2.4.1.119.zip
If the returned content contains the `Content-Range` field, the server supports checkpoint restart.
```

[](id:so)
## Dynamically Downloading .so Libraries
`.so` library packages are in `jniLibs/arm64-v8a` and `jniLibs/armeabi-v7a`.
![](https://qcloudimg.tencent-cloud.cn/raw/785d9f1a64b556343ea8959f14fec646.png)


<dx-tabs>
::: To reuse the download service in the demo
1. Calculate the MD5 value of the two ZIP packages. To do so on macOS, directly run `MD5 file path/filename` in Terminal or use an applicable tool.
2. Upload the packages to your server and get the download URLs.
3. Update the values of the following constants in `ResDownloadConfig` in the demo project:
![](https://qcloudimg.tencent-cloud.cn/raw/2c6e6b4e36eca9a7b17181f567efe01c.png)
4. Call `ResDownloadUtil.checkOrDownloadFiles` to start download.
:::
::: To use your own download service
1. Download and decompress the packages and set their paths in the SDK. For example, after decompressing a package, set `so path = /data/data/com.tencent.pitumotionDemo.effects/files/xmagic_libs`.
<img src="https://qcloudimg.tencent-cloud.cn/raw/c4ee096758d599be54310d740c5026d4.png" width=400px>
>! We strongly recommend you download `.so` libraries to the private directory of your app rather than an external storage device to prevent them from being mistakenly deleted by clearing tools. We also recommend you download the `.so` libraries of v8a or v7a based on the CPU architecture of user mobile phones to expedite downloads. You can refer to `LaunchActivity` in the demo project.
2. Call the following code to load `.so` libraries and authenticate the license.
```java
XmagicApi.setLibPathAndLoad(path);
auth();
```
:::
</dx-tabs>

>! 
>- When the SDK version is updated, the corresponding `.so` libraries may also change, and you need to download the `.so` libraries again. We recommend you refer to the method in the demo and use the MD5 value for verification.
>- Regardless of whether you choose to download `.so` libraries on your own or reuse the download service in the demo, check whether they have been downloaded before calling the `auth` API of the SDK. `ResDownloadUtil` provides the following method for checking. If they have been downloaded, set their paths in the SDK as shown below:
```java
String validLibsDirectory = ResDownloadUtil.getValidLibsDirectory(LaunchActivity.this,

isCpuV8a() ? ResDownloadConfig.DOWNLOAD_MD5_LIBS_V8A : ResDownloadConfig.DOWNLOAD_MD5_LIBS_V7A);
if (validLibsDirectory == null) {
     Toast.makeText(LaunchActivity.this,"Libraries are not downloaded. Download them first",Toast.LENGTH_LONG).show();
     return;
}
XmagicApi.setLibPathAndLoad(validLibsDirectory);
auth();
```


## Dynamically Downloading `assets` Resources
You can dynamically download `assets` resources as follows:

1. Configure the following in `assets` in your local project:
     - **On 2.4.0 or later**: No files in the local `assets` directory need to be retained.
     - **On versions earlier than 2.4.0**: You need to retain the license file and four JSON configuration files: `brand_name.json`, `device_config.json`, `phone_info.json`, and `score_phone.json`.
2. Find the `download_assets.zip` package in the SDK.
![](https://qcloudimg.tencent-cloud.cn/raw/b04e8d991a4aef086229a8610ad8f883.png)
3. Calculate the MD5 value of the ZIP package in the same way as described above for the [.so files](#so), Then, upload the packages to the server to get the download addresses.
<dx-tabs>
::: To reuse the download service in the demo
1. Update the download address and MD5 value in the following figure.
![](https://qcloudimg.tencent-cloud.cn/raw/a59277a9a3a9d5c000b103fce7ea2885.png)
2. Call `ResDownloadUtil.checkOrDownloadFiles` to start download and call `ResDownloadUtil.getValidAssetsDirectory` to get the path of the downloaded `assets`. For detailed directions, see `LaunchActivity.java`.
:::
::: To use your own download service
After downloading and decompressing the above ZIP package, you need to reorganize the file structure as follows:
<img src="https://qcloudimg.tencent-cloud.cn/raw/8ad5eeb526671bea433967c91aa377bc.png" width=400px>
Here, names in the red box such as `light_assets` and `light_material` cannot be changed arbitrarily. We recommend you directly reuse the `organizeAssetsDirectory` method in `ResDownloadUtill` to organize the structure.
:::
</dx-tabs>

>! 
>- When the SDK version is updated, the corresponding `assets` may also change, and you need to download the `assets` again to ensure compatibility. We recommend you refer to the method in the demo and use the MD5 value for verification.
>- Regardless of whether you choose to download the `assets` on your own or reuse the download service in the demo, check whether `assets` have been downloaded before capturing video. `ResDownloadUtil` provides the following method for checking. If they have been downloaded, set their paths in the SDK. For detailed directions, see `LaunchActivity.java`.
```java
String validAssetsDirectory = ResDownloadUtil.getValidAssetsDirectory(LaunchActivity.this,ResDownloadConfig.DOWNLOAD_MD5_ASSETS);
if (validAssetsDirectory == null) {
      Toast.makeText(LaunchActivity.this,"The `assets` are not downloaded. Download them first",Toast.LENGTH_LONG).show();
      return;
}
XmagicResParser.setResPath(validAssetsDirectory);
startActivity(intent);
```

## Downloading Animated Effect Resources `MotionRes`
Some basic editions don't have animated effect resources. You can skip this section based on your actual conditions.

Animated effects are divided into six types, and each type has several ZIP packages, each of which contains an animated effect. The file content varies by your purchased edition.
![](https://qcloudimg.tencent-cloud.cn/raw/e289586793242d7a9b363b42cacb0f38.png)
Animated effect resources can be downloaded as needed. For example, download can start after a user enters the relevant feature page or after clicking the icon of an animated effect.

You need to upload these ZIP packages to the server and get the download address of each ZIP package.
>!**The `MotionRes` directory of downloaded animated effect resources must be at the same level as `light_assets` and `light_material` described in the previous section**. In addition, each animated effect needs to be extracted and cannot be placed in the same ZIP package.

![](https://qcloudimg.tencent-cloud.cn/raw/96876dfb2d76901b4e20a3847b0be280.png)

To download `MotionRes`, refer to the `ResDownloadUtil.checkOrDownloadMotions` method. We recommend you download such resources one by one.

**To reuse the download service in the demo, replace the value of the `MOTION_RES_DOWNLOAD_PREFIX` constant in `ResDownloadConfig` with your download URL prefix.**