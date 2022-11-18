
If most of your files are large static files, enabling Range GETs can help increase the file response speed during origin-pull and improve the large file delivery efficiency.

## Feature Overview
Range GETs refers to origin-pull based on range requests. `Range` is one of the HTTP request headers, which is used to get files in the specified range. You can use a range request to request only partial file content from the server. For example, if a request carries the HTTP header `range: bytes=0-999`, the first 1,000 bytes of the file will be returned to the user.
In CDN, after Range GETs is enabled, origin-pull requests will carry the `Range` header by default. If the partial file requested by a user is not cached on the node or its cache has expired, CDN will perform Range GETs to pull and cache the requested partial file to the node and return it to the user. After Range GETs is disabled, if the user request doesn't carry the `Range` header, CDN will still pull the entire file during origin-pull.
For large files such as APK, audio, and video files, you can use range requests to effectively improve the delivery efficiency of large files, shorten the response time, and reduce the pressure on the origin.

## Notes
1. Before enabling Range GETs, first confirm that the origin supports range requests; otherwise, the operation may fail.
2. After Range GETs is enabled, resources will be cached in shards on the node, and these shards have the same cache expiration time and follow the cache expiration rule defined by the user.
3. If all your resources are small static files, or if you use a COS origin and data processing features such as image processing, we recommend you not enable Range GETs; otherwise, origin-pull may fail.
4. If all your resources are large static files and the origin supports range requests, or you use a COS origin and do not use any data processing features such as image processing, we recommend you enable Range GETs to improve the delivery efficiency and response speed.

## Configuration Description

### Configuration in domain management
1. Log in to the [CDN console](https://console.cloud.tencent.com/cdn).
2. Click **Domain Management** on the left sidebar to enter the domain name management list.
3. Select the target domain name and click **Manage** to enter the domain name configuration page.
4. Click the **Origin-pull Configuration** tab to view the Range GETs configuration items.
![](https://qcloudimg.tencent-cloud.cn/raw/eeea737602e1248ca1856a16a80df1b7.png)
5. In Range GETs configuration, Range GETs is disabled for all files by default. You can also add multiple custom rules for files as needed. Range GETs rules can be matched by file extension, file directory, and full path.

| Configuration Item | 	Description |
|--|--|
| Type 	| You can select **All Files**, **File Extension**, **File Directory**, or **Full Path**:<br><br>All Files: This Range GETs rule applies to all files. It is the default rule and cannot be deleted.<br>File Extension: This Range GETs rule applies to the specified file extensions.<br>File Directory: This Range GETs rule applies to the specified file directories.<br>Full Path: This Range GETs rule applies to the specified file paths. |
| Content |	Enter the content based on the selected file type: <br>If **Type** is **File Extension**, you can enter one or multiple file extensions separated by ";".<br>If **Type** is **File Directory**, you can enter one or multiple file directories separated by ";", and the entered content cannot end with "/", such as `/test;/a/b/c`.<br>If **Type** is **Full Path**, you can enter one or multiple full file paths separated by ";", such as `/index.html;/test/\*.jpg`. The file path supports the \* wildcard. |
| Range GETs |	It can be enabled or disabled: <br>Enable: If Range GETs is enabled, range requests will be used for origin-pull requests.<br>Close: If Range GETs is disabled, range requests won't be used for origin-pull requests. |

### Recommended configuration
If your files are larger than 4 MB in size, we recommend you enable Range GETs for such files. If only part of your files are large ones, we recommend you enable Range GETs for them through match by file type, file directory, or full path and disable Range GETs for other files.

### Configuration limitations
You can configure up to 20 Range GETs rules. The lower the rule, the higher the priority. When a user requests a file, the file will be matched with rules in sequence by priority, and the rule with the highest priority will be executed preferentially after a successful match.

## Configuration Samples

**Sample 1**
If Range GETs needs to be enabled for all files, configure Range GETs for the domain name `cloud.tencent.com` as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/1227e1b23eec3ceecad49b80ed64c5a0.png)
User A makes a request for the `http://cloud.tencent.com/test.apk` resource. After the node receives the request and finds that the cached `test.apk` file has already expired, it will initiate a range request to get and cache the resource by shards, as Range GETs is enabled for all files currently. If user B also makes a range request for the same file on the same node at this time and the shards stored on the node match the specified byte segments in the range request, the resource will be directly returned to user B without waiting to have all shards obtained.

**Sample 2**
If Range GETs needs to be enabled for only part of your files, configure Range GETs for the domain name `cloud.tencent.com` as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/b0b80635b4291e10347621e07c7cd252.png)
When user A makes a request for the `http://cloud.tencent.com/test.apk` resource, as the bottom rule has a higher priority than the top rule, Range GETs will be used for the request if the node resource is not hit or the cached resource has expired. If user B makes a request for the `http://cloud.tencent.com/test.jpg` resource, as it only matches the rule for all files, Range GETs won't be used when origin-pull is performed for the request.

