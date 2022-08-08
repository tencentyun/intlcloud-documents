TRTC can check a user’s network quality before they enter a room or join a call. If the network quality is not satisfactory, we recommend you prompt the user to move to a better network environment to ensure smooth calls.

To monitor the network quality during a call, just register the [NETWORK_QUALITY](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.NETWORK_QUALITY) callback. This document describes how to check the network quality before a call based on [NETWORK_QUALITY](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.NETWORK_QUALITY).

## Directions

1. Call [TRTC.createClient](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createClient) to create two clients: `uplinkClient` and `downlinkClient`.
2. Make the two clients enter the same room.
3. Have `uplinkClient` publish the local stream and listen for the [NETWORK_QUALITY](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.NETWORK_QUALITY) event to monitor the upstream network quality.
4. Have `downlinkClient` play the other client’s stream and listen for the [NETWORK_QUALITY](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.NETWORK_QUALITY) event to check the downstream network quality.
5. The whole process lasts for about 15 seconds, and the average network quality is taken eventually to evaluate the upstream and downstream network quality.

>! The process of checking network quality incurs a small [basic service fee](https://intl.cloud.tencent.com/document/product/647/34610). If a resolution is not specified, the stream will be published at a resolution of 640 x 480.

## Sample Code

```js
let uplinkClient = null; // Check the upstream network quality
let downlinkClient = null; // Check the downstream network quality
let localStream = null; // Stream for test
let testResult = {
  // Record the upstream network quality data
  uplinkNetworkQualities: [],
  // Record the downstream network quality data
  downlinkNetworkQualities: [],
  average: {
    uplinkNetworkQuality: 0,
    downlinkNetworkQuality: 0
  }
}

// 1. Check the upstream network quality
async function testUplinkNetworkQuality() {
  uplinkClient = TRTC.createClient({
    sdkAppId: 0, // The SDKAppID
    userId: 'user_uplink_test',
    userSig: '', // The `UserSig` of `uplink_test`
    mode: 'rtc'
  });

  localStream = TRTC.createStream({ audio: true, video: true });
  // Set the video profile based on the actual business scenario
  localStream.setVideoProfile('480p'); 
  await localStream.initialize();

  uplinkClient.on('network-quality', event => {
    const { uplinkNetworkQuality } = event;
    testResult.uplinkNetworkQualities.push(uplinkNetworkQuality);
  });

  // Enter the room where the check will be performed. The room ID must be random to avoid conflicts
  await uplinkClient.join({ roomId: 8080 }); 
  await uplinkClient.publish(localStream);
}

// 2. Check the downstream network quality
async function testDownlinkNetworkQuality() {
  downlinkClient = TRTC.createClient({
    sdkAppId: 0, // The SDKAppID
    userId: 'user_downlink_test',
    userSig: '', // The `UserSig`
    mode: 'rtc'
  });

  downlinkClient.on('stream-added', async event => {
    await downlinkClient.subscribe(event.stream, { audio: true, video: true });
    // After successful subscription, listen for the network quality event
    downlinkClient.on('network-quality', event => {
      const { downlinkNetworkQuality } = event;
      testResult.downlinkNetworkQualities.push(downlinkNetworkQuality);
    });
  })
  // Enter the room where the check will be performed. The room ID must be random to avoid conflicts
  await downlinkClient.join({ roomId: 8080 });
}

// 3. Start the check
testUplinkNetworkQuality();
testDownlinkNetworkQuality();

// 4. Stop the check after 15 seconds and calculate the average network quality
setTimeout(() => {
  // Calculate the average upstream network quality
  if (testResult.uplinkNetworkQualities.length > 0) {
    testResult.average.uplinkNetworkQuality = Math.ceil(
      testResult.uplinkNetworkQualities.reduce((value, current) => value + current, 0) / testResult.uplinkNetworkQualities.length
    );
  }

  if (testResult.downlinkNetworkQualities.length > 0) {
    // Calculate the average downstream network quality
    testResult.average.downlinkNetworkQuality = Math.ceil(
      testResult.downlinkNetworkQualities.reduce((value, current) => value + current, 0) / testResult.downlinkNetworkQualities.length
    );
  }
    
  // The check ends. Clear the relevant status.
  uplinkClient.leave();
  downlinkClient.leave();
  localStream.close();
}, 15 * 1000);
```

## Result

After performing the above steps, you can get the average upstream and downstream network quality. The enumerated values of the network quality are as listed below:

| Value | Description                                                         |
| :--- | :----------------------------------------------------------- |
| 0    | Unknown, which indicates that the current client hasn't established an upstream/downstream connection    |
| 1    | Excellent                                                 |
| 2    | Good                                                 |
| 3    | Fair                                                 |
| 4    | Poor                                                   |
| 5    | Very poor                                                 |
| 6    | The network connection has been closed. **Note: For downstream network, this value indicates that all downstream connections have been closed.** |

<dx-alert infotype="notice" title="Suggestion:">
If the result is above 3, we recommend you ask the user to check their network and try changing the network environment to ensure call quality. <br>You can also use the following methods to reduce bandwidth consumption:
 - If the result for the upstream network quality is above 3, to reduce bandwidth consumption, you can call [LocalStream.setVideoProfile()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#setVideoProfile) to reduce the bitrate or call [LocalStream.muteVideo()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#muteVideo) to disable video.
 - If the result for the downstream network quality is above 3, to reduce bandwidth consumption, you can subscribe to the low-quality stream (see [Enabling Dual-Stream Mode](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-27-advanced-small-stream.html)) or subscribe to audio only.
</dx-alert>




