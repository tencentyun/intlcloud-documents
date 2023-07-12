## Overview

This document provides an overview of APIs and SDK code samples for blind watermarking.

For blind watermark APIs, see [Blind Watermarking](https://intl.cloud.tencent.com/document/product/1045/43029).


## Adding Blind Watermark

#### Feature description

You can add a blind watermark when uploading or downloading an object.

#### Sample 1: Adding a blind watermark during upload

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
        // CI's persistent processing API during upload
        'Pic-Operations':
          '{"is_pic_info": 1, "rules": [{"fileid": "desample_photo.jpg", "rule": "watermark/3/type/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAwMDQucGljc2gubXlxY2xvdWQuY29tL3NodWl5aW4uanBn"}]}',
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
  handleFileInUploading();
};
```

#### Sample 2: Adding a blind watermark during download

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
      QueryString: `watermark/3/type/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAwMDQucGljc2gubXlxY2xvdWQuY29tL3NodWl5aW4uanBn`,
    },
    function (err, data) {
      console.log(err || data);
    },
  );
}
```
