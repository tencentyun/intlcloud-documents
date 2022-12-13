This document describes how to install and configure Terraform.

## Step 1. Install Terraform[](id:Step1)
1. Go to [Terraform official website](https://www.terraform.io/downloads.html) and use the command line to install Terraform directly or download the binary installation file.
2. Unzip the file and configure the global path.
Skip this step if you use the command line.
<dx-tabs>
::: Linux and macOS
 1. Run the following command to unzip the file. Replace 1.x.x with the actual version number of Terraform to be installed.
```bash
unzip terraform_1.x.x_linux_amd64.zip
```
 2. Run the following command to add the current directory to the `~/.profile` file.
```bash
echo $"export PATH=\$PATH:$(pwd)" >> ~/.bash_profile
```
 3. Run the following command to make the global path configuration take effect.
```bash
source ~/.bash_profile
```
:::
::: Windows
1. On the desktop, right-click the **This PC** icon and select **Properties** in the pop-up menu.
2. In the pop-up window, click **Advanced system settings**.
3. In the **System Properties** window that pops up, click **Environment Variables**.
4. In **System variables**, add the absolute path of `terraform.exe` to `Path` as shown below:
This document uses Windows 10 as an example, and `terraform.exe` is located in `D:\xxxx\terraform`.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/QSXQ889_WXWorkCapture_16705665289563.png)
5. Click **OK**.

:::
</dx-tabs>
3. Run the following command to check whether the installation is successful.
```bash
terraform  -version
```
If the following information is returned (the version number may be different), the installation is successful:
```bash
> Terraform v1.0.10
> on darwin_amd64
> Your version of Terraform is out of date! The latest version
> is 1.1.0. You can update by downloading from https://www.terraform.io/downloads.html
```

## Step 2. Configure security credentials[](id:capi)
Before using Terraform for the first time, go to the [TencentCloud API Key](https://console.cloud.tencent.com/cam/capi) page to apply for `SecretId` and `SecretKey`. If you already have them, go to step 3.

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview) and select **Access Key** > **Manage API Key** on the left sidebar.
2. On the **Manage API Key** page, click **Create Key** to create a pair of `SecretId/SecretKey`.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/R599851_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16705554473578.png)
3. You can authenticate in two ways:
<dx-tabs>
::: Authentication by environment variable
Add the following content to the environment variable configuration:
Replace `<your-secret-id>` and `<your-secret-key>` with `SecretId` and `SecretKey` obtained in the [Get credentials](#capi) step.
```
export TENCENTCLOUD_SECRET_ID=<your-secret-id>
export TENCENTCLOUD_SECRET_KEY=<your-secret-key>
```
:::
::: Authentication by Static Credential
Create a `provider.tf` file in the user directory and enter the following content:
Replace `<your-secret-id>` and `<your-secret-key>` with `SecretId` and `SecretKey` obtained in the [Get credentials](#capi) step.
```
provider "tencentcloud" {
    secret_id = "<your-secret-id>"
    secret_key = "<your-secret-key>"
}
```
:::
</dx-tabs>

4. At this point, you have installed Terraform and configured the environment variable. You can now proceed to [create a site through Terraform](https://www.tencentcloud.com/document/product/1145/51434).