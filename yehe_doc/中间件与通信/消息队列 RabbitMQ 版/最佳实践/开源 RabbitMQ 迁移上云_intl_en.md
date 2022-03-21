## Overview
This document describes how to migrate metadata from open-source RabbitMQ to TDMQ for RabbitMQ.

## Prerequisite

Before the metadata import, you need to first export the metadata file from open-source RabbitMQ. For metadata file export instructions, see [Export open-source RabbitMQ metadata](#export).

## Directions

### Export open-source RabbitMQ metadata[](id:export)

#### Export metadata via the console

1. Open the browser and log in to the open-source RabbitMQ console.
2. On the **Overview** tab page, click **Export definitions**, and enter the filename for download. Select “All” or a specific vhost for the “Virtual host” field and click **Download broker definitions** on the right to export the metadata file of all vhosts or the specified vhost.
![](https://qcloudimg.tencent-cloud.cn/raw/5faa9f9ac376fe202882d5a090fd0c53.png)

#### Export metadata with the HTTP-based API of open-source RabbitMQ

1. Open the terminal.
2. Enter the command below to export the metadata file from open-source RabbitMQ.
	- Export the metadata of all vhosts:
	```plaintext
	wget http://<Open-source RabbitMQ IP address>:15672/api/definitions --user <Open-source RabbitMQ username>  --password <Open-source RabbitMQ password>  -O <Metadata file storage path>
	```
	- Export the metadata file of a specified vhost:
	```plaintext
	wget http://<Open-source RabbitMQ IP address>:15672/api/definitions/<Vhost name> --user <Open-source RabbitMQ username>  --password <Open-source RabbitMQ password>  -O <Metadata file storage path>
	```
>!If &lt;Vhost name&gt; contains a slash (/), replace the slash with “2%F”. For example, “/vhost” needs to be changed to “2%Fvhost”.

### Import the metadata to the TDMQ for RabbitMQ console

1. Log in to the [TDMQ for RabbitMQ console](https://console.cloud.tencent.com/tdmq/rabbit-cluster) and click **Migration to Cloud** on the left sidebar.
2. On the **Migration to Cloud** page, select a region and click **Create Task**.
![](https://qcloudimg.tencent-cloud.cn/raw/5f52006a9fcc1df81b0e822aae37d9fb.png)
3. On the task creation page, create a task to import the open-source RabbitMQ metadata and fill in the required fields.
<dx-tabs>
::: Cluster migration
![](https://qcloudimg.tencent-cloud.cn/raw/815bdd1d86c2d2dc585920987aa040f0.png)
:::
::: Vhost import
![](https://qcloudimg.tencent-cloud.cn/raw/e1afafb104c5e2ed26e6764a64beafdf.png)
:::
</dx-tabs>


Field description:

| Field       | Description                                                         |
| :--------- | :----------------------------------------------------------- |
| Task Type   | Select either “Cluster migration” or “Vhost import”. If you select the former, the metadata of all the open-source RabbitMQ vhosts will be imported. If you select the latter, the metadata of a single vhost will be imported. |
| Cluster       | Select a target cluster that is to be imported. You can select an existing cluster or create a new one.     |
| Vhost Name  | This field is required if the task type is “Vhost import”.              |
| Message TTL   | This field specifies the ACK timeout of an unconsumed message. If the task type is “Cluster migration”, the metadata of all vhosts will be imported, and the message TTL will be applied to all the imported vhosts. To modify this field, you can select a cluster on the **Cluster** page, click the **Vhost** tab, and click **Edit** in the **Operation** column. |
| Metadata File | Select and upload a metadata file exported from open-source RabbitMQ. The file content can be modified in the editing box. For more information on the file format, see [Metadata file format description](#format). |

4. Click **Create Task** to submit the migration-to-cloud task.
After that, the metadata file format will be automatically verified. Once the verification is passed, you will be redirected to the **Migration to Cloud** page to view the migration progress.

>!Only one migration task can be executed in a TDMQ for RabbitMQ cluster at a time, that is, a new task can be created only after the last task is finished.


### View migration task details

1. Select a region on the [Migration to Cloud]https://console.cloud.tencent.com/tdmq/rabbit-migrate page, and you can view the list of all migration tasks in this region.
![](https://qcloudimg.tencent-cloud.cn/raw/cddd79fa84d2f4beeb2ca08500e4feab.png)
2. The **Status** column displays the execution status of each migration task. Below are the status descriptions:

| Status     | Description                                                         |
| :------- | :----------------------------------------------------------- |
| Migrating   | The metadata file is being migrated.                                         |
| <nobr>Succeeded</nobr> | The metadata files of all vhosts have been successfully migrated.           |
| Failed | The metadata file of a single vhost failed to imported (for the “Vhost import” task type); or the metadata files of all vhosts failed to be imported (for the “Cluster migration” task type). |
| Some failed | The metadata files of some vhosts failed to be imported (for the “Cluster migration” task type).       |
| Timed out | The metadata file import timed out.                                       |

3. Click **View Details** in the **Operation** column to view the metadata file import details.
	 ![](https://qcloudimg.tencent-cloud.cn/raw/475a0e7aa59ff87b654a20c12a2b4d5c.png)

## Metadata import description

### Metadata file format description[](id:format)

| Task type                         | Cluster migration                                                     | Vhost  import                                                  |
| :------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| File format                         | json                                                         | json                                                         |
| Field requirement                         | The metadata file must contain the vhost list. Besides, the exchange, queue, and binding lists must contain the "vhost" field. |                                                              |
| Naming convention                         | The vhosts, exchanges, queues, and bindings must be named in compliance with the naming conventions in TDMQ for RabbitMQ. For details, see [Use Limits](https://intl.cloud.tencent.com/document/product/1112/43063) | The exchanges, queues, and bindings must be named in compliance with the naming conventions in TDMQ for RabbitMQ. For details, see [Use Limits](https://intl.cloud.tencent.com/document/product/1112/43063) |
| Export method of open-source RabbitMQ metadata file | On the **Overview** tab page in the RabbitMQ console, click **Export definitions** and select **All** for the **Virtual host** field to export the metadata of all vhosts. If you want to exclude some vhosts from the migration task, delete them in the vhost list before the cluster migration. | On the **Overview** tab page in the RabbitMQ console, click **Export definitions** and select a specific vhost for the **Virtual host** field to export its metadata. |

### Metadata compatibility description

The table below describes whether TDMQ for RabbitMQ is compatible with open-source RabbitMQ metadata:

| Metadata field        | Description                                                         | Compatible                                                       |
| :---------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| rabbitmq_version  | Cluster version of open-source RabbitMQ.                                     | No                                                           |
| users             | User information of open-source RabbitMQ.                                     | No                                                           |
| vhosts            | Vhost list in open-source RabbitMQ                                | Yes. However, the default open-source RabbitMQ vhost named “/” will be automatically renamed “\_\_default_vhost\_\_” according to the naming conventions in TDMQ for RabbitMQ. |
| permissions       | An open-source RabbitMQ user’s vhost management permissions.                            | No                                                           |
| parameters        | Runtime parameters of open-source RabbitMQ.                                       | No                                                           |
| global_parameters | Global parameters of open-source RabbitMQ.                                       | No                                                           |
| policies          | Optional parameters that open-source RabbitMQ sets for a vhost’s queues or exchanges, such as TTL and queue length limit. | No. If you want to use these optional parameters, you can go to the TDMQ for RabbitMQ console to edit them, or delete them and create new ones in the editing box on the **Create Migration Task** page. |
| queues            | Open-source RabbitMQ queues.                                         | Yes                                                           |
| exchanges         | Open-source RabbitMQ exchanges.                                    | Yes                                                           |
| bindings          | Open-source RabbitMQ bindings.                                     | Yes                                                           |

