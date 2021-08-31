In the ECDN Console, you can enable, disable, and delete the acceleration service or modify the projects for acceleration domain names.
>? If your application has been migrated to the CDN console, you can go to the console for operation by referring to [Content Delivery Network](https://intl.cloud.tencent.com/document/product/228).
## Enabling Acceleration Service
You can **activate** a **deactivated** domain name in the following steps. It takes about 5 minutes to enable the acceleration service.
Log in to the [ECDN Console](https://console.cloud.tencent.com/dsa) and click **Domain Management** on the left sidebar to enter the **Domain Management** page. In the "Operation" column of the target domain name, click **Activate**.
![](https://main.qcloudimg.com/raw/f41254a8573147db7d1036dd685d9ee0.png)

If you want to activate multiple acceleration domain names in batches, you can check them and click **Activate ECDN** above.  
![](https://main.qcloudimg.com/raw/98ff0d10d85f6a967c05d9424eb6667c.png)

## Disabling Acceleration Service
You can **deactivate** an **activated** domain name in the following steps. After the domain name is deactivated, it will no longer be accelerated, but its configuration will be retained. It takes about 5 minutes for domain name deactivation to take effect.

Log in to the [ECDN Console](https://console.cloud.tencent.com/dsa) and click **Domain Management** on the left sidebar to enter the **Domain Management** page. In the "Operation" column of the target domain name, click **Deactivate**.  
![](https://main.qcloudimg.com/raw/1173e5276326801e272f37f40c5370fe.png)

If you want to deactivate multiple acceleration domain names in batches, you can check them and select **Deactivate ECDN** in the **More Actions** drop-down list above.  

>!
>Before disabling the acceleration service, make sure that your domain names have been resolved to the origin server, as ECDN nodes will no longer provide acceleration service for them and will directly return the status code 404 for received user requests after acceleration is disabled. To avoid affecting your user access experience, you are recommended to perform the following steps when disabling the acceleration service:  
>1. Change the acceleration domain name resolution
Resolve the acceleration domain name to the origin server and make sure that it will not be resolved to the ECDN domain name through the CNAME record. Change of the domain name resolution generally takes 10–30 minutes to take effect in most regions.  
>2. Check the traffic change
After the domain name resolution is switched to the origin server, user requests will no longer be forwarded to the ECDN acceleration platform. In the ECDN Console, you can see that the access traffic of the corresponding domain name will drop significantly. Before disabling the service, please confirm that the ECDN access traffic of the corresponding domain name has decreased to 0; otherwise, directly disabling the service will affect user access.  
>3. Disable the acceleration service

![](https://main.qcloudimg.com/raw/4c6ee7fe1302671f4627a1058061ab6b.png)

After confirming that all or most users no longer use ECDN for access, you can deactivate the domain name in the following steps:  

>!
>- Domain name deactivation will affect user access. Please do so with caution.  
>- After the domain name resolution is switched to the origin server, user requests may still be forwarded to ECDN cache nodes, as local DNS servers of a minority of users do not follow the domain name TTL rule. In this case, those users need to change their local DNS server addresses or set `hosts` resolution.
>- Generally, you are recommended to switch the domain name resolution to the origin server first and then disable the domain name acceleration service after 24 hours.

## Deleting Acceleration Domain Name

You can **delete** a **deactivated** domain name. Its configuration will not be retained upon deletion.

Log in to the [ECDN Console](https://console.cloud.tencent.com/dsa) and click **Domain Management** on the left sidebar to enter the **Domain Management** page. In the "Operation" column of the target domain name, select **Delete** in the **More** drop-down list.
![](https://main.qcloudimg.com/raw/7832491620414e8194b9cd96dc6b4845.png)

If you want to delete multiple acceleration domain names in batches, you can check the target domain names and select **Delete** in the **More Actions** drop-down list above.
![](https://main.qcloudimg.com/raw/aae06204d5b3914afdc8b36db78b5b78.png)

## Modifying Project of Domain Name

To facilitate management, you can modify the project of your domain name in the following steps.
1. Log in to the [ECDN Console](https://console.cloud.tencent.com/dsa) and click **Domain Management** on the left sidebar to enter the **Domain Management** page. In the "Operation" column of the target domain name, select **Modify Project** in the **More** drop-down list.
![](https://main.qcloudimg.com/raw/2e99c52ef12a195148f5f5293fea7faf.png)
2. The **Project** drop-down list will be displayed in the pop-up dialog box. You need to select a project for the domain name. Click **OK** to modify the domain name's project.
![](https://main.qcloudimg.com/raw/dde68173ff938198d1bb877685b927b7.png)

If you want to modify the project of multiple acceleration domain names in batches, you can check the target domain names and select **Modify Project** in the **More Actions** drop-down list above.
![](https://main.qcloudimg.com/raw/2cc9d25b957da9334faba33751a23879.png)

>! 
> - You can use the project feature to manage Tencent Cloud resources by project. Tencent Cloud Project Management can be applied to multiple products at the same time.  
> - You can create and modify projects on the [Account Center - Project Management](https://console.cloud.tencent.com/project) page in the Tencent Cloud Console.
