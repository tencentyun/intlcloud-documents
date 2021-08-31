You need to create a stack when you use TIC for the first time. Stacks can also be created based on your business requirements.

## Prerequisites
Before creating a stack, you must [authorize TIC](https://intl.cloud.tencent.com/document/product/1043/36010#tic-.E6.8E.88.E6.9D.83) on the **Settings** page in the TIC console.

## Directions


1. Log in to the [TIC console](https://console.cloud.tencent.com/tic).
2. In the left sidebar, choose **Orchestration** -> **Stacks** to go to the **Stacks** page.
3. Click **New stack**. On the **New Stack** page, perform the following steps.

#### Step 1: Select Mode
1. **Provider**: the default value is **Tencent Cloud**. Currently, only **Tencent Cloud** is available.
2. **Region**: select a region where all resources in the stack will reside.
3. **Specify Template**: specify how you want to create the stack.
 - **URL**: only Tencent Cloud COS and GitHub are supported. Only one file can be obtained at a time.
 - **Private templates**: select a private template. For more information, see [Template Management](https://intl.cloud.tencent.com/document/product/1043/37185).
 - **Public templates**: select a public template. For more information, see [Template Management](https://intl.cloud.tencent.com/document/product/1043/37185).
 - **Enter template content**: enter infrastructure code. Multi-file compiling and common shortcuts (such as **Ctrl+S**, **Ctrl+Z**, and **Ctrl+X**) are supported.
![](https://main.qcloudimg.com/raw/8a4065e9bcf415073bbf4926eac6f068.png)
4. Click **Next** to go to Step 2.

#### Step 2: Configure Stack

1. Modify resource parameters in the template as needed. A stack draft named "draft-xxx" is automatically created on the backend to save your code.
2. Click **Next** to go to Step 3.
![](https://main.qcloudimg.com/raw/dde7ee93c999a2e0f55469acaead2709.png)

#### Step 3: Plan

TIC will verify the syntax, simulate a stack creation, and return the plan result. If the result meets you requirements, click **Next** to go to Step 4.
![](https://main.qcloudimg.com/raw/80377e5a281b18c6b4aff8f0004c37aa.png)

#### Step 4: Apply
1. Enter the stack name and description.
2. Click **Confirm**.
3. In the confirmation dialog box, click **Confirm**. TIC will then submit a creation request, and you will be redirected to the **Event** tab of the new stack.
