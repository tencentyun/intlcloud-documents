### When can I create a data channel?
A data channel is created based on a normal connection. We recommend you create a data channel after `onConnectSuccess`. For more information, see [Data Channel](https://www.tencentcloud.com/document/product/1158/51428)

### Is there any limit on the size of a data packet to be transferred?
There is no limit on the size of a data packet to be transferred. However, a UDP packet can be up to 64 KB in size, and we recommend you keep the packet size less than 1500 bytes (i.e., the maximum transmission unit (MTU)). If the packet is too large, we recommend you split it; otherwise, too much data will be upstreamed, which tends to cause congestion and affect the user experience.

### Will the local proxy port received by the cloud application change?
Generally, the port won't change. However, it will change after a reconnection, for example, when the user refreshes the page and enters the application again on the frontend.
