The following are the descriptions of error codes in the X-ErrNo field in the Headers of the return when image download fails.

| Error code | Meaning |
| ------ | ---------------------------------------- |
| -103 | Invalid request; request message cannot be recognized |
| -104 | Invalid appid. The appid contained in Url is invalid, or the domain name is not bound to the appid |
| -105 | Invalid style name. The style name or alias specified in Url is not configured |
| -106 | Invalid url. Url does not meet format requirements |
| -107 | Invalid Host header field |
| -108 | Invalid Referer |
| -109 | Invalid style name ID. The image corresponding to the style name was not found. It may be a new style name after uploading the image, so the data corresponding to the style name cannot be generated when the image is uploaded.
| -110 | This image is in the blacklist |
| -120 | When forwarding traffic to the real server to get data, the data returned by the real server is exceptional and the image data cannot be obtained normally |
| -124 | Download offset error. Range resuming offset for the HTTP request may be set incorrectly |
| -154 | The original image protection mechanism prohibits download by this url |
| -156 | 302 process is forced to execute |
| -162 | Business configuration is in arrears, so downloading images is prohibited |
| -163 | Business configuration does not exist |
| -164 | Heat map download; limited |
| -165 | Offensive download request; limited |
| -166 | Message format error |
| -167 | File is too large to support image download |
| -168 | File is too large to support image download |
| -441 | Image is in a non-compliant format and cannot be compressed |
| -442 | Image exceeds limit size |
| -447 | Image resolution exceeds limit |
| -901 | Compression timed out |
| -902 | Traffic forwarding timed out; mirror storage function forwards the request to the developer's real server but no response is received and timeout occurs |
| -5062 | Suspected image violation |
| -6101 | Image does not exist, is not uploaded or has been deleted |
| -29033 | Download request has no valid range |
| -29034 | Download offset is larger than file size |
| -40168 | The original image is empty |
| -46152 | Invalid bucketName |
| -46154 | Invalid APPID |
| -46614 | File has not been fully uploaded yet, and download is prohibited |
| -46617 | Blacklist is hit |
| -46618 | Signature verification failed |
| -46619 | Signature expired |
| -46620 | Bucket is banned |
| -46621 | File is banned |
| -46627 | User is currently in the blacklist |
| -46642 | appid does not exist |
| -46646 | File is banned |
