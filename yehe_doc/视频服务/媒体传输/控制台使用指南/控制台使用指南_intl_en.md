The MediaConnect service is managed at the flow level in the MediaConnect Console, and each flow corresponds to a stream transfer linkage. You can quickly and stably transfer video streaming media and comprehensively monitor the quality of the video streams during the transfer in the console.

## 1. Region Selection


Region indicates the starting point of your flow transfer linkage. You can select an AZ at the top of the console page before you start using the service. Currently, multiple nodes in Asia, Europe, West US and other regions can be selected in the console. If you need to deploy more nodes, please feel free to [contact us](https://intl.cloud.tencent.com/contact-sales).

## 2. Main UI

![](https://main.qcloudimg.com/raw/ede8fc9543079f0ed9ae11af6c3e7867.png)

The main UI of the MediaConnect Console displays all the flows you have created and their running status. Each flow supports the input of primary and backup streams. You can push the two streams at the same time to ensure the transfer stability. You can click "Start/Stop" in the "Operation" column on the right to start/pause the transfer. A flow that is being transferred cannot be deleted.

## 3. Flow Creation

Click "Create Flow" at the top of the console, and then you can enter the flow name and select a `Max Bandwidth` (valid values include 10 Mbps, 20 Mbps, and 50 Mbps).

Then, you need to configure the relevant information of the input source: after selecting the transfer protocol, you need to set the `Latency` parameter. This parameter affects the size of buffers to save data sent and received by the server, and we recommend increasing this parameter if the network condition is poor. This parameter is set to 120 ms by default in the console, and you can modify it as needed.

>? For the `Latency` parameter, you can perform a ping test on the IP address given after the creation to determine the optimal value. In addition, you can also directly use the default value and then adjust the `Latency` value on the sender side to achieve the same goal. 

![](https://main.qcloudimg.com/raw/cc8fa08079c4b37902ac8ce9aa707b4e.png)

MediaConnect supports transfer encryption and decryption based on the SRT protocol. If the stream you push to MediaConnect is an encrypted flow, you can enable "Decryption Settings", enter the `Decryption key`, and select the `Key Length` for MediaConnect to decrypt your upstream.

![](https://main.qcloudimg.com/raw/fa39d86e4fd351e94421b0b9a44e4cb8.png)

In addition, you can also set the IP allowlist (in CIDR format) of the input source, so that streams can be pushed to this flow only from IPs in the allowlist.
You can also configure descriptive information for the flow's input source, so that you can distinguish different input sources.
After you click "Create", the flow will be created. MediaConnect will automatically generate the input IP addresses of the primary and backup tunnels for the created flow, and then you can push to these addresses.

> ! The flow cannot be used before an output node is created.

## 4. Flow View

Click the name of the flow you just created on the main UI to enter the flow details page, where you can view the flow information and input source status and configure a flow output node.
You can click the editing icon in the top-right corner to edit the flow.

![](https://main.qcloudimg.com/raw/d6897c517e505289ee4a97ff2b74941f.png)

## 5. Outputs

You can view the information of all output nodes on the "Outputs" tab on the flow details page, where you can also create, delete, or edit an output node.

> ! This operation is not allowed for running flows.

![](https://main.qcloudimg.com/raw/58635595342363458b60bcd704641a60.png)

You can click "Create Output" to create an output. MediaConnect supports the one-flow-multi-output mechanism, so you can configure output nodes in different regions for the same flow input source.

![](https://main.qcloudimg.com/raw/2bc94f3f111e3b9087bf1184ca2da641.png)

MediaConnect supports remuxing the transfer protocol. You can select the output protocol when creating an output. If you select the SRT protocol, you need to enter the `Destination IP` address and `Port` (primary and backup).You can also make `Latency Setting` here. The default value is 120 ms and you can modify it as needed.

>! The primary and backup tunnels of an output node are independent from each other and correspond to the primary and backup tunnels of the input source respectively. This means that the stream you push to the primary tunnel of the flow will be output to the primary destination address after being transferred through MediaConnect, while the stream pushed to the backup tunnel of the flow will be output to the backup destination address after being transferred through MediaConnect, and the two are independent.
> The primary output address is required, while the backup output address is optional.

If you need to encrypt the output stream of the SRT protocol, you can enable encryption here, and then you need to enter the encryption key and select the key length.

![](https://main.qcloudimg.com/raw/d1db5d2467bc2407a49e0c7cbb037853.png)

If you select the RTMP protocol for output, you need to enter the `Destination URL` and `Stream Key` (primary and backup). The logic of the primary/backup tunnels is the same as above.

![](https://main.qcloudimg.com/raw/60eb05dc28c112e7f0bc22c9dcb6ae94.png)

## 6. Flow Start/Stop

After creating the flow and output node, click "Start" to successfully run the flow. When you are done using the flow, click "Stop" to stop it.
![](https://main.qcloudimg.com/raw/160685a685708d2aacb24ff28c3a8bbc.png)
