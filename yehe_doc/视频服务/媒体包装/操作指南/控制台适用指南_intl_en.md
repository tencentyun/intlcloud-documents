The MediaPackage Console manages streams by channels and can be divided into three components: channel, input, and endpoint.

## 1. Channel

A channel holds the basic input/output stream configurations. You can create and configure a channel to input a live stream with a specified protocol, or create an origin-pull endpoint (see "Endpoint" section) to output the live stream.
Create a channel in the following steps:
Click "Create Channel".
Enter a channel name and select an input protocol (HLS and DASH supported).
Save the configurations.
Once a channel is created, you will be redirected to the channel details page, where the channel name, ID (automatically generated in the backend), and the specified input protocol are displayed. Two inputs will be automatically generated based on the protocol (see "Input" section).
On the channel list page, you can manage all channels that have been created. You can view channel details, and modify or delete a channel. To delete a channel associated with endpoints, delete all endpoints first.

## 2. Input

Input is the basic unit of channel. Based on the channel you created, the backend will automatically generate two inputs and corresponding URLs to which you can push the live stream.

![](https://main.qcloudimg.com/raw/ca34978793d405f87e5329aadc0c7a3d.png)

The input component supports authentication. You can configure authentication for each input. The backend will automatically generate a username and password for it, and authenticate streams using HTTP authentication. You can also click "Rotate credentials" as shown in the following figure.
Note: once you rotate credentials, the existing channel credentials will become invalid.

![](https://main.qcloudimg.com/raw/9fff5688aab8cfbc36027a8db1374c1a.png)


## 3. Endpoint

Endpoints pull streams from an origin server. You can create endpoints on a channel in the following steps:

![](https://main.qcloudimg.com/raw/d0e8a53648a9799d4b9c3fa10e26d98b.png)

Click "Create Endpoints".
Enter the endpoint name and type. By default, the endpoint type is the same as the input protocol.
Enable/disable the IP blocklist/allowlist and Authkey as needed.
Save the configurations.

**You can configure an endpoint with IP blocklist/allowlist to allow streams pushed from valid IP ranges or reject those from invalid IP ranges. You can also configure Authkey, and authenticate streams through the X-TENCENT-PACKAGE field in the HTTP header.**

Once endpoints are created, you will be redirected to the endpoint list page. You can modify or delete an endpoint, and use the generated endpoint URL to pull streams from an origin server and distribute them.
