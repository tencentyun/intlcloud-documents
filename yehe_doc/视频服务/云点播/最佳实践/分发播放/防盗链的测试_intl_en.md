VOD provides a [hotlink protection](https://intl.cloud.tencent.com/document/product/266/33984) feature that enables you to set hotlink protection for video playback URLs as needed, helping implement control over video playback.

However, setting hotlink protection for domain names in use without testing involves the following risks:

- Playback failures for users in the production network environment.
- Unsatisfactory effects of playback control.

For example, if you need to control the validity period of video playback URLs, you need to enable [key hotlink protection](https://intl.cloud.tencent.com/document/product/266/33986):

* If the `sign` signature parameter in the generated hotlink protection is miscalculated, **enabling hotlink protection may cause playback failures of all videos in the production network environment**.
* If the `t` expiration time parameter in the generated hotlink protection is too large, the **video playback URL will not expire as scheduled after hotlink protection is enabled**.

Therefore, before hotlink protection is enabled for domain names, tests need to be conducted to ensure that the desired results can be achieved. In addition, hotlink protection testing should not affect users in the production network environment (i.e., it should be secure for the production network environment).

## Implementing Secure Hotlink Protection Test

VOD provides you with secure hotlink protection test schemes.

### Terminology
The involved terms are described as below:

* **Default VOD domain name**: official domain name used for playing back VOD videos in the production network environment. Any "custom VOD domain name" can be set as the default domain name. For more information, please see [Custom Domain Name](https://intl.cloud.tencent.com/document/product/266/35572).
* **VOD test domain name**: test domain name used for troubleshooting. It should not be used in a production network environment, and we recommend you not set it as the default domain name.
* **Production application backend**: application backend service of the business, from which users in the production network environment can get video playback URLs.
* **Test application backend**: application backend service in the business testing environment, from which test client gets video playback URLs.

### Scheme details

Generally, a user in the production network environment gets a video playback URL from the production application backend, and a test client from the test application backend. The domain names in the two URLs are the same (i.e., the default VOD domain name). During hotlink protection test, the default VOD domain name shall not be changed directly; otherwise, users will be affected.

<img src="https://main.qcloudimg.com/raw/85d3b79bc4255be32804c53438bc8ec2.png" width="450">

To prevent hotlink protection test from affecting users in the production network environment, you need to prepare an additional "test domain name", which is isolated from the default VOD domain name used in the production network environment. During hotlink protection test, you should only manage the hotlink protection configuration of the test domain name.

VOD also provides a "test domain name proxy" (IP: `122.152.250.73`). You just need to modify the HOST table on the test client to resolve the default VOD domain name to this proxy. Video playback requests from the test client will be forwarded to the test domain name through the proxy (red path in the figure below), while playback requests from users in the production network environment will still be forwarded to the official domain name (black path in the figure below).

<img src="https://main.qcloudimg.com/raw/ea7c413d0bc993554b4b5521ffc7adcf.png" width="450">

Therefore, you can freely modify the hotlink protection configuration of the test domain name and test the playback URL distributed by the test application backend without worrying about any impact on users in the production network environment.

<img src="https://main.qcloudimg.com/raw/9d47fd2140a3bdc7a20aa6347407b009.png" width="450">

After fully verifying hotlink protection on the test client and test application backend and confirming that everything is correct, you can take the steps below:

1. Change the rule of the playback URL distributed by the official application backend to that on the test application backend.
2. Change the hotlink protection configuration of the default VOD domain name to that of the test domain name.

In this way, the hotlink protection of the default VOD domain name can take effect, and the hotlink protection configuration verified after test can be applied to the production network environment.

## Examples

Below is an example of enabling key hotlink protection to show you the steps of hotlink protection testing:

1. Enable hotlink protection for the test domain name.
2. Get an original playback URL.
3. The test client can still play back the video at the original URL.
4. Modify the HOST table on the test client.
5. The test client can no longer play back the video at the original URL.
6. The test client can play back the video at the URL with hotlink protection parameters.
7. The official application backend generates the URL with hotlink protection parameters.
8. Enable hotlink protection for the default VOD domain name.

#### Background


Log in to the VOD Console (suppose your `appid` is `125xxx655`), add an official domain name and a test domain name in **[Domain Management](https://console.cloud.tencent.com/vod/distribute-play/domain)**, and set the former as the default domain name. By default, key hotlink protection is not enabled for domain names in the initial state.

#### 1. Enable hotlink protection for the test domain name

Select the test domain name, click **Settings** > **Key Hotlink Protection**, enable it, and click **Generate Key** to generate a hotlink protection key. Then, click **OK** and wait for the configuration to take effect.

#### 2. Get an original playback URL

The original playback URL of a video refers to the URL without [hotlink protection parameters](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE.E5.8F.82.E6.95.B0), which can be obtained in [Media Assets](https://console.cloud.tencent.com/vod/media) in the console.

#### 3. The test client can still play back the video at the original URL

![](https://main.qcloudimg.com/raw/a991036d94d654078c94a4b0c19d778d.png)
At this point, the test client can still play back the video at the original URL. Run the `curl` command, and the HTTP status code returned is 200.

#### 4. Modify the HOST table on the test client

Modify the HOST table (`C:\Windows\System32\drivers\etc\hosts` on Windows or `/private/etc/hosts` on macOS) by adding the record ```122.152.250.73 test domain name``` and then save the change.

Then, run ```ping test domain name``` to verify whether the modification has taken effect.

#### 5. The test client can no longer play back the video at the original URL

After modifying the HOST table, the test client can no longer play back the video at the original URL, and the HTTP status code returned will be `403 Forbidden`. This is because after the HOST table is modified, the video playback requests initiated by the test client will be mapped to the preset VOD test domain name, and the correct hotlink protection parameters must be included in the URL before the video can be played back.

#### 6. The test client can play back the video at the URL with hotlink protection parameters

Generate a URL with hotlink protection parameters according to the key hotlink protection [generation rules](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F), which is `https://xxx.com/ca7xxx655/cfbxxx349/PkxxxIA.mov?t=5bd6be00&sign=18cxxx9deb`. Run ```curl```, and the HTTP status code returned will be 200.

The test application backend distributes the URL with hotlink protection parameters according to the hotlink protection generation rules and verify the URL on the test client.

#### 7. The official application backend generates the URL with hotlink protection parameters

After test, the official application backend distributes the URL with hotlink protection parameters according to the same rules as that of the test application backend.

#### 8. Enable hotlink protection for the default VOD domain name

Open the **Key Hotlink Protection** module of the **test domain name** in the console and copy the key; then open the **Key Hotlink Protection** module of the **default VOD domain name**, paste the key of the test domain name to the **Hotlink Protection Key** text box, and click **OK**.

After the domain name configuration takes effect, the hotlink protection configuration will be applied to the default VOD domain name used in the production network environment and take effect officially.
