## Operation Scenarios
You can create a CMK in the KMS Console or by calling the CreateKey API. After successful creation, you can enable, disable, or rotate the CMK, implement permission control, or perform other operations. This document describes how to create a CMK in the console.


## Directions

1. Log in to the [KMS Console](https://console.cloud.tencent.com/kms2).
2. Select the region where you want to create a key and click **Create**.
![](https://main.qcloudimg.com/raw/838c5da28a939ea45cda7de11804142c.jpg)
3. Enter the following information in the pop-up box:
 - Key Name: This is required and must be unique within the region. It can contain letters, numbers, `_`, `-`, and cannot begin with "KMS-".
 - Description: This is optional and used to specify the type of data to be protected, or the application to be used in conjunction with the CMK.
 - Key Material Source: This is required. You can choose to generate the key in KMS or import your own key.
<img src="https://main.qcloudimg.com/raw/80e70ea8aeea96ba11656f429be0c24b.png" width="70%">
4. Click **OK** to go back to the key list, and then you can see the new key at the top of the list.



