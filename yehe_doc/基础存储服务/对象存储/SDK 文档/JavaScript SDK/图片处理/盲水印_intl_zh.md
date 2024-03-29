## 简介

本文档提供关于盲水印的相关的 API 概览以及 SDK 示例代码。

关于盲水印 API 文档请参见 [盲水印](https://intl.cloud.tencent.com/document/product/1045/43029)。


## 添加盲水印

#### 功能说明

盲水印支持在上传时添加以及下载时添加。

#### 示例代码一：上传时添加盲水印

```html
<!-- html 页面 DOM 元素 -->

<!-- 选择要上传的文件 -->
<input id="fileSelector" type="file" />
<!-- 点击按钮上传 -->
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
        // 万象持久化接口，上传时持久化
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
    document.getElementById('msg').innerText = '未选择上传文件';
    return;
  }
  handleFileInUploading();
};
```

#### 示例代码二：下载时添加盲水印

```html
<!-- html 页面 DOM 元素 -->

<!-- 点击按钮下载文件并在下载时使用图片处理 -->
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
