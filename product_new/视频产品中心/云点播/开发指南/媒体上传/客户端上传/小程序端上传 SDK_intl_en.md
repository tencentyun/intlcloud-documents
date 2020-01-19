VOD provides a video upload SDK for WeChat Mini Program. For more information on the upload process, please see [Guide for Upload from Client](/document/product/266/9219).

- If you need the SDK source code, please click [here](https://github.com/tencentyun/vod-wx-sdk-v2/).
- If you need the Demo source code, please click [here](https://github.com/tencentyun/vod-wx-sdk-v2/tree/master/demo).

## Video Upload Steps

**1. Import the SDK**

```
const VodUploader = require('../../lib/vod-wx-sdk-v2.js');
```

**2. Define the function to get an upload signature**

```
getSignature: function(callback) {
    wx.request({
        url: 'https://xzb.qcloud.com/get_vod_sign',
        method: 'POST',
        data: {
            Action: 'GetVodSignatureV2'
        },
        dataType: 'json',
        success: function(res) {
            if (res.data && res.data.data.signature) {
                callback(res.data.data.signature);
            } else {
                return 'Failed to get the signature';
            }
        }
    });
}
```

>
- `url` is the URL of your signature distribution service. For more information, please see [Guide for Upload from Client](https://cloud.tencent.com/document/product/266/9219).
- For the rule of `signature` calculation, please see [Signature for Upload from Client](https://cloud.tencent.com/document/product/266/9221).

**3. Upload a video**
Video upload is implemented by calling `VodUploader.start`, and video selection is implemented by the `wx.chooseVideo` method in the WeChat Mini Program API. Below is an example:

```
 VodUploader.start({
    mediaFile: videoFile, // Pass in the `file` parameter called back by `chooseVideo`, which is required
    getSignature: getSignature, // The function to get the signature, which is required

    mediaName: fileName, // Video name, which is optional. You are strongly recommended to enter this parameter, and if it is left empty, "From WeChat Mini Program" will be used by default
    coverFile: coverFile, // Video cover, which is optional
    success: function(result) {
        console.log('success');
        console.log(result);
    },
    error: function(result) {
        console.log('error');
        console.log(result);
        wx.showModal({
            title: 'Upload failed',
            content: JSON.stringify(result),
            showCancel: false
        });
    },
    progress: function(result) {
        console.log('progress');
        console.log(result);
    },
    finish: function(result) {
        console.log('finish');
        console.log(result);
        wx.showModal({
            title: 'Upload succeeded',
            content: 'fileId:' + result.fileId + '\nvideoName:' + result.videoName,
            showCancel: false
        });
    }
});
```

## Notes

1. As the WeChat Mini Program does not have an API to get the actual filename, you need to enter the video name before uploading the video; otherwise, the SDK will set the video name to "From WeChat Mini Program".
1. Resumable upload and multipart upload are not supported.
1. In the WeChat Mini Program domain name information, simply add `vod2.qcloud.com` to a valid domain name for `request` and `uploadFile`.
