# Uploading Resources

## Background
When backend APIs are used, due to requirements for stability and regional isolation of resources, we first need to use COS links to replace all files to be uploaded, and the Tencent Cloud backend will then download required files via HTTP GET requests based on these links.

## Input Requirements
  /Note: If you have not activated COS or don't know how to use it, but you want to complete the integration quickly, see the Best Practices first./ 
 
The input links must meet the following requirements:
- A link must be a COS domain name, and the bucket region must be same as the region given in the API to use. For example, for a service using `ap-singapore` as the region, the link should be like this: https://<your-bucket>-<your-appid>.cos.ap-singapore.myqcloud.com. For details, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224?lang=en&pg=). 
- A link must be directly accessible to a GET request from a public network.
	
## Best Practices
### Uploading with created COS buckets
	If you have COS buckets or you need to store files in your COS buckets for any other reason, you can use this method:
- Use the [Put Bucket](https://intl.cloud.tencent.com/zh/document/product/436/7738) API or [Creating a Bucket](https://intl.cloud.tencent.com/zh/document/product/436/13309) in the console. Make sure the bucket region is same as the region of the API to use.
- Upload the object with the [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) API. 
- Calculate the 32-bit MD5 checksum of the object (the object downloaded in the Tencent Cloud backend will be checked with this checksum to prevent file disorder).
- [Download via Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/14116?lang=en&pg=). Make sure this link is available for getting the object within a specified period.

### Transferring resources with `CreateUploadUrl`

If you do not need to use your COS buckets, we provide a separate API [CreateUploadUrl](https://intl.cloud.tencent.com/zh/document/product/1061/37028?!editLang=en) to help you temporarily store resources and generate addressable links:
- Use [CreateUploadUrl](https://intl.cloud.tencent.com/zh/document/product/1061/37028?!editLang=en) to input `TargetAction` (such as `DetectReflectLivenessAndCompare`) and region (such as `ap-singapore`).
- Within the specified period, upload the resources using the `HTTP PUT` method based on the returned `UploadUrl`.
- Calculate the 32-bit MD5 checksum of the object (the object downloaded in the Tencent Cloud backend will be checked with this checksum to prevent file disorder).
- Input `ResourceUrl` and the calculated `MD5` in the `DetectReflectLivenessAndCompare` API.

## Other Notes

### Data storage security
	The `CreateUploadUrl` API provided by us does not support directly deleting data, and the data will be cleaned on a regular basis (per two hours currently). If you pursue a more rigorous and safer practice, we recommend you use your COS buckets, and take some precautions for the objects to upload after you use the API.
	
### Roles of MD5
The Content-MD5 is used to provide content integrity check to prevent your object from being overwritten. Even if you use the same object or link in multiple comparison requests, our backend still returns a low similarity result, and you may be unaware of this error. Therefore, you need to calculate MD5 with your backend, which is also true in the SDK case as the SDK doesn’t provide an MD5 check for the reason of backend disorder.
	
	
	
## FAQs

### Common errors during integration
- The service returns `invalid resourceUrl`. In this case, check whether the input URL meets the COS domain name requirement stated in the # Input Requirements.
- The service returns `FailedOperation.DownLoadError`. In this case, check whether the input URL is directly accessible from a public network.
- The service returns `MD5 Error`. In this case, check whether the content downloaded via the URL is same as what you calculated. For example, the `DetectReflectLivenessAndCompare` API needs two different URLs.

Other errors that are not easy to be identified during integration may be content errors, such as invalid LiveData in the `DetectReflectLivenessAndCompare` API or the error `FailedOperation.LifePhotoDetectFaces`. The cause may be that you need to upload the binary data but not the Base64 data of the image.

### FAQs Online
	Some inevitable algorithm problems may appear after successful integration of the service. If this is the case, you can record the returned RequestIDs and your request parameters, and [contact us](https://intl.cloud.tencent.com/zh/contact-us). 

# Downloading resources
	
Some APIs return images. For example, `DetectReflectLivenessAndCompare` returns `BestFrame`. We do transfer these images with short-term URLs. You need to download or transfer these images in time before we clear them.
	
