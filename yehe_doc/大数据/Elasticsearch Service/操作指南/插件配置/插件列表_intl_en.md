

Tencent Cloud Elasticsearch Service (ES) provides over 10 plugins such as open-source Elasticsearch plugins and Tencent Cloud's proprietary plugins to deliver a wealth of plugin features. After purchasing an ES instance, you can install/uninstall these plugins on the plugin list page as needed. This document describes how to do so.

### Notes

Rolling restart of the cluster will be triggered after you install or uninstall a plugin; therefore, please do so with caution.

### Directions

1. Log in to the Tencent Cloud ES Console.

2. On the cluster list page, click a cluster ID to enter the cluster details page.

3. Click **Plugin List** to enter the plugin list management page.

   ![1594269905799](https://main.qcloudimg.com/raw/7c320711d9f98d7f754e79251ce378df.jpg)

4. Click "Install" or "Uninstall" in the "Operation" column on the right of the target plugin.

5. In the pop-up dialog box, read the notes and click "OK" after confirming that everything is correct. Then, the plugin change operation will start, and the cluster will be restarted. You can view the change progress in **Cluster Change Log**.

### Plugin Information

ES supports the following plugins:

| Plugin Name | Default Status | Description | Supported Operations |
---|---|---|---
analysis-icu | Not installed | Elasticsearch Unicode text analysis plugin | Installation, uninstallation
analysis-ik | Installed | Elasticsearch IK analysis plugin, which cannot be uninstalled by default | Dictionary update
analysis-kuromoji | Not installed | Elasticsearch Japanese analysis plugin | Installation, uninstallation
analysis-phonetic | |Uninstalled | Elasticsearch phonetic symbol analysis plugin | Installation, uninstallation
analysis-pinyin | Installed | Elasticsearch Pinyin analysis plugin | Installation, uninstallation
analysis-qq | Not installed | Elasticsearch QQ analysis plugin | Installation, uninstallation, dictionary update
analysis-smartcn | Not installed | Elasticsearch smart Chinese analysis plugin | Installation, uninstallation
analysis-stconvert| Installed | Elasticsearch Simplified and Traditional Chinese analysis plugin | Installation, uninstallation
ingest-attachment | Not installed | Apache Tika information extraction plugin | Installation, uninstallation
ingest-geoip | Not installed | IP address resolution plugin, which has already been integrated into ES 6.8.2 and above and does not need to be installed separately | Installation, uninstallation
ingest-user-agent | Not installed | Browser user agent information extraction plugin, which has already been integrated into ES 6.8.2 and above and does not need to be installed separately | Installation, uninstallation
mapper-murmur3 | Not installed | Plugin used to calculate and store field hash values during index creation | Installation, uninstallation
mapper-size | Not installed | Plugin used to record the size of documents before compression during index creation | Installation, uninstallation
repository-cos | Installed | [Plugin used to store Elasticsearch snapshots into COS](https://intl.cloud.tencent.com/document/product/845/19549), which cannot be uninstalled by default | None
repository-hdfs | Not installed | Plugin used to support Hadoop Distributed File System (HDFS) | Installation, uninstallation
sql | Not installed | Open-source SQL parsing plugin. It does not need to be installed in Basic Edition and Platinum Edition ES clusters as they have already incorporated the SQL parsing feature | Installation, uninstallation









