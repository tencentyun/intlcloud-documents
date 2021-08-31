## Creating Task Template
For more information on task template, please see "Task Template" in [Glossary](https://intl.cloud.tencent.com/document/product/599/10396). You can create a task template in the [BatchCompute Console](https://console.cloud.tencent.com/batch/task) in the following steps:
1. Log in to the [BatchCompute Console](https://console.cloud.tencent.com/batch/task). If you haven't activated the BatchCompute service, activate it as prompted on the BatchCompute Console page.
2. Select **Task Template** on the left sidebar and select the target region at the top of the page.
3. Click **Create** to enter the "Create Task Template" page and create a template as shown below:
![](https://main.qcloudimg.com/raw/1791e9f754b7529c487dc0f10eb4bb98.png)
Main parameters include:
 - **Compute Environment Type**:
	 - **Existing Compute Environment**: you can select an existing compute environment.
	 - **Automatic Compute Environment**: you don't need to pre-create a fixed compute environment. After a job is submitted, a CVM instance will be created automatically to run the task and terminated automatically after task completion.
   - 	**Resource Configuration**: you can click **Detailed CVM Configuration** for further customization. For more information, please see [CVM Product Documentation](https://intl.cloud.tencent.com/document/product/213).
   - **Number of Resources**: this determines the number of resources for concurrent task execution. For more information, please see "Task Instance" in [Glossary](https://intl.cloud.tencent.com/document/product/599/10396).
   - **Image**: for more information, please see "Image" in [Glossary](https://intl.cloud.tencent.com/document/product/599/10396).
4. Click **Next** to set the program configuration information as shown below:
![](https://main.qcloudimg.com/raw/423bf1b3ac0639169d9ba4ece661732f.png)
   - **Execution Method**: if "Package" is selected, "Package Address" is required, which is stored in [COS](https://intl.cloud.tencent.com/document/product/436).
   - **Package Address/Stdout Log/Stderr Log**: they should be in a fixed format. For more information, please see [How to Enter COS and CFS Paths](https://intl.cloud.tencent.com/document/product/599/13996).
5. Click **Next** to set the storage mapping as shown below:
![](https://main.qcloudimg.com/raw/dfcff0f1f896906316fd9227b105d54e.png)
   - **Input path mapping**: for Linux, [COS](https://intl.cloud.tencent.com/document/product/436) and [CFS](https://intl.cloud.tencent.com/document/product/582) are supported; for Windows, [CFS](https://intl.cloud.tencent.com/document/product/582) is supported. For the format requirements of COS and CFS paths, please see [How to Enter COS and CFS Paths](https://intl.cloud.tencent.com/document/product/599/13996). In addition, please note that the format of local paths vary by operating system.
   - **Output path mapping**: [COS](https://intl.cloud.tencent.com/document/product/436) is supported. For the format requirements of COS path, please see [How to Enter COS and CFS Paths](https://intl.cloud.tencent.com/document/product/599/13996).
6. Click **Next**. After confirming that the task template JSON file is correct, click **Save** to complete task template creation.
![](https://main.qcloudimg.com/raw/3aadaf52ef74160eb1cd7e92b401e4e6.png)

## Deleting Task Template
If you no longer need to use a task template, you can delete it on the "Task Template" list page.
![](https://main.qcloudimg.com/raw/cfcdac39a8b7abb42c4d442e3bf948ed.png)

## Modifying Task Template
If you need to edit an existing task template, you can click the task template ID on the "Task Template" list page to enter the task template configuration page and edit the configuration items as shown below:
![](https://main.qcloudimg.com/raw/bb50e54947c48a241faca8f2fb369fcc.png)
