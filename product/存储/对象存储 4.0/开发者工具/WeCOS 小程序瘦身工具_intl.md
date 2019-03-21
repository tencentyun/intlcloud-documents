## Feature Description
To make Mini Programs run more smoothly, WeChat only supports uploading compiled code packages that are less than 1 MB. However, during development of Mini Programs, image resources are often large in size, and code packages may exceed 1 MB.

With the WeCOS tool, image resources in Mini Programs can be automatically uploaded to COS, and then removed from the project directory with the image resource address in codes replaced by online address. As a result, the size of the code package is reduced.

Installation and configuration instructions for WeCOS are as follows:
## Preparations
1. Sign up for a Tencent Cloud account at the [Tencent Cloud official website](https://intl.cloud.tencent.com/). For more information, see [Signing up for Tencent Cloud](/doc/product/378/9603).
2. Log in to [COS Console](https://console.cloud.tencent.com/cos4), activate the COS service, and then [create a bucket](/doc/product/436/6232).
3. Get the [WeCOS tool](https://github.com/tencentyun/wecos) in GitHub.
4. Download the environment at the [Node.js official website](https://nodejs.org/) and install it.

## Starting Installation
Execute the following command to install WeCOS:

```js
npm install -g wecos
```

## Basic Configuration
Create the `wecos.config.json` file under a directory at the same level as the Mini Program directory. The file configuration example is described as follows:

```json
{
  "appDir": "./app",
  "cos": {
    "secret_id": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    "secret_key": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    "bucket": "wxapp-1251902136",
    "region": "ap-guangzhou", 
    "folder": "/"
  }
}
```

"region": The region abbreviation selected when a bucket is created.
"folder": The bucket directory in which resources are stored.

### Configuration items

| Configuration Item | Type | Description |
| ------ | ------------ | ---------------------------------------- |
| appDir | String | The directory of a Mini Program project. Default: `./app`. |
| cos | Object | Required. For configuration information such as bucket and region, see [Bucket Overview](https://cloud.tencent.com/document/product/436/13312). Keys and other information can be found in the [Cloud API Key Console](https://console.cloud.tencent.com/cos4/secret). |


## Getting Started
Execute the following command under a directory at the same level as the configuration file:
```
wecos
```

>!Before executing the command, you need to create the `wecos.config.json` file under a directory at the same level as the configuration file.

## Advanced Configuration

| Configuration Item | Type | Description |
| ------------------- | ------------- | --------------------------------------- |
| backupDir | String | Backup directory. Default: `./wecos_backup`. |
| uploadFileSuffix | Array | Suffix of the uploaded image. Default: `[".jpg", ".png", ".gif"]`. |
| uploadFileBlackList | Array | Blacklist of image resources. Default: `[]`. |
| replaceHost | String | Replaces the specified domain name with targetHost. Default: `''`. |
| targetHost | String | Custom domain name is used. Default: `''`. |
| compress | Boolean | Indicates whether to compress images. Default: `false`. |
| watch | Boolean | Indicates whether to listen to the project directory in real time. Default: `true`. |

#### Configure backup directory
WeCOS deletes the images under a project after uploading them to COS, which may result in risks of source file loss. Therefore, the backup feature is provided to back up each uploaded image to a directory at the same level as the project directory. You can modify the name of the backup directory using the following configurations. If you want to disable the feature, set the value to null:
```
  "backupDir": "./wecos_backup"
```
#### Configure image suffix
You can use the image suffix provided by WeCOS to define the format of images allowed to be uploaded. Images in jpg, png and gif are supported by WeCOS by default. If you want to upload images in other formats (such as webp), add the format in the configuration item, as shown below:

```
  "uploadFileSuffix": [".jpg",".png",".gif",".webp"]
```

#### Configure image blacklist
During the development, you can use WeCOS blacklist to prevent some images from being uploaded to COS. You can add either a directory or a file name to the blacklist.

```
  "uploadFileBlackList": ["./images/logo.png","./logo/"]
```

#### Custom domain name
To use your domain name as the file link in COS, replace the default domain name with targetHost (`http://` can be omitted):

```
  "targetHost": "http://example.com"
```

To change the domain name for the image link in the code, configure replaceHost and targetHost.

```
  "replaceHost": "http://wx-12345678.myqcloud.com",
  "targetHost": "https://example.com"
```

#### Enable image compression
Although the program package size decreases significantly with images uploaded to COS, excessive image dimensions may also cause access delay, thus affecting user experience.
Apart from uploading images to the cloud, WeCOS also provides image compression based on [Tencent Cloud's Cloud Infinite](https://cloud.tencent.com/product/ci). On the [Cloud Infinite Console](https://console.cloud.tencent.com/ci), create a bucket that has the same name with the bucket used to store the uploaded resource in COS, enter the bucket and enable image compression in the style page, and then the resources will be compressed before being uploaded.

```
  "compress": true
```

#### Configure real-time listener
By default, WeCOS listens to project directories in real time and automatically process image resources. During the development, if you want to disable the real-time listener after one-time processing, modify the configuration by executing the following command line, and then the listener will be disabled after one execution.

```
  "watch": false
```

## Advanced Usage
If the above method still cannot meet your demands, WeCOS also allows you to configure custom modules by means of direct referencing, thus satisfying your requirements. The configuration example is as follows:

```
var wecos = require('wecos');

// option is optional (String|Object).
// Enter a string to specify the configuration file path.
// Pass an object to specify the configuration item.
wecos([option]);

// Specify the configuration file path.
wecos('./wecos-config.js');

// Specify the configuration item.
wecos({
    appDir: './xxx',
    cos: {
        ...
    }
});
```

## Related Resources
- [WeCOS-UGC-DEMO](https://github.com/tencentyun/wecos-ugc-upload-demo) - Demo on Uploading Resources of Mini Programs to COS
- [COS-AUTH](https://github.com/tencentyun/cos-auth) - Demo on the COS Authentication Server

