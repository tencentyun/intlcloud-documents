## Introduction

Stream mixing is not needed if only one audio/video stream is played in a room. But in case of multiple audio/video streams, **MixTranscoding** is needed to combine the multiple streams into one to make the recording/storage easy and allow for Relayed Live Streaming to the LVB CDN.

You can enable On-Cloud MixTranscoding using the **setMixTranscodingConfig** API in TRTCCloud to mix multiple streams into one.

## Supported Platforms

| iOS | Android | Mac OS | Windows | WeChat Mini Program | Chrome |
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|     &#10003;  |    &#10003;    |    &#10003;   |    &#10003;    |    ×    |   ×    |

> WeChat Mini Program and HTML5 do not support the setMixTranscodingConfig API on mobile devices and PCs. You can enable this feature using the [REST API](https://intl.cloud.tencent.com/document/product/267/8832) in LVB.


## How Cloud MixTranscoding Works
During On-Cloud MixTranscoding, the recorded video images are decoded and then spliced into one image, which is then encoded to generate a new video stream.



Because both mix and transcoding involve decoding and re-encoding the original audio/video data, they may take a while. Therefore, a mixed stream has a playback latency 1 or 2 seconds longer than individual streams.

## Sample Code

Call the `setMixTranscodingConfig` API of TRTCCloud to enable On-Cloud MixTranscoding.
Before enabling Cloud MixTranscoding, you need to configure the parameter `TRTCTranscodingConfig` to specify the relative positions of the subimages in the mixed image.

- **Objective-C**

``` Objective-C
//Sample code for Cloud MixTranscoding
- (void)enableTranscoding
{
    TRTCTranscodingConfig *config = [[TRTCTranscodingConfig alloc] init];
    // Set the resolution to 1280×720p and the bitrate to 1500 Kbps
    config.videoWidth      = 1280;
    config.videoHeight     = 720;
    config.videoBitrate    = 1500;
    config.videoFramerate  = 20;
    config.videoGOP        = 2;
    config.audioSampleRate = 48000;
    config.audioBitrate    = 64;
    config.audioChannels  = 2;

    // Set the anchor image position in the mixed image
    TRTCMixUser *broadCaster = [[TRTCMixUser alloc] init];
    broadCaster.userId = @"broadcaster"; // Use "broadcaster" as the anchor's userId
    broadCaster.zOrder = 0; //Spread out on the screen at the bottom layer
    broadCaster.rect = CGRectMake(0, 0, 1080, 720);

    // Set the viewer image position (position at the lower left corner, with the edge distance to the corner being 10 pixels)
    TRTCMixUser *audience = [[TRTCMixUser alloc] init];
    audience.userId = @"audience"; // Use "audience" as the viewer's userId
    audience.zOrder = 1; // Place the viewer image on top of the anchor image
    audience.rect = CGRectMake(10, 470, 360, 240); //Position at the lower left corner

    config.mixUsers = @[broadcaster, audience];
    [trtcCloud setMixTranscodingConfig:config];
}
```

- **Java**

``` java
//Enable Cloud MixTranscoding
public void enableTranscoding() {
    TRTCCloudDef.TRTCTranscodingConfig config = new TRTCCloudDef.TRTCTranscodingConfig();
    // Set the resolution to 1280×720p and the bitrate to 1500 Kbps
    config.videoWidth = 1080;
    config.videoHeight = 720;
    config.videoBitrate = 1500;
    config.audioSampleRate = 48000;
    config.audioBitrate = 64;
    config.audioChannels = 2;

    // Set the anchor image position in the mixed image
    TRTCCloudDef.TRTCMixUser broadCaster = new TRTCCloudDef.TRTCMixUser();
    broadCaster.userId = "broadcaster"; // Use "broadcaster" as the anchor's userId
    // Spread out on the screen at the bottom layer
    broadCaster.zOrder = 0;
    broadCaster.x = 0;
    broadCaster.y = 0;
    broadCaster.width = 1080;
    broadCaster.height = 720;

    TRTCCloudDef.TRTCMixUser audience = new TRTCCloudDef.TRTCMixUser();
    audience.userId = "audience"; // Use "audience" as the viewer's userId
    // Position the viewer image on top of the anchor image and at the lower left corner of screen
    audience.zOrder = 1;
    audience.x = 10;
    audience.y = 470;
    audience.width = 360;
    audience.height = 240;

    config.mixUsers = new ArrayList<>();
    config.mixUsers.add(broadCaster);
    config.mixUsers.add(audience);

    trtcCloud.setMixTranscodingConfig(config);
}

```

- **C++**

``` C++
// Enable On-Cloud MixTranscoding
void enableTranscoding()
{
    TRTCTranscodingConfig config;
    // Set the resolution to 1280×720p and the bitrate to 1500 Kbps
    config.videoWidth = 1080;   
    config.videoHeight = 720;
    config.videoBitrate = 1500; 
    config.audioSampleRate = 48000;
    config.audioBitrate = 64;
    config.audioChannels = 2;

    std::vector<TRTCMixUser> mixUsers;

    // Set the anchor image position in the mixed image
    TRTCMixUser broadCaster;
    broadCaster.userId = "broadcaster"; // Use "broadcaster" as the anchor's userId
    broadCaster.zOrder = 0; //Spread out on the screen at the bottom layer
    broadCaster.rect.left = 0;
    broadCaster.rect.top = 0;
    broadCaster.rect.right = 1280;
    broadCaster.rect.bottom = 720;

    // Set the viewer image position (position at the lower left corner, with the edge distance to the corner being 10 pixels)
    TRTCMixUser audience;
    audience.userId = "audience";// Use "audience" as the viewer's userId
    audience.zOrder = 1;    // Position the viewer image on top of the anchor image and at the lower left corner of the screen
    audience.rect.left = 920;
    audience.rect.top = 480;
    audience.rect.right = 1080;
    audience.rect.bottom = 720;

    mixUsers.push_back(std::move(broadCaster));
    mixUsers.push_back(std::move(audience));
    
    config.mixUsersArray = &mixUsers[0]; // mixUsers cannot be null
    config.mixUsersArraySize = mixUsers.size();

    trtcCloud->setMixTranscodingConfig(config);
}
```

- **C#**

```c#
// Enable On-Cloud MixTranscoding
private void enableTranscoding()
{
    TRTCTranscodingConfig config = new TRTCTranscodingConfig();
    // Set the resolution to 1280×720p and the bitrate to 1500 Kbps
    config.videoWidth = 1080;   
    config.videoHeight = 720;
    config.videoBitrate = 1500; 
    config.audioSampleRate = 48000;
    config.audioBitrate = 64;
    config.audioChannels = 2;

    TRTCMixUser[] mixUsers = new TRTCMixUser[2]; // The length depends on the number of subimages in the mixed image.

    // Set the anchor image position in the mixed image
    TRTCMixUser broadCaster = new TRTCMixUser();
    broadCaster.userId = "broadcaster"; // Use "broadcaster" as the anchor's userId
    broadCaster.zOrder = 0; //Spread out on the screen at the bottom layer
    broadCaster.rect.left = 0;
    broadCaster.rect.top = 0;
    broadCaster.rect.right = 1280;
    broadCaster.rect.bottom = 720;

    // Set the viewer image position (position at the lower left corner, with the edge distance to the corner being 10 pixels)
    TRTCMixUser audience = new TRTCMixUser();
    audience.userId = "audience";// Use "audience" as the viewer's userId
    audience.zOrder = 1;    // Position the viewer image on top of the anchor image and at the lower left corner of the screen
    audience.rect.left = 920;
    audience.rect.top = 480;
    audience.rect.right = 1080;
    audience.rect.bottom = 720;

    mixUsers[0] = broadCaster;
    mixUsers[1] = audience;
    
    config.mixUsersArray = mixUsers; // mixUsers cannot be null
    config.mixUsersArraySize = mixUsers.Count;

    mTRTCCloud.setMixTranscodingConfig(config);
}
```
