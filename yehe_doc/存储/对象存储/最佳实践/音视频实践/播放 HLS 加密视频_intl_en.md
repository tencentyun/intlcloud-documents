## Background

To ensure the security of video content and prevent unauthorized download and distribution of videos, COS data processing provides the feature of encrypting HLS video content, which is more secure than privately readable files. Encrypted videos cannot be distributed to users without access for playback. Even if they are downloaded, they are still encrypted and cannot be redistributed maliciously. This protects your video copyrights from being infringed upon.

Based on the [HLS encryption](https://intl.cloud.tencent.com/document/product/436/47861) process, this practice builds a basic key management service and combines with [Tencent Cloud VOD superplayer](https://intl.cloud.tencent.com/document/product/266/33977) to play back video files transcoded and encrypted by COS HLS.

## Directions

#### Step 1. Encrypt a video

Encrypt a video file in the COS bucket as instructed in [Preventing Video Leakage with HLS Encryption](https://intl.cloud.tencent.com/document/product/436/47861).

#### Step 2. Set up the key service

1. Call the [key API](https://console.cloud.tencent.com/api/explorer?Product=kms&Version=2019-01-18&Action=Decrypt&SignVersion=) to generate KMS API sample code based on your programming language.

2. The following takes Node.js as an example to describe how to build a key service based on the sample code with Koa and call the KMS API to get a decryption key.
```
const Koa = require('koa')
const cors = require('koa2-cors')
const app = new Koa()
const tencentcloud = require("tencentcloud-sdk-nodejs")

app.use(cors()) // CORS configuration
app.use(async (ctx) => {
  // The URI request in the generated m3u8 file will carry the parameters by default
  const { Ciphertext, KMSRegion } = ctx.query

  const KmsClient = tencentcloud.kms.v20190118.Client
  const clientConfig = {
    credential: {
      // Account API key, which can be obtained at https://console.cloud.tencent.com/cam/capi
      secretId: "SecretId",
      secretKey: "SecretKey",
    },
    
    region: KMSRegion, // Region, such as "ap-guangzhou"
    profile: {
      httpProfile: {
      	endpoint: "kms.tencentcloudapi.com",
      },
    },
  };

  // Create a KMS object instance
  const client = new KmsClient(clientConfig);
  const params = {
  	"CiphertextBlob": Ciphertext,
  };
  
	try {
    // Initiate a request to get the decryption key
    const res = await client.Decrypt(params)
    
    // Take out the key and return its binary data after Base64-decryption
    const plaintext = res.Plaintext
    const plainBuff = Buffer.from(plaintext, 'base64');
    ctx.body = plainBuff
  } catch (error) {
    console.log(error);
  }
  
})

// Listen on port 8080.
app.listen('8080', () => {
  console.log('127.0.0.1:8080');
})
```

#### Step 3. Play back the encrypted video on the web

1. Import the player style and script files into the page:
```
<!--Player style file-->
<link href="https://web.sdk.qcloud.com/player/tcplayer/release/v4.2.2/tcplayer.min.css" rel="stylesheet"/>
<!--If you want to play back HLS videos through HTML5 in a browser such as Chrome and Firefox, you need to import `hls.min.0.13.2m.js` before importing `tcplayer.v4.2.2.min.js`.-->
<script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.2.2/libs/hls.min.0.13.2m.js"></script>
<!--Player script file-->
<script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.2.2/tcplayer.v4.2.2.min.js"></script>
```
We recommend you deploy the above static resources on your own when using the player SDK. [Click here to download the player resources](https://web.sdk.qcloud.com/player/tcplayer/release/v4.2.2/release.zip).
Deploy the folder generated after decompression. Do not adjust the directories in the folder; otherwise, resource import exceptions may occur.
2. Set the player container node.
Add a player container where you want to play back videos. For example, you can add the following code to `index.html` (the container ID, width, and height are customizable).
```
<video id="player-container-id" width="414" height="270" preload="auto" playsinline webkit-playsinline>
</video>
```
>?
> - The player container must be a `<video>` tag.
> - The `player-container-id` in the sample is the ID of the player container, which can be customized.
> - We recommend you set the size of the player container zone through CSS, which is more flexible than the attribute and can achieve effects such as fit to full screen and container adaption.
> - The `preload` attribute in the sample specifies whether to load the video after the page is loaded, which is usually set to `auto` for faster start of the playback. Other options include `meta` (only loads the metadata after the page is loaded) and `none` (does not load the video after the page is loaded). Due to system restrictions, videos will not be automatically loaded on mobile devices.
> - The `playsinline` and `webkit-playsinline` attributes are used to implement inline playback when the standard mobile browser does not hijack the video playback. They are just for reference here and can be used as needed.
> - If the `x5-playsinline` attribute is set, the X5 UI player will be used in the TBS kernel.
> 
3. On the bucket list page, get the **m3u8** file object address of the video encrypted in step 1.

4. Initialize the player and pass in the m3u8 object address.
```
var player = TCPlayer('player-container-id', {}); // `player-container-id` is the player container ID, which must be the same as that in HTML
player.src(https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/path/example.m3u8); // m3u8 object address
```

#### Step 4. View the effect

1. The m3u8 file and decryption key are successfully obtained.

2. The video is decrypted and played back successfully.




