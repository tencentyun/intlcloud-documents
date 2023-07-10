### What do I do if the client network is normal, while the access to COS over HTTP is very slow, or the error message "Connection reset" is reported?
In some regions, carriers may hijack COS endpoints. Therefore, you are advised to access COS over HTTPS.

### What do I do if the upload progress reaches 100%, but the `failCallBack` method is called?
The 100% upload progress indicates only the SDK packet sending progress. The upload is successful only when the `successCallBack` method is called. If an exception occurs when the `Complete Multipart Upload` request is sent, the `failCallBack` method will be called.

### What do I do if a permission error is reported when I use `CosTransferManger` for upload/download?
The Head operation will be performed when `CosTransferManger` downloads an object. Therefore, the `HeadObject` and `GetObject` permissions should be granted for the download. For an upload operation, permissions on all simple upload and multipart upload APIs should be granted.

### What do I do if an error, such as `lock timeout`, `no credential for sign`, or expired signature, is reported?
If you are using a temporary key, check whether the key returned by the `initWithSessionCredentialCallback` method is updated in time or is valid. If it is a temporary key, it needs to carry the token.

### What do I do if `calculate md5 error` is reported during upload?
The possible cause is either that you have modified the file during the upload, changing the MD5 checksum, or the network is poor, causing a packet receive error on the server.

### What do I do if `ServerError` is returned for a request?
If you access COS using a proxy, the possible cause is that the proxy returned the incorrect packet, causing the SDK to fail the parsing. You can capture the packet received by the client to verify the packet.

### What do I do if the 403 permission error is reported when I call an API?
In general, a permission error is irrelevant to SDK. You can check your permissions or [contact us](https://www.tencentcloud.com/contact-sales).

