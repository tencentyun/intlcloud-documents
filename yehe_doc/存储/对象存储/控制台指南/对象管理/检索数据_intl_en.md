## Overview

COS Select allows you to filter out desired data at the storage level, significantly reducing the amount of data transferred by COS, thereby lowering your usage costs, and improving data acquisition efficiency. In COS Console, you can extract the content of individual files stored in buckets using standard SQL templates we provide or by entering statements that meet syntax rules.

>
>- COS Select currently only supports objects in json and csv file formats, and public cloud regions in mainland China.
>- Please make sure the file to be extracted complies with the specification of COS Select. For more information on the specification of COS Select, see [SELECT Overview](https://cloud.tencent.com/document/product/436/37635).
>- COS Select in the console supports data extraction of up to 40M for 128MB files. If you need to process larger files or extract more data, please use [API](https://cloud.tencent.com/document/product/436/37641) or SDK.

## Steps

1. Log into the [COS Console](https://console.cloud.tencent.com/cos5).
2. In the left sidebar, click **Bucket List**.
3. Click the bucket name to enter the bucket where the object is stored.
   ![](https://main.qcloudimg.com/raw/44d78203df8d6b4506e7870e7cd827b1.png)
4. In the "File List" module of the bucket, locate the object to be extracted and click **Extract** in the right-side "Operation" column.
	 ![](https://main.qcloudimg.com/raw/2e507efa3b6f9ccda41a45b7bb3038d1.png)
5. Enter the extract object content page in the console, select the type, header field, separator, and compression format of the file to be extracted.
	 ![](https://main.qcloudimg.com/raw/b6390a741fc0b3dd6880752ed78d7ca5.png)
6. Click **Select an SQL Template**, select the desired template statement, and click **OK**.
	 ![](https://main.qcloudimg.com/raw/0b3886fd501962d7eff5efd0b3bb4a89.png)
7. Edit the statement in the text box based on the actual file and click **Run SQL**.
8. After the process is finished, you can view the first 100 results in the text box at the bottom. To obtain complete data, click **Export**.
	 ![](https://main.qcloudimg.com/raw/b269aa12cd63d838559642b60f0f598c.png)
	 
