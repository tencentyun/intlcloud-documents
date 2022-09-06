# Directions

## Integration Preparations
- Sign up for a Tencent Cloud account and log in to the [FaceID console](https://console.intl.cloud.tencent.com/faceid) to activate the service. 

## Terms and Definitions

- Customer H5: The H5 page developed by a customer
- Customer Server: The business backend of a customer
- Tencent Cloud API: The backend APIs provided by Tencent Cloud and used to obtain the face recognition credentials and the results
- Tencent Cloud H5: The authentication page developed by Tencent Cloud

## Sequence Diagram (Simplified)

![1](https://qcloudimg.tencent-cloud.cn/raw/97952f84b9b010959070ccbeb8551dbe.png)

Backend APIs: [ApplyWebVerificationToken](https://www.tencentcloud.com/document/product/1061/49953) and [GetWebVerificationResult](https://www.tencentcloud.com/document/product/1061/49950)
## Sequence Diagram (Detailed)

In the real case, you need to input the URL of the comparison image to the backend API for getting the token. For use instructions and causes, see [Passing Resources](https://intl.cloud.tencent.com/document/product/1061/46849?!editLang=en).
*`CreateUploadUrl` serves as an independent role in the diagram*

![2](https://qcloudimg.tencent-cloud.cn/raw/872a25f5cbcd02d9b9e9418aed8cae2b.png)

Backend APIs: [ApplyWebVerificationToken](https://www.tencentcloud.com/document/product/1061/49953), [GetWebVerificationResult](https://www.tencentcloud.com/document/product/1061/49950), and [CreateUploadUrl](https://www.tencentcloud.com/document/product/1061/47648)

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

>!
>
>1. Due to H.264 copyright restrictions, Chrome and Chrome WebView-based browsers on Huawei devices don't support the real-time communication technology.
>2. Under circumstances where the real-time communication technology isn't supported, web face recognition will switch from reflection-based liveness detection to video recording mode, so as to ensure that the user can properly complete the identity verification process.

##### Mode switch description

In the web face recognition process, reflection-based liveness detection mode will be used first. However, if the real-time communication compatibility requirements cannot be met, the process will automatically switch to video-based liveness detection mode. The service processes in the two modes are as follows:

Web face recognition process in reflection-based liveness detection mode:

![img](https://qcloudimg.tencent-cloud.cn/raw/5bc060671b612d043a5dbb354f2f513a.png)

Web face recognition process in video-based liveness detection mode:

![img](https://qcloudimg.tencent-cloud.cn/raw/7ea4ecb0d5815ef727df1b9ee97d1935.png)

##### Camera access description for reflection-based liveness detection

When you call the web face recognition service, reflection-based liveness detection mode requires the user's camera access. If the user denies the access request, the face recognition and access request process needs to be entered again. Certain browsers cannot pull the access granting page; in this case, the user can try clearing the browser's cache.

| Returned Message                                                     | Action                             |
| ------------------------------------------------------------ | ------------------------------------ |
| Unable to access your camera/mic. Please make sure that there is no other app requesting access to them and try again. | Advise the user to check whether the required camera is in use. |
| Mic and camera permissions of your device are required during the whole verification. Please clear your browser cache and try again. | Advise the user to enter again and grant the camera access. |
| Please check whether the camera/mic can be accessed normally and try again | Advise the user to check whether the required camera works properly. |
