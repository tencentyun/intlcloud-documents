## Feature Overview

When an image fails to be downloaded, X-ErrNo contained in the header of the response packet refers to the error code field. In this case, you can handle the error according to the following list.

>? For other download error codes that are passed through from COS, see [COS Error Codes](https://www.tencentcloud.com/document/product/436/7730).
>

## Error Codes

### Download errors

| Error Code | Description                                                         | Action                                                     |
| ------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| -103   | Invalid request. The request packet cannot be recognized.                                | Check the content of the request.                                               |
| -104 | Invalid APPID. The APPID contained in the URL is invalid, or the domain name is not bound to the APPID. | Check whether the APPID is correct. |
| -105 | Invalid style name. The style name or alias specified in the URL is not set. | Check the style configuration or style name. |
| -106   | Invalid URL. The URL format is invalid.                         | Check the URL format.                                    |
| -107   | Invalid Host header field                                             | Check whether Host is correct.                                         |
| -108   | Invalid Referer                                               | Check the Referer configuration.                                      |
| -109   | Invalid style name ID. The image corresponding to the style name is not found. This style name may have been added after the image was uploaded, and therefore data corresponding to this style name could not be generated when the image was uploaded. |                                 -                             |
| -110   | The image is blocked.                                             |                   -                                        |
|-113 | The file type is not supported. | For the input file types supported by file preview, see [Rules and Restrictions](https://intl.cloud.tencent.com/document/product/1045/33425). |
| -120 | Data returned by the origin is abnormal during origin-pull, and consequently image data cannot be properly retrieved. | Check the data on the origin. |
| -124 | A download offset error has occurred. The setting of Range (checkpoint restart offset) for the HTTP request may be incorrect. | Check the checkpoint restart offset setting. |
| -154   | Download is prohibited for this URL by the original image protection mechanism.                                | Use the style to access the image.                                               |
| -156   | Forcible execution of the 302 process                                              |                   -                                           |
| -162   | Image downloading is not allowed due to overdue payment.                                 | Top up your account promptly.                                                   |
| -163   | The business configuration does not exist.                                               | Check relevant configuration items.                                             |
| -164   | The request frequency is too high.                                               | Reduce the request frequency, or [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact us. |              - |
| -165   | Attack download requests are restricted.      |           -       |
| -166   | Invalid message format                                                 |          -                                                   |
| -167   | The image file is too large and cannot be downloaded.                                   | Reduce the size of the file.                                               |
| -168   | The image file is too large and cannot be downloaded.                                    | Reduce the size of the file.                                               |
| -441 | Unsupported image format. The image cannot be compressed. | Use a CI supported image format for image processing. Valid formats: JPG, BMP, GIF, PNG, WEBP |
| -442   | The image size exceeds the limit.                                             | Ensure that image dimensions are equal to or less than 9,999 pixels.                     |
|  -443   |   Unsupported image format                                       |  Use a supported image format. For details, see [Specifications and Limits](https://intl.cloud.tencent.com/document/product/1045/33425).               |
| -447   | Image resolution exceeds the limit or the GIF file contains too many frames.                                | Limit image dimensions to 9,999 pixels (limit the frame number of GIF files).    |
| -901   | Compression times out.                          |            -            |
| -902 | Origin-pull times out. Specifically, when the image storage feature forwards a request to the developer's origin, the timer expires before a response is received. | Check the origin data or origin-pull configuration. |
| -3006 | The file is encrypted and cannot be parsed. | - |
| -3008 | The file is empty and cannot be parsed. | - |
| -3011 | The file type is not supported. | For the input file types supported by file preview, see [Specifications and Limits](https://intl.cloud.tencent.com/document/product/1045/33425). |
| -3015 | The requested page number does not exist.          | -    |
| -3075 | This file exceeds 100 MB and cannot be parsed. | Ensure that the file size is equal to or less than 100 MB. |
| -5062  | The image may be illegal.           | Check whether the content of the image is illegal.     |
| -6101 | The image does not exist, is not uploaded, or has been deleted. | Check the raw data of the request. |
| -29033 | The download request does not contain a valid range.                          |           -        |
| -29034 | The download offset is greater than the file size.                                  |           -       |
| -29214 | Frequency control is triggered.                                       | Reduce the request frequency, or [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact us. |
| -40168 | The original image is null.                                                 | Check the raw data of the request.                                             |
| -46152 | Invalid bucket name                                           | Check whether the bucket name is valid. |
| -46154 | Invalid APPID                                                 | Check whether the APPID is valid.                                        |
| -46614 | Downloading is not allowed for a file that is being uploaded.                                   | Send the download request after the file upload is completed. |
| -46617 | A blocked entry is hit.                                                   | Check whether the content of the image is illegal.                                |
| -46618 | Signature authentication fails.                                                 | Check whether the signature is correct.                                        |
| -46619 | The signature is expired.                                                    | Update the signature.                                                   |
| -46620 | The bucket is blocked.                                                | Your bucket is blocked. [Submit a ticket](https://console.cloud.tencent.com/workorder/category) for further assistance. |
| -46621 | The file is blocked. | Your resource is blocked. [Submit a ticket](https://console.cloud.tencent.com/workorder/category) for further assistance. | -
| -46627 | The user is currently on the blocklist. | Your account is blocked. [Submit a ticket](https://console.cloud.tencent.com/workorder/category) for further assistance. |
| -46628 | The file does not exist.                                                   | Check whether the file to be downloaded exists.                        |
| -46642 | The APPID does not exist.                                    | Check whether the APPID is correct.                                     |
| -46646 | The file is blocked.                                                   | The file is blocked. Check whether the content of the file is illegal.  |
| -46661 | No access permission | Contact the resource owner for permission. |


### Persistence processing errors

| Error Code | Description | Action |
| ------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
|-60998| An image processing parameter is invalid. | Check whether image processing rules are correct. |
|-60997| The number of image processing rules exceeds the limit. | Persistence processing currently supports a maximum of five rules. Therefore, ensure that at most five rules are configured. |
|-60996| The file is too large to process. | Ensure that the file size is less than or equal to 32 MB. |
|-60987| Failed to retrieve the image | Check the URL of the image. |
|-60983| Invalid host | Check the host. |
|-60972| Invalid region | Check if the region in the request supports CI. For more information on regions that support CI, see [Regions and Domain Names](https://intl.cloud.tencent.com/document/product/1045/33423). |
|-60967| The image style does not exist. | Check the image style. |
|-60957| The number of used styles exceeds the limit. | Currently, a maximum of 100 styles are supported. If you need more styles, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact us. |
|-60955| Invalid URL | Check whether the URL is correct. |
|-60950| No file is specified. | Specify the file to be processed in the request. |
|-60949| The request frequency is too high. | Reduce the request frequency. To increase the frequency limit, [submit a ticket](https://console.cloud.tencent.com/workorder/category). |
|-60948| The account is suspected of violation. | Your APPID is blocked. [Submit a ticket](https://console.cloud.tencent.com/workorder/category) for further assistance. |
|-60938| Incomplete signing information | Check the required items in the signing information. |
|-60936| The request is rejected. | Access denied |
|-60932| Signature error | The signature is invalid. Check whether the signing information matches. |
|-62999| Invalid image format | Check whether the image format is valid. |

### File preview errors


| Error Code | Description | Action |
| ------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
|-3006 | The file is encrypted. | Use a decrypted file. |
|-3008 | The file length is 0. | Check whether the file is normal. |
|-3011 | The file type is not supported. | Check whether the file type is supported. For the supported file types, see [Specifications and Limits](https://intl.cloud.tencent.com/document/product/1045/33425). |
|-3015 | The number of requested page is greater than the total number of document pages. | Check whether the number of the requested page is correct. |


### Content moderation errors

| Error Code | Description                                                         | Action                                                     |
| :----- | :----------------------------------------------------------- | :----------------------------------------------- |
| -61011 | The file does not exist.                                                 | Check whether the file exists.                             |
| -65007 | File content error. Decoding failed.                                      | Check whether the file format is correct.                         |
| -65010 | Failed to download the file                                               | Check whether the file link is correct. For a file with private read permission, the file link must be signed. |
| -65011 | The file is too large to process.                                         | Currently, an excessively large file cannot be moderated.                       |
| -65012 | The image resolution is too low to process.                                   | Currently, images with excessively low resolution are not supported.                     |
| -65013 | The file is not processed because it does not meet requirements (e.g., unsupported file suffix or excessively large size). | Check whether the file meets requirements. |
| -65014 | No CI role (CI_QCSRole)                                | Bind a CI role.                             |
| -65015 | No moderation scenario is used.                                             | Use at least one moderation scenario for moderation.              |
| -65016 | BizType used does not exist.                                      | Enter a correct BizType.                           |
| Other   | Internal error                                                    | -                                               |



### Media processing errors

| Error Code | Error Message                           | Description                                                      |
| :----- | :----------------------------------------------------------- | :----------------------------------------------- |
| 1007 | InternalError | Internal error |
| 1010| InvalidUrl                       |       Invalid URL |
| 1011| InvalidContent                   |       Invalid request body |
| 1012| MissingAuthorization             |       Missing signature     |
| 1013| InvalidAuthorization             |        Invalid signature    |
| 1014| SignatureExpired                 |      Signature expired    |
| 1015| InvalidArgument                    |       Invalid argument    |
| 1016| MissingContent                     |      Missing request body   |
| 1017| InvalidHost                        |      Invalid host   |
| 1018| AccessDenied                     |         Access denied    |
| 1019| SecretidNotExist                 |        The key does not exist  |
| 1020| SlowDown                         |         Frequency control   |
| 1021| InvalidContentType               |     Invalid request body type   |
| 1100| BucketAlreadyBinded               |    The bucket is already bound   |
| 1103| ResourceNotFound                 |         Resource not found   |
| 1106| QueueNotFound                     |     Queue not found   |
| 1107| TemplateNotFound                 |      Template not found   |
| 1109| BindedBucketNumLimit               |    The number of bound buckets exceeds the upper limit   |
| 1110| CreatedTemplateNumLimit             |      The number of created templates exceeds the upper limit   |
| 1111| MediaBucketUnBinded                |   The bucket is not bound   |
| 1112| TemplateNameDuplicate               |    Duplicate template name   |
| 1114| ActiveWorkflowForbiddenUpdate        |           The workflow that has been enabled cannot be updated   |
| 1120| WorkFlowNumLimit                 |  The number of created workflows exceeds the upper limit   |
| 1124| WriteTargetBucketDenied            |       Writing to the bucket is forbidden   |
| 1145| QueueNumLimit                   |The number of created queues exceeds the upper limit   |

