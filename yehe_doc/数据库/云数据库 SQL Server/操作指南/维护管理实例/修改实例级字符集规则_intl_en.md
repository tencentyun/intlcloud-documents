TencentDB for SQL Server allows you to modify the instance-level character set collation when creating an instance. This operation can be performed only on the purchase page. The character set of an instance provides a collation for system data, i.e., the case sensitivity and accent sensitivity attributes. Selecting a collation for your database will affect the results of relevant database operations.

This document describes how to modify the character set collation.
>!
>- **As modifying the instance-level character set collation requires separately configuring physical machine resources**, [submit a ticket](https://console.cloud.tencent.com/workorder/category) and specify the desired character set collation before purchase.
>- If you have modified the character set collation for your instance, and a subsequent **scale-out involves data migration**, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
>- The default collation of instance character sets is Chinese_PRC_CI_AS.

## Prerequisites
You have [submitted a ticket](https://console.cloud.tencent.com/workorder/category) to apply for changing the collation of character sets.

## Directions
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver#/).
2. In the instance list, click **Create Database Instance**.
3. On the instance purchase page, set the **Character Set Collation** under the **System Time Zone** parameter.
![](https://qcloudimg.tencent-cloud.cn/raw/380eaefaa279fba8246359816c1e04e3.png)
4. For more information on how to configure other parameters on the purchase page, see [Creating TencentDB for SQL Server Instance](https://www.tencentcloud.com/document/product/238/31571). After setting all the parameters, click **Buy Now**.
5. You can query the configured character set collation under **Basic Info** on the **Instance Details** tab.
![](https://qcloudimg.tencent-cloud.cn/raw/1e07ab15b0fc8896280c03e7ff92f912.png)

## Collation description

| Collation Option | Description | 
|---------|---------|
| _CS | Case-sensitive. This option indicates that lowercase letters will precede their corresponding uppercase letters during sorting. | 
| _CI | Case-insensitive. This option indicates that the sorting will be case-insensitive. | 
| _AS | Accent-sensitive. This option indicates that the sorting will be accent-sensitive; for example, "a" and "ấ" are different characters. | 
| _AI | Accent-insensitive. | 

## Instance character set suffix description

| Instance Character Set Suffix | Description | 
|---------|---------|
|_CI_AI| Case-insensitive and accent-insensitive. |
|_CI_AS| Case-insensitive and accent-sensitive. |
|_CS_AI| Case-sensitive and accent-insensitive. |
|_CS_AS| Case-sensitive and accent-sensitive. |

## Collation by server
The following table lists the default collations defined by certain OS region settings.

| Windows Region Settings | Default Collation |
|---------|---------|
| Afrikaans (South Africa) | Latin1_General_CI_AS | 
| Alsatian (France) | Latin1_General_CI_AS | 
| Basque (Basque) | Latin1_General_CI_AS | 
| Bosnian (Bosnia and Herzegovina, Latin) | Latin1_General_CI_AS | 
| Bulgarian (Bulgaria) | Cyrillic_General_CI_AS | 
| Chinese (Macao SAR) | Latin1_General_CI_AI | 
| Chinese (PRC) | Chinese_PRC_CI_AS | 
| Dutch (Netherlands) | Latin1_General_CI_AS | 
| English (Australia) | Latin1_General_CI_AS | 
| English (India) | Latin1_General_CI_AS | 
| English (Canada) | Latin1_General_CI_AS | 
| English (New Zealand) | Latin1_General_CI_AS | 
| English (United Kingdom) | Latin1_General_CI_AS | 
| English (United States) | Latin1_General_CI_AS | 
| Filipino (Philippines) | Latin1_General_CI_AS | 
| Italian (Italy) | Latin1_General_CI_AS | 
| Thai (Thailand) | Thai_CI_AS | 

