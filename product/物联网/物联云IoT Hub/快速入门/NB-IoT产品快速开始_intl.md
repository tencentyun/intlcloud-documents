[//]: # (chinagitpath:XXXXX)

The differences between NB-IoT products and general products can be found in **Console User Manual** > **Product Management** > **[Product Type](https://cloud.tencent.com/document/product/634/18348)**.

## 1. Application Scenarios and Features
- You have a China Telecom NB-IoT module, which reports and sends data between the device and application platform and queries the last report time of the data.  
- You only need to configure the IoT Hub to achieve the above features. You don’t need to configure the China Telecom NB-IoT platform. 
- After the NB-IoT module is connected to the ISP's network using the device's serial commands, the data is reported to the ISP's NB-IoT platform using the AT command. The data is sent from the ISP to the IoT Hub platform through callback and forwarded to your platform or Tencent Cloud components or storage services based on the rules you configure. Similarly, your platform can call the RestAPI of the IoT Hub platform to send the data to the device.  
![Data flow](https://main.qcloudimg.com/raw/8d320cf009b8f405760a2b12b94e91f5/NB-IoT_freamwork.png)

## 2. Steps
### 2.1 Create an NB-IoT product and device
1. Go to the [Console](https://console.cloud.tencent.com/iotcloud) to create an NB-IoT product and select the key authentication method.  
![](https://main.qcloudimg.com/raw/8e5034baf6383a449a1b1552d775fe55/NB-IoT_product.png)
2. After successful creation, you can view the basic information of the product.  
![](https://main.qcloudimg.com/raw/c4a3ddb2dbdffc7a6beec29fef12c4ed/NB-IoT_product_info.png)
3. Create a device (NB01) in the **Device List** and select China Telecom NB-IoT as the ISP.  
![Return of device creation](https://main.qcloudimg.com/raw/dcb3d03f5845141e86f9c6a23347bcea/NB-IoT_device.png)
4. Click **Manage** to query the device details.  
![](https://main.qcloudimg.com/raw/7a649fdadca776f5d506f3af83a46b56/NB-IoT_device_info.png)

### 2.2 Create a rule engine
In this example, the reported data is forwarded to your application platform using HTTP POST requests with JSON packets.  
The rule engine also supports forwarding to Tencent Cloud's storage components and message queues.  
![Create a rule engine](https://main.qcloudimg.com/raw/26acf7aa274fe686e857fda1e70b98d2/NB-IoT_forward_app.png)  
For detailed steps, see [Rule Engine Details](https://cloud.tencent.com/document/product/634/14446).
### 2.3 Download the NB-IoT SDK
Download the SDK [here](https://cloud.tencent.com/document/product/634/11928).
### 2.4 Configure the C-SDK sample program
samples/nbiot/nbiot_sample.c is the sample code for uplink data encoding and downlink data decoding.  
The SDK's uplink data encoding mainly helps encode the payload to be transferred into the data transferred by the AT command, including population of fields such as topic, authentication and transfer quality control.  
The downlink data decoding mainly parses the information such as the topic, payload and transfer quality sent by the IoT backend.  
#### 2.4.1 Encode the uplink data
1. API  
int IOT_NB_setMessage(unsigned char* msg, unsigned int* length, NBIoTSetMessage* nbiotMsg);  
-msg      The generated hexadecimal uplink message encoding  
-length   Length of the hexadecimal uplink message in bytes  
-nbiotMsg The structure of the message sent by the NB-IoT device, including address, version, signature type, expiry time, transfer quality, topic, payload and key 
 
#### 2.4.2 Decode the downlink data
1. API  
int IOT_NB_getMessage(NBIoTGetMessage* nbiotMsg, unsigned char* msg);  
-nbiotMsg The structure of the message content parsed by the NB-IoT device, including address, version, signature type, expiry time, transfer quality, topic and payload  
-msg      The hexadecimal downlink message encoding sent by the NB-IoT platform to the device 
 
### 2.5 Access the device
1. Insert the IoT card into the NB-IoT module and power it on.  
2. The device sends an AT command through the serial port TTL. Configure the network and confirm the network status (China Telecom NB-IoT module Lierda NB05-01 is used as an example here, and the initialization processes of other modules may vary slightly). 
```
AT+CFUN=0 // Turn off the RF feature
AT+CGMR // Query the firmware version (optional)
AT+CGSN=1 // Query the IMEI number. If ERROR is returned, the IMEI number has not been set for the module and needs to be set in the following step
AT+NTSETID=1, 201612091450303 // Set the IMEI number. This step is required only if there is no IMEI number. It can only be set once and repeated setting is invalid
AT+NCDP=XX.XX.XX.XX // Set the IP address of the IOT platform, which is needed for the CoAP protocol. The IP address of the China Telecom platform is 117.60.157.137
AT+CGDCONT=1,”IP”,”PCCW” // Set the APN. Currently, enter ”IP”,”PCCW” for Shanghai OPENLAB and confirm with Tencent Cloud in advance for other network environments 
AT+NRB // Soft restart
AT+CFUN=1 // Enable full RF feature
AT+CSCON=1 // Set base station connection notification (optional)
AT+CEREG=2 // Set core network connection notification (optional)
AT+NMMI=1 // Downlink data notification
AT+CGATT=1 // Automatically search for the network
AT+NUESTATS // Query UE status, including RSRP, SINR, coverage level and cell information (optional)
AT+CGPADDR // Query the assigned IP address to determine whether the network is connected to  
```
3. Report the data  
```
AT+NMGS=len,data // Send len bytes of data. If the transfer succeeds, OK will be replied; otherwise, ERROR
+NNMI:4, AAAA0000 // Receive a response message "4"
```
len,data is generated by the SDK in step 2.5. For detailed data format, see the SDK description.  
After the AT+NMGS command is executed, OK is replied after the NB-IoT module sends the data. At this time, the data has been sent to the base station, which has not necessarily received the data successfully.  
If a data reporting confirmation message AAAA0000 is received, the China Telecom platform has received the data. (You can set the number of retries for data reporting as needed, and it is recommended to set the timeout to 3 seconds.)  
4. The application platform receives the data  
The application platform receives data pushed by HTTP POST with the following body content:
```
{"payload":xxxx, "seq":12345, "timestamp":140000245, "topic":"/xx/xx/xx", "devicename":"xx", "productid":"xx"}
```  
5. Send the data   
The data is sent to the device through the [message publishing](https://cloud.tencent.com/document/product/634/12278) RestAPI. After the RestAPI publishes the message, the device will receive the data returned by the serial port TTL. If the data is not received promptly, the reason is that the connection between the NB-IoT module and the platform is not a persistent connection, so the platform cannot detect whether the NB-IoT module is online. As soon as the device actively reports the data once, the message sent will be returned immediately. 
 
### 2.6 Query the status
The connection between the NB-IoT module and the platform is not a persistent connection, so the platform cannot detect whether the NB-IoT module is online. How can you know whether the device status is normal?  
A [device status querying API](https://cloud.tencent.com/document/product/634/18341) is provided to query the last data reporting time of the device. You can compare it with the current time to determine the device status.  
For example, the interval for data reporting by your NB-IoT device is 20 hours, but the last reported time is three days ago, so it can be determined that the device is in exceptional status.  

