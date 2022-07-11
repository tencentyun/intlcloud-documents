## Getting a Bill with COS Bucket APIs

Step 1. Create and authorize a bucket as instructed in [Storing Bill to COS Bucket](https://intl.cloud.tencent.com/document/product/1085/48340).

Step 2. Apply for a key for accessing Tencent Cloud through the API.

1. Log in [here](https://console.intl.cloud.tencent.com/cam/capi).

2. Click **Create Key** and enter the SMS verification code to create a key.

![image-20220705141223303](/Users/crystaljingtan/Library/Application Support/typora-user-images/image-20220705141223303.png)

Step 3. Get the name of the compressed bill package through the API.

>!For the following two steps, see the sample code.

1. See [GET Bucket (List Objects)](https://intl.cloud.tencent.com/document/product/436/30614).

2. Use the above API for listing files. Prefix filtering and path filtering are supported.

3. Extract the list of files to be downloaded based on the file list and the agreed naming convention as described in the sample.

   | Bucket File Type | Filename | File Format | Upload Time | Remarks |
   | ------------------------------------------------- | ------------------------------------------------- | -------- | ------------------- | ------------------------------------------------------------ |
   | Daily detailed bills (including reseller bills and customer bills) | 200020475883-20210810-bill_details.zip | ZIP | 2021-08-11 15:45:00 | Bill details for a day will be stored in the COS bucket at 3 AM on the next day (or 8 PM if the next day is the first day of a month). The decompressed package contains one CSV file. If the number of bill details exceeds the maximum number of rows allowed in Excel, the bill will be split into multiple CSV files as shown below. |
   | Monthly detailed bills (including reseller bills and customer bills) | 200018967974-202201-by_used_time-bill_details.zip | ZIP      | 2021-08-11 15:45:00 | All bill details in a month will be updated on the second day of the next month. The decompressed package contains one CSV file. If the number of bill details exceeds the maximum number of rows allowed in Excel, the bill will be split into multiple CSV files as shown below. |
   
   ![img](https://docimg9.docs.qq.com/image/rAc1LAyuGHpSf-teducK8w?w=275&h=102&_type=png)

Step 4. Download the compressed package.

1. See [GET Object](https://intl.cloud.tencent.com/document/product/436/7753).

2. Call the above download API and pass in parameters (the names of the files to be downloaded and local path) to download the files.

3. Write the code for decompressing and reading the CSV files.

>?
>1. For descriptions of bill fields in the bucket, see [Billing Details](https://intl.cloud.tencent.com/document/product/1085/43050).
>2. The bills displayed in the current month are not finalized yet and are for reference only. We recommend you call the API on the third day of the next month to get the detailed bills of the current month.
>3. Fees on detailed bills can be accurate to eight decimal places, while fees shown on bills by instance are rounded off to two decimal places. The actual amount is deducted by two decimal places.
>4. To distinguish between reseller and customer bills, filter bills by UIN.