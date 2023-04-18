You can view the network monitoring data of a connection or dedicated tunnel via the console or an API to facilitate the troubleshooting. To use the API, see [Connection Monitoring Metrics](https://intl.cloud.tencent.com/document/product/248/10994).

## Directions
1. Log in to the [Direct Connect](https://console.cloud.tencent.com/vpc/dc) console.
2. Perform the following steps to view the network monitoring data of a connection.
 1. Click **Connections** on the left sidebar.
 2. Locate the target connection and click <img width="3%" src="https://main.qcloudimg.com/raw/52d8549cc2412c6527f332a3b88be44d.png"  > in the **Monitoring** column.
>?Only the monitoring data of operating connections can be viewed.
 3. The **Monitoring** page displays **Network Outbound Bandwidth** and **Network Inbound Bandwidth**. Select **Last 24 hours**, **Last 7 days** or a custom time period to display the monitoring data accordingly.
      - **Network Outbound Bandwidth**: average outbound traffic of the connection per second.
      - **Network Inbound Bandwidth**: average inbound traffic of the connection per second.
      - **Packet Loss**: number of packets discarded on the port per minute.
      - **Packet Error**: number of packet errors on the port per minute.
3. Perform the following steps to view the network monitoring data of a dedicated tunnel.
 1. Click **Exclusive virtual interface** on the left sidebar.
 2. Locate the target dedicated tunnel and click <img width="3%" src="https://main.qcloudimg.com/raw/52d8549cc2412c6527f332a3b88be44d.png"  > in the **Monitoring** column.
 3. The **Monitoring** page displays **Network Outbound Bandwidth**, **Network Inbound Bandwidth**, **Packets Out**, and **Packets In**. Select **Last 24 hours**, **Last 7 days** or a custom time period to display the monitoring data accordingly.
      - **Network Outbound Bandwidth**: average outbound traffic of the dedicated tunnel per second.
      - **Network Inbound Bandwidth**: average inbound traffic of the dedicated tunnel per second.
      - **Packets Out**: total outbound traffic of the dedicated tunnel.
      - **Packets In**: total inbound traffic of the dedicated tunnel.
4. Perform the following steps to view the network monitoring data of a direct connect gateway.
 1. Log in to the Direct Connect Gateway console. Click **Direct Connect Gateway** in the left sidebar.
 2. Locate the target direct connect gateway and click <img width="3%" src="https://main.qcloudimg.com/raw/52d8549cc2412c6527f332a3b88be44d.png" > in the **Monitoring** column.
 3. The **Monitoring** page displays **Network Outbound Bandwidth**, **Network Inbound Bandwidth**, **Packets Out**, **Packets In**, **Outbound Traffic**, and **Inbound Traffic**. Select **Last 24 hours**, **Last 7 days** or a custom time period to display the monitoring data accordingly.
    - **Network Outbound Bandwidth**: average outbound traffic of the direct connect gateway per second.
    - **Network Inbound Bandwidth**: average inbound traffic of the direct connect gateway per second.
    - **Packets Out**: total number of outbound traffic packets of the dedicated tunnel.
    - **Packets In**: total number of inbound traffic packets of the dedicated tunnel.
    - **Outbound Traffic**: total outbound traffic of the dedicated tunnel.
    - **Inbound Traffic**: total inbound traffic of the dedicated tunnel.
    - **Packet loss (Out)**: total number of outbound packets discarded on the dedicated tunnel.
    - **Packet loss (In)**: total number of inbound packets discarded on the dedicated tunnel.
