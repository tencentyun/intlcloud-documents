If the public IP address of a CVM instance is under DDoS attacks, it has been exposed. Therefore, after accessing the DDoS protective IP, you need to replace the exposed public IP address to prevent the attackers from bypassing the protective IP and continuing to directly attack the real server IP.

To replace the public IP address of the CVM instance, follow the steps below:

## I. Converting CVM Instance's IP to EIP
If the public IP address of the current CVM instance is not an EIP, you need to convert it to an EIP first, so that the original IP address can be retained after the replacement.
First, go to the [CVM Console](https://console.cloud.tencent.com/cvm/overview). In the "Primary IP" column, click the "Convert to EIP" button as shown by the arrow below and then click **Convert to EIP** in the pop-up.
![](https://main.qcloudimg.com/raw/2f65c454cfeaba3ecc977431351c5351.png)
![](https://i.imgur.com/N7NpuCT.png)
>**Note:**
>When converting the current public IP to an EIP, the service will not be interrupted.

## II. Converting EIP to Public IP
In the "Operation" column, under "More", select "Unbind EIP" in "IP Operation" and then "Assign a free public IP after unbinding", and click **OK**. At this point, the CVM instance's IP has been updated to a public IP address.
![](https://i.imgur.com/srrYYJS.png)
![](https://i.imgur.com/TqSUUtM.png)

>**Note:**
If your CVM instance has already used an EIP, you can directly bind it to other existing EIPs.

In the first step, click **Other EIPs** instead of **Convert to EIP**, then you will be redirected to the "Bind EIP" page; click the "Select EIP" box, select an IP and click **OK** to assign a new public IP address to the CVM instance.
![](https://i.imgur.com/dKrhPA0.png)
![](https://i.imgur.com/ZERnCIK.png)
