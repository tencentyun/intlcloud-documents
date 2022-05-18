
## Quick Start
This document guides you through the console steps to submit a job, render objects with 3ds Max 2018, and export the rendered objects. 

### Step 1. Create a custom image
1. Create a custom image. See [Windows Custom Image](https://intl.cloud.tencent.com/document/product/599/13035) 
2. Install 3ds Max 2018. See [Official Homepage](https://www.autodesk.com/products/3ds-max/overview) 
>- Disable the Windows Firewall temporarily to avoid blocking software downloads.
>- Select an appropriate graphics card model by referring to the [Graphics Card Selection Guide](https://knowledge.autodesk.com/zh-hans/support/3ds-max/learn-explore/caas/CloudHelp/cloudhelp/2015/CHS/3DSMax/files/GUID-3D6B4C8E-8C0D-4A9C-BFB0-2463803268CE-htm.html) to avoid graphics card initialization failures. Nitrous Software is recommended for general usage.

### Step 2. Prepare files to render
You can choose to store the files to render on [COS](https://intl.cloud.tencent.com/zh/document/product/436) or [CFS](https://intl.cloud.tencent.com/zh/document/product/582). Complete the mounting configuration. BatchCompute will mounts the COS or CFS path to the local machine before the rendering job runs, which allows the rendering software to access files stored on COS or CFS as local files.

- COS is recommended for small-sized objects. See [Uploading Objects](https://intl.cloud.tencent.com/document/product/436/13321).
- CFS is recommended for large-sized objects.

### Step 3. Create a task template
1. Log in to the BatchCompute console and choose **[Task Template](https://console.cloud.tencent.com/batch/task)** on the left sidebar.
2. Select the target region at the top on the **Task Template** page and click **Create**.
3. Click **Create**, complete the configurations in the **New Task Template** page.
![](https://main.qcloudimg.com/raw/0a6bff4423320bb7318225f13a56a24e.png)
 - **Name**: enter a custom name for the template. “rendering” is used here as an example.
 - **Description**: enter the description of the template. “3ds Max 2018 Demo” is used here as an example.
 - **Compute Environment**: Select as needed. **Auto** is selected in this example.
 - **Specification**: choose as needed
 - **Image**: enter the ID of image used to create the compute environment.
 - **Instance Quantity**: number of instances to launch
 - **Timeout period**, **Retry attempts**: Keep the default values.
3. Click **Next** and configure application information, as shown below: 
![](https://main.qcloudimg.com/raw/15650e325d5507a0302896e44de45f7f.png)
 - **Execution method**: Package.
 - **Package address**: enter the Take the COS as example, `cos://barrygz-1251783334.cos.ap-guangzhou.myqcloud.com/render/max.tar.gz`
 - **Stdout log**: see [Entering COS & CFS Paths](https://intl.cloud.tencent.com/document/product/599/13996)
 - **Stderr log**: See above
 - **Command line**: `3dsmaxcmd Demo.max -outputName:c:\\render\\image.jpg`.
4. Click **Next** to configure storage mapping, as shown below:
![](https://main.qcloudimg.com/raw/a7d312aa78f460b30ed67d1758b395ba.png)
 - **Output path mapping - Local path**: `C:\\render\\`.
 - **Output path mapping - COS/CFS path**: See [Entering COS & CFS Paths](https://intl.cloud.tencent.com/document/product/599/13996)
5. Click **Next** to preview the JSON file of the task.
6. Confirm that the configuration is correct and click **Save**.

### Step 4. Submit a job
1. Click **Job** on the left sidebar to enter the **Jobs* page.
2. Select a target region at the top on the page and click **Create**.
3. Configure the basic job information in the **New Job** window, as shown below:
![](https://main.qcloudimg.com/raw/95ad2a781a05eb5306a6afadc4096565.png)
 - **Job name**: enter a custom name. “max” is used here for example.
 - **Priority**: keep as default.
 - **Description**: enter the description of the job. “3ds Max 2018 Demo” is used here as an example.
3. Open the **Task flow** page, locate the task **rendering** from the left and drag it to the canvas.
![](https://main.qcloudimg.com/raw/6465facbf8bcac90153b4a055d78c4a1.png)
4. Open **Task Details** on the right, check the configuration, and click **Complete**.
5. To query job running information, please see [Querying Information](https://intl.cloud.tencent.com/document/product/599/14567)
6. See below for the demonstration of rendering.
![](https://main.qcloudimg.com/raw/940a3048a62c3db4379ff18b5219832e.jpg)
7. Query the rendering results. See **Viewing Object Information**


## Subsequent Operations
This document illustrates a simple rendering job to demonstrate fundamental BatchCompute capabilities. You can try the advanced capabilities of BatchCompute as instructed in the Console User Guide.
- **Various CVM configurations**: BatchCompute provides a variety of CVM configuration options. You can customize your own CVM configuration based on your business scenario.
- **Remote storage mapping**: Batch Compute optimizes storage access and simplifies access to remote storage services into operations in the local file system.
- **Concurrent multi-object rendering**: You can launch multiple instances to read and render different objects at the same time. The instances are distinguished by [environment variables](https://intl.cloud.tencent.com/document/product/599/11752).
