VOD provides a web upload SDK for scenarios where audio/video files are uploaded through a browser. If you need the SDK source code, please click [here](https://github.com/tencentyun/vod-js-sdk-v6).

## Simple Video Upload

#### How to import an SDK

- **Import through script**
If webpack is not used, a `script` tag can be used for import. This method will expose the global variable `TcVod`.
```html
<script src="//unpkg.com/vod-js-sdk-v6"></script>
```
Click [here](https://tencentyun.github.io/vod-js-sdk-v6/) to view the demo imported through script. The source code of the demo can be viewed [here](https://github.com/tencentyun/vod-js-sdk-v6/blob/master/docs/index.html).
- **Import through npm**
If webpack (such as Vue or React) is used, npm can be used for import.
```js
// After running `npm install vod-js-sdk-v6`, import directly on the page by running `import`
import TcVod from 'vod-js-sdk-v6'
```
Click [here](https://github.com/tencentyun/vod-js-sdk-v6/tree/master/docs/import-demo) to view the source code of the demo imported through npm.

> The SDK relies on Promise, which should be imported if your browser version is low.

#### Defining the function to get an upload signature

```js
function getSignature() {
  return axios.post(url).then(function (response) {
    return response.data.signature;
  })
};
```

> `url` is the URL of your signature distribution service. For more information, please see [Guide for Upload from Client](https://intl.cloud.tencent.com/document/product/266/33921).
> For the rule of `signature` calculation, please see [Signature for Upload from Client](https://intl.cloud.tencent.com/document/product/266/33922).

#### Video upload example



```js
// If imported through `import`, run `new TcVod(opts)`
// new TcVod.default(opts) is the usage imported through script
const tcVod = new TcVod.default({
  getSignature: getSignature // The function to get the upload signature described above
})

const uploader = tcVod.upload({
  mediaFile: mediaFile, // Media file (video, audio, or image) in `File` type
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
  // deal with doneResult
}).catch(function (err) {
  // deal with error
})


```

>The upload method automatically selects simple upload or multipart upload based on the file size, eliminating your need to take care of every step in multipart upload.

## Advanced Features

#### Uploading both video and cover

```js
const uploader = tcVod.upload({
  mediaFile: mediaFile,
  coverFile: coverFile,
})

uploader.done().then(function (doneResult) {
  // deal with doneResult
})
```

#### Getting upload progress

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
  // deal with doneResult
})
```

For the callback values of `xxx_upload` and `xxx_progress`, please see [Multipart Upload/Copy Task Operation](https://intl.cloud.tencent.com/document/product/436/31538#.E5.88.86.E7.89.87.E4.B8.8A.E4.BC.A0.E5.AF.B9.E8.B1.A1).

#### Canceling upload

The SDK supports canceling ongoing video or cover upload:

```js
const uploader = tcVod.upload({
  mediaFile: mediaFile,
  coverFile: coverFile,
})

uploader.cancel()
```

#### Resumable upload

The SDK supports automatically resumable upload with no human intervention required. When the upload is terminated unexpectedly (for reasons such as the browser is closed or the network connection is interrupted), you can upload the file again from where it left off, which helps reduce the upload time.

## API Description

#### TcVod

| Parameter Name | Required | Type | Description |
| ------------ | ---- | -------- | --------- |
| getSignature | Yes | Function | The function to get the upload signature. |
| appId | No | number | Once entered, this parameter will be automatically carried in the built-in statistics report. |
| reportId | No | number | Once entered, this parameter will be automatically carried in the built-in statistics report. |

#### TcVod.upload

| Parameter Name | Required | Type | Description |
| ------------ | ---- | -------- | --------- |
| mediaFile | No | File | Media file (video, audio, or image). |
| coverFile | No | File | Cover file. |
| mediaName | No | string | The filename that will overwrite the metadata in the media file. |
| fileId | No | string | Passed in when the cover is modified. |
| reportId | No | number | Once entered, this parameter will be automatically carried in the built-in statistics report and overwrite the settings in the constructor. |

#### Event

| Event Name | Required | Event Description |
| ------------ | ---- |  --------- |
| media_upload | No | When the media file is successfully uploaded. |
| cover_upload | No | When the cover is successfully uploaded. |
| media_progress | No | Media file upload progress. |
| cover_progress | No | Cover file upload progress. |

## FAQs

1. **How to get the `File` object?**
Use the `input` tag with the ` type` being `file` to get the` File` object.
2. **Is there a size limit for an uploaded file?**
Up to 60 GB.
3. **What browsers does the SDK support?**
Chrome, Firefox, and other mainstream browsers that support `HTML5` as well as IE 10 or above.
4. **How to implement upload pause or resumable upload?**
Automatically resumable upload is implemented at the underlying layer of the SDK; therefore, the essence of pause is to call the `uploader.cancel()` method. Similarly, upload resumption after pause is also done by calling the initial `tcVod.upload` method. The difference lies in that the parameters of this method when the upload is resumed should be the previously cached parameters (for example, a global variable can be used to store the parameters when the upload is started and then cleared after upload is completed).


