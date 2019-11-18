You can use a parameter template to manage how the parameters of a database engine are configured. A database parameter set is just like a container of engine configuration values which can be applied to one or more database instances.

## Creating a Parameter Template
To use your own database parameter template, simply create a new one, modify the required parameters, and apply it to your database.
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb).
2. Select **Parameter Template** on the left sidebar.
 ![](https://main.qcloudimg.com/raw/ba2e21784ea990684ae8ed459057c28d.png)
3. Click **Create Template** and configure the following parameters in the pop-up dialog box:
 - **Template Name**: Enter a unique template name.
 - **Template Description**: Enter a brief description of the parameter template.
 - **DB Version**: Select the required database version.
![](https://main.qcloudimg.com/raw/5851500ccdec4359b47709a28d3f6fac.png)
4. After confirming that everything is correct, click **Create and Set Parameters**.

## Copying a Parameter Template
If you have already created a database parameter template and want to include most of its custom parameters and values in the new template, simply copy the parameter template.

### Copying an Existing Parameter Template
1. In the parameter template list, click **Modify** in the "Action" column of the template to be copied.
2. Click **Save as Template** at the top right.
3. Configure the following parameters in the pop-up dialog box:
  - **Template Name**: Enter a unique template name.
  - **Template Description**: Enter a brief description of the parameter template.
4. After confirming that everything is correct, click **Create and Save**.

### Copying a Parameter Template Using the Instance Parameter Configuration Feature
1. Select **Instance List** on the left sidebar and click an instance name to enter the management page.
2. Select **Database Management** > **Parameter Settings** > **Save as Template**.
3. Configure the following parameters in the pop-up dialog box:
  - **Template Name**: Enter a unique template name.
  - **Template Description**: Enter a brief description of the parameter template.
![](https://main.qcloudimg.com/raw/674773f75e45bee43bdb9bbc6e043927.png)
4. After confirming that everything is correct, click **Create and Save**.

## Deleting a Parameter Template
If a parameter template is created redundantly or no longer needed, it can be easily deleted.
1. Select **Parameter Template** on the left sidebar.
2. In the parameter template list, select the template to be deleted and click **Delete** in the "Operation" column.
3. Click **Delete** in the pop-up dialog box.

## Modifying a Parameter
After purchasing a TencentDB for MySQL instance, you can use its default parameter values, adjust such values based on your business needs, or modify the parameter configuration of its parameter template which then can be applied to other instances in the same business scenario.

### Modifying Parameter Values Using the Parameter Configuration Feature
1. Select **Instance List** on the left sidebar and click an instance name to enter the management page.
2. Click **Parameter Settings** on the **Database Management** tab.
3. On the parameter configuration page, click **Modify Parameters** to modify parameters in batches. Then, click **Confirm Modification**.
   Or, on the parameter configuration page, click the **Edit** icon next to the **Current Value** of a parameter to modify the specific parameter. Then, click the **Save** icon next to the value.

### Modifying Parameter Values in a New or Existing Parameter Template
1. Select **Parameter Template** on the left sidebar.
2. In the parameter template list, select the template to be modified and click **Modify** in the "Operation" column.
3. On the parameter viewing and modifying page, click **Modify Parameters** to modify parameters in batches. Then, click **Confirm Modification**.
   Or, on the parameter viewing and modifying page, click the **Edit** icon next to the **Current Value** of a parameter to modify the specific parameter. Then, click the **Save** icon next to the value.

## Importing Parameters
You can use or modify the default parameter values provided by a TencentDB for MySQL instance or import existing parameter configuration in your business system. Please note that parameters not in the parameter setting list or parameter template list won't be imported.

## Importing Parameters to Parameter Configuration
1. Select **Instance List** on the left sidebar and click an instance name to enter the management page.
2. Click **Parameter Settings** on the **Database Management** tab.
3. Click **Import Parameters** on the parameter configuration page.
4. Click **Select File** in the pop-up dialog box.
![](https://main.qcloudimg.com/raw/db3a614f69be5517657aa5a86aaaefa4.png)
5. When selecting the local parameter configuration file, please note that the file format should be the same as that used by the MySQL database server. You can also use the file template of the exported parameters; otherwise, the system will prompt for importing failure.
6. Click **Import and Overwrite Original Parameters**.

### Importing Parameters to a Parameter Template
1. Select **Parameter Template** on the left sidebar.
2. In the parameter template list, select the template to be modified and click **Modify** in the "Operation" column.
3. Click **Import Parameters** on the viewing and modifying page.
4. Click **Select File** in the pop-up dialog box.
![](https://main.qcloudimg.com/raw/db3a614f69be5517657aa5a86aaaefa4.png)
5. When selecting the local parameter configuration file, please note that the file format should be the same as that used by the MySQL database server. You can also use the file template of the exported parameters; otherwise, the system will prompt for importing failure.
6. Click **Import and Overwrite Original Parameters**.
