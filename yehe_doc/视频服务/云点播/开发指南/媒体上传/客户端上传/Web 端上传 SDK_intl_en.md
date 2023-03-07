VOD provides an SDK for uploading files from browsers. You can download the SDK source code at [GitHub](https://github.com/tencentyun/vod-js-sdk-v6).

## Uploading Videos

### Importing the SDK

#### Importing by using a script tag
If Webpack is not used, you can import the SDK using a script tag. This method will expose the global variable `TcVod`. You can choose either of the two ways below:

- **Download to the local file system**
	[Download](https://github.com/tencentyun/vod-js-sdk-v6) the SDK source code to your local file system and use the code below to import the SDK:
```html
<script src="./vod-js-sdk-v6.js"></script>
```
>? Change the value of `src` to the local path of the source code.

- **Import from CDN**
	Use the code below to import the SDK from a CDN:
```html
<script src="https://cdn-go.cn/cdn/vod-js-sdk-v6/latest/vod-js-sdk-v6.js"></script>
```

Click [here](https://tencentyun.github.io/vod-js-sdk-v6/) to try a demo that imported the SDK using a script tag. The source code of the demo can be found [here](https://github.com/tencentyun/vod-js-sdk-v6/blob/master/docs/index.html).

#### Importing by using npm
If Webpack (such as Vue or React) is used, You can use npm to import the SDK:
```js
// Run `npm install vod-js-sdk-v6`, and use the command below to import the SDK directly on the page:
import TcVod from 'vod-js-sdk-v6'
```

Click [here](https://github.com/tencentyun/vod-js-sdk-v6/tree/master/docs/import-demo) to view the source code of a demo that imports the SDK using npm.

>! The SDK relies on promises, which you should import if your browser version is old.

### Defining the function to get an upload signature

```js
function getSignature() {
  return axios.post(url).then(function (response) {
    return response.data.signature;
  })
};
```

>? 
>- `url` is the URL of your signature distribution service. For more information, see the [Guide](https://intl.cloud.tencent.com/document/product/266/33921) for upload from a client.
>- For details on how to calculate `signature`, see [Signature for Upload from Client](https://intl.cloud.tencent.com/document/product/266/33922).
>- The upload signature contains information such as the **subapplication ID**, **video category**, and **task flow**. For more information, see [Descriptions of Signature Parameters](https://www.tencentcloud.com/document/product/266/33922).

### Video upload example


```js
// If the SDK is imported using the `import` command, run `new TcVod(opts)`.
// If the SDK is imported using a script tag, use `new TcVod.default(opts)`.
const tcVod = new TcVod.default({
  getSignature: getSignature // The function to get the upload signature
})

const uploader = tcVod.upload({
  mediaFile: mediaFile, // The media file (video, audio, or image), whose data type is file.
})
uploader.on('media_progress', function(info) {
  console.log(info.percent) // The upload progress
})

// Callback of the result
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
>- `opts` in `new TcVod(opts)` refers to parameters of the `TcVod` API. For details, see [API Description](#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0).
>- The upload API automatically selects simple upload or multipart upload based on the file size. You don’t need to manually set up multipart upload.
>- To upload to a subapplication, see [Subapplication System - Upload from client](https://intl.cloud.tencent.com/document/product/266/33987).

## Advanced Features

### Uploading both the video and thumbnail

```js
const uploader = tcVod.upload({
  mediaFile: mediaFile,
  coverFile: coverFile,
})

uploader.done().then(function (doneResult) {
  // Deal with doneResult
})
```

### Getting the upload progress

The SDK can notify you of the upload progress via callbacks:

```js
const uploader = tcVod.upload({
  mediaFile: mediaFile,
  coverFile: coverFile,
})
// When the video upload is completed
uploader.on('media_upload', function(info) {
  uploaderInfo.isVideoUploadSuccess = true;
})
// The video upload progress
uploader.on('media_progress', function(info) {
  uploaderInfo.progress = info.percent;
})
// When the thumbnail upload is completed
uploader.on('cover_upload', function(info) {
  uploaderInfo.isCoverUploadSuccess = true;
})
// The thumbnail upload progress
uploader.on('cover_progress', function(info) {
  uploaderInfo.coverProgress = info.percent;
})

uploader.done().then(function (doneResult) {
  // Deal with doneResult
})
```

For details about the return values of `xxx_upload` and `xxx_progress`, see [Object Operations](https://www.tencentcloud.com/document/product/436/43552).

### Canceling upload

The SDK supports canceling ongoing video or thumbnail upload:

```js
const uploader = tcVod.upload({
  mediaFile: mediaFile,
  coverFile: coverFile,
})

uploader.cancel()
```

### Checkpoint restart

The SDK supports automatic checkpoint restart for uploads. If an upload is interrupted unexpectedly (for example, because the browser is closed or the network is disconnected), you can continue uploading the file from where it left off.

## API Description

### TcVod

| Parameter  | Required | Type | Description |
| ------------ | ---- | -------- | --------- |
| getSignature | Yes | Function | The function used to get the upload signature. |
| appId | No | number | If this parameter is set, it will be carried by the built-in statistical report system. |
| reportId | No | number | If this parameter is set, it will be carried by the built-in statistical report system. |

### TcVod.upload

| Parameter  | Required | Type | Description |
| ------------ | ---- | -------- | --------- |
| mediaFile | No | File | The media file (video, audio, or image). |
| coverFile | No | File | The thumbnail file. |
| mediaName | No | string | The filename, which will overwrite the filename in the metadata. |
| fileId | No | string | The ID of the new thumbnail file. |
| reportId | No | number | If this parameter is set, it will be carried by the built-in statistical report system and will overwrite the settings in the constructor. |
| fileParallelLimit | No    | number     | The maximum number of concurrent uploads allowed in the same instance. Default value: 3. |
| chunkParallelLimit    | No    | number     | The maximum number of upload parts allowed for the same file. Default value: 6.  |
| chunkRetryTimes    | No    | number     | The maximum number of retry attempts for multipart upload. Default value: 2 (three upload requests in total).  |
| chunkSize    | No    | number     | The part size (bytes) for multipart upload. Default value: 8388608 (8 MB).  |
| progressInterval    | No    | number     | The interval (ms) of sending the `onProgress` callback. Default value: 1000.  |

### Events

| Event Name | Required | Description |
| ------------ | ---- |  --------- |
| media_upload | No | The media file is successfully uploaded. |
| cover_upload | No | The thumbnail is successfully uploaded. |
| media_progress | No | The media file upload progress. |
| cover_progress | No | The thumbnail file upload progress. |

## FAQs

1. **How do I get the file object?**
Use the `input` tag and set `type` to `file`.
2. **Is there a size limit for upload?**
The maximum file size allowed is 60 GB.
3. **What browsers does the SDK support?**
The SDK supports Chrome, Firefox, and other mainstream browsers that support HTML5. It can also be used on IE 10 or later.
4. **How to pause and resume an upload?**
Automatic checkpoint restart is implemented at the underlying layer of the SDK. Therefore, to pause an upload, simply call `uploader.cancel()`, and to resume an upload after pause, call `tcVod.upload`. Note that when you use `tcVod.upload` to resume an upload, you need to pass in the same parameters used when you initiate the upload (you can use a global variable to save the parameters when you initiate the upload and delete them after upload.)
5. **Does the SDK support `https:` upload?**
Yes, it does. The SDK uses `http:` for upload on HTTP pages and `https:` on non-HTTP pages. 