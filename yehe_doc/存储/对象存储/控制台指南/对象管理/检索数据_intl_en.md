### Introduction

COS Select allows you to filter out desired data at the storage level, significantly reducing the amount of data transferred by COS, thereby lowering your usage costs, and improving data acquisition efficiency. On the COS Console, you can extract the content of individual files stored in buckets using the standard SQL templates we provide or by entering statements that comply with syntax rules.

>-COS Select currently only supports objects in json and csv file formats as well as public cloud regions in the Chinese mainland.
>-Please make sure the file to be extracted complies with COS Select specifications. For more information on COS Select specifications, see [SELECT Overview](https://intl.cloud.tencent.com/document/product/436/32472).
>-COS Select on the console supports data extraction of up to 40M for files of up to 128 MB in size. If you need to process larger files or extract more data, please use the [SELECT Object Content] API(https://intl.cloud.tencent.com/document/product/436/32360) or SDK.

### Directions

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5).
2. On the left sidebar, click **Bucket List**.
3. Click the bucket name to enter the bucket where the object is stored.

4. Locate the object to extract under the **File List** tab, and select **More Actions** > **Extract** under **Operation**.
	
5. Enter the extract object content page in the console, and select the type, header field, separator, and compression format of the file to be extracted.
	 ![](https://main.qcloudimg.com/raw/b6390a741fc0b3dd6880752ed78d7ca5.png)
6. Click **Select an SQL Template**, select the desired template statement, and click **OK**.
	 ![](https://main.qcloudimg.com/raw/0b3886fd501962d7eff5efd0b3bb4a89.png)
7. Edit the statement in the text box based on your actual file and then click **Run SQL**.
8. After the process is finished, you can view the first 100 results in the text box at the bottom. To obtain the complete set of data, click **Export**.
	 ![](https://main.qcloudimg.com/raw/b269aa12cd63d838559642b60f0f598c.png)
