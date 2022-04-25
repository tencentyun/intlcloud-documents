## Overview

COS Select allows you to filter out desired data at the storage level, significantly reducing the amount of data transferred by COS, thereby lowering your usage costs, and improving data acquisition efficiency. In the COS console, you can extract data from individual files stored in buckets using the standard SQL templates we provide or by specifying statements that comply with syntax rules.

>?
>
>- COS Select currently supports objects in JSON or CSV format only in public cloud regions (Chinese mainland), and objects in Parquet format only in Beijing region.
>- Please make sure the file to be extracted complies with COS Select specifications. For more information on COS Select specifications, please see [SELECT Overview](https://intl.cloud.tencent.com/document/product/436/32472).
>- COS Select in the console supports extraction of up to 40 MB data from a maximum of 128 MB files. To process larger files or extract more data, please use the [API](https://intl.cloud.tencent.com/document/product/436/32360) or SDKs.

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Locate the bucket where the object resides and click the bucket name.
4. Click **File List** on the left sidebar.
5. Find the target object and click **More Actions > Extract** on the right.
>? Currently, only objects in the STANDARD, STANDARD_IA, and INTELLIGENT TIERING storage classes can be extracted.
>
6. Configure the fields **File Type**, **Header Field**, **Separator**, **Compression Format**, and **Export Format**.
![](https://main.qcloudimg.com/raw/b6390a741fc0b3dd6880752ed78d7ca5.png)
7. Click **Select SQL Template**.
8. In the pop-up window, select the template statement you want to use for extraction and click **OK**.
![](https://main.qcloudimg.com/raw/0b3886fd501962d7eff5efd0b3bb4a89.png)
9. Edit the statement in the text box based on your actual file and then click **Run SQL**.
![](https://main.qcloudimg.com/raw/b269aa12cd63d838559642b60f0f598c.png)
Now you can see the first 100 results in the text box at the bottom. To obtain the complete set of data, click **Export Extraction Results**.


