Inputs are the source of streams for StreamLive channels. An input is usually associated with 1 security group and 1 StreamLive channel.

## Prerequisites
- You have activated [StreamLive](https://www.tencentcloud.com/products/mdl). 
- You have logged in to the [StreamLive console](https://console.intl.cloud.tencent.com/mdl/input).

## Input management
Select **Input Management** on the left sidebar. On this page, you can view the name, type, state and ID of created inputs. Each input is usually associated with one security group and one StreamLive channel. The state of an input that has been associated with a channel is **Attached**. Each input has two independent pipelines (A and B), which can push streams at the same time to ensure data availability.

![](https://qcloudimg.tencent-cloud.cn/raw/19becd1c0a3678da5db222a4723ae5b6.png)


## Creating an input
You can create PULL or PUSH inputs. On the **Input Management** page, click **Create Input** and complete the following settings in the pop-up window:
![](https://qcloudimg.tencent-cloud.cn/raw/0a58997dcc3241c77a07a05a458569c4.png)

- **Name**: The input name, which can be 1-32 characters long and can contain numbers, letters, and underscores (_).
- **Type**: The input type. Currently, RTMP_PUSH, RTP_PUSH, RTP-FEC_PUSH, UDP_PUSH, SRT_PUSH,RTMP_PULL, HLS_PULL, MP4_PULL, RTSP_PULL, and SRT_PULL are supported.
- **Security Group**: If you are creating a PUSH input, you must associate it with an input security group.

##### RTMP_PUSH
If the input type is RTMP_PUSH, you need to enter an application name and stream name for the destination.
![](https://qcloudimg.tencent-cloud.cn/raw/0f449d8038bed66bcada1faa0481c92c.png)

##### SRT_PUSH
If the input type is SRT_PUSH, you can enter a stream ID for the destination (optional).
![](https://qcloudimg.tencent-cloud.cn/raw/f4a9ec18c0de6d127fce99d8c91aad89.png)

##### PULL
If the input type is PULL, you need to enter an input address, which is used as the source of the PULL input.
![](https://qcloudimg.tencent-cloud.cn/raw/28291755993b3efb3b3bdd4b63bfd40d.png)


## Modifying an input
To modify an input, find it on the **Input Management** page and click **Edit** on the right. Modify its settings in the pop-up window and click **Confirm**.
![](https://qcloudimg.tencent-cloud.cn/raw/45f415840a5b45d0a97baa965f05a45c.png)

## Deleting an input
To delete an input, find it on the **Input Management** page, click **Delete** on the right, and click **Confirm** in the pop-up window.
![](https://qcloudimg.tencent-cloud.cn/raw/19becd1c0a3678da5db222a4723ae5b6.png)


>! 
>- You can create up to five inputs by default.
>- The source of an input must contain at least one video pipeline.
>- In case of MPEG-TS multiplexing, up to eight pipelines can transfer data simultaneously.

