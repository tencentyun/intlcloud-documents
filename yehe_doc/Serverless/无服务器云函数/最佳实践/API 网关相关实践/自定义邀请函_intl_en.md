## Overview
This document describes how to use SCF in combination with API Gateway to customize an invitation, so that you can generate an invitation simply by entering the guest name.



## Directions

### Creating function
1. Log in to the SCF Console and select **[Functions](https://console.cloud.tencent.com/scf/list)** on the left sidebar.
2. At the top of the "Functions" page, select the **Guangzhou** region and click **Create** to enter the function creating page.
3. Create a function as follows in "Basic Info" on the "Create Function" page and click **Next** as shown below:

 - **Function Name**: enter a custom name. This document uses `test` as an example.
 - **Runtime Environment**: select "Python 2.7".
 - **Create Method**: select **Function Template**.
 - **Fuzzy Search**: enter "Custom invitation" and search.
Click **Learn More** in the template to view relevant information in the "Template Details" pop-up window, which can be downloaded.
4. On the "Function configuration" page, keep the default configuration and click **Complete**.

### Creating gateway trigger
A gateway trigger is used to pass the name of an invitation to the function through an API call. The specific steps are as follows:
1. Select **Trigger Management** on the left of the "Function configuration" page and click **Create a Trigger**.
2. In the "Create a Trigger" pop-up window, add an API gateway trigger for the function.

The main parameters are as follows. Keep the remaining parameters as default:
 - **Trigger Method**: select "API Gateway Trigger".
 - **API Service Type**: select "Create API Service".
 - **Enable Integration Response**: check this option.
3. Click **Submit**.



### Creating bucket
A bucket is used to store custom invitations. The specific steps are as follows:
1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5/bucket) and select **Bucket List** on the left sidebar.
2. Click **Create Bucket** on the "Bucket List" page.
3. In the "Create Bucket" pop-up window, create a bucket.
.
The main parameter information is as follows. Keep the remaining parameters as default:
 - **Name**: enter a custom name. This document uses `test` as an example.
 - **Region**: select "Guangzhou".
 - **Access Permission**: select "Public Read/Private Write".
4. Click **OK**.
2. Select **Basic Configuration** on the left of the bucket and click **Add a Rule** in "CORS (Cross-Origin Resource Sharing) Setting".
3. In the "Add CORS Rule" pop-up window, add a rule.

The main parameter information is as follows. Keep the remaining parameters as default:
 - **Origin**: enter <b>*</b>.
 - **Allow-Methods**: select "GET".
 - **Expose-Headers**: enter **-**.
4. Click **Submit**.


### Modifying function configuration
1. On the "[Functions](https://console.cloud.tencent.com/scf/list?rid=1&ns=default)" page, click the function name to enter the "Function configuration" page.
2. On the "Function configuration" page, click **Edit** in the top-right corner and configure the function as follows.
 - **Execution Role**: check "Enable" and select **a permission policy containing COS data read/write permissions**. `SCF_QcsRole` is selected here as an example.
.
 - **Environment Variable**: add the following environment variables and configure them as.
.
<table>
<tr>
<th>key</th><th>value</th>
</tr>
<tr>
<td>region</td><td>Bucket region, which starts with `ap-` and ends with the region name.</td>
</tr>
<tr>
<td>target_bucket</td><td>Name of the created bucket.</td>
</tr>
<tr>
<td>target_path</td><td>Destination bucket path.</td>
</tr>
</table>
3. Click **Save**.

### Generating invitation
You can apply for an invitation in two ways:

#### Method 1
Run the following command on the command line.
```
curl API gateway trigger URL  -d 'Name of the invited guest'
```
The download address of the invitation can be obtained on the device, such as:
```
curl https://service-xxxx.gz.apigw.tencentcs.com/release/test-123456 -d 'name'
https://testxxxx.com//invitation-yun-ServerlessDays.jpg%
```

#### Method 2
1. Download the [HTML page](https://github.com/tencentyun/scf-demo-repo/blob/master/Python2.7-Add_Text_To_Pictures/invitation.html) and change the URL to the URL of the API gateway trigger.

2. Open the HTML page, enter the name of the invited guest to generate a poster, and access the URL to download it.

