## Overview
VOD provides a [hotlink protection](https://intl.cloud.tencent.com/document/product/266/33984) feature that enables you to set hotlink protection for video playback URLs as needed, helping implement control over video playback.

However, setting hotlink protection for domain names in use without testing involves the following risks:

- Playback failures for users in the production network environment.
- Unsatisfactory effects of playback control.

For example, if you need to control the validity period of playback URLs, you need to enable [key hotlink protection](https://intl.cloud.tencent.com/document/product/266/33986):

* If the `sign` signature parameter in the generated hotlink protection is miscalculated, **enabling hotlink protection may cause playback failures of all videos in the production network environment**.
* If the `t` expiration time parameter in the generated hotlink protection is too large, the **video playback URL will not expire as scheduled after hotlink protection is enabled**.

Therefore, before hotlink protection is enabled for domain names, tests need to be conducted to ensure that the desired results can be achieved. In addition, hotlink protection testing should not affect users in the production network environment (i.e., it should be secure for the production network environment).

## Implementing Secure Hotlink Protection Test

VOD provides you with secure hotlink protection test schemes.

### Terminology
The terms involved are described as below:

* **Default VOD domain name**: it is the official domain name used for playing back VOD videos in the production network environment. Either a "preset domain name" or "custom domain name" can be set as the default domain name. For more information, please see [Custom Domain Name](https://intl.cloud.tencent.com/document/product/266/14056).
* **Preset VOD test domain name**: a test domain name for troubleshooting (which is generally `xxx-test.vod2.myqcloud.com`). It shall not be used in a production network environment or set as the default domain name.
* **Production application backend**: application backend service of a business, from which users in the production network environment can get video playback URLs.
* **Test application backend**: application backend service in the business testing environment, from which test client gets video playback URLs.

### Scheme details

Generally, a user in the production network environment gets a video playback URL from the production application backend, and a test client from the test application backend. The domain names in the two URLs are the same (i.e., the default VOD domain name). During hotlink protection test, the default VOD domain name shall not be changed directly; otherwise, users will be affected.

<img src="https://main.qcloudimg.com/raw/4117ff809dd401c6f0f6c7569d731b21.png" width="450">

To prevent hotlink protection test from affecting users in the production network environment, VOD provides a "preset VOD test domain name", which is isolated from the default VOD domain name used in the production network environment. During hotlink protection test, you should only manage the hotlink protection configuration of the test domain name.

VOD also provides a "test domain name proxy" (IP: `122.152.250.73`). You just need to modify the HOST table on the test client to resolve the default VOD domain name to this proxy. Playback requests from the test client will be forwarded to the test domain name through the proxy (red path in the figure below), while playback requests from users in the production network environment will still be forwarded to the official domain name (black path in the figure below).

<img src="https://main.qcloudimg.com/raw/3c461eb955a8b526816341f5116ff19c.png" width="450">

Therefore, you can freely modify the hotlink protection configuration of the test domain name and test the playback URL distributed by the test application backend without worrying about any impact on users in the production network environment.

<img src="https://main.qcloudimg.com/raw/6f891fcbebef12da423e42ec5ab59e1e.png" width="450">

After fully verifying hotlink protection on the test client and test application backend and confirming that everything is correct, you can take the steps below:

1. Change the rule of the playback URL distributed by the official application backend to that on the test application backend.
2. Change the hotlink protection configuration of the default VOD domain name to that of the preset VOD test domain name.

In this way, the hotlink protection of the default VOD domain name can take effect, and the hotlink protection configuration verified after test can be applied to the production network environment.

## Examples

Below is an example of enabling key hotlink protection to show you the steps of hotlink protection testing:

1. Enable hotlink protection for the preset VOD test domain name.
2. Get an original playback URL.
3. The test client can still play back the video at the original URL.
4. Modify the HOST table on the test client.
5. The test client can no longer play back the video at the original URL.
6. The test client can play back the video at the URL with hotlink protection parameters.
7. The official application backend generates the URL with hotlink protection parameters.
8. Enable hotlink protection for the default VOD domain name.

#### Background

![](https://main.qcloudimg.com/raw/98a0a1c95a0874cb8ebdf39f321753d5.png)
After logging into the VOD Console, a user (e.g., appid: `125xxx655`) will see the following two domain names in **[Domain Name Management](https://console.cloud.tencent.com/vod/distribute-play/domain)**:

* Preset VOD domain name (`125xxx655.vod2.myqcloud.com`).
* Preset VOD test domain name (`125xxx655-test.vod2.myqcloud.com`).

In the initial state, the preset VOD domain name `125xxx655.vod2.myqcloud.com` is the default VOD domain name with key hotlink protection not enabled.

#### 1. Enable hotlink protection for the preset VOD test domain name

Select the preset VOD test domain name (`125xxx655-test.vod2.myqcloud.com`), click **Settings** > **Key Hotlink Protection**, enable it, and click **Generate Key** to generate a hotlink protection key. Then, click **OK** and wait for the configuration to take effect.

#### 2. Get an original playback URL

The original playback URL of a video refers to the URL without [hotlink protection parameters](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE.E5.8F.82.E6.95.B0), which can be obtained in [Media Assets](https://console.cloud.tencent.com/vod/media) in the console. The URL used in this example is `https://125xxx655.vod2.myqcloud.com/ca7xxx655/cfbxxx349/PkxxxIA.mov`.

#### 3. The test client can still play back the video at the original URL

![](https://main.qcloudimg.com/raw/a991036d94d654078c94a4b0c19d778d.png)
At this point, the test client can still play back the video at the original URL. Run the `curl` command, and the HTTP status code returned is 200.

#### 4. Modify the HOST table on the test client

Modify the HOST table (`C:\Windows\System32\drivers\etc\hosts` on Windows or `/private/etc/hosts` on macOS) by adding the record ```122.152.250.73 125xxx655.vod2.myqcloud.com``` and then save the change.

Then, run ```ping 125xxx655.vod2.myqcloud.com``` to verify whether the modification has taken effect.

#### 5. The test client can no longer play back the video at the original URL

After modifying the HOST table, the test client can no longer play back the video at the original URL, and the HTTP status code returned will be `403 Forbidden`. This is because after the HOST table is modified, the video playback requests initiated by the test client will be mapped to the preset VOD test domain name, and the correct hotlink protection parameters must be included in the URL before the video can be played back.

#### 6. The test client can play back the video at the URL with hotlink protection parameters

Generate a URL with hotlink protection parameters according to the key hotlink protection [generation rules](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F), which is `https://125xxx655.vod2.myqcloud.com/ca7xxx655/cfbxxx349/PkxxxIA.mov?t=5bd6be00&sign=18cxxx9deb`. Run ```curl```, and the HTTP status code returned will be 200.

The test application backend distributes the URL with hotlink protection parameters according to the hotlink protection generation rules and verify the URL on the test client.

#### 7. The official application backend generates the URL with hotlink protection parameters

After test, the official application backend distributes the URL with hotlink protection parameters according to the same rules as that of the test application backend.

#### 8. Enable hotlink protection for the default VOD domain name

Open the **Key Hotlink Protection** module of the **preset VOD test domain name** in the console and copy the key; then open the **Key Hotlink Protection** module of the **default VOD domain name**, paste the key of the test domain name to the **Hotlink Protection Key** text box, and click **OK**.

After the domain name configuration takes effect, the hotlink protection configuration will be applied to the default VOD domain name used in the production network environment and take effect officially.
