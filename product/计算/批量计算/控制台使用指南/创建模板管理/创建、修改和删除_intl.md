### Creating a Task Template

For more information about task template, see "Task Template" in the [Glossary](). You can create a task temple in the [Batch Console]() through the following steps.
1. Log in to the [Batch Console](). If you have not activated Batch yet, follow on-screen prompts on the Batch Console homepage to activate it.

2. Click "Task template" in the left navigation bar, select the target region and click **Create**.
![](https://mc.qcloudimg.com/static/img/b6d89f6a4b4e0c8cc0469606948b8e41/image.jpg)

3. Configure basic information.
   - Resource configuration: You can click "Detailed CVM configuration" for further customization. For more information about configuration, see [CVM Product Documentation](https://intl.cloud.tencent.com/document/product/213).
   - Number of resources: This determines the number of resources for concurrent task execution. For more information, see "Task Instance" in the [Glossary](https://intl.cloud.tencent.com/document/product/599/10396).
   - Image: For more information, see "Image" in the [Glossary](https://intl.cloud.tencent.com/document/product/599/10396).
   ![](https://mc.qcloudimg.com/static/img/2e4c9a7879539ae70b907f669e4a8b78/image.jpg)

4. Configure application information.
   - Execution method: If "Package" is selected, you need to enter the "package address". The "package address" is stored in [COS](https://intl.cloud.tencent.com/document/product/436).
   - Package address/Stdout log/Stderr log: A fixed format is required. For more information, see [Entering COS or CFS Path]().
![](https://mc.qcloudimg.com/static/img/ed418b2351814d567c0beceb3183ec9d/image.jpg)

5. Configure the storage mapping.
   - Input path mapping: For Linux, [COS](https://intl.cloud.tencent.com/document/product/436) and [CFS](https://intl.cloud.tencent.com/document/product/582) are supported; for Windows, [CFS](https://intl.cloud.tencent.com/document/product/582) is supported. For the format requirements of COS and CFS paths, see [Entering COS or CFS Path](). In addition, the format of local paths vary for different operating systems.
   - Output path mapping: [COS](https://intl.cloud.tencent.com/document/product/436) is supported. For formats, see [Entering COS or CFS Path]().
   ![](https://mc.qcloudimg.com/static/img/b86945c2ee04dcb89d1ce9aa2a62955c/image.jpg)

6. After the task template JSON file is confirmed to be correct, click **Save** to complete task template creation.
![](https://mc.qcloudimg.com/static/img/779bfc1f07af787612d2fb1db5ce70d1/image.jpg)

## Deleting a Task Template
If you no longer need to use a task template, you can delete it in the task template list.
![](https://mc.qcloudimg.com/static/img/9d207da685ef89b75a93818851f5050f/image.jpg)

## Modifying a Task Template
To edit an existing task template, you can click the task template ID to enter the task template configuration page and edit the configuration items.
![](https://mc.qcloudimg.com/static/img/bab3f74591f80db4022716f897d57893/image.jpg)
