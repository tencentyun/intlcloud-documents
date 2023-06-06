

### Web Identity Verification Integration Description

##### Prerequisites

1. You have signed up for a Tencent Cloud account and completed identity verification.
2. You have activated eKYC in the [console](https://console.intl.cloud.tencent.com/faceid).

##### Integration steps

1. Call the API for [generating an upload URL](Generating-Upload-URL.md) to get `UploadUrl` and `ResourceUrl` and upload the image for comparison to `UploadUrl`. After the image is uploaded successfully, you can access the image resource at `ResourceUrl`.
2. Pass in the web callback address redirected to after identity verification, and call the API for [applying for a web identity verification token](applying-for-web-identity-verification-token.md) on the server, so as to get the URL used to start web identity verification and the token for the current verification.
3. Redirect to the identity verification URL in the browser on the frontend for the user to complete web identity verification on the webpage.
4. After completing identity verification, the user will be redirected to the callback address you passed in (where the token for the identity verification process will be automatically added).
5. On the callback page, you need to use the token on the frontend to call the API for [getting the web identity verification result](getting-web-identity-verification-result.md) on the server, so as to get the result.

Integration sequence diagram

![img](https://qcloudimg.tencent-cloud.cn/raw/a554aedf1bf02f57165a24eae09acf1b.png)

##### Compatibility description

The web real-time communication technology has the following compatibility requirements for browsers and mobile operating systems:

<table>
	<tr><td>Mobile OS</td><td>Browser</td><td>Compatibility Requirements</td></tr>
	<tr ><td rowspan="3" style= "vertical-align: middle;">iOS</td><td>Browser built in WeChat</td><td>iOS 14.3+ and WeChat 6.5+</td></tr>
	<tr><td>Safari</td><td>iOS 11.1.2+ and Safari 11+</td></tr>
	<tr><td>Chrome</td><td>iOS 14.3+</td></tr>
	<tr><td rowspan="3" style= "vertical-align: middle;">Android</td><td>Browser built in WeChat</td><td>Supported</td></tr>
	<tr><td>Built-in browsers</td><td>Android 7+, with great compatibility with the built-in browsers of Huawei, OPPO, vivo, MEIZU, Honor, and Samsung (80% supported) and average compatibility with the built-in browser of Xiaomi (30% supported)</td></tr>
	<tr><td>Other browsers</td><td>Android 7+, where Chrome is supported, but QQ Browser and UC Browser are not</td></tr>
</table>

Note:

1. Due to H.264 copyright restrictions, Chrome and Chrome WebView-based browsers on Huawei devices don't support the real-time communication technology.
2. Under circumstances where the real-time communication technology isn't supported, web face recognition will switch from reflection-based liveness detection to video recording mode, so as to ensure that the user can properly complete the identity verification process.

##### Mode switch description

In the web face recognition process, reflection-based liveness detection mode will be used first. However, if the real-time communication compatibility requirements cannot be met, the process will automatically switch to video-based liveness detection mode. The service processes in the two modes are as follows:

Web face recognition process in reflection-based liveness detection mode:

![img](https://qcloudimg.tencent-cloud.cn/raw/5bc060671b612d043a5dbb354f2f513a.png)

Web face recognition process in video-based liveness detection mode:

![img](https://qcloudimg.tencent-cloud.cn/raw/f15bd944c395b48bdbf3e0f9df3c873c.png)

##### Camera access description for reflection-based liveness detection

When you call the web face recognition service, reflection-based liveness detection mode requires the user's camera access. If the user denies the access request, the face recognition and access request process needs to be entered again. Certain browsers cannot pull the access granting page; in this case, the user can try clearing the browser's cache.

| Returned Message                                                     | Action                             |
| ------------------------------------------------------------ | ------------------------------------ |
| Unable to access your camera/mic. Please make sure that there is no other app requesting access to them and try again. | Advise the user to check whether the required camera is in use. |
| Mic and camera permissions of your device are required during the whole verification. Please clear your browser cache and try again. | Advise the user to enter again and grant the camera access. |
| Please check whether the camera/mic can be accessed normally and try again | Advise the user to check whether the required camera works properly. |
