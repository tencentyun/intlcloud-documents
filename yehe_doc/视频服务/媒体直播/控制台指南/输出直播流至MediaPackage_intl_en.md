
MediaLive supports integration with MediaPackage and directly outputs HLS/DASH live streams to MediaPackage under the same account, which helps you build your own origin servers and perform video distribution and playback.
### Step 1: Enable MediaPackage
Please enable the MediaPackage service before outputting to MediaPackage. Log in to the [MediaPackage console](https://console.cloud.tencent.com/mdp/channel) to create a channel.
### Step 2: Complete the channel creation of MediaPackage
Click “Create Channel” on the upper left corner to create a channel. Enter a channel name and select a protocol that is consistent with the MediaLive output type. For example: select HLS if the output type of MediaLive is HLS_MediaPackage.
![](https://main.qcloudimg.com/raw/024c629fe57a6c3fd4761aadaf45a32e.jpg)

>! MediaLive and MediaPackage need to be in the same region.
>

### Step 3: Create an endpoint
After the channel has been created, you will enter the details page of the channel to create an endpoint node. You can also choose whether to enable the IP allowlist, IP blocklist or the authentication function according to your actual business needs.
 ![](https://main.qcloudimg.com/raw/c3bce6fe0f437599c6acb5de6752c21f.jpg)

### Step 4: Obtain the endpoint URL and the channel ID
The created endpoint URL is the playback/origin server URL.
![](https://main.qcloudimg.com/raw/5b98c4ebc014ebaeb9acb56cf436f876.jpg)

>? When setting the output of MediaLiveSelect, you can select MediaPackage as the output type and fill in the Channel ID of MediaPackage.
>

### Step 5: Select HLS_MEDIAPACKAGE or DASH_MEDIAPACKAGE as the output group type
Return to the MediaLive console. When configuring the output, you can select either HLS_MEDIAPACKAGE or DASH_MEDIAPACKAGE as the output group type (depending on your actual business needs and the channel type of the MediaPackage you just created), and then fill in the MediaPackage channel ID.
![](https://main.qcloudimg.com/raw/a6716afaa492de5d744ca1ef03b4c1d5.jpg)

### Step 6: Save and submit the configuration
You can go back to [MediaLive channel creation](https://intl.cloud.tencent.com/document/product/1048/38374) to complete the other channel configurations. Click “Done” to save and submit the configurations.
