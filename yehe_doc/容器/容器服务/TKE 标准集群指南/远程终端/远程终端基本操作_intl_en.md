## Connecting to a Container through Remote Terminal
1. Log in to the TKE console and select **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. On the **Cluster Management** page, click the cluster ID (cls-xxx) to go to the cluster details page.
3. In the left sidebar, select **Node Management** > **Node**. On the **Node List** page, click the node ID to go to the Pod management page.
4. In the instance list, click **Remote login** in the **Operation** column of the instance.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/CgXp682_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221223160402.png)
<dx-alert infotype="notice" title="">
Containers meeting any of the following conditions do not support remote login:
- The namespace is kube-system.
- A bash is not built in the container image.
For FAQs about the remote terminal, see [here](https://intl.cloud.tencent.com/document/product/457/8638).
</dx-alert>
5. In the container login pop-up window, select shell and select **Login** on the right side of the container you want to log in.


## Running Commands for Containers Without Shell
1. Go to the remote terminal page.
2. Enter the command to be run below and click **Enter**, as shown in the following figure:
![](https://qcloudimg.tencent-cloud.cn/raw/68d5298797ff405816af9bf74e169f44.png)

## Uploading and Downloading Files
1. Go to the remote terminal page.
2. Click **File** and select **Upload File** or **Download File**.
![](https://qcloudimg.tencent-cloud.cn/raw/1869cf17e59d25858c8fe44abe0a59f6.png)
 - **Upload File**: Specify the directory to which the files are to be uploaded.
 - **Download File**: Specify the path of the files to be downloaded.


