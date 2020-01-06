## Description

When an image fails to be downloaded, X-ErrNo contained in the header of the response packet refers to the error code field. In this case, you can handle the error according to the following list.

## Error Code List

### Error Codes upon Download

| Error Code | Description | Action |
| ------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| -103 | Invalid request. The request packet cannot be recognized. | Check the content of the request. |
| -104 | Invalid APPID. The APPID contained in the URL is invalid, or the domain name is not bound to the APPID. | Check whether the APPID is correct. |
| -105 | Invalid style name. The style name or alias specified in the URL is not set. | Check the style configuration or style name. |
| -106 | Invalid URL. The URL format is invalid. | Check the URL format. |
| -107 | Invalid Host header field. | Check whether Host is correct. |
| -108 | Invalid Referer. | Check the Referer setting. |
| -109 | Invalid style name ID. The image corresponding to the style name is not found. This style name may have been added after the image was uploaded, and therefore data corresponding to this style name could not be generated when the image was uploaded. | N/A |
| -110 | The image is blacklisted. | N/A |
| -120 | Data returned by the origin server is abnormal during origin-pull, and consequently image data cannot be properly retrieved. | Check the data on the origin server. |
| -124 | A download offset error has occurred. The setting of Range (resumable download offset) for the HTTP request may be incorrect. | Check the Range setting. |
| -154 | Download is prohibited for this URL by the original image protection mechanism. | Use the style to access the image. |
| -156 | Forcible execution of the 302 process. | N/A |
| -162 | The business configuration is in arrears, and image downloading is prohibited. | Top up your account promptly. |
| -163 | The business configuration does not exist. | Check relevant configuration items. |
| -164 | The request frequency is too high. | Reduce the request frequency, or [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact us. |              -
| -165 | Aggressive download requests are restricted. | N/A |
| -166 | The message format is invalid. | N/A |
| -167 | The image file is too large and cannot be downloaded. | Reduce the size of the file. |
| -168 | The image file is too large and cannot be downloaded. | Reduce the size of the file. |
| -441 | The format of the image is invalid. Therefore, the image cannot be compressed. | Use an image format that is supported by CI for image processing. CI supports the following image formats: jpg, bmp, gif, png, and webp. | N/A |
| -442 | The image size exceeds the limit. | Ensure that both the image width and length are equal to or less than 9,999 pixels. |
| -447 | The image resolution exceeds the limit. | Ensure that both the image width and length are equal to or less than 9,999 pixels. |
| -901 | Compression times out. | N/A |
| -902 | Origin-pull times out. Specifically, when the image storage feature forwards a request to the developer’s origin server, the timer expires before a response is received. | Check the origin server data or origin-pull configuration. |                                    
| -5062 | The image may be illegal. | Check whether the content of the image is illegal. |
| -6101 | The image does not exist, is not uploaded, or has been deleted. | Check the source data of the request. |                                         
| -29033 | The download request does not carry a valid range. | N/A |
| -29034 | The download offset is greater than the file size. | N/A |
| -29214 | Frequency control is triggered. | Reduce the request frequency, or [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact us. |
| -40168 | The original image is null. | Check the raw data of the request. |
| -46152 | The bucket name is invalid. | Check whether the bucket name is valid. |                                 
| -46154 | The APPID is invalid. | Check whether the APPID is valid. |
| -46614 | Downloading is disallowed for a file that is being uploaded. | Send the download request after the file is uploaded. |                              
| -46617 | An blacklisted entry is hit. | Check whether the content of the image is illegal. |
| -46618 | Signature authentication fails. | Check whether the signature is correct. |
| -46619 | The signature is expired. | Update the signature. |
| -46620 | The bucket is blocked. | Your bucket is blocked. In this case, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact us. |
| -46621 | The file is blocked. | Your resource is blocked. In this case, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact us. |
| -46627 | The user is currently blacklisted. | Your account is blocked. In this case, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact us. |
| -46628 | The file does not exist. | Check whether the file to be downloaded exists. |
| -46642 | The APPID does not exist. | Check whether the APPID is correct. |
| -46646 | The file is blocked. | The file is blocked. Check whether the content of the file is illegal. |                    

### Error codes in persistence processing
| Error Code | Description | Action |
| ------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| -60998 | An image processing parameter is invalid. | Check whether image processing rules are correct. |
| -60997 | The number of image processing rules exceeds the limit. | Persistence processing currently supports a maximum of five rules. Therefore, ensure that at most five rules are configured. |
| -60996 | The file is too large to process. | Ensure that the file size is equal to or less than 32 MB. |
| -60987 | The image fails to be obtained. | Check the URL of the image. |
| -60983 | The host is invalid. | Check the host. |
| -60972 | The region is invalid. | Check whether the region of the request supports CI. For more information on regions that support CI, see [Regions and Domain Names](https://intl.cloud.tencent.com/document/product/1045/33423). |
| -60967 | The image style does not exist. | Check the image style. |
| -60957 | The number of used styles exceeds the limit. | Currently, a maximum of 100 styles are supported. If you need more styles, contact us. |
| -60955 | The URL is invalid. | Check whether the URL is correct. |
| -60950 | No file is specified. | Specify the file to be processed in the request. |
| -60949 | The request frequency is too high. | Reduce the request frequency. To increase the frequency limit, contact us. |
| -60948 | The account is suspended for policy violations. | Your APPID is blocked. In this case, please contact us. |
| -60938 | The signing information is incomplete. | Check the required items in the signing information. |
| -60936 | The request is denied. | AccessDenied |
| -60932 | The signature is incorrect. | The signature is incorrect. In this case, check whether the signing information matches. |
| -62999 | The image format is invalid. | Check whether the image format is valid. |


For other error codes passed through from the COS download side, see [COS Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

