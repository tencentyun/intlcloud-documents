## Overview

This document provides an overview of APIs and SDK code samples for blind watermarking.

For blind watermark APIs, see [Blind Watermark](https://cloud.tencent.com/document/product/436/46782).

## Adding Blind Watermark

#### Feature description

You can add a blind watermark when uploading or downloading an object.

#### Sample 1: Adding a blind watermark during upload

```html
<view>
  <button type="primary" bindtap="button">Add a blind watermark during upload</button>
</view>
```

```javascript
Page({
  button: function () {
    wx.chooseMessageFile({
      count: 10,
      type: 'all',
      success: function (res) {
        var file = res.tempFiles[0];
        wxfs.readFile({
          filePath: file.path,
          success: function (res) {
            cos.putObject(
              {
                Bucket: 'examplebucket-1250000000',
                Region: 'COS_REGION',
                Key: file.name,
                Body: res.data,
                Headers: {
                  // CI's persistent processing API during upload
                  'Pic-Operations': '{"is_pic_info": 1, "rules": [{"fileid": "desample_photo.jpg", "rule": "watermark/3/type/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAwMDQucGljc2gubXlxY2xvdWQuY29tL3NodWl5aW4uanBn"}]}',
                },
              },
              (err, data) => {
                console.log(err || data);
              },
            );
          },
          fail: (err) => console.error(err),
        });
      },
      fail: (err) => console.error(err),
    });
  },
});
```

#### Sample 2: Adding a blind watermark during download

```html
<view>
  <button type="primary" bindtap="button">Add a blind watermark during download</button>
</view>
```

```javascript
Page({
  button: function () {
    cos.getObject(
      {
        Bucket: 'examplebucket-1250000000',
        Region: 'COS_REGION',
        Key: 'exampleImage',
        QueryString: `watermark/3/type/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAwMDQucGljc2gubXlxY2xvdWQuY29tL3NodWl5aW4uanBn`,
      },
      (err, data) => {
        console.log(err || data);
      },
    );
  },
});
```

