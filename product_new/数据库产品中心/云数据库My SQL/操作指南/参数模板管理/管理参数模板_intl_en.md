You can use a parameter template to manage how the parameters of a database engine are configured. A database parameter set is just like a container of engine configuration values which can be applied to one or more database instances.
The parameter template has the following features. You can log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb) and select **Parameter Templates** on the left sidebar to view and modify parameters:
- Specify the default parameter template.
- Create templates by modifying the default parameters to generate optimized custom parameter schemes.
- Generate templates by importing parameters from MySQL configuration file `my.conf`.
- Save parameter settings as templates.
- Import parameters from templates when setting parameters for one or multiple instances.
> All database instances that have applied a parameter template will not get all parameter updates of the template. If you want to apply new parameters to a batch of database instances, you can apply them by importing a template during batch parameter settings.

## Creating a Parameter Template
To use your own database parameter template, simply create a new one, modify the required parameters, and apply it to your database.
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb).
2. Select **Parameter Template** on the left sidebar.
![](https://main.qcloudimg.com/raw/ba2e21784ea990684ae8ed459057c28d.png)
3. Click **Create Template** and configure the following parameters in the pop-up dialog box:
 - **Template Name**: enter a unique template name.
 - **Database Version**: select the required database version.
 - **Template Description**: enter a brief description of the parameter template.
![](https://main.qcloudimg.com/raw/5851500ccdec4359b47709a28d3f6fac.png)
4. After confirming that everything is correct, click **Create and Set Parameters**.
5. After the creation is completed, you can modify, import, and export parameters on the template details page.

## Applying a Parameter Template to a Database
1. Select **[Instance List](https://console.cloud.tencent.com/cdb)** on the left sidebar and click an instance name to enter the management page.
2. Select **Manage Database** > **Parameter Settings** > **Import from Template**.
3. In the pop-up dialog box, select a parameter template and click **Import and Overwrite Original Parameters**.

## Copying a Parameter Template
If you have already created a database parameter template and want to include most of its custom parameters and values in the new template, simply copy the parameter template.

### Method 1. Copy an existing parameter template
1. Select **[Parameter Templates](https://console.cloud.tencent.com/mysql/param-templates)** on the left sidebar and click **View Details** in the "Operation" column of the template to be copied.
2. On the details page, click **Save as Template** at the top.
3. Configure the following parameters in the pop-up dialog box:
  - **Template Name**: enter a unique template name.
  - **Template Description**: enter a brief description of the parameter template.
4. After confirming that everything is correct, click **Save**.

### Method 2. Copy a parameter template using the instance parameter setting feature
1. Select **[Instance List](https://console.cloud.tencent.com/cdb)** on the left sidebar and click an instance name to enter the management page.
2. Select **Manage Database** > **Parameter Settings** > **Save as Template**.
3. Configure the following parameters in the pop-up dialog box:
  - **Template Name**: enter a unique template name.
  - **Template Description**: enter a brief description of the parameter template.
4. After confirming that everything is correct, click **Create and Save**.

## Deleting a Parameter Template
If a parameter template is created redundantly or no longer needed, it can be easily deleted.
1. Select **[Parameter Template](https://console.cloud.tencent.com/mysql/param-templates)** on the left sidebar.
2. In the parameter template list, select the template to be deleted and click **Delete** in the "Operation" column.
3. Click **OK** in the pop-up dialog box.

## Modifying a Parameter
After purchasing a TencentDB for MySQL instance, you can use its default parameter values, adjust such values based on your business needs, or modify the parameter configuration of its parameter template which then can be applied to other instances in the same business scenario.

### Method 1. Modify parameter values by using the parameter configuration feature
1. Select **[Instance List](https://console.cloud.tencent.com/cdb)** on the left sidebar and click an instance name to enter the management page.
2. Click **Parameter Settings** on the **Manage Database** tab.
3. On the parameter configuration page, click **Batch Modify Parameters** to modify parameters in batches. Then, click **Confirm Modifications**.
   Or, on the parameter configuration page, click the **Edit** icon next to the **Current Value** of a parameter to modify the specific parameter. Then, click the **Save** icon next to the value.

### Method 2. Modify parameter values in a new or existing parameter template
1. Select **[Parameter Template](https://console.cloud.tencent.com/mysql/param-templates)** on the left sidebar.
2. In the parameter template list, select the template to be modified and click **View Details** in the "Operation" column.
3. On the details page, click **Batch Modify Parameters** to modify parameters in batches. Then, click **Confirm Modifications**.
   Or, on the details page, click the **Edit** icon next to the **current parameter value** of a parameter to modify the specific parameter. Then, click the **Save** icon next to the value.

## Importing Parameters
You can use or modify the default parameter values provided by a TencentDB for MySQL instance or import existing parameter configuration in your business system. Please note that parameters not in the parameter setting list or parameter template list won't be imported.

### Method 1. Import parameters by using a parameter template
1. Select **[Parameter Template](https://console.cloud.tencent.com/mysql/param-templates)** on the left sidebar.
2. In the parameter template list, select the template to be modified and click **View Details** in the "Operation" column.
3. Click **Import Parameters** on the details page.
4. Click **Select File** in the pop-up dialog box.
5. When selecting the local parameter configuration file, please note that the file format should be the same as that used by the MySQL database server. You can also use the file template of the exported parameters; otherwise, the system will prompt for importing failure.
6. Click **Import and Overwrite Original Parameters**.

### Method 2. Import parameters by using the instance parameter setting feature
1. Select **[Instance List](https://console.cloud.tencent.com/cdb)** on the left sidebar and click an instance name to enter the management page.
2. Click **Parameter Settings** on the **Manage Database** tab.
3. Click **Import Parameters** on the parameter configuration page.
4. Click **Select File** in the pop-up dialog box.
5. When selecting the local parameter configuration file, please note that the file format should be the same as that used by the MySQL database server. You can also use the file template of the exported parameters; otherwise, the system will prompt for importing failure.
6. Click **Import and Overwrite Original Parameters**.
