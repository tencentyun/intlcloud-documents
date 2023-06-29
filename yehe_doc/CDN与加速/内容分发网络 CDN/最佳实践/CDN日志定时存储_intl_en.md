# Regularly Storing CDN Logs

This document describes how to use Tencent Cloud SCF to create two functions in order to regularly store CDN logs into COS.

# Key Steps

This document describes how to create the "storage" and "task distribution" functions, use them together, and configure a timer trigger in order to regularly store CDN logs into COS.

There are four key steps:

A. Prepare the Tencent Cloud API access key and COS information

B. Create the storage function (cdn-save-log-into-cos)

C. Create the task function (cdn-dispatch-log-jobs)

D. Configure the timer

# Directions

## A. Prepare the following resources before creating the functions

1. Tencent Cloud API access key

Go to the [access key management page](https://console.cloud.tencent.com/cam/capi), query or create a key, and record the following information:

Access credential name (`SecretId`), such as `AKIDRVI54XXn10r58oZpmzbBOnwt47xO1LRv`

Access credential key (`SecretKey`), such as `3t0SYPHRIpjmAAUPfKM8b4yXnff4Aq56`

2. COS bucket

Log in to the [COS Console](https://console.cloud.tencent.com/cos), access the **Bucket List** to query or create a bucket, access the bucket to view its **Basic Information**, and record the following information:

Bucket name (`Bucket Name`), such as `examples-1251002854`

Bucket region (`Region`), such as `ap-chengdu`

## B. Create the storage function (cdn-save-log-into-cos)

1. Log in to the [SCF Console](https://console.cloud.tencent.com/scf) and click **Function Service**.

2. Select **Create** and enter **cdn-save-log-into-cos** as the function name.

3. Select **Function Template**, search with the keyword "CDN", select the "cdn-save-log-into-cos" template, and click "Next" to access the function configuration page:
![](https://main.qcloudimg.com/raw/402a01a22ca748386617afd2fc7255a2.png)

4. Click **Complete** to create the function.
![](https://main.qcloudimg.com/raw/69f87dc5f7314f0cdb21f45684b403ed.png)

## C. Create the task function (cdn-dispatch-log-jobs)

1. Log in to the [SCF Console](https://console.cloud.tencent.com/scf) and click **Create**.

2. Select **Function Template**, search with the keyword "CDN", and select the "cdn-dispatch-log-jobs" template.

3. Enter **cdn-dispatch-log-jobs** as the function name and click "Next".

4. Click **Complete** to create the function.

![](https://main.qcloudimg.com/raw/b82b157292163ca06b9f43e74bd1a8de.png)

5. Click the **Function Code** tab. In the code editing box, modify the Python code by entering the following configuration information:

In the `config` variable on row 143, enter the corresponding configuration information:

- Set fields such as `secret_id`, `secret_key`, `cos_region`, `cos_bucket`, and `scf_region`.
- If you set the function name as instructed in step B and do not want to modify it, you can retain the original value of `scf_function`.
- The default value of `cdn_host` is an empty array (i.e., the logs of all domain names under the account will be stored). If needed, you can enter the list of specified domain names.

![](https://main.qcloudimg.com/raw/8ed596f7843acacc0e3974057922cd0d.png)

6. Click **Save**.

7. Click **Test** to check whether the code runs properly. After the testing program stops running, you can access the COS Console and check whether the corresponding logs are stored in COS.

## D. Configure the timer

After you create the two functions above, the list on the SCF Console will be as shown below:

1. Click **cdn-dispatch-log-jobs** to access its details.

![](https://main.qcloudimg.com/raw/55382244ab24832e280b040f284cd09a.png)

2. Click the **Trigger Management** tab and click **Create a Trigger**.

![](https://main.qcloudimg.com/raw/36949d35a75f77515caacee834427064.png)

3. Select **Scheduled triggering** as the trigger method, enter a custom scheduled task name, select **Every 5 mins** as the trigger period, and click **Submit**.

![](https://main.qcloudimg.com/raw/fe157cb0c234693920c3efc36ed9c7e3.png)

Once you complete all the steps above, CDN logs will be regularly stored into COS.