## Connecting to a Container Through a Remote Terminal
1. Log in to the TKE console and click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. On the "Cluster Management" page, click the cluster ID (cls-xxx) to go to the cluster details page.

3. On the cluster details page, choose **Node Management** > **Nodes** in the left sidebar.
4. On the "Node List" page, click the node ID to go to the pod management page.
5. Click **Remote Login** for the instance to log in to the remote terminal.

>Containers meeting any of the following conditions do not support remote login:
> - The namespace is kube-system.
> - No bash is available in the container image.

## Running Commands for Containers Without Shell
1. Go to the remote terminal page.
2. Enter the command to run in the entry box at the bottom, and then click "OK", as shown in the following figure:
![](https://main.qcloudimg.com/raw/e019990698f5dc555950bde7052b2aeb.png)

## Uploading and Downloading Files
1. Go to the remote terminal page.
2. Click the file assistant at the bottom, select file uploading or downloading, as shown in the following figure:
 - For uploading, you need to specify the path to the file to be uploaded.
 - For downloading, you need to specify the path for storing the file to be downloaded.
![](https://main.qcloudimg.com/raw/37a2b9bdc9bb6b0e878c9c8f5b4bc35e.png)
