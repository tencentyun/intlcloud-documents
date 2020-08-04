You need to create a stack when you use TIC for the first time. Stacks can also be created based on your business requirements.

## Prerequisites
Before creating a stack, you must [authorize TIC](https://intl.cloud.tencent.com/document/product/1043/36010#tic-.E6.8E.88.E6.9D.83) on the **Settings** page in the TIC console.

## Directions


1. Log in to the [TIC console](https://console.cloud.tencent.com/tic).
2. In the left sidebar, choose **Orchestration** -> **Stacks** to go to the **Stacks** page.
3. Click **New**. On the **New Stack** page that appears, perform the following steps.

#### Step 1: Select Mode
1. Select a provider from the **Provider** drop-down list. The default value is **Tencent Cloud**. Currently, only **Tencent Cloud** is available.
2. Select a region where resources in the stack belong from the **Region** drop-down list.
3. In the **Specify Template** area, specify how you want to create the stack.
 - **URL**: only Tencent Cloud COS and GitHub are supported. Only 1 file can be obtained at a time.
 - **Private templates**: select a private template. For more information, see [Template Management](https://intl.cloud.tencent.com/document/product/1043/37185).
 - **Public templates**: select a public template. For more information, see [Template Management](https://intl.cloud.tencent.com/document/product/1043/37185).
 - **Enter template content**: enter infrastructure code. Multi-file compiling and common shortcuts (such as **Ctrl+S**, **Ctrl+Z**, and **Ctrl+X**) are supported.
![](https://main.qcloudimg.com/raw/c0efc0cbff42503ab674d6834ed6aa93.png)
4. Click **Next** to go to Step 2.

#### Step 2: Configure Stack

1. Modify resource parameters in the template as needed. A stack draft named "draft-xxx" is automatically created on the backend to save your code.
2. Click **Next** to go to Step 3.
![](https://main.qcloudimg.com/raw/ee91a68e03ec880627ff61091e582a1e.png)

#### Step 3: Plan

TIC checks the syntax, simulates a stack creation, and returns the plan results. If the plan results are as expected, click **Next** to go to Step 4.
![](https://main.qcloudimg.com/raw/34817ae5fdd594182480290a65607b47.png)

#### Step 4: Apply
1. Enter the stack name and description.
2. Click **Confirm**.
3. In the confirmation dialog box, click **Confirm**. Then, TIC submits a creation request and you are redirected to the **Event** tab of the new stack.
