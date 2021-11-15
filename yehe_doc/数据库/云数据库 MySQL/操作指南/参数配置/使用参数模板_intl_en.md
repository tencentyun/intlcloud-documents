Besides the system parameter templates provided by TencentDB for MySQL, you can create custom parameter templates to configure parameters in batches as needed.

You can use a parameter template to configure and manage the parameters of a database engine. A template is like a container of the values of database engine parameters, which can be applied to one or more TencentDB instances.
You can log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb) and click **Parameter Templates** on the left sidebar to create, view, and manage parameter templates which support the following features:
- Support default parameter templates.
- Create templates by modifying the default parameters to generate custom parameter optimization schemes.
- Import the MySQL configuration file `my.conf` to generate templates.
- Save parameter configurations as templates.
- Import parameters from templates to apply to one or more instances.
>!Instances that already use a parameter template won’t update their parameters when the parameter template updates, so you need to manually update the instance parameters in batches.
>To apply new parameters to a batch of instances, you can import a template that includes these parameters and apply the template to multiple instances.


## Creating a Parameter Template
You can create a parameter template, modify the parameter values, and apply the template to instances.
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/mysql/parameter-templates), select **Parameter Templates** on the left sidebar, and click **Create Template**.
![](https://main.qcloudimg.com/raw/bd2e7b2373beade127ddafbe46a7ba68.png)
2. In the pop-up dialog box, specify the following configurations, and click **Create and Set Parameters**.
 - **Template Name**: enter a unique template name.
 - **Database Version**: select a database version.
 - **Template Description**: enter a brief description of the parameter template.
![](https://main.qcloudimg.com/raw/a93abb9d05b05c0018c46d5efa027221.png)
3. After the creation is completed, you can modify, import, and export parameters on the template details page.

## Applying a Parameter Template to Instances
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/mysql/parameter-templates) and select **Parameter Templates** on the left sidebar.
2. In the parameter template list, locate the desired template and click **Apply to Instances** in the **Operation** column.
![](https://main.qcloudimg.com/raw/4598668de63c22bcbef5f7a20b262f02.png)
3. On the displayed page, specify the execution mode and instances, make sure that all parameter values are correct, and click **Submit**.
 - **Execution Mode**: **Immediate execution** is selected by default. If you select **During maintenance window**, the parameter modification task will be executed and take effect during the [instance maintenance period](https://intl.cloud.tencent.com/document/product/236/10929).
 - **MySQL Instance**: select one or more instances that need to apply the parameter template in the specified region.
 - **Parameter Comparison**: view the changed parameter values of the selected instance.
 >!Before applying a parameter template to multiple instances, please make sure the parameters can be applied to those instances.
 >
![](https://main.qcloudimg.com/raw/cdb5878b84b497bbea7d981cb4e9749d.png)
4. (Optional) If a parameter modification or batch modification task has been submitted but you want to cancel it, you can select **[Task List](https://console.cloud.tencent.com/mysql/task)** on the left sidebar in the console, locate the task, and click **Cancel** in the **Operation** column. You can cancel a task only before it is executed. The task state should be "Waiting for execution".
![](https://main.qcloudimg.com/raw/98b1462f86e0b274ab8380726c5ddc52.png)


## Copying a Parameter Template
To include most of the custom parameters and values of an existing parameter template in a new template, you can copy the existing template.

### Method 1. Copying an existing parameter template
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/mysql/parameter-templates), select **Parameter Templates** on the left sidebar, click the parameter template name or **View Details** in the **Operation** column in the template list, and enter the parameter template details page.
2. Select **More** > **Save as Template** at the top.
3. In the pop-up dialog box, specify the following configurations: 
  - **Template Name**: enter a unique template name.
  - **Template Description**: enter a brief description of the parameter template.
4. After confirming that everything is correct, click **Save**.

### Method 2. Saving parameters of an instance as a parameter template
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), select **Instance List** on the left sidebar, and click an instance ID/name in the instance list to access the instance management page.
2. Select **Database Management** > **Parameter Settings** and click **Save as Template**.
3. In the pop-up dialog box, specify the following configurations:
  - **Template Name**: enter a unique template name.
  - **Template Description**: enter a brief description of the parameter template.
4. After confirming that everything is correct, click **Create and Save**.


## Modifying Parameter Values in a Parameter Template
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/mysql/parameter-templates), select **Parameter Templates** on the left sidebar, click the parameter template name or **View Details** in the **Operation** column in the template list, and enter the parameter template details page.
2. Click **Batch Modify Parameters** or click <img src="https://main.qcloudimg.com/raw/788902e3f8c335cf17de420f7181c2a8.png"  style="margin:0;"> in the **Current Value** column to modify the parameter value.
>!If you click **Import Parameters**, you need to upload a local parameter configuration file. To avoid importing failures, the configuration file should be in the same format as the configuration file of the MySQL database server, or you can use the file template of the exported parameters.
>
![](https://main.qcloudimg.com/raw/d582cbb01aec5e7c6072fb2b04f74b45.png)

## Importing a Parameter Template
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/mysql/parameter-templates), select **Parameter Templates** on the left sidebar, click the parameter template name or **View Details** in the **Operation** column in the template list, and enter the parameter template details page.
2. Click **Import Parameters**.
>!If you click **Import Parameters**, you need to upload a local parameter configuration file. To avoid importing failures, the configuration file should be in the same format as the configuration file of the MySQL database server, or you can use the file template of the exported parameters.
>
3. In the pop-up dialog box, select a file to upload and click **Import and Overwrite Original Parameters**.

## Exporting a Parameter Template
#### Method 1
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/mysql/parameter-templates) and select **Parameter Templates** on the left sidebar.
2. In the parameter template list, locate the desired template and click **Export** in the **Operation** column.

#### Method 2
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/mysql/parameter-templates), select **Parameter Templates** on the left sidebar, click the parameter template name or **View Details** in the **Operation** column in the template list, and enter the parameter template details page.
2. Select **More** > **Export Parameters** at the top.

## Deleting a Parameter Template
If a parameter template is created redundantly or no longer needed, it can be easily deleted.
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/mysql/parameter-templates) and select **Parameter Templates** on the left sidebar.
2. In the parameter template list, locate the desired template and click **Delete** in the **Operation** column.
3. Click **OK** in the pop-up dialog box.


## See Also
For suggestions for configuration of key parameters, please see [Suggestions on Parameter Settings](https://intl.cloud.tencent.com/document/product/236/38056).
