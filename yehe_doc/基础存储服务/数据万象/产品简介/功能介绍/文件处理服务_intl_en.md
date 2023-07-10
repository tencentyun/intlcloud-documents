## Overview

File processing features such as hash calculation, decompression, and compression and packaging are provided for all files stored in COS. Currently, the following file processing features are supported:


| Feature | Description |
| :------------- | :----------------------------------------------------------- |
| Hash calculation | It calculates the file hash. Currently, the following hash calculation algorithms are supported: MD5, SHA-1, and SHA-256.<br>File size limits:<li>Sync request: Below 128 MB.<li>Async request: Below 50 GB. |
| File decompression | It decompresses .zip, .tar, .gz, or .7z packages in the cloud and dumps the extracted files to COS.<br>File size limit: Below 5 TB. |
| Multi-file zipping | It compresses multiple files into a .zip, .tar, or tar.gz format.<br>File limit: Up to 10,000 files of less than 50 GB in total can be zipped. |



>?
> - The file processing service is provided and charged by CI. For billing details, see [File Processing Fees](https://www.tencentcloud.com/document/product/1045/52070).
> - Currently, the file processing service is available only in Beijing and Shanghai regions.

## Use Cases

### Data verification

The file hash calculation feature can be used to quickly check the data consistency.

### Daily tools

On-cloud PaaS file compression and decompression features are provided, which enable you to preview files after decompression and enrich online preview scenarios.

## How to Use

The file processing feature is provided by CI, so you need to click [here](https://console.cloud.tencent.com/ci) to activate CI first.

After activating CI, you can enable file processing in the COS console and then use the feature in the console or via an API.

### Using the COS console

#### In the file list

You can click **More Actions** in the bucket file list to perform file processing operations such as hash calculation on files. For more information, see Processing File in File List.

#### Through a job

You can perform file processing operations through **jobs and workflows**. For more information, see Configuring File Hash Calculation Job.

>!Currently, this feature can be used only through a job but not a workflow.



