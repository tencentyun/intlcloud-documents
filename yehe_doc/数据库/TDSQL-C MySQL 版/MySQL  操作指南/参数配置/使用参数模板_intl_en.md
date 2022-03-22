In addition to the various system parameter templates provided by TDSQL-C for MySQL, you can also create custom parameter templates to configure parameters in batches as needed.

You can use a parameter template to configure and manage the parameters of a database engine. A template is like a container of the values of database engine parameters, which can be applied to one or more database instances.
You can log in to the [TDSQL-C console](https://console.cloud.tencent.com/cynosdb) and click **Parameter Template** on the left sidebar to view parameters. The following parameter template features are supported:

- Use system default parameter templates, including high-performance and high-stability parameter templates.
- Create custom templates by modifying a default parameter template.
- Generate templates by importing parameters from configuration file `my.conf`.
- Save parameter configurations as templates.
- Import parameters from templates to apply to one or more instances.
- Compare two parameter templates.

>!
>- If the parameters in the template are updated, the instance parameters are not updated unless they are manually re-applied to the instances.
>- You can apply the parameter changes to single or multiple instances by importing a template.

## Creating Parameter Template
You can create a parameter template, modify the parameter values, and apply the template to instances.

1. Log in to the [TDSQL-C console](https://console.cloud.tencent.com/cynosdb), select **Parameter Template** on the left sidebar, and click **Create Template**.
![](https://qcloudimg.tencent-cloud.cn/raw/73fdf6f7bebd3d2fa1b8571fec24f667.png)
2. In the pop-up window, configure the following parameters and click **OK**:
  - **Template Name**: enter a unique template name.
  - **Template Description**: enter a brief description of the parameter template.
  - **Database Version**: select a database version.
3. After the creation is completed, you can modify, import, and export parameters on the template details page.

## Copying Parameter Template
To include most of the custom parameters and values of an existing parameter template in a new template, you can copy the existing template.

### Method 1. Copying an existing parameter template
1. Log in to the [TDSQL-C console](https://console.cloud.tencent.com/cynosdb), select **Parameter Template** on the left sidebar, and click **View/Modify** in the **Operation** column of a template to enter the template details page.
2. Click **Save as Template** at the top of the template details page.
3. In the pop-up window, specify the following configurations:
  - **Template Name**: enter a unique template name.
  - **Template Description**: enter a brief description of the parameter template.
4. After confirming that everything is correct, click **Save**.

### Method 2. Saving parameters of an instance as a parameter template
1. Log in to the [TDSQL-C console](https://console.cloud.tencent.com/cynosdb) and click a cluster ID in the cluster list to enter the cluster management page.
2. On the cluster management page, select the **Parameter Settings** tab and click **Save as Template**.
3. In the pop-up window, specify the following configurations:
  - **Template Name**: enter a unique template name.
  - **Template Description**: enter a brief description of the parameter template.
4. After confirming that everything is correct, click **Save**.

## Modifying Parameter Values in Parameter Template
1. Log in to the [TDSQL-C console](https://console.cloud.tencent.com/cynosdb), select **Parameter Template** on the left sidebar, and click **View/Modify** in the **Operation** column of a template to enter the template details page.
2. Click **Modify Parameters** or <img src="https://main.qcloudimg.com/raw/788902e3f8c335cf17de420f7181c2a8.png"  style="margin:0;"> in the **Current Value** column to modify parameter values.
>!If you click **Import Parameters**, you need to upload a local parameter configuration file. To avoid importing failures, the configuration file should be in the same format as the configuration file of the MySQL database server, or you can use the file template of the exported parameters.
>

## Importing Parameter Template
1. Log in to the [TDSQL-C console](https://console.cloud.tencent.com/cynosdb), select **Parameter Template** on the left sidebar, and click **View/Modify** in the **Operation** column of a template to enter the template details page.
2. On the template details page, click **Import Parameters**.
>!If you click **Import Parameters**, you need to upload a local parameter configuration file. To avoid importing failures, the configuration file should be in the same format as the configuration file of the MySQL database server, or you can use the file template of the exported parameters.
>
3. In the pop-up window, select a file and click **Import and Overwrite Original Parameters**.

## Exporting Parameter Template
#### Method 1
1. Log in to the [TDSQL-C console](https://console.cloud.tencent.com/cynosdb) and select **Parameter Template** on the left sidebar.
2. In the parameter template list, locate the target template and click **Export** in the **Operation** column.

#### Method 2
1. Log in to the [TDSQL-C console](https://console.cloud.tencent.com/cynosdb), select **Parameter Template** on the left sidebar, and click **View/Modify** in the **Operation** column of a template to enter the template details page.
2. Click **Export Parameters** at the top of the template details page.

## Deleting Parameter Template
If a parameter template is created redundantly or no longer needed, it can be easily deleted.
1. Log in to the [TDSQL-C console](https://console.cloud.tencent.com/cynosdb) and select **Parameter Template** on the left sidebar.
2. In the parameter template list, locate the target template and click **Delete** in the **Operation** column.
3. In the pop-up window, click **OK**.

## Subsequent Operations
For suggestions for configuration of key parameters, see [Suggestions on Parameter Settings](https://intl.cloud.tencent.com/document/product/1098/44600).

