New developers can follow the 5 steps listed below to build a simple website (all steps are required without a certain sequence):
![](https://main.qcloudimg.com/raw/57063be2a96fd3171e6df44568c97d22.png)
### Register a domain name with Tencent Cloud or Transfer a domain name to Tencent Cloud
Domain name registration is basic for establishing any service on the internet. A domain name is required before you can build a website.
 - If you already have a domain name at another registrar, you can transfer it to Tencent Cloud.
 - If you don't have one, you need to [register a domain name](https://buy.cloud.tencent.com/domain).

It is recommended that you use a simple and easy-to-remember name comprised of letters based on the nature of your website. If you plan to build a Chinese website, you can use Chinese pinyin as the domain name (such as `baidu.com`), to make it easier for you to promote the website and leave an impression on visitors.
Open the [Tencent Cloud official website](https://cloud.tencent.com/), and click **Products** -> **Domain Name and Website** -> **Domain Service** from the top navigation bar. Then, query the domain name you want to purchase, select the usage period, and complete the payment to obtain your domain name.
>**Note:**
>As required by the registry, for domain names with the suffixes ".com/.cn/.net/.xyz/.club/.info/.mobi/.中国", identity verification must be completed within 5 work days after registration, or they will be put into Serverhold status and cannot be used.

### ICP licensing
According to the regulations of MIIT, websites without permission or an ICP license cannot engage in any internet information services, otherwise it is considered illegal. To ensure the persistent and normal operation of your website, get an ICP license before setting up a website. The website cannot be accessed until you obtain the ICP license number issued by MIIT. If your domain name has not been licensed, complete [ICP licensing](https://console.cloud.tencent.com/beian) first.
Log in to the console, click **ICP License** on the upper-right corner to go to the **ICP Licensing** page and apply for an ICP license for your purchased domain name. For more information, see [here](https://cloud.tencent.com/document/product/243/655).

### Purchase a CVM
You need a place on the internet to store the information of your website. Therefore, you should [purchase a CVM](https://intl.cloud.tencent.com/product/cvm).
Featuring high security and flexible configuration, Tencent Cloud Virtual Machine (CVM) is more than enough for you to build a personal blog or a small website. If you have sufficient budget, it is recommended to prioritize performance attributes based on your actual demand. For example, you can select a CVM with large memory and CPU to cater for high computing capacity, or select one with large bandwidth and memory to accommodate high access requests.
Open [Tencent Cloud official website](https://cloud.tencent.com/), and click **Products** -> **Compute** -> **Cloud Virtual Machine** from the top navigation bar. Click **Buy Now** to open the CVM purchase page and select a model that suits your website best.
**1. Select a region and model:** Select a region nearest to your customers, so that they can access your website quickly.
 - CPU: It represents the computing capacity of a CVM. It is recommended to choose a CPU with 2 cores or more if your website expects a lot of traffic and contains many dynamic pages.
 - Memory: Select this according to the size of your website. You can use a smaller memory for a personal blog or an enterprise presentation website, or a larger memory for websites such as online stores or news websites.

**2. Select an image:** The basic environment provided by Tencent Cloud, which contains an operating system and initialized components. You can configure the application environment and relevant software on your own.
**3. Select storage and network:** Select a suitable disk size and network bandwidth for your CVM.
 - Disk: This depends on the data amount of your website. You should consider the space left when selecting this option. In addition, the I/O speed of a disk determines the speed of reading files.
 - Bandwidth: Select a suitable bandwidth according to the nature of your website. Text-based or image-based Websites or forums require very little bandwidth, in which case 2 MB is enough basically. While websites that are mainly used for video playback or download may require a bandwidth of 10 MB or more.

**4. Settings:** Set a CVM name, a user name and a password.
Then, submit the purchase order to complete the purchase process.

### Build a website
Since the preparation work is done, you only need to build a simple website on the CVM your purchased to get your very own website on the Internet.
To build a WordPress blog platform, see [here](https://intl.cloud.tencent.com/document/product/213/8044).
To build a Discuz forum platform, see [here](https://intl.cloud.tencent.com/document/product/213/8043).

### Domain name resolution
Domain name resolution is a necessary step to allow your website to be accessed by its domain name. You can select Tencent Cloud DNSPod resolution to ensure that your website enjoys a stable, fast and secure resolution service. To access your website using the purchased domain name, [domain name resolution](https://console.cloud.tencent.com/cns/domains) is required.
Log in to the [Tencent Cloud Console](https://console.cloud.tencent.com/), click **Products** -> **Domain Name and Website** -> **Domain Service** to go to the domain name list. Click **Resolve** in the **Operation** column of the corresponding domain name and add a resolution record to finish the resolution setup. For more information, see [here](https://cloud.tencent.com/document/product/302/3446).
After completing the above steps, open a browser and access your domain name to browse your website.

