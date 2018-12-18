If the following note is present on the record management page of the domain name, it means that the DNS server is incorrect, and you need to modify the domain name's DNS to the prompted DNS address for the resolution to take effect.
![1](//mc.qcloudimg.com/static/img/461b3011772da9f667c9e54dd45ef660/image.png)
>**Note:**
>The DNS addresses vary for different resolution packages. Please modify them according to the prompts.

### Modifying DNS for a Domain Name Registered with Tencent Cloud
If a domain name is registered with Tencent Cloud or has been transferred to Tencent Cloud, you can modify the DNS server by taking the following steps:
1. Log in to the [Tencent Cloud Console](https://console.cloud.tencent.com/) and select **Products** -> **Domain Services**.
![1](https://main.qcloudimg.com/raw/a6db6f18b3144223eabddcffd34d628f.png)
2. Select the domain name and click **Manage**.
![2](//mc.qcloudimg.com/static/img/1dbc9f9c19eb5543fcde41577e817ff0/image.png)
3. **Modify** the DNS server.
![3](//mc.qcloudimg.com/static/img/f4178f07026b20d51e6cf7ae7a41c07c/image.png)
4. Enter the specified DNS server address.
![4](https://mc.qcloudimg.com/static/img/0b866d917b994eb84eab2a58b6cd16e3/5.png)

If the domain name is managed by another registrar, you need to go to the domain name management page of the registrar and modify to the specified domain name DNS.
The following are examples for Alibaba Cloud (Wanwang) and GoDaddy.

### Modifying DNS at Alibaba Cloud (Wanwang)
1. Select the domain name that needs to be resolved by Tencent Cloud, enter **Modify/Create DNS** on the domain name management page and click **Modify domain name DNS**;
![](https://mccdn.qcloud.com/static/img/2ade9bc496f296f14186df348835ed8e/image.png)
2. Enter f1g1ns1.dnspod.net and f1g1ns2.dnspod.net and wait up to 72 hours before the change takes effect globally.
![](https://mccdn.qcloud.com/static/img/bca1fc5a448568567c3498b3d2c0da4d/image.png)

### Modifying DNS at GoDaddy
1. Log in at [GoDaddy](http://www.godaddy.com) and click **Manage** for **DOMAINS**.
![1](https://mccdn.qcloud.com/static/img/857a65f25a4c950dab04f36c6773bf20/GD-1.png)
2. In the list of domain names, select the one for which to modify the DNS and click **Set Nameservers** in the domain name's drop-down list.
![2](https://mccdn.qcloud.com/static/img/d692fab785a928ebbfc183637bdd9c31/GD-2.png)
3. Select **Custom** and click **Add Nameserver** in the lower left corner.
![3](https://mccdn.qcloud.com/static/img/2b5194f50b656d4d75666d2357f784b6/GD-3.png)
4. Enter f1g1ns1.dnspod.net and f1g1ns2.dnspod.net, click **Add Nameserver** -> **Save** and wait for the global recursive DNS server to refresh (within up to 72 hours).
![4](https://mccdn.qcloud.com/static/img/bed919b5d4fe0b33b6bc9f537dce1a8d/GD-4.png)
![5](https://mccdn.qcloud.com/static/img/8c4f15a5fa913037a06f752ac62ac22b/GD-5.png)

