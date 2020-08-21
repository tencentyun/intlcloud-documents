### Elasticsearch Service July 2020 Release

This release incorporates the following features:

**1. Preset plugin list**

With this release, more than 10 open source and Tencent self-developed plugins are now supported, providing a rich set of features that can be installed/uninstalled as needed. For more information, please visit:
https://intl.cloud.tencent.com/document/product/845/37440

**2. Custom synonym dictionary**

You can now upload a synonym file to quickly configure a synonym dictionary. For more information, please visit: 
https://intl.cloud.tencent.com/document/product/845/36418

**3.Rolling and blue/green deployment options for cluster configuration adjustment**

If you choose a rolling update, nodes in the cluster are restarted one by one on a rolling basis. Service is not interrupted, but production environment access may be impacted during the process. If you choose a blue/green deployment process, new nodes matching the number of existing nodes are added to the original cluster, enabling you to switch to the new nodes seamlessly when the new configuration is completed without needing to restart the cluster. This process is smoother but is more time-consuming, making it suitable for cases that have a high requirement for the business availability. For more information, please visit:

https://intl.cloud.tencent.com/document/product/845/35713

**4.Cloud disk encryption in Beijing, Shanghai, and Guangzhou regions**

Cloud disk encryption effectively protects data privacy and meets security compliance requirements. There is no need for code adjustments and has almost no impact on service performance. Please note that this feature cannot be disabled once enabled, that is, an encrypted cloud disk cannot be converted to an unencrypted one.



Tencent Cloud ES Team

July 2020
