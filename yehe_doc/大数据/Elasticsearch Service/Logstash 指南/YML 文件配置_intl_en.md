This document describes how to configure the YML parameters of a Tencent Cloud Logstash instance in the ES console.

## Directions
1. Log in to the [ES console](https://console.cloud.tencent.com/es) and click **Logstash Instance** on the left sidebar to enter the Logstash instance list page.
2. Click the **ID/Name** of the target instance to enter its basic information page.
3. On the instance information page, switch to the **Advanced Configuration** tab, click **Modify Configuration**, and modify the YML parameters according to your business needs. For detailed parameter descriptions, see [logstash.yml](https://www.elastic.co/guide/en/logstash/current/logstash-settings-file.html).
![](https://qcloudimg.tencent-cloud.cn/raw/0204bf0e2f450885e417b3dcb8c5a515.png)
4. After configuring the YML parameters, click **Save**. You will be prompted to restart the Logstash instance. The changes can take effect only after the instance is restarted, so the instance will be restarted after you click **Confirm**. You can view the restart progress in **Change History**.
