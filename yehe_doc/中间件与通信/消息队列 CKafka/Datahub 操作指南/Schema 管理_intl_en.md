## Overview

DataHub offers the schema management feature. You can associate a created schema to a specific data access task to verify the format of the accessed data according to the schema.

## Directions

### Creating Schema

1. Log in to the [CKafka console](https://console.intl.cloud.tencent.com/ckafka).
2. Select **Schema Management** on the left sidebar, select the region, click **Create Schema**, and enter the schema name.
   ![](	https://qcloudimg.tencent-cloud.cn/raw/1dec3b1d34b51ab98957e59eb099e73f.png)
   - Schema Name: Enter the schema name. It can only contain letters, digits, underscores, or symbols ("-" and".").
   - Description: Enter the optional schema description.
   - Field Configuration: Add up to 100 fields.
     - Field Name: Enter the field name.
     - Type: Eight types are supported, namely, BOOLEAN, INT8, INT16, INT32, INT64, FLOAT32, FLOAT64, and STRING.
     - allowNull: Verify whether this field exists in the upstream. The value "true" indicates if this field doesn't exist in the upstream, the default value field you specify here will be automatically added instead.
> ?
>
> Detailed description of whether the field configuration is NULL:
>
> - true 
>   - The upstream field exists and meets the requirements: Write.
>   - The upstream field exists but doesn't meet the requirements: Do not write.
>   - The upstream field doesn't exist: Write the default value.
>
> - false  
>   - The upstream field exists and meets the requirements: Write.
>   - The upstream field exists but doesn't meet the requirements: Do not write.
>   - The upstream field doesn't exist: Do not write.
     - Description: Enter the field description.
3. Click **OK**.

### Deleting schema


On the schema management page, click **Delete** in the **Operation** column and confirm the deletion in the pop-up window.



### Associating task

After a schema is created, it can be associated with a specific data access task.

1. On the schema management list page, click the ID of the target schema to enter its basic information page.
2. Select the **Associated Task** tab at the top of the page, click **Associate Task**, and select the specific data access task.



### Disassociating task



1. On the schema management list page, click the ID of the target schema to enter its basic information page.
2. Select the **Associated Task** tab at the top of the page and click **Disassociate** in the **Operation** column of the target associated task.


> ?Once disassociated, the schema will no longer be used to verify data format.
