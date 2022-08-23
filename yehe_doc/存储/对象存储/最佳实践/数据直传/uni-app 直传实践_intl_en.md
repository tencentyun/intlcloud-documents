## Overview
This document describes how to use simple code to upload files to a COS bucket directly via uni-app without using an SDK.

>? This document is based on the XML API [PostObject](https://intl.cloud.tencent.com/document/product/436/14690).
>

## Solution

### Directions

1. Select a file in the frontend, and the frontend sends the file extension to the server.
2. The server generates a random COS file path with time according to the file extension, calculates the corresponding PostObject policy signature, and returns the URL and signing information to the frontend.
3. The frontend calls the [PostObject API](https://intl.cloud.tencent.com/document/product/436/14690) to upload the file to COS.

### Strengths

- Permission security: The PostObject policy signature effectively limits the security permission scope and can only be used to upload to a specified file path.
- Path security: The server determines the random COS file path, which effectively avoids the problem of overwriting existing files and security risks.
- Multi-terminal compatibility: The file selection and upload APIs provided by uni-app can be used to make the same code compatible with multiple terminals (web, mini programs, or apps).


## Prerequisites

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5) and create a bucket to obtain the `Bucket` (bucket name) and `Region` (region name). For more information, please see [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309).
2. Log in to the [CAM console](https://console.cloud.tencent.com/cam/capi) and obtain the `SecretId` and `SecretKey` of your project.
3. Go to the details page of the newly created bucket, choose **Security Management** > **CORS (Cross-Origin Resource Sharing)**, and click **Add a Rule**. A configuration example is shown in the following figure. For more information, see [Setting Cross-Origin Access](https://intl.cloud.tencent.com/document/product/436/13318).



## Directions

>! Before formal deployment, it is recommended that you add a permission verification step for your website itself on the server side.
>

### Frontend upload

1. Implement a server API to generate random file paths, calculate signatures, and return them to the frontend. For implementation details, see the [post-policy example](https://github.com/tencentyun/cos-demo/tree/main/server/post-policy/).
2. Use HBuilderX's default template to create a uni-app app.
The created app is a Vue project.
3. Copy the following code to replace the content of the `pages/index/index.vue` file and modify the `post-policy` API call link to make it point to your server address (the server API implemented in step 1).
```html
<template>
   <view class="content">
      <button type="default" @click="selectUpload">Select file upload</button>
      <image v-if="fileUrl" class="image" :src="fileUrl"></image>
   </view>
</template>

<script>
   export default {
      data() {
         return {
            title: 'Hello',
            fileUrl: ''
         };
      },
      onLoad() {

      },
      methods: {
         selectUpload() {

            var vm = this;

            // URL-encode more characters.
            var camSafeUrlEncode = function (str) {
               return encodeURIComponent(str)
                       .replace(/!/g, '%21')
                       .replace(/'/g, '%27')
                       .replace(/\(/g, '%28')
                       .replace(/\)/g, '%29')
                       .replace(/\*/g, '%2A');
            };

            // Get the upload path and credential
            var getUploadInfo = function (extName, callback) {
               // Pass in the file extension to enable the backend to generate a random COS object path and return the upload domain name and the policy signature required by the `PostObject` API.
               // Refer to the server example at https://github.com/tencentyun/cos-demo/tree/main/server/post-policy
               uni.request({
                  url: 'http://127.0.0.1:3000/post-policy?ext=' + extName,
                  success: (res) => {
                     callback && callback(null, res.data.data);
                  },
                  error(err) {
                     callback && callback(err);
                  },
               });
            };

            // Initiate an upload request, and the upload uses the `PostObject` API and policy signature protection.
            // API documentation: https://intl.cloud.tencent.com/document/product/436/14690#.E7.AD.BE.E5.90.8D.E4.BF.9D.E6.8A.A4
            var uploadFile = function (opt, callback) {
               var formData = {
                  key: opt.cosKey,
                  policy: opt.policy, // Base64 policy string
                  success_action_status: 200,
                  'q-sign-algorithm': opt.qSignAlgorithm,
                  'q-ak': opt.qAk,
                  'q-key-time': opt.qKeyTime,
                  'q-signature': opt.qSignature,
               };
               // If the server uses a temporary key for calculation, you need to pass in `x-cos-security-token`.
               if (opt.securityToken) formData['x-cos-security-token'] = opt.securityToken;
               uni.uploadFile({
                  url: 'https://' + opt.cosHost, // This is only an example, not the real API address.
                  filePath: opt.filePath,
                  name: 'file',
                  formData: formData,
                  success: (res) => {
                     if (![200, 204].includes(res.statusCode)) return callback && callback(res);
                     var fileUrl = 'https://' + opt.cosHost + '/' + camSafeUrlEncode(opt.cosKey).replace(/%2F/g, '/');
                     callback && callback(null, fileUrl);
                  },
                  error(err) {
                     callback && callback(err);
                  },
               });
            };

            // Select the file
            uni.chooseImage({
               success: (chooseImageRes) => {
                  var file = chooseImageRes.tempFiles[0];
                  if (!file) return;
                  // Get the path of the local file to upload
                  var filePath = chooseImageRes.tempFilePaths[0];
                  // Get the extension of the file to upload and then the backend can generate a random COS path
                  var fileName = file.name;
                  var lastIndex = fileName.lastIndexOf('.');
                  var extName = lastIndex > -1 ? fileName.slice(lastIndex + 1) : '';
                  // Get the domain name, path, and credential for pre-upload
                  getUploadInfo(extName, function (err, info) {
                     // Upload the file
                     info.filePath = filePath;
                     uploadFile(info, function (err, fileUrl) {
                        vm.fileUrl = fileUrl;
                     });
                  });
               }
            });
         },
      }
   }
</script>

<style>
   .content {
      padding: 20px 0;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
   }

   .image {
      margin-top: 20px;
      margin-left: auto;
      margin-right: auto;
   }
</style>
```
4. In HBuilderX, choose **Run** > **Run to browser** > **Chrome**. Then you can select files to upload in the browser.
The execution result is as shown below:

 - Direct upload effect:
![uni-app direct upload effect](https://qcloudimg.tencent-cloud.cn/raw/ef40cb5ea3ce5a0586dd1a70d6b2d4ad.jpg)

## Demo Code Address

Demo download address: [upload-demo](https://github.com/tencentyun/cos-demo/tree/main/uni-app/upload-demo)

