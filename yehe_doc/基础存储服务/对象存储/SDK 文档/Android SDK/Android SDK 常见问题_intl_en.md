### What do I do if the client network is normal, while the access to COS over HTTP is very slow, or the error message "Connection reset" is reported?
In some regions, carriers may hijack COS endpoints. Therefore, you are advised to access COS over HTTPS.

### What do I do if `ETag` is not included in the `Complete Multipart Upload` request and an error message "400 Bad Request" is reported?
The possible cause is that the `ETag` header is filtered out by the network. After the parts are uploaded, the SDK fails to parse the `ETag` parameter and reports the error in the Complete Multipart Upload operation.

### What do I do if `QCloudResultListener` or other callback functions did not work?
If you view logs to determine whether a callback function works, the possible cause is that the log level is set too high, or the desired log is filtered out by other filtering rules. You can adjust the filtering rule, or set breakpoints in the callback function to determine whether the callback function works properly.

### What do I do if `NoClassDefFoundError` is reported when I call an API?
The SDK depends on the bolts and OkHttp common classes. If the methods in these classes cannot be found, you might have imported these two dependencies to your project, and the version number is too low. You are advised to use a version consistent with the SDK version or a later one.

### What do I do if the SDK failed to obtain permissions to the phone?
To upload files to or download files from an external storage device, you must have network permission and read/write permissions on the device. Other permissions, such as location permission and device information permission, are not mandatory. If you have strict requirements on permissions, you can skip importing the MtaUtils package or upgrade the SDK to 5.5.8 or above.

### What do I do if the `java.security.cert.CertPathValidatorException: Trust anchor for certification path not found` error is reported when HTTPS is used?
If you access COS via a proxy, check whether the proxy supports HTTPS. If not, please [contact us](https://www.tencentcloud.com/contact-sales).

### What do I do if the upload progress reaches 100%, while the `onFailed` method is called?
The 100% upload progress indicates only the SDK packet sending progress. The upload is successful only when the `onSuccess` method is called. If an exception occurs when the `Complete Multipart Upload` request is sent, the `onFailed` method will be called. You can check the exception details and solution based on the `onFailed` callback information.

### What do I do if an error, such as `400 Bad Request` and `409 Conflict`, occurs in a multipart upload?
Use the advanced API `TransferManager` provided by the SDK for upload/download if possible. Encapsulating the multipart upload API may easily cause an error.

### What do I do if a permission error is reported when I use `TransferManager` for upload/download?
The Head operation will be performed when `TransferManager` downloads an object. Therefore, the `HeadObject` and `GetObject` permissions should be granted for the download. For an upload operation, permissions on all simple upload and multipart upload APIs should be granted.

### What do I do if an error, such as `lock timeout`, `no credential for sign`, or expired signature, is reported?
If you have implemented the `BasicLifecycleCredentialProvider#fetchNewCredentials()` method, please check whether the key is updated in time, or whether it is still valid. For a temporary key, the token should be carried.

### What do I do if the `java.lang.RuntimeException: Can't create handler inside thread that has not called Looper.prepare()` error is reported?
If the error is reported when the `TransferManager#upload()` method is called in the master thread, this is a false positive reported by the MTA and can be ignored. You can also upgrade your SDK to 5.5.8 or above to solve this issue.

### What do I do if an application error is reported when I directly operate the UI in a callback?
The SDK callback thread is not necessarily the master thread. Please do not operate the UI directly.

### What do I do if `calculate md5 error` is reported during upload?
The possible cause is either that you have modified the file during the upload, changing the MD5 checksum, or the network is poor, causing a packet receive error on the server.

### What do I do if `ServerError` is returned for a request?
If you access COS using a proxy, the possible cause is that the proxy returned the incorrect packet, causing the SDK to fail the parsing. You can capture the packet received by the client to verify the packet.

### What do I do if the 403 permission error is reported when I call an API?
In general, a permission error is irrelevant to SDK. You can check your permissions or [contact us](https://www.tencentcloud.com/contact-sales).

### Does Android SDK support checkpoint restart?

Advanced APIs of the Android SDK of COS support checkpoint restart. To implement checkpoint restart, refer to the descriptions of the advanced APIs in [Uploading and Copying Objects](https://www.tencentcloud.com/document/product/436/37674).

