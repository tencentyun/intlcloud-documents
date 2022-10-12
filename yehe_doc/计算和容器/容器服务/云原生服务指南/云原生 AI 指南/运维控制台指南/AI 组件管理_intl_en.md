## Overview 

After creating an AI environment, you can combine AI add-ons as needed to set up an AI platform. This document describes how to add, delete, modify, and query AI add-ons.
>!The underlying layer of AI add-ons is implemented based on [Helm Chart](https://helm.sh). After you create an AI environment, we recommend you not manage AI add-ons on the relevant page in the application marketplace. Instead, directly manage them **in the AI environment**, so as to avoid data inconsistency.
>
## List of AI Add-Ons

| Add-On | Use Case | Description |
|---------|---------|---------|
| [TF Operator](https://intl.cloud.tencent.com/document/product/457/49365) | Model training | After installing it, you can run TF standalone/distributed training jobs. |
| [MPI Operator](https://intl.cloud.tencent.com/document/product/457/49366) | Elastic training | You can run elastic training jobs to fully utilize the computing resources.  |
| [Fluid](https://intl.cloud.tencent.com/document/product/457/47667) | Cache acceleration | Fluid provides data prefetch and acceleration for cloud applications by using a distributed cache engine (GooseFS/Alluxio) with data observability, portability, and horizontal scalability.  |
| [Elastic Jupyter Operator](https://intl.cloud.tencent.com/document/product/457/49367) | Algorithm debugging | Elastic Jupyter Operator provides an on-demand elastic Jupyter Notebook service to assign computing resources as needed.  |

## AI Add-On Lifecycle Management
### Creating an AI add-on
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cloud Native AI** on the left sidebar.
2. On the **AI Environment** list page, click the ID of the target AI environment to enter its **Basic Information** page.
3. On the left sidebar, click **Add-On Management**.
4. Click **Create** to enter the **Create AI Add-On** page and set the parameters.
	The main parameters are described as follows:
	- Add-On Name: Custom add-on name.
	- Namespace: The namespace for installing the add-on.
	- Chart: The installation package of the add-on. Only one add-on can be installed at a time.
	- Parameter: Add-on configuration parameters. After the add-on is created, you can still update its parameters as instructed in "Updating an AI add-on".
5. Click **Done**.

### Viewing an AI add-on

After creating an AI environment, you can view the list of installed AI add-ons in the AI environment.


### Deleting an AI add-on

1. Select the ID of an AI environment to enter its **Basic Information** page.
2. On the left sidebar, click **Add-On Management**.
3. Select **Delete** on the right of the target add-on.
4. In the **Delete Add-On** pop-up window, read the notes on deletion and click **Confirm**.


### Updating an AI add-on

1. Select the ID of an AI environment to enter its **Basic Information** page.
2. On the left sidebar, click **Add-On Management**.
3. Select **Update configuration** on the right of the target add-on.
4. On the **Update Add-On** pop-up page, configure add-on parameters as needed and click **Done**.











