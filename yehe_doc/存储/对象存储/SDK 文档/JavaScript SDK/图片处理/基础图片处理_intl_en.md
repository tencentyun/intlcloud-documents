## Overview

This document provides an overview of APIs and SDK code samples related to basic image processing.

<table>
   <tr>
      <th>Service</td>
      <th>Feature</td>
      <th>Description</td>
   </tr>
   <tr>
      <td rowspan=11>Basic Image Processing</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36366">Scaling</a></td>
      <td>Proportional scaling, scaling image to target width and height, and more</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36367">Cropping</a></td>
      <td>Cut (regular cropping), crop (scaling and cropping), iradius (inscribed circle cropping), and scrop (smart cropping)</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36368">Rotation</a></td>
      <td>Adaptive rotation and common rotation</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36369">Format conversion</a></td>
      <td>Format conversion, GIF optimization, and progressive display</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36370">Quality conversion</a></td>
      <td>Changes the quality of images in JPG and WEBP formats</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36371">Gaussian blurring</a></td>
      <td>Blurs images</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36372">Sharpening</a></td>
      <td>Sharpens images</td>
   </tr>
   <tr>
      <td>Watermarking</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36373">Image watermarks</a>, <a href="https://intl.cloud.tencent.com/document/product/436/36374">text watermarks</a></td>
   </tr>
   <tr>
      <td>Obtaining image information</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36375">Basic information</a>, <a href="https://intl.cloud.tencent.com/document/product/436/36376">EXIF data</a>, <a href="https://intl.cloud.tencent.com/document/product/436/36377">average hue</a></td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36378">Removing metadata</a></td>
      <td>Includes EXIF data</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36379">Quick thumbnail template</a></td>
      <td>Performs quick format conversion, scaling, and cropping to generate thumbnails</td>
   </tr>
</table>

The watermark text must be URL-safe Base64-encoded, which can be done by importing `js-base64`.

Sample code:

```javascript
1. Install dependencies in the project.
npm install --save js-base64

2. Import the `encode` method into the code.
import { encode } from 'js-base64';

// Text watermark content
var text = 'Tencent Cloud CI';
// Valid text watermark
var safeBase64 = encode(text).replaceAll('+', '-').replaceAll('/', '_').replaceAll('=', '');
// The following `Pic-Operations` can be used:
'Pic-Operations': `{"is_pic_info": 1, "rules": [{"fileid": "waterMask.jpg", "rule": "watermark/2/text/${safeBase64}"}]}`
```


## Processing Image Upon Upload

The following example shows how to automatically process an image when you upload it to COS.

When the image is uploaded successfully, COS will save both the original and the processed images. You can later obtain the processing results using a general download request.

### Sample code

```html
<!-- DOM element in the HTLM file -->

<!-- Choose an image to upload -->
<input id="fileSelector" type="file" />
<!-- Click the button to upload the image -->
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
        // Use the imageMogr2 API to scale the image (specifying the width of the output image to 200, with the height scaled automatically).
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
    document.getElementById('msg').innerText = 'File to upload not selected';
    return;
  }
  handleFileInUploading(file);
};
```

## Processing an In-Cloud Image

The following example shows how to process an in-cloud image and store the processing result in COS.

### Sample code

```html
<!-- DOM element in the HTLM file -->

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
        // Use the imageMogr2 API to scale the image (specifying the width of the output image to 200, with the height scaled automatically).
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

## Processing an Image upon the Download

The following sample shows how to process an image upon the download:

### Sample code

```html
<!-- DOM element in the HTLM file -->

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

## Generating a Signed URL with Image Processing Parameters

### Sample code

```javascript
// Generate a signed URL (effective for 30 minutes) with image processing parameters.
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
      // Use the browser to open the URL for preview or trigger the download
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
      // Use the browser to open the URL for preview or trigger the download
      console.log(data.URL);
    }
  },
);
```

