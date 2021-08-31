## Description

When an image fails to be downloaded, X-ErrNo contained in the header of the response packet refers to the error code field. In this case, you can handle the error according to the following list.

## Error Codes

### Error Codes upon download

| Error Code | Description | Action |
| ------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| -103 | Invalid request. The request packet cannot be recognized. | Check the content of the request. |
| -104 | Invalid APPID. The APPID contained in the URL is invalid, or the domain name is not bound to the APPID. | Check whether the APPID is correct. |
| -105 | Invalid style name. The style name or alias specified in the URL is not set. | Check the style configuration or style name. |
| -106 | Invalid URL. The URL format is invalid. | Check the URL format. |
| -107 | Invalid Host header field. | Check whether Host is correct. |
| -108 | Invalid Referer. | Check the Referer configuration. |
| -109 | Invalid style name ID. The image corresponding to the style name is not found. This style name may have been added after the image was uploaded, and therefore data corresponding to this style name could not be generated when the image was uploaded. | N/A |
| -110 | The image is blocked. | N/A |
| -120 | Data returned by the origin server is exceptional during origin-pull, and consequently image data cannot be properly retrieved. | Check the data on the origin server. |
| -124 | A download offset error has occurred. The setting of Range (checkpoint restart offset) for the HTTP request may be incorrect. | Check the checkpoint restart offset setting. |
| -154 | Download is prohibited for this URL by the original image protection mechanism. | Use the style to access the image. |
| -156 | Forcible execution of the 302 process. | N/A |
| -162 | There is overdue payment, and image downloading is prohibited. | Make payment promptly. |
| -163 | The business configuration does not exist. | Check relevant configuration items. |
| -164 | The request frequency is too high. | Reduce the request frequency, or [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact us. |              -
| -165 | Aggressive download requests are restricted. | N/A |
| -166 | The message format is invalid. | N/A |
| -167 | The image file is too large and cannot be downloaded. | Reduce the size of the file. |
| -168 | The image file is too large and cannot be downloaded. | Reduce the size of the file. |
| -441 | Unsupported image format. Image failed to compress. | Use a CI supported image format for image processing. Valid formats are: jpg, bmp, gif, png, and webp. |                                                 -
| -442 | The image size exceeds the limit. | Ensure that image dimensions are equal to or less than 9,999 pixels. |
| -443 | Unsupported image format | Use a supported image format. For details, see [Rules and Limits](https://intl.cloud.tencent.com/document/product/1045/33425). |
| -447 | Image resolution exceeds the limit or the GIF file contains too many frames. | Limit image dimensions to 9999 pixels (limit the frame number of GIF files). |
| -901 | Compression timeout. | N/A |
| -902 | Origin-pull times out. Specifically, when the image storage feature forwards a request to the developer’s origin server, the timer expires before a response is received. | Check the origin server data or origin-pull configuration. |                                    
| -5062 | The image may be illegal. | Check whether the content of the image is illegal. |
| -6101 | The image does not exist, is not uploaded, or has been deleted. | Check the source data of the request. |                                         
| -29033 | The download request does not contain a valid range. | N/A |
| -29034 | The download offset is greater than the file size. | N/A |
| -29214 | Frequency control is triggered. | Reduce the request frequency, or [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact us. |
| -40168 | The original image is null. | Check the raw data of the request. |
| -46152 | The bucket name is invalid. | Check whether the bucket name is valid. |                                 
| -46154 | The APPID is invalid. | Check whether the APPID is valid. |
| -46614 | Downloading is not allowed for a file that is being uploaded. | Send the download request after the file has finished uploading. |                              
| -46617 | A blocked entry is hit. | Check whether the content of the image is illegal. |
| -46618 | Signature authentication fails. | Check whether the signature is correct. |
| -46619 | The signature is expired. | Update the signature. |
| -46620 | The bucket is blocked. | Your bucket is blocked. [Submit a ticket](https://console.cloud.tencent.com/workorder/category) for further assistance. |
| -46621 | The file is blocked. | Your resource is blocked. In this case, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact us. |
| -46627 | The user is currently blocked. | Your account is blocked. In this case, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact us. |
| -46628 | The file does not exist. | Check whether the file to be downloaded exists. |
| -46642 | The APPID does not exist. | Check whether the APPID is correct. |
| -46646 | The file is blocked. | The file is blocked. Check whether the content of the file is illegal. |                    

### Error codes in persistence processing
| Error Code | Description | Action |
| ------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| -60998 | An image processing parameter is invalid. | Check whether image processing rules are correct. |
| -60997 | The number of image processing rules exceeds the limit. | Persistence processing currently supports a maximum of five rules. Therefore, ensure that at most five rules are configured. |
| -60996 | The file is too large to process. | Ensure that the file size is equal to or less than 32 MB. |
| -60987 | Failed to retrieve the image. | Check the URL of the image. |
| -60983 | Invalid host. | Check the host. |
| -60972 | Invalid region. | Check if the region in the request supports CI. For more information on regions that support CI, see [Regions and Domain Names](https://intl.cloud.tencent.com/document/product/1045/33423). |
| -60967 | The image style does not exist. | Check the image style. |
| -60957 | The number of used styles exceeds the limit. | Currently, a maximum of 100 styles are supported. If you need more styles, contact us. |
| -60955 | Invalid URL. | Check whether the URL is correct. |
| -60950 | No file is specified. | Specify the file to be processed in the request. |
| -60949 | The request rate is too high. | Reduce the request rate. To increase the rate limit, contact us. |
| -60948 | The account is blocked. | Your account is blocked. [Submit a ticket](https://console.cloud.tencent.com/workorder/category) for further assistance. |
| -60938 | Incomplete signing information. | Check the required items in the signing information. |
| -60936 | The request is denied. | AccessDenied. |
| -60932 | The signature is incorrect. | The signature is incorrect. In this case, check whether the signing information matches. |
| -62999 | Invalid image format. | Check whether the image format is valid. |


For information on COS error codes, see [COS Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
