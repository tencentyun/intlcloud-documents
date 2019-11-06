## Overview

COS Select allows you to filter out the desired data at the storage level, which significantly reduces the amount of data transferred by COS and thereby lowers your usage costs and improves your data acquisition efficiency. In the COS Console, you can extract the contents of individual files stored in buckets using the basic SQL templates we provide or by entering syntax-compliant statements.

## Notes

- Please make sure that the file to be extracted complies with the specification of COS. For more information on the specification of COS Select, see [SELECT Overview](https://intl.cloud.tencent.com/document/product/436/32472).
- The extraction feature in the console allows you to extract up to 40 MB of data from a file of up to 128 MB. If you need to process larger files or extract more data, you need to use APIs or SDKs.

## Directions

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5).
2. On the left sidebar, click **Bucket List**.
3. Click the bucket name to enter the bucket where the object is stored.
   ![](https://main.qcloudimg.com/raw/44d78203df8d6b4506e7870e7cd827b1.png)
4. In the "File List" module of the bucket, click **Extract** in the "Operation" column to the right of the object to be extracted.
	 ![](https://main.qcloudimg.com/raw/2e507efa3b6f9ccda41a45b7bb3038d1.png)
5. Enter the extraction page in the console and select the type, header field, delimiter, and compression format of the file to be extracted.
	 ![](https://main.qcloudimg.com/raw/b6390a741fc0b3dd6880752ed78d7ca5.png)
6. Click **Select an SQL Template**, select the desired template statement, and click **OK**.
	 ![](https://main.qcloudimg.com/raw/0b3886fd501962d7eff5efd0b3bb4a89.png)
7. Edit the statement in the text box based on the actual file and click **Run SQL**.
8. After the process is finished, you can view the first 100 results in the text box at the bottom. To obtain complete data, click **Export Extraction Result**.
	 ![](https://main.qcloudimg.com/raw/b269aa12cd63d838559642b60f0f598c.png)
	 
