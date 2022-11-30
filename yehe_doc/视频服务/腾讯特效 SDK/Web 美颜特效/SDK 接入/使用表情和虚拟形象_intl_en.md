The Tencent Effect SDK has supported animojis and virtual avatars since v0.3.0.

## Checking Support
Animojis and virtual avatars rely on a WebGL2 environment. The SDK offers a static method for you to check whether a browser supports the capability.
```javascript
import {ArSdk} from 'tencentcloud-webar'
if (ArSdk.isAvatarSupported()) {
    // Initialize the features

} else {
    alert('This browser does not support virtual avatars')
    // Hide the features
}
```

## Animojis
### Getting models
After initialization, you can get the built-in models. Currently, the SDK offers four built-in models.
```javascript
const avatarARList = await sdk.getAvatarList('AR')
```

>! Configuring animojis and virtual avatars will automatically remove other effects such as makeup and stickers, and vice versa.

### Using a model
After you get a list of the built-in models, you can select one by specifying the `EffectId` parameter.
```javascript
ar.setAvatar({
  mode: 'AR', // Set the mode to AR
  effectId: avatarARList[0].EffectId// Pass in the ID of the model
}, () => {
  // success callback
  
});
```
### Custom models
To use custom models, please [contact us](https://intl.cloud.tencent.com/contact-us).


## Virtual Avatars
### Getting models
After initialization, you can get the built-in avatar models. Currently, the SDK offers 10 built-in avatar models.
```javascript
const avatarVRList = await sdk.getAvatarList('VR')
```

### Setting the mode
```javascript

ar.setAvatar({
  mode: 'VR', // Set `mode` to `VR`
  effectId: avatarVRList[0].EffectId, // Pass in the ID of the avatar model
  backgroundUrl: 'https://webar-static.tencent-cloud.com/assets/background/1.jpg',
}, () => {
    // success callback

  
});
```

>! If you set the mode to VR, you will also need to specify the URL of the background image. If you do not specify it, a black background will be used.

### Custom models
You can customize a virtual avatar to use in the Tencent Effect SDK in two ways:
- Method 1: `readyplayer.me`
- Method 2: [Vroid](https://vroid.com/en/studio)

After exporting the model, you need to upload it to the CDN and configure it in the SDK using a URL.
```javascript
ar.setAvatar({
  mode: 'VR', // Set `mode` to `VR`
  url: 'https://xxxx.glb', // Pass in the ID of the built-in model
  backgroundUrl: 'https://webar-static.tencent-cloud.com/assets/background/1.jpg',
}, () => {
    // success callback

});
```
Currently, custom models only support the GLB and VRM formats.
