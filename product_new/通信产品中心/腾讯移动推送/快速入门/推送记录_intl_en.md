## Operation scenarios
This document guides you to query push records in the TPNS Console (message ID, title, content, sending time, and operation).


## Directions
1. Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns) and select **User Operations** > **TPNS** > **Push Records** in the left sidebar.
2. On the **Push Records** page, click **Detailed Data**.
3. On the **Detailed Data** page, the data from each push process is displayed in funnel format. Android and iOS data funnels are different.

**Android terminals:**
 - Self-built channel
   - Planned delivery: the total number of devices that match the push conditions and use the self-built channel.
   - Actual delivery: The number of devices that maintain a persistent connection with the TPNS backend server.
   - Arrival: the number of devices to which the message successfully arrived.
   - Display: the number of devices on which the message was displayed.
   - Clicks: the number of devices on which the message was clicked.
   - Clears: the number of devices on which the message was cleared.
 - Vendor-specific channels
   - Planned delivery: The total number of devices that match the push conditions and use the vendor channel.
   - Actual delivery: Pushed to the vendor server, and the vendor server responds with the number of successful deliveries.
>The vendor channel does not return the “arrival”, “display”, “clicks”, or “clears” information. When the selected channel is **All**, these four indicators are reported through the self-built channel.

**iOS terminals:**
 - Planned delivery: the total number of devices that match the push conditions.
 - Backend delivery: the number of deliveries the TPNS backend successfully sends to APNs.
 - APNs receipt: the number of messages which arrive to APNs, and which APNs returns successful receipt.
 - Clicks: the number of devices on which the message was clicked.


