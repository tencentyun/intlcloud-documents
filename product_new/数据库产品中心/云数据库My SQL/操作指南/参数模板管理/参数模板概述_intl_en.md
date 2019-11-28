You can use a parameter template to manage how the parameters of a database engine are configured. A database parameter set is just like a container of engine configuration values which can be applied to one or more database instances.
Currently, a parameter template has the following features. You can log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb) and click **Parameter Template** on the left sidebar to view and modify parameters.
- A default parameter template can be set.
- New templates can be created. You can create custom parameter optimization schemes simply by slightly modifying the default parameters.
- Parameters can be imported from the `my.conf` MySQL configuration file to generate a template.
- Parameter configurations can be saved as templates.
- You can import the configuration from a template when configuring parameters for one or more instances.
>Database instances that use a database parameter template will not get all parameter updates in that template automatically. If you want to apply the new parameters to the instances in batches, you can import the updated template when setting parameters in batches.


![](https://main.qcloudimg.com/raw/f2f53de2288693a4630082c9bc4ef9dd.png)

