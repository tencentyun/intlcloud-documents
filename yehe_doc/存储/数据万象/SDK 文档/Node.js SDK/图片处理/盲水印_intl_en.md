## Overview

This document provides an overview of APIs and SDK code samples for blind watermarking.

For blind watermark APIs, see [Blind Watermarking](https://intl.cloud.tencent.com/document/product/1045/43029).


## Adding Blind Watermark

#### Feature description

You can add a blind watermark when uploading or downloading an object.

#### Sample 1: Adding a blind watermark during upload

```javascript
const filePath = "temp-file-to-upload" // Local file path
cos.putObject({
   Bucket: 'examplebucket-1250000000',
   Region: 'COS_REGION',
   Key: 'exampleobject',
   Body: fs.createReadStream(filePath), // Uploaded file object
   Headers: {
	   // CI's persistent processing API during upload
	   'Pic-Operations': '{"is_pic_info": 1, "rules": [{"fileid": "desample_photo.jpg", "rule": "watermark/3/type/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAwMDQucGljc2gubXlxY2xvdWQuY29tL3NodWl5aW4uanBn"}]}'
  },
}, function(err, data) {
   console.log(err || data);
});
```

#### Sample 2: Adding a blind watermark during download

```javascript
cos.getObject({
    Bucket: 'examplebucket-1250000000',
    Region: 'COS_REGION',
    Key: 'exampleobject',
    QueryString: 'watermark/3/type/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAwMDQucGljc2gubXlxY2xvdWQuY29tL3NodWl5aW4uanBn',
}, function (err, data) {
   console.log(err || data);
   fs.writeFileSync('filepath', data.Body);  // Save the image locally
});
```
