VOD provides a web upload SDK for scenarios where audio/video files are uploaded through a browser. If you need the SDK source code, please click [here](https://github.com/tencentyun/vod-js-sdk-v6).

## Simple Upload of Video

### Importing SDK

#### Importing by using script tag
If webpack is not used, a `script` tag can be used for import in the following ways. This method will expose the global variable `TcVod`.
- **Download to the local file system**
	Click [here](https://github.com/tencentyun/vod-js-sdk-v6) to download the SDK source code to the local file system, and import it by running the following command:
```html
<script src="./vod-js-sdk-v6.js"></script>
```
>?Change the value of `src` to the path to the source code you saved locally.
- **Import with CDN**
	Import with CDN in the following ways:
```html
<script src="https://cdn-go.cn/cdn/vod-js-sdk-v6/latest/vod-js-sdk-v6.js"></script>
```

Click [here](https://tencentyun.github.io/vod-js-sdk-v6/) to view the demo imported through script. The source code of the demo can be viewed [here](https://github.com/tencentyun/vod-js-sdk-v6/blob/master/docs/index.html).

#### Importing by using npm command
If webpack (such as Vue or React) is used, `npm` can be used for import.
```js
// After running npm install vod-js-sdk-v6, import directly on the page by running import
import TcVod from 'vod-js-sdk-v6'
```

Click [here](https://github.com/tencentyun/vod-js-sdk-v6/tree/master/docs/import-demo) to view the source code of the demo imported through npm.

>!The SDK relies on Promise, which should be imported if your browser version is low.


### Defining the function to get an upload signature

```js
function getSignature() {
  return axios.post(url).then(function (response) {
    return response.data.signature;
  })
};
```

>? `url` is the URL of your signature distribution service. For more information, please see [Guide](https://intl.cloud.tencent.com/document/product/266/33921) for upload from client.
> For details on how to calculate `signature`, please see [Signature for Upload from Client](https://intl.cloud.tencent.com/document/product/266/33922).

### Video upload example



```js
// If imported through import, run new TcVod(opts)
// new TcVod.default(opts) is imported through script
const tcVod = new TcVod.default({
  getSignature: getSignature // The function to get the upload signature described above
})

const uploader = tcVod.upload({
  mediaFile: mediaFile, // Media file (video, audio, or image) in File type
})
uploader.on('media_progress', function(info) {
  console.log(info.percent) // Progress
})

// Callback result description
// type doneResult = {
//   fileId: string,
//   video: {
//     url: string
//   },
//   cover: {
//     url: string
//   }
// }
uploader.done().then(function (doneResult) {
  // Deal with doneResult
}).catch(function (err) {
  // Deal with error
})


```

>?
>- `opts` in `new TcVod(opts)` refers to parameters of the `TcVod` API. For more information, please see [API Description](#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0).
>- The upload method automatically selects simple upload or multipart upload based on the file size, eliminating your need to take care of every step in multipart upload.
>- To upload to the specified subapplication, please see [Subapplication System - Upload from client](https://intl.cloud.tencent.com/document/product/266/33987).

## Advanced Features

### Uploading both video and cover

```js
const uploader = tcVod.upload({
  mediaFile: mediaFile,
  coverFile: coverFile,
})

uploader.done().then(function (doneResult) {
  // Deal with doneResult
})
```

### Getting upload progress

The SDK supports displaying the current upload progress in the form of callback:

```js
const uploader = tcVod.upload({
  mediaFile: mediaFile,
  coverFile: coverFile,
})
// When the video upload is completed
uploader.on('media_upload', function(info) {
  uploaderInfo.isVideoUploadSuccess = true;
})
// Video upload progress
uploader.on('media_progress', function(info) {
  uploaderInfo.progress = info.percent;
})
// When the cover upload is completed
uploader.on('cover_upload', function(info) {
  uploaderInfo.isCoverUploadSuccess = true;
})
// Cover upload progress
uploader.on('cover_progress', function(info) {
  uploaderInfo.coverProgress = info.percent;
})

uploader.done().then(function (doneResult) {
  // Deal with doneResult
})
```

For more information about callback values of `xxx_upload` and `xxx_progress`, please see description on multipart upload/replication tasks in [Object Operations](https://intl.cloud.tencent.com/document/product/436/31538).

### Canceling upload

The SDK supports canceling ongoing video or cover upload:

```js
const uploader = tcVod.upload({
  mediaFile: mediaFile,
  coverFile: coverFile,
})

uploader.cancel()
```

### Checkpoint restart

The SDK supports automatic checkpoint restart with no human intervention required. When the upload is terminated unexpectedly (for reasons such as the browser is closed or the network connection is interrupted), you can upload the file again from where it left off, which helps reduce the upload time.

## API Description

### TcVod

| Parameter  | Required | Type | Description |
| ------------ | ---- | -------- | --------- |
| getSignature | Yes | Function | Function used to acquire the upload signature. |
| appId | No | number | Once entered, this parameter will be automatically carried in the built-in statistics report. |
| reportId | No | number | Once entered, this parameter will be automatically carried in the built-in statistics report. |

### TcVod.upload

| Parameter  | Required | Type | Description |
| ------------ | ---- | -------- | --------- |
| mediaFile | No | File | Media file (video, audio, or image). |
| coverFile | No | File | Cover file. |
| mediaName | No | string | The filename that will overwrite the metadata in the media file. |
| fileId | No | string | Passed in when the cover is modified. |
| reportId | No | number | Once entered, this parameter will be automatically carried in the built-in statistics report and overwrite the settings in the constructor. |

### Events

| Event Name | Required | Event Description |
| ------------ | ---- |  --------- |
| media_upload | No | When the media file is successfully uploaded. |
| cover_upload | No | When the cover is successfully uploaded. |
| media_progress | No | Media file upload progress. |
| cover_progress | No | Cover file upload progress. |

## FAQs

1. **How to get the `File` object?**
Use the `input` tag with the `type` being `file` to get the `File` object.
2. **Is there a size limit for an uploaded file?**
Up to 60 GB.
3. **What browsers does the SDK support?**
Chrome, Firefox, and other mainstream browsers that support `HTML5` as well as IE 10 or above.
4. **How to implement upload pause or resumable upload?**
Automatic resumable upload is implemented at the underlying layer of the SDK; therefore, the essence of pause is to call the `uploader.cancel()` method. Similarly, upload resumption after pause is also done by calling the initial `tcVod.upload` method. The difference lies in that the parameters of this method when the upload is resumed should be the previously cached parameters (for example, a global variable can be used to store the parameters when the upload is started and then cleared after upload is completed).

