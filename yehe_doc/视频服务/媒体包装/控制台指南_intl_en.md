## Overview 

StreamPackage is a high-quality video packaging and origin platform. It offers professional, stable, secure, and easy-to-use video packaging and delivery services globally and helps you enhance origin resilience. You can use StreamPackage to securely and reliably distribute video streams at a large scale.

StreamPackage manages tasks at the channel level. It packages compressed and encoded audio and video tracks into certain formats for distribution.

## Console Overview

The StreamPackage console provides a rich set of easy-to-use and flexible features. It manages tasks at the channel level and functions through four main sections: channel, input, endpoint, and CDN.

![img](https://main.qcloudimg.com/raw/2d70be467d74639158d0be4ea94692d2.png)

## Prerequisites

- You have a domain for playing videos from CDNs (if you want to use Tencent Cloud’s live streaming CDN for content distribution).
- You have activated [CSS](https://console.cloud.tencent.com/live).
- You have logged in to the [StreamPackage console](https://console.cloud.tencent.com/mdp/channel).


## Directions

### 1. Select an AZ

Currently, StreamPackage services are available in Mumbai (India), Bangkok (Thailand), Seoul (South Korea), Tokyo (Japan), Frankfurt (Germany), and Singapore. If you want to deploy your business in other regions, please [contact us](https://intl.cloud.tencent.com/contact-sales).

![](https://qcloudimg.tencent-cloud.cn/raw/14e4406387923306e201024a529f3d2b.png)

### 2. Create a channel

A channel holds basic information about inputs and outputs. You can configure a channel to receive live streams that use a specific protocol. You can also create endpoints to generate content to be distributed.

1. Click **Create Channel**.
2. Enter a channel name and select an input protocol (HLS and DASH are supported).

![img](https://main.qcloudimg.com/raw/f545e69458ff80b55c6775219d574374.png)

3. Complete other HLS/DASH settings.

- **Max Segment Duration** indicates the maximum duration of HLS TS segments or DASH M4S segments pushed to this channel. The default is 15 seconds.
- **Max Playlist Duration** indicates the maximum total duration of the HLS M3U8 or DASH MPD playlist pushed to this channel. The default is 600 seconds.

>? If you are sending two streams, one primary stream and one backup stream, to the channel for failover, we recommend you set **Max Segment Duration** slightly longer than actually needed.


4. Click **Create**.

### 3. View channel information

#### Viewing channel information

After the channel is created, you will be directed to the channel details page (you can also go to the details page by clicking the channel name or **Info** on the right). This page displays the channel's name, ID (automatically generated), input protocol, and other settings. StreamPackage will generate two inputs of the specified protocol for the channel.

![img](https://main.qcloudimg.com/raw/d962c942d07f8303832d070c7d0d2a26.png)

#### Viewing inputs

An input is the basic unit of the content StreamPackage receives. After a channel is created, StreamPackage will automatically generate two inputs as well as two input URLs for the channel. You can send streams to the URLs.

![img](https://main.qcloudimg.com/raw/9fc040a6cb575be7411327476f0fe7a1.png)

You can enable authentication for an input: Click **Authentication** in the **Operation** column.  StreamPackage will generate a username and a password for HTTP authentication. Click **Rotate credentials** to complete the configuration.

![img](https://main.qcloudimg.com/raw/6927ebe8232a26cb341aa1b69f008e45.png)

>! Once you rotate credentials, the existing credentials of the channel will become invalid.

#### Creating an endpoint

You can create endpoints for a channel so that streams can be pulled from the channel.

1. Click **Create Endpoint**.

![img](https://main.qcloudimg.com/raw/ce143b55735dee33f7e708c5ea19f89a.png)

2. Enter an endpoint name. The endpoint type is the same as the channel’s input type by default. If the input type is HLS, you can also select CMAF as the endpoint type. This means StreamPackage can package HLS streams into CMAF streams (DASH).

![](https://qcloudimg.tencent-cloud.cn/raw/fef800b9890ad8c7df531792d20657d7.png)  

3. You can also enable IP allowlist/blocklist and AuthKey if necessary.

- IP allowlist/blocklist: Allow only specific IP address ranges to push or disallow specific IP address ranges to push.

- AuthKey: Perform authentication using the HTTP header field X-TENCENT-PACKAGE.

![](https://qcloudimg.tencent-cloud.cn/raw/3255d5b26c1ad65a64102fbd6a302157.png)  



4. Click **Create** and the endpoint is created. You can modify or delete the endpoint. From the endpoint URL generated, you can pull streams and distribute them.

![img](https://main.qcloudimg.com/raw/219346607e144822c43173ba1e055905.png)

#### Configuring a CDN distribution

You can create a CDN distribution for a StreamPackage channel to distribute the streams in the channel via Tencent Cloud’s live streaming CDN. To achieve this, you need to activate CSS and **grant CSS access to StreamPackage and StreamPackage access to CSS**.

Before we proceed, make sure you understand the following terms:

- LVB CDN: StreamPackage allows you to quickly distribute streams in a channel via the LVB CDN.
- CDN domain/CDN playback domain: A playback domain in the LVB CDN, which can be used to distribute live streams.


1. Activate CSS

Before you configure a CDN distribution, make sure you have activated [CSS](https://console.cloud.tencent.com/live?from=product-banner-use-lvb).

2. Grant StreamPackage access to CSS

In the StreamPackage console, go to the details page of the channel for which you want to configure a CDN distribution, select the **CDN** tab, and click **Authorization**.

>? After the authorization, you will be able to configure a CSS playback domain for a StreamPackage channel.

![img](https://main.qcloudimg.com/raw/d0f1bc546937e0fbbb111bd6d97f2557.png)

Click **Click here**. To distribute streams via the LVB CDN, you need to allow StreamPackage to access certain resources. This is achieved via a service role. Click **Authorize Now** to go to the **Role Management** page, and click **Grant** to grant StreamPackage the permission to use related APIs.

![img](https://main.qcloudimg.com/raw/c2e6a9006094003091539f31d1d4c63c.png)![img](https://main.qcloudimg.com/raw/a6476145b574ebbfe7f828dbbbfce984.png)

![img](https://main.qcloudimg.com/raw/b18b2fbb7440d557ee82093d44660258.png)

You will be directed back to the StreamPackage console. Click **Authorization completed**.

![img](https://main.qcloudimg.com/raw/2e7a6e29600485b593323658cf738b7d.png)

![img](https://main.qcloudimg.com/raw/3374604fff9c19ec580eb6a43af7f86e.png) 

Click **Next**.

3. Grant CSS access to StreamPackage

Click **Click here** to go to the CDN console and allow the LVB CDN to use StreamPackage. After the authorization, you will see that the authorization status for StreamPackage has become **Activated** in the CSS console.

![img](https://main.qcloudimg.com/raw/3be8efcd4c8302b15df46be54daebed4.png)

![img](https://main.qcloudimg.com/raw/c63def0152b6d95901929b7abc093d59.png)

Return to the StreamPackage console and click **Completed**.

![img](https://main.qcloudimg.com/raw/2616575aa0b6d56323eafcfac0aec9f8.png)


Click **Authorization Completed**. **You have now granted the LVB CDN access to StreamPackage and StreamPackage access to the LVB CDN (which means you can now configure a CDN playback domain for a StreamPackage channel and the LVB CDN can pull streams from a StreamPackage channel).**

![img](https://main.qcloudimg.com/raw/5e3084a78e0ce61a0a9eabd5a61c9a90.png)


4. Configure a CDN playback domain

After completing the authorization, under the **CDN** tab, click **Edit Configuration** to configure a CDN distribution.

![img](https://main.qcloudimg.com/raw/4d2031b1fe8c42a1a05c7b619291e1dd.png)

Enter the domain you want to use for CDN playback and click **Confirm**.

![img](https://main.qcloudimg.com/raw/ee8a3bf7ab68b655bba010df76bac910.png)

![img](https://main.qcloudimg.com/raw/1fd6d414ef8fb41cee52c0a489c79395.png)

>?
>- After a new playback domain is added, the system will assign it a CNAME which ends with `.liveplay.myqcloud.com`. To make the CNAME accessible, you need to add a CNAME record for the domain at your DNS provider. For detailed directions, see [Configuring CNAME for Domain Name](https://intl.cloud.tencent.com/document/product/267/31057).
>- The default acceleration region for a CDN playback domain configured in the StreamPackage console is outside the Chinese mainland. If you need to distribute live streams inside the Chinese mainland, according to relevant laws and regulations, ICP filing is required for your domain. You can click **Go to the CSS CDN Console to Perform More Actions**.

#### Playing streams via the configured playback domain

To achieve playback via the configured playback domain, after you associate a StreamPackage channel with a CDN playback domain, replace the domain in the channel’s endpoint URL with the CDN playback domain.

For example:

Suppose the endpoint URL of your channel is:

http://123456789.ap-seoul.streampackage.srclivepull.myqcloud.com/v1/017697a3513109df73abda3c4b26/017697a918bf09dfabc033b04d43/main.m3u8

Then your CDN playback address is:

http://CDN playback domain name/v1/017697a3513109df73abda3c4b26/017697a918bf09dfabc033b04d43/main.m3u8

After the configuration is completed, please contact us for configuration optimization to ensure a better experience for you.

>? Using the LVB CDN for distribution will incur playback traffic fees. For details, see [Billing of LVB](https://www.tencentcloud.com/document/product/267/2818?lang=en&pg=).

### 4. Edit and delete a channel

You can manage created channels on the **Channel Management** page. Click **Info** in the **Operation** column to view channel details. Click **Edit** to edit a channel, and click **Delete** to delete a channel. Note that you cannot delete a channel bound with endpoints. Delete the endpoints first before deleting a channel.

![img](https://main.qcloudimg.com/raw/bd7b3e8c0033d6591f5b61b2974dc12a.png)