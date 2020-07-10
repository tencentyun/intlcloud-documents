
## Quick Start
This document describes how to submit a job in the BatchCompute Console to render and export a 3ds Max 2018 image.

### Step 1. Make a custom image
1. Create a custom image.
2. Install 3ds Max 2018 as instructed by the [official website](https://www.autodesk.com/products/3ds-max/overview).
>
>- Please temporarily disable the Windows Firewall to avoid blocking software downloads.
> For more information on how to select an appropriate graphics card type to avoid graphics card initialization failure, please see [Display Driver Selection Dialog](https://knowledge.autodesk.com/zh-hans/support/3ds-max/learn-explore/caas/CloudHelp/cloudhelp/2015/CHS/3DSMax/files/GUID-3D6B4C8E-8C0D-4A9C-BFB0-2463803268CE-htm.html). In normal circumstances, you are recommended to select "Nitrous Software".

### Step 2. Prepare the rendering files
There are two mainstream ways to store the rendering materials: [Cloud Object Storage (COS)](https://intl.cloud.tencent.com/document/product/436) and [Cloud File Storage (CFS)](https://intl.cloud.tencent.com/document/product/582). By configuring the mount parameters, BatchCompute will mount COS or CFS to the local storage before the rendering job runs, so the renderer can access COS or CFS as if it were a local file.

- If the rendering materials are small, you are recommended to compress them into a gzip package and upload the package to COS. For more information, please see [Uploading Object](https://intl.cloud.tencent.com/document/product/436/13321).
- If the rendering materials are large, you are recommended to store them in CFS.

### Step 3. Create a task template
1. Log in to the BatchCompute Console and select **[Task Template](https://console.cloud.tencent.com/batch/task)** on the left sidebar.
2. Select the target region at the top on the "Task Template" page and click **Create**.
3. Click **Create** to enter the "Create Task Template" page and create a template as shown below:
![](https://main.qcloudimg.com/raw/ebfa42f6ffda0420c78e902fbe420134.png)
  * **Name**: custom name, such as `rendering`.
  * **Description**: custom description, such as `3ds Max 2018 Demo`.
  * **Compute Environment Type**: select as needed. **Automatic Compute Environment** is selected in this example.
  * **Resource Configuration**: S1.LARGE8 (4-core 8 GB).
  * **Image**: custom image ID. Please select one as needed.
  * **Number of Resources**: number of concurrent renderings, such as 1
  * **Timeout Period and Number of Retries**: keep the default values.
3. Click **Next** to configure the program information as shown below:
![](https://main.qcloudimg.com/raw/15650e325d5507a0302896e44de45f7f.png)
  * **Execution Method**: PACKAGE.
  * **Package Address**: COS as an example, `cos://barrygz-1251783334.cos.ap-guangzhou.myqcloud.com/render/max.tar.gz`.
  * **Stdout Log**: for more information on the format, please see [How to Enter COS and CFS Paths](https://intl.cloud.tencent.com/document/product/599/13996).
  * **Stderr Log**: same as Stdout log.
  * **Command Line**: `3dsmaxcmd Demo.max -outputName:c:\\render\\image.jpg`.
4. Click **Next** to set the storage mapping as shown below:
![](https://main.qcloudimg.com/raw/a7d312aa78f460b30ed67d1758b395ba.png)
  * **Output path mapping - local path**: `C:\\render\\`.
  * **Output path mapping - COS or CFS path**: for formats, please see [Entering COS or CFS Path](https://intl.cloud.tencent.com/document/product/599/13996).
5. Click **Next** to preview the task's JSON file.
6. After confirming that everything is correct, click **Save**.

### Step 4. Submit a job
1. Click **Job** on the left sidebar to enter the "Job" list page.
2. Select the target region at the top of the page and click **Create**.
3. In the "Create Job" window, configure basic information of the job as shown below:
  ![](https://main.qcloudimg.com/raw/95ad2a781a05eb5306a6afadc4096565.png)
  * **Job Name**: `max`.
  * **Priority**: default value.
  * **Description**: `3ds Max 2018 Demo`.
3. Select the **rendering** task on the left on the task flow page and drag the task to the canvas on the right.
![](https://main.qcloudimg.com/raw/6465facbf8bcac90153b4a055d78c4a1.png)
4. Enable **Task Details** on the right on the task flow page, confirm that the configuration is correct, and click **Complete**.
5. Query the job running information. For more information, please see [Querying Information](https://intl.cloud.tencent.com/document/product/599/14567).
6. Below is the rendering process demonstration.
![](https://main.qcloudimg.com/raw/940a3048a62c3db4379ff18b5219832e.jpg)
7. Query the rendering result. For more information, please see [Viewing Object Information](https://intl.cloud.tencent.com/document/product/436/13326).


## Subsequent Operations
This document illustrates a simple single-instance rendering job to show the most basic capabilities of BatchCompute. You can continue to test the advanced capabilities of BatchCompute as instructed in the Console User Guide.
- **Various CVM configurations**: BatchCompute provides a variety of CVM configuration options. You can customize your own CVM configuration based on your business scenario.
- **Remote storage mapping**: BatchCompute optimizes storage access and simplifies access to remote storage services into operations in the local file system.
- **Concurrent multi-image rendering**: BatchCompute supports specifying the number of concurrent rendering instances which are distinguished between through [environment variables](https://intl.cloud.tencent.com/document/product/599/11752) with each instance reading a different material for concurrent rendering.
