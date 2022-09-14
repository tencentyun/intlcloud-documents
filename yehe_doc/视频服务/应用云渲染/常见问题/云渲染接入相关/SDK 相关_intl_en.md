## SDK for JavaScript
### Why does the console report the "setServerDescription" error in the browser?
Generally, this error occurs because the structure hierarchy of the request used by `CreateSession` to get `ServerSession` is incorrect. You can print the returned result to understand how to get `ServerSession`. 

### Why is a failure (other than 0) returned when I enable the data channel?
You need to create a data channel after receiving `onConnectSuccess` called back by the SDK.

### How do I implement automatic landscape/portrait mode switching on the mobile client?
As the cloud stream is fixed in landscape mode, the image needs to be rotated to be displayed in portrait mode on the mobile client. You can pass in the `autoRotateContainer` (container rotation) and `autoRotateMountPoint` (mount point rotation) parameters to `init`.

### Which cursor modes are there?
Currently, there are three modes:
- `0`: No cursor is delivered.
- `1`: The delivered cursor is rendered by the SDK.
- `2`: The cursor is rendered in the cloud, which has a longer latency than mode `1`.

We recommend you use mode `0` or `1` preferentially. The default mode is `0`. For the specific implementation process, see [SDK for JavaScript APIs](https://intl.cloud.tencent.com/document/product/1158/49627).

## SDK Plugin
### Why is the click direction of the stick button incorrect?
We recommend you create a stick after `connectSuccess` and try again.
