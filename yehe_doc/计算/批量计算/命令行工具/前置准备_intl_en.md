Before installing TCCLI, make sure that your system has the Python environment installed. For details, see prerequisites instructed in [Installing TCCLI] (https://intl.cloud.tencent.com/document/product/1013/33464).

## Step 1: Installing TCCLI	

### Installing TCCLI
Run commands based on the actual situation.
- **TCCLI not installed**
Run the following command to quickly install TCCLI via pip. For details, please see [Installing TCCLI](https://intl.cloud.tencent.com/document/product/1013/33464).
```
$ sudo pip install tccli
```
- **TCCLI installed**
Run the following command to quickly upgrade TCCLI through pip:
```
$ sudo pip install --upgrade tccli
```

### Verifying installation  
Run the following command to check whether TCCLI is successfully installed and has Batch-related capabilities:
```
tccli batch help
```
The returned result is as follows, indicating that TCCLI is successfully installed:
```
NAME
        batch
DESCRIPTION
        batch-2017-03-12
USEAGE
        tccli batch <action> [--param...]
OPTIONS
        help
        show the tccli batch help info
        --version
        specify a batch api version
AVAILABLE ACTION
        DescribeComputeEnv
        Used to query details of the computing environment
        CreateTaskTemplate
        Used to create a task template
```

## Step 2: Configuring TCCLI	
1. Log in to the [API Key Management](https://console.cloud.tencent.com/cam/capi).
2. Click **Create Key** or use an available key to record `SecretID` and `SecretKey`. See the figure below:
![](https://main.qcloudimg.com/raw/0edc3a84752d2ae4524e971156f7e5f3.png)
3. Run the command `tccli configure` and enter the TCCLI configuration information. For details, please see [Configuring TCCLI] (https://intl.cloud.tencent.com/zh/document/product/1013/33465).
```
$ tccli configure
TencentCloud API secretId[None]:
TencentCloud API secretKey[None]:
region[None]:
output[json]:
```


## Step 3: Preparing the COS Directory


### Creating a bucket and sub-folders [](id:create)
1. Log in to the COS console and choose **[Bucket List](https://console.cloud.tencent.com/cos5/bucket)** in the left sidebar.
2. Create a bucket and create 3 folders in the bucket. See the figure below:
![](https://main.qcloudimg.com/raw/0add1b49c44f4b2740ddc44e3164216b.png)


### Acquiring COS-related endpoints [](id:get)
1. Click **Basic Configuration** on the left to view the endpoint in **Basic Information**. See the figure below:
![](https://main.qcloudimg.com/raw/cc6a49e7164226efa1cdfe3bcde60a35.png)
2. Acquire the endpoints of subfolders in the COS bucket.
<dx-alert infotype="explain" title="">
Acquire COS-related endpoints based on the actual situation.
</dx-alert>
The acquired COS bucket endpoint is `https://batchdemo-xxxxxxxxx.cos.ap-guangzhou.myqcloud.com`. The endpoints of the three folders created in [Creating a Bucket and Sub-folders](#create) can be acquired by combining `domain and sub-folder names` as follows:

 * `cos://batchdemo-xxxxxxxxx.cos.ap-guangzhou.myqcloud.com/logs/`
 * `cos://batchdemo-xxxxxxxxx.cos.ap-guangzhou.myqcloud.com/input/`
 * `cos://batchdemo-xxxxxxxxx.cos.ap-guangzhou.myqcloud.com/output/`



## Step 4: Downloading the Demo File
Access the [Batch demo](http://batchdemo-1251783334.cosgz.myqcloud.com/demo/BatchDemo.zip), download the test package, and decompress it.

<dx-alert infotype="explain" title="">
The demo is provided in the format of the Python+Batch CLI. Since BatchCompute has many capabilities and configuration items, you can work with it more conveniently by using Python scripts.
</dx-alert>






## Step 5: Modifying Demo Custom Information


<dx-alert infotype="notice" title="">
Change the general part of the custom information about the Batch demo. Modify all files in Demo as follows:
</dx-alert>


Use the following custom information in `1_SimpleStart.py` as an example:
```
# custom (Change to your info)
imageId = "img-m4q71qnf"
Application = {
    "DeliveryForm": "LOCAL",
    "Command": " python -c \"fib=lambda n:1 if n<=2 else fib(n-1)+fib(n-2); print(fib(20))\" "
}
StdoutRedirectPath = "cos://batchdemo-xxxxxxxxxx.cos.ap-guangzhou.myqcloud.com/logs/"
StderrRedirectPath = "cos://batchdemo-xxxxxxxxxx.cos.ap-guangzhou.myqcloud.com/logs/"
```
The following table lists the information to be modified.
<table>
	<tr>
	<th>Configuration Item</th>
	<th>Description</th>
	</tr>
	<tr>
	<td>imageId</td>
	<td>
		<ul class="params">
		<li>Custom images are created based on this image. For more information, see <a href="https://intl.cloud.tencent.com/document/product/599/13035">Windows Custom Image</a>.</li>
		</ul>
	</td>
	</tr>
	<tr>
	<td>StdoutRedirectPath</td>
	<td rowspan=2>Enter the complete log folder endpoint acquired in <a href="#get">Acquiring COS-related endpoints</a>.</td>
	</tr>
	<tr>
	<td>StderrRedirectPath</td>
	</tr>
	<tr>
	<td>Application</td>
	<td>The startup command. Use the default setting.</td>
	</tr>
</table>


```
cmd = "tccli batch SubmitJob \
    --version 2017-03-12 \
    --Placement '{\"Zone\": \"ap-guangzhou-2\"}' \
    --Job ' %s ' "%(json.dumps(testJob))
```
The demo specifies Guangzhou Zone 2 for resource application. You can select the corresponding availability zone to apply for resources based on the default region configured in TCCLI.
For more information about regions and availability zones, see [Regions and AZs](https://intl.cloud.tencent.com/document/product/213/6091).

## Step 6: Testing
Experience the Batch usage methods and computing capability in the following sequence according to the reference course.
1. 1_SimpleStart.py: [Quick Start](https://intl.cloud.tencent.com/document/product/599/10551)
2. 2_RemoteCodePkg.py: [Running Remote Package](https://intl.cloud.tencent.com/document/product/599/10552)
3. 3_StoreMapping.py: [Mapping Remote Storage](https://intl.cloud.tencent.com/document/product/599/10983)


<style>
	.params{margin-bottom:0px !important;}
</style>


