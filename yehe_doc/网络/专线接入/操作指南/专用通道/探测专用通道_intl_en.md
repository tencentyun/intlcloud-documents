The Direct Connect console provides a tunnel tool that sends a detection packet from Tencent Cloud IP to customer IP to test the network connectivity. After [a dedicated tunnel is created](https://intl.cloud.tencent.com/document/product/216/19250) or [modified](https://intl.cloud.tencent.com/document/product/216/19251), we recommend using the tunnel tool to test the connection between Tencent Cloud and IDC.

## Prerequisites
- Modifying the bandwidth is currently in beta. To try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
- The dedicated tunnel should be a 2.0 tunnel, which can be checked on the [Basic Information](https://console.cloud.tencent.com/dc/conn/detail?id=dcx-6lmo2guk) page.

## Directions
1. Log in to the [Direct Connect console](https://console.cloud.tencent.com/vpc/dcConn) and click **Dedicated Tunnels** on the left sidebar to access the **Dedicated Tunnels** page.
2. Click the **ID/Name** of the target dedicated tunnel to enter its details page.
3. Select the **Tunnel Tool** tab.
4. Configure the number and volume of the packets, and click **Start Probing**. Determine if the network is connected based on the loss delay.

