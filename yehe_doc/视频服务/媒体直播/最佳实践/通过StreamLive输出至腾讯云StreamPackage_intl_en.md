You can use StreamLive together with StreamPackage and output HLS/DASH live streams directly to StreamPackage under the same account. This allows you to build your own origin server for video distribution and playback.

### Activating StreamPackage

Before outputting to StreamPackage, you need to [activate the StreamPackage service](https://console.cloud.tencent.com/mdp/channel) and create a StreamPackage channel.

### Creating a StreamPackage channel

Click **Create Channel** in the top-left corner to create a channel. Enter a channel name. For **Input Protocol**, select the same protocol as the output type. For example, if the output type is **HLS_StreamPackage**, select **HLS**.

>! StreamLive and StreamPackage must be in the same region.

![img](https://main.qcloudimg.com/raw/ca0ae9e483499e4489a8db47b7bb290b.png)

### Creating an endpoint

After creating the channel, you will enter its details page, where you can create an endpoint and select whether to enable IP blocklist/allowlist or authentication.

![img](https://main.qcloudimg.com/raw/da2c4f2cefcbb73aa5ba68f75579937c.png)

### Getting the endpoint address and channel ID

The URL of the endpoint created is the playback/origin server address.

![img](https://main.qcloudimg.com/raw/30594049a37593a5d8827990bd9a13a1.png)

>? You will need the channel ID when configuring outputs in StreamLive.

![img](https://main.qcloudimg.com/raw/c66b1bb5f1c9f570225310e66f8e0a66.png)

### Selecting the output type

Go back to the StreamLive console, based on your needs and the type of the StreamPackage channel just created, select **HLS_STREAMPACKAGE** or **DASH_STREAMPACKAGE** for **Output Group Type**, and enter the channel ID in StreamPackage.

![img](https://main.qcloudimg.com/raw/486e54380f8bbecd2430c01ad8265c86.png)

### Saving and submitting the configuration

Complete other channel configuration in [StreamLive Channel Management](https://intl.cloud.tencent.com/document/product/1048/45214) and save and submit the configuration.
