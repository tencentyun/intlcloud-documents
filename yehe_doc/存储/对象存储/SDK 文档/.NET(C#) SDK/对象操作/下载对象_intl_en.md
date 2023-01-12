## Overview

This document provides an overview of APIs and SDK code samples related to object download.

| API | Operation | Description |
| ------------------------------------------------------------ | -------- | ------------------ |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system |

## SDK API References

For the parameters and method description of all the APIs in the SDK, see [API Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Advanced APIs (Recommended)

### Downloading an object (checkpoint restart)

The advanced version of the GET Object API uses more encapsulated logic to allow you to suspend, resume (via checkpoint restart), or cancel download requests.

>? 
> - If your .NET Framework version is 4.0 or earlier, advanced APIs are not available. For more information, please see [Backward Compatibility](https://intl.cloud.tencent.com/document/product/436/42378).
> - Advanced APIs support concurrent multipart downloads from v5.4.26. To download the latest version of SDK, go to [Releases](https://github.com/tencentyun/qcloud-sdk-dotnet/releases) or refer to [Getting Started](https://intl.cloud.tencent.com/document/product/436/30594).
> 

#### Sample 1: Downloading an object

[//]: #	".cssg-snippet-transfer-download-object"

```cs
using COSXML.Model.Object;
using COSXML.Auth;
using COSXML.Transfer;
using System;
using COSXML;
using System.Threading.Tasks;

namespace COSSnippet
{
    public class TransferDownloadObjectModel {

      private CosXml cosXml;

      TransferDownloadObjectModel() {
        CosXmlConfig config = new CosXmlConfig.Builder()
          .SetRegion("COS_REGION") // Set the default region. For abbreviations of COS regions, visit https://cloud.tencent.com/document/product/436/6224.
          .Build();
        
        string secretId = "SECRET_ID";   // SecretId of the TencentCloud API. For more information about how to obtain the API key, see https://console.cloud.tencent.com/cam/capi.
        string secretKey = "SECRET_KEY"; // SecretKey of the TencentCloud API. For more information about how to obtain the API key, see https://console.cloud.tencent.com/cam/capi.
        long durationSecond = 600;          // Validity period of the request signature in seconds
        QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
          secretKey, durationSecond);
        
        this.cosXml = new CosXmlServer(config, qCloudCredentialProvider);
      }

      /// Download an object via advanced API
      public async Task TransferDownloadObject()
      {
        // Initialize TransferConfig
        TransferConfig transferConfig = new TransferConfig();
        // Manually set the part threshold for advanced APIs to 20 MB (default), which is supported from v5.4.26
        //transferConfig.DivisionForDownload = 20 * 1024 * 1024;
        // Manually set the part size of advanced APIs to 10 MB (default: 5 MB). We recommend you not set the size to a very small value because this may result in frequent retries or unacceptable download speeds.
        //transferConfig.SliceSizeForDownload = 10 * 1024 * 1024;
        
        // Initialize TransferManager
        TransferManager transferManager = new TransferManager(cosXml, transferConfig);
        
        String bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
        String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key
        string localDir = System.IO.Path.GetTempPath();// Local file directory
        string localFileName = "my-local-temp-file"; // Filename of the local file
        
        // Download an object
        COSXMLDownloadTask downloadTask = new COSXMLDownloadTask(bucket, cosPath, 
          localDir, localFileName);
	
        // Manually set maximum tasks (default: 5) for advanced APIs, which is supported from v5.4.26
        //downloadTask.SetMaxTasks(10);
        downloadTask.progressCallback = delegate (long completed, long total)
        {
            Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
        };

        try {
          COSXML.Transfer.COSXMLDownloadTask.DownloadTaskResult result = await 
            transferManager.DownloadAsync(downloadTask);
          Console.WriteLine(result.GetResultInfo());
          string eTag = result.eTag;
        }
        catch (COSXML.CosException.CosClientException clientEx)
        {
          // Request failed
          Console.WriteLine("CosClientException: " + clientEx);
        }
        catch (COSXML.CosException.CosServerException serverEx)
        {
          // Request failed
          Console.WriteLine("CosServerException: " + serverEx.GetInfo());
        }
      }


      static void Main(string[] args)
      {
        TransferDownloadObjectModel m = new TransferDownloadObjectModel();

        /// Download an object via advanced API
        m.TransferDownloadObject().Wait();
      }
    }
}
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferDownloadObject.cs).
>

#### Sample 2: Setting checkpoint restart for download

[//]: #	".cssg-snippet-transfer-download-resumable"

```cs
COSXMLDownloadTask downloadTask = new COSXMLDownloadTask(request);
 // Enable checkpoint restart. If an object is not completely downloaded, the download will be started from the checkpoint.
 // If the local file contains content that does not meet the requirements of the current download, the download may fail. You can delete the file and try again.
 downloadTask.SetResumableDownload(true);
 try {
   COSXML.Transfer.COSXMLDownloadTask.DownloadTaskResult result = await 
   transferManager.DownloadAsync(downloadTask);
   Console.WriteLine(result.GetResultInfo());
   string eTag = result.eTag;
 } catch (Exception e){
   Console.WriteLine("CosException: " + e);
 }
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferDownloadObject.cs).
>

#### Sample 3: Batch download

[//]: #	".cssg-snippet-transfer-batch-download-objects"

```cs
TransferConfig transferConfig = new TransferConfig();

// Initialize TransferManager
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

// Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
string bucket = "examplebucket-1250000000";
string localDir = System.IO.Path.GetTempPath();// Local file directory

for (int i = 0; i < 5; i++) {
  // Download an object
  string cosPath = "exampleobject" + i; // Location identifier of an object in the bucket, i.e. the object key
  string localFileName = "my-local-temp-file"; // Filename of the local file
  COSXMLDownloadTask downloadTask = new COSXMLDownloadTask(bucket, cosPath, 
    localDir, localFileName);
  await transferManager.DownloadAsync(downloadTask);
}
```
>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferDownloadObject.cs).
>

#### Sample 4: Limiting single-URL download speed
[//]: #".cssg-snippet-transfer-download-objects-with-speed-limit"
```cs
TransferConfig transferConfig = new TransferConfig();

// Initialize TransferManager
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

String bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key
string localDir = System.IO.Path.GetTempPath();// Local file directory
string localFileName = "my-local-temp-file"; // Filename of the local file
        
GetObjectRequest request = new GetObjectRequest(bucket, 
        cosPath, localDir, localFileName);
request.LimitTraffic(8 * 1000 * 1024); // Limit the speed to 1 MB/s.

COSXMLDownloadTask downloadTask = new COSXMLDownloadTask(request);
await transferManager.DownloadAsync(downloadTask);
```


>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferDownloadObject.cs).
>

#### Sample 5: Downloading objects from a folder
[//]: #".cssg-snippet-transfer-download-objects-from-folder"
```cs
using COSXML.Common;
using COSXML.CosException;
using COSXML.Model;
using COSXML.Model.Object;
using COSXML.Model.Tag;
using COSXML.Model.Bucket;
using COSXML.Model.Service;
using COSXML.Utils;
using COSXML.Auth;
using COSXML.Transfer;
using System;
using COSXML;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Reflection;
using System.Text;
using System.Threading;
using System.Threading.Tasks;

namespace COSSnippet
{
  public class TransferDownloadObjectModel {

    private CosXml cosXml;
    private string nextMarker;

    TransferDownloadObjectModel() {
      CosXmlConfig config = new CosXmlConfig.Builder()
        .SetRegion("COS_REGION") // Set the default region. For abbreviations of COS regions, visit https://cloud.tencent.com/document/product/436/6224.
        .Build();
        
      string secretId = "SECRET_ID";   // SecretId of the TencentCloud API. For more information about how to obtain the API key, see https://console.cloud.tencent.com/cam/capi.
      string secretKey = "SECRET_KEY"; // SecretKey of the TencentCloud API. For more information about how to obtain the API key, see https://console.cloud.tencent.com/cam/capi.
      long durationSecond = 600;          // Validity period of each request signature in seconds
      QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
        secretKey, durationSecond);
        
      this.cosXml = new CosXmlServer(config, qCloudCredentialProvider);
  }

	public void GetObjectsFromFolder()
	{
    // Note: There is no actual API for downloading objects from a folder in COS
    // You can download objects from a folder or perform other similar operations by a combination of listing specified prefixes and downloading all the listed object keys.
    // Next, list objects and download them asynchronously.
		String nextMarker = null;
	   
		List<string>  downloadList = new List<string>();
		string bucket = "examplebucket-1250000000";
		string prefix = "folder1/"; // Specify a prefix.
		// Request until there is no next page of data
		do
		{
			// Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
			GetBucketRequest listRequest = new GetBucketRequest(bucket);
			// Obtain all objects and subdirectories in folder1/.
			listRequest.SetPrefix(prefix);
			listRequest.SetMarker(nextMarker);
			// Execute the list object request.
			GetBucketResult listResult = cosXml.GetBucket(listRequest);
			ListBucket info = listResult.listBucket;
			// List objects
			List<ListBucket.Contents> objects = info.contentsList;
			// nextMarker for the next page
			nextMarker = info.nextMarker;
			
			// List objects
			foreach (var content in objects)
			{
			downloadList.Add(content.key);
			Console.WriteLine("adding key:" + content.key);
			}
	  } while (nextMarker != null);
		Console.WriteLine("download list construct done, " + downloadList.Count + " objects added");

		TransferConfig transferConfig = new TransferConfig();
		TransferManager transferManager = new TransferManager(cosXml, transferConfig);
		string localDir = System.IO.Path.GetTempPath();// Local file directory
	  
		List<Task> taskList = new List<Task>();
		for (int i = 0; i < downloadList.Count; i++)
		{
			// Traverse the task list and write downloaded contents to the filename_i file.
			COSXMLDownloadTask downloadTask = new COSXMLDownloadTask(bucket, downloadList[i], 
				localDir, "filename_" + i.ToString());
			// Download asynchronously and add to the task list.
			Task task = transferManager.DownloadAsync(downloadTask);
			taskList.Add(task); 
		}
		Console.WriteLine("download tasks submitted, total " + taskList.Count + " tasks added");
		
		//Wait for all tasks in TaskList to finish.
		foreach(Task task in taskList)
		{
			task.Wait();
			Console.WriteLine("download completed");
		}
  }

      static void Main(string[] args)
      {
        TransferDownloadObjectModel m = new TransferDownloadObjectModel();
        /// Download objects from the folder in batches.
        m.GetObjectsFromFolder();
      }
    }
}

```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/GetObject.cs).
>

#### Sample 6: Suspending, resuming, or canceling a download

To suspend a download, use the code below:

[//]: # (.cssg-snippet-transfer-download-pause)
```cs
downloadTask.Pause();
```

To resume a suspended download, use the code below:

[//]: # (.cssg-snippet-transfer-download-resume)
```cs
downloadTask.Resume();
```

To cancel an upload, use the code below:

[//]: # (.cssg-snippet-transfer-download-cancel)
```cs
downloadTask.Cancel();
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferDownloadObject.cs).
>

## Simple Operations

### Downloading an object

#### Feature description

This API is used to download an object to the local file system.

#### Sample 1: Simple download of a single object

[//]: #	".cssg-snippet-get-object"

```cs
using COSXML.Model.Object;
using COSXML.Auth;
using System;
using COSXML;

namespace COSSnippet
{
    public class GetObjectModel {

      private CosXml cosXml;

      GetObjectModel() {
        CosXmlConfig config = new CosXmlConfig.Builder()
          .SetRegion("COS_REGION") // Set the default region. For abbreviations of COS regions, visit https://cloud.tencent.com/document/product/436/6224. 
          .Build();
        
        string secretId = "SECRET_ID";   // SecretId of the TencentCloud API. For more information about how to obtain the API key, see https://console.cloud.tencent.com/cam/capi.
        string secretKey = "SECRET_KEY"; // SecretKey of the TencentCloud API. For more information about how to obtain the API key, see https://console.cloud.tencent.com/cam/capi.
        long durationSecond = 600;          // Validity period of the request signature in seconds
        QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
          secretKey, durationSecond);
        
        this.cosXml = new CosXmlServer(config, qCloudCredentialProvider);
      }

      /// Download an object
      public void GetObject()
      {
        //.cssg-snippet-body-start:[get-object]
        try
        {
          // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
          string bucket = "examplebucket-1250000000";
          string key = "exampleobject"; // Object key
          string localDir = System.IO.Path.GetTempPath();// Local file directory
          string localFileName = "my-local-temp-file"; // Filename of the local file
          GetObjectRequest request = new GetObjectRequest(bucket, key, localDir, localFileName);
          // Set the progress callback
          request.SetCosProgressCallback(delegate (long completed, long total)
          {
            Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
          });
          // Execute the request
          GetObjectResult result = cosXml.GetObject(request);
          // Request succeeded
          Console.WriteLine(result.GetResultInfo());
        }
        catch (COSXML.CosException.CosClientException clientEx)
        {
          // Request failed
          Console.WriteLine("CosClientException: " + clientEx);
        }
        catch (COSXML.CosException.CosServerException serverEx)
        {
          // Request failed
          Console.WriteLine("CosServerException: " + serverEx.GetInfo());
        }
      }

      static void Main(string[] args)
      {
        GetObjectModel m = new GetObjectModel();
        /// Download an object
        m.GetObject();
      }
    }
}

```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/GetObject.cs).
>

#### Sample 2: Downloading an object to memory

[//]: #	".cssg-snippet-get-object"

```cs
using COSXML.Model.Object;
using COSXML.Auth;
using System;
using COSXML;

namespace COSSnippet
{
    public class GetObjectModel {

      private CosXml cosXml;

      GetObjectModel() {
        CosXmlConfig config = new CosXmlConfig.Builder()
          .SetRegion("COS_REGION") // Set the default region. For abbreviations of COS regions, visit https://cloud.tencent.com/document/product/436/6224. 
          .Build();
        
        string secretId = "SECRET_ID";   // SecretId of the TencentCloud API. For more information about how to obtain the API key, see https://console.cloud.tencent.com/cam/capi.
        string secretKey = "SECRET_KEY"; // SecretKey of the TencentCloud API. For more information about how to obtain the API key, see https://console.cloud.tencent.com/cam/capi.
        long durationSecond = 600;          // Validity period of the request signature in seconds
        QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
          secretKey, durationSecond);
        
        this.cosXml = new CosXmlServer(config, qCloudCredentialProvider);
      }

      /// Download the returned bytes data
      public void downloadToMem() {
        try
        {
          // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
          string bucket = "examplebucket-1250000000";
          string key = "exampleobject"; // Object key
        
          GetObjectBytesRequest request = new GetObjectBytesRequest(bucket, key);
          // Set the progress callback
          request.SetCosProgressCallback(delegate (long completed, long total)
          {
            Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
          });
          // Execute the request
          GetObjectBytesResult result = cosXml.GetObject(request);
          // Get content for the byte array
          byte[] content = result.content;
          // Request succeeded
          Console.WriteLine(result.GetResultInfo());
        }
        catch (COSXML.CosException.CosClientException clientEx)
        {
          // Request failed
          Console.WriteLine("CosClientException: " + clientEx);
        }
        catch (COSXML.CosException.CosServerException serverEx)
        {
          // Request failed
          Console.WriteLine("CosServerException: " + serverEx.GetInfo());
        }
      }

      // .cssg-methods-pragma

      static void Main(string[] args)
      {
        GetObjectModel m = new GetObjectModel();

        /// Download the object to memory
        m.downloadToMem();
        // .cssg-methods-pragma
      }
    }
}

```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/GetObject.cs).
>
