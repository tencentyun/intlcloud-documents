
You can monitor services in TKE by managing **ServiceMonitor** or **PodMonitor**.

## Preparations

- The Prometheus agent has been installed in the TKE cluster. For more information, please see Agent Management.
- Click a **Cluster ID** in the TKE cluster list to enter the **Integrate with TKE** page.

## Directions

1. Click **Scrape Configuration** on the **Integrate with TKE** page to enter the scrape configuration management page.
2. Click **Create** to pop up the scrape configuration creation page, select the scrape configuration type, and modify the YAML configuration as prompted.
<img src="https://qcloudimg.tencent-cloud.cn/raw/6b30df6f617e43733b5205657f40280d.png" style = "width:80%">
3. After completing the configuration, click **OK**.
>?Some configuration items will be automatically generated after the scrape configuration is created. Please do not modify them.
