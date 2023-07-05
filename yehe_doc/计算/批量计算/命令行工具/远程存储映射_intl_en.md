## Operation Scenarios
Remote mapping is used as an auxiliary feature by BatchCompute for storage services to map remote storage, such as COS and CFS, to a local folder.


## Prerequisites
Complete the preparations as instructed in [Preparations](https://intl.cloud.tencent.com/document/product/599/10548) and learn how to configure the general part of the custom information.

## Directions
### Uploading input data file
1. Create `number.txt` with the following content:
```
1
2
3
4
5
6
7
8
9
```
2. Log in to the COS Console and click **[Bucket List](https://console.cloud.tencent.com/cos5/bucket)** on the left sidebar.
3. Select the ID of the created bucket, click **Objects**, select **input**, and upload `number.txt` as shown below:
![](https://main.qcloudimg.com/raw/82be55909b293aa026539d47c996a1c4.png)

### Viewing and modifying demo
>Modify the general part of the custom information in `3_StoreMapping.py` as instructed in [Preparations](https://intl.cloud.tencent.com/document/product/599/10548).
>
Open `3_StoreMapping.py` in an editor.
```
# custom (Change to your info)
imageId = "img-m4q71qnf"
Application = {
    "DeliveryForm": "PACKAGE",
    "Command": "python ./codepkg/sumnum.py",
    "PackagePath": "http://batchdemo-xxxxxxxxx.cos.ap-guangzhou.myqcloud.com/codepkg/codepkg.tgz"
}
StdoutRedirectPath = "your cos path"
StderrRedirectPath = "your cos path"
InputMapping = {
    "SourcePath": "cos://batchdemo-xxxxxxxxx.cos.ap-guangzhou.myqcloud.com/input/",
    "DestinationPath": "/data/input/"
}
OutputMapping = {
    "SourcePath": "/data/output/",
    "DestinationPath": "your output remote path"
}
```
Compared to [`2_RemoteCodePkg.py`](https://intl.cloud.tencent.com/document/product/599/10552), some of the parameters in the custom part are modified as follows:
<table>
	<tr>
	<th>Configuration Item</th>
	<th>Description</th>
	</tr>
	<tr>
	<td>Application</td>
	<td>Modify `Command` to `sumnum.py`. </td>
	</tr>
	<tr>
	<td>InputMapping</td>
	<td>	Input mapping.
	<ul class="params">
	<li>`SourcePath` remote storage address: modify this address to the path of the **input** folder in "Preparations". For more information, please see <a href="https://intl.cloud.tencent.com/document/product/599/10548#.E8.8E.B7.E5.8F.96-cos-.E7.9B.B8.E5.85.B3.E8.AE.BF.E9.97.AE.E5.9F.9F.E5.90.8D">Getting COS Endpoints</a>.</li>
	<li>`DestinationPath` local directory: retain the original setting for the time being.</li>
	</ul>
</td>
	</tr>
	<tr>
	<td>OutputMapping</td>
	<td>Output mapping.
	<ul class="params">
	<li>`SourcePath` local directory: retain the original setting for the moment.</li>
	<li>`DestinationPath` remote storage address: modify this address to the path of the **output** folder in "Preparations". For more information, please see <a href="https://intl.cloud.tencent.com/document/product/599/10548#.E8.8E.B7.E5.8F.96-cos-.E7.9B.B8.E5.85.B3.E8.AE.BF.E9.97.AE.E5.9F.9F.E5.90.8D">Getting COS Endpoints</a>.</li>
	</ul>
	</td>
	</tr>
</table>

**sumnum.py** is composed as below:
Open `input/number.txt`, add up all numbers in each row, and write the result into `output/result.txt`.
```
import os

inputfile = "/data/input/number.txt"
outputfile = "/data/output/result.txt"

def readFile(filename):
    total = 0
    fopen = open(filename, 'r')
    for eachLine in fopen:
        total += int(eachLine)
    fopen.close()
    print "total = ",total
    fwrite = open(outputfile, 'w')
    fwrite.write(str(total))
    fwrite.close()

print("Local input file is ",inputfile)
readFile(inputfile)
```


### Submitting job
Run the following command to run the Python script.
The demo encapsulates the job submission process by using Python scripts and the BatchCompute command line tool.
```
python 3_StoreMapping.py
```
The returned result is as follows, indicating that the job is successfully submitted:
```
{
    "RequestId": "8eaeb01e-94a6-41a1-b40f-95f15417c0b4", 
    "JobId": "job-97smiptb"
}
```

If the submission operation fails, check the returned value or [contact us](https://intl.cloud.tencent.com/document/product/599/10806) for assistance.

### Viewing status
Please see [Viewing Status](https://intl.cloud.tencent.com/document/product/599/10551) in Quick Start.

### Viewing result
1. Log in to the COS Console and click **[Bucket List](https://console.cloud.tencent.com/cos5/bucket)** on the left sidebar.
2. Select the ID of the created bucket, click **Files**, and select **output** as shown below:
BatchCompute copies the output data from the local directory to the remote directory. The execution results of `3_StoreMapping.py` are stored in `result.txt`, which is automatically synced to COS.
![](https://main.qcloudimg.com/raw/3f72ff4fd2232fd4a5da62d8aabc11ae.png)
`result.txt` is composed as below:
```
45
```

<style>
	.params{margin-bottom:0px !important;}
</style>
