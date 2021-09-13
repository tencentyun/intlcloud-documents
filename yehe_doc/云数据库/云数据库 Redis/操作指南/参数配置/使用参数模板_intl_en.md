Besides the system parameter templates provided by TencentDB for Redis, you can create custom parameter templates to configure parameters in batches as needed.

You can use a parameter template to configure and manage the parameters of a database engine. A template is like a container of the values of database engine parameters, which can be applied to one or more TencentDB instances.

Parameter templates support the following features:
- Support the default parameter templates.
- Create custom templates by modifying the default parameters.
- Save parameter configurations as templates.
- Import parameters from templates to apply to one or more instances.
>!
>- Instances that already use a parameter template won’t update their parameters when the parameter template updates, so you need to manually update the instance parameters in batches.
>- To apply new parameters to a batch of instances, you can import a template that includes these parameters and apply the template to multiple instances.

## Creating a Parameter Template
You can create a parameter template, modify the parameter values, and apply the template to instances.

1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), select **Parameter Templates** on the left sidebar, and click **Create Template**.
2. In the pop-up dialog box, specify the following configurations, and click **Create and Set Parameters**.
 - **Template Name**: enter a unique template name.
 - **Database Version**: select a database version.
 - **Template Description**: enter a brief description of the parameter template.
3. After it is created, you can modify it on the template details page.

## Applying a Parameter Template to Instances
### Applying to existing instances
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis) and select **Parameter Templates** on the left sidebar.
2. In the parameter template list, locate the desired template, and click **Apply to Instance** in the **Operation** column. Or, click **View Details**, enter the template details page, and click **Apply to Instance**.
3. On the displayed page, specify the execution mode and instances, make sure that all parameter values are correct, and click **Submit**.
 - **Redis Instance**: select one or more instances that need to apply the parameter template in the specified region.
 - **Parameter Comparison**: view the changed parameter values of the selected instance.
>!Before applying a parameter template to multiple instances, please make sure that the instances do support those parameters.
>

### Applying to new instances
On the [instance purchase page](https://Intl.buy.cloud.tencent.com/redis), select a default or custom parameter template for the new instances.

## Copying a Parameter Template
To include most of the custom parameters and values of an existing parameter template in a new template, you can copy the existing template and modify it.

### Method 1. Copying an existing parameter template
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), select **Parameter Templates** on the left sidebar, click the parameter template name or **View Details** in the **Operation** column in the template list, and enter the parameter template details page.
2. Click **Save as Template**.
3. In the pop-up dialog box, specify the following configurations: 
  - **Template Name**: enter a unique template name.
  - **Template Description**: enter a brief description of the parameter template.
4. After confirming that everything is correct, click **Save**.

### Method 2. Saving parameters of an instance as a parameter template
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), select **Instance List** on the left sidebar, click an instance ID, and enter the instance management page.
2. On the **Parameter Settings** tab, click **Save as Template**.
3. In the pop-up dialog box, specify the following configurations: 
 - **Template Name**: enter a unique template name.
 - **Template Description**: enter a brief description of the parameter template.
4. After confirming that everything is correct, click **Create and Save**.

## Modifying Parameter Values in a Parameter Template
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), select **Parameter Templates** on the left sidebar, click the parameter template name or **View Details** in the **Operation** column in the template list, and enter the parameter template details page.
2. Click **Batch Modify Parameters** or <img src="https://main.qcloudimg.com/raw/788902e3f8c335cf17de420f7181c2a8.png"  style="margin:0;"> in the **Current Value** column to modify parameter values.

## Deleting a Parameter Template
If a parameter template is created redundantly or no longer needed, it can be easily deleted.
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis) and select **Parameter Templates** on the left sidebar.
2. In the parameter template list, locate the desired template and click **Delete** in the **Operation** column.
3. Click **OK** in the pop-up dialog box.

