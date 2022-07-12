## Overview

This document provides an overview of APIs and SDK code samples for basic image processing.

<table>
   <tr>
      <th>Service</td>
      <th>Feature</td>
      <th>Description</td>
   </tr>
   <tr>
      <td rowspan=11>Basic image processing</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36366">Scaling</a></td>
      <td>Proportional scaling, scaling image to target width and height</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36367">Cropping</a></td>
      <td>Regular cropping, cropping and scaling, inscribed circle cropping, intelligent face cropping</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36368">Rotation</a></td>
      <td>Adaptive rotation, regular rotation</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36369">Format conversion</a></td>
      <td>Format conversion, GIF format optimization, progressive display</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36370">Quality change</a></td>
      <td>Quality change for JPG and WebP images</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36371">Gaussian blurring</a></td>
      <td>Image blurring</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36372">Sharpening</a></td>
      <td>Image sharpening</td>
   </tr>
   <tr>
      <td>Watermarking</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36373">Image watermark</a>, <a href="https://intl.cloud.tencent.com/document/product/436/36374">text watermark</a></td>
   </tr>
   <tr>
      <td>Image information acquisition</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36375">Basic information</a>, <a href="https://intl.cloud.tencent.com/document/product/436/36376">EXIF information</a>, <a href="https://intl.cloud.tencent.com/document/product/436/36377">average hue</a></td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36378">Metadata removal</a></td>
      <td>Including EXIF information</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36379">Quick thumbnail template</a></td>
      <td>Quick image format conversion, scaling, and cropping for thumbnail generation</td>
   </tr>
</table>



## Processing Image During Upload

The following example shows how to automatically process an image when you upload it to COS.

When the image is uploaded successfully, COS will save both the original and the processed images. You can later obtain the processing results by using a general download request.

### Sample code

```html
<!-- DOM element on the HTLM page -->

<!-- Choose a file to upload -->
<input id="fileSelector" type="file" />
<!-- Click the button for upload-->
<input id="submitBtn" type="submit" />
```

```javascript
function handleFileInUploading(file) {
  cos.putObject(
    {
      Bucket: 'examplebucket-1250000000',
      Region: 'COS_REGION',
      Key: file.name,
      Body: file,
      Headers: {
        // Use the `imageMogr2` API to scale the image (by specifying the width of the output image to 200, with the height scaled proportionally).
        'Pic-Operations':
          '{"is_pic_info": 1, "rules": [{"fileid": "desample_photo.jpg", "rule": "imageMogr2/thumbnail/200x/"}]}',
      },
    },
    function (err, data) {
      console.log(err || data);
    },
  );
}

document.getElementById('submitBtn').onclick = function (e) {
  var file = document.getElementById('fileSelector').files[0];
  if (!file) {
    document.getElementById('msg').innerText = 'No file selected for upload';
    return;
  }
  handleFileInUploading(file);
};
```

## Processing In-Cloud Image

The following example shows how to process an image stored in COS and save the processing result to COS.

### Sample code

```html
<!-- DOM element on the HTLM page -->

<!-- Click the button to process the in-cloud image -->
<input id="submitBtn" type="submit" />
```

```javascript
function handleFileInBucket() {
  cos.request(
    {
      Bucket: 'examplebucket-1250000000',
      Region: 'COS_REGION',
      Key: 'exampleImage',
      Method: 'POST',
      Action: 'image_process',
      Headers: {
        // Use the `imageMogr2` API to scale the image (by specifying the width of the output image to 200, with the height scaled proportionally).
        'Pic-Operations':
          '{"is_pic_info": 1, "rules": [{"fileid": "desample_photo.jpg", "rule": "imageMogr2/thumbnail/200x/"}]}',
      },
    },
    function (err, data) {
      console.log(err || data);
    },
  );
}

document.getElementById('submitBtn').onclick = function (e) {
  handleFileInBucket();
};
```

## Processing Image During Download

The following example shows how to process an image during download.

### Sample code

```html
<!-- DOM element on the HTLM page -->

<!-- Click the button to download and process the image -->
<input id="submitBtn" type="submit" />
```

```javascript
function getObject() {
  cos.getObject(
    {
      Bucket: 'examplebucket-1250000000',
      Region: 'COS_REGION',
      Key: 'exampleobject',
      QueryString: `imageMogr2/thumbnail/200x/`,
    },
    function (err, data) {
      console.log(err || data);
    },
  );
}
```

## Generating Signed URL with Image Processing Parameters

### Sample code

```javascript
// Generate a signed URL (valid for 30 minutes) with image processing parameters.
cos.getObjectUrl(
  {
    Bucket: 'examplebucket-1250000000',
    Region: 'COS_REGION',
    Key: 'exampleobject',
    Query: {
        `imageMogr2/thumbnail/200x/`: ''
    },
    Expires: 1800,
    Sign: true,
  },
  function (err, data) {
    if (data) {
      console.log(data.URL);
    }
  },
);

// Generate an unsigned URL with image processing parameters.
cos.getObjectUrl(
  {
    Bucket: 'examplebucket-1250000000',
    Region: 'COS_REGION',
    Key: 'exampleobject',
    Query: {
      `imageMogr2/thumbnail/200x/`: ''
    },
    Sign: false,
  },
  function (err, data) {
    if (data) {
      console.log(data.URL);
    }
  },
);
```

