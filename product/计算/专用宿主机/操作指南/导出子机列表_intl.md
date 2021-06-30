You can export the list of instances on a specified host in the console and customize the fields contained in the export list. You can check up to 26 fields, including: ID, host name, status, region, availability zone, host type, operating system, image ID, CPU, memory, bandwidth, public IP, private IP, system disk type, system disk size, data disk type, data disk size, network, subnet, associated VPC, creation time, expiration time, host billing method, network billing mode, project and tag.

### Steps

1. Log in to the [CDH Console](https://console.cloud.tencent.com/cvm/cdh).

2. Select a region. Click the **ID/Host Name** of the target dedicated host to enter its details page, select the CVM list tab, and click **Download** as shown below.

   ![Instance list export entry](https://main.qcloudimg.com/raw/a0f8ddc84abdcb88c03560e5e5bebbe8.jpg)

3. Select the fields to be exported and click **OK**.
    ![Customizing export fields](https://main.qcloudimg.com/raw/d2bea2d8e05fdde1cce1373d784e5e2a.png)

4. Download the cvm.csv which contains the following items:
    ![Exported instance list](https://main.qcloudimg.com/raw/d6a3596b09b55acf1ed71855d844367b.png)
