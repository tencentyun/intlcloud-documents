Currently, EMR v1.3.1 and v2.0.1 support [Apache Knox](https://knox.apache.org/?spm=a2c4g.11186623.2.10.22b554deZiOUor). After completing the following preparations, you can access the web UIs of services such as Yarn and HDFS on the internet.

## Preparations
- You have signed up for a Tencent Cloud account and created an EMR cluster.
- In EMR version 1.3.1 and 2.0.1, Knox is a required component by default when a cluster is created. If you use a legacy version, please [contact our customer service](https://intl.cloud.tencent.com/support) to help you install Knox.

## Accessing Knox
Access by using the public IP address of the cluster. You are recommended to modify the CVM security group rule of this IP to limit the accessing IP address on the TCP:30002 port to your own IP address.
1. View the public IP address in the cluster details.
2. Access the URL of the corresponding service in a browser.
   - HDFS UI: https://{public IP address of the cluster}:30002/gateway/emr/hdfs
   - Yarn UI: https://{public IP address of the cluster}:30002/gateway/emr/yarn
   - Hive UI: https://{public IP address of the cluster}:30002/gateway/emr/hive
   - HBase UI: https://{public IP address of the cluster}:30002/gateway/emr/hbase/webui
   - Hue UI: https://{public IP address of the cluster}:30002/gateway/emr/hue
   - Storm UI: https://{public IP address of the cluster}:30002/gateway/emr/stormui
   - Ganglia UI: https://{public IP address of the cluster}:30002/gateway/emr/ganglia/
   - Presto UI: https://{public IP address of the cluster}:30002/gateway/emr/presto/
   - Oozie UI: https://{public IP address of the cluster}:30002/gateway/emr/oozie/
3. The browser may display an error message saying that **your connection is not private**. This is because that the Knox service uses a self-signed certificate. Please confirm again that you are accessing the public IP address of your own cluster and the port is 30002. Then, select **Advanced** > **Proceed**.
4. In the login box that pops up, the username is root, and the default password is the one entered when the cluster was created. **It is recommended to change the password by clicking **Reset Native UI Password** on the page.**


