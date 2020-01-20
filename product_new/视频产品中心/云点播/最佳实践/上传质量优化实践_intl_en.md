## Introduction
No matter whether it is an upload from client or server, the following common quality problems may be encountered during file transfer:

1. Why is the file upload so slow?
2. How to speed up upload?
3. How to improve the upload success rate?
4. How to fix upload failures on mobile devices on weak networks?

The metrics that measure upload quality include upload speed and success rate.
- The upload speed often affects the user experience in the most intuitive manner. For example, if users upload a video of 50 MB which is not completed after half an hour, they may lose patience, leading to the possibility of customer loss.
- The upload success rate is a guarantee of service quality. After the initial upload fails due to network problems, the possibility of initiating the upload again by the user will decrease. The immediate consequence will be user complaints. Therefore, ensuring high upload success rate is the most fundamental requirement.
 
This document describes the causes of and solutions to problems in VOD upload scenarios. You can make comparisons based on your actual business scenarios and choose appropriate solutions to improve the upload quality.

## Things Affecting Upload Quality

### Network bandwidth
Network bandwidth refers to the amount of data that can be transferred in a time unit. The higher the bandwidth, the greater the amount of data uploaded per time unit, and the faster the upload. Upload is an end-to-end activity, so the bandwidth at both ends has an impact on the upload quality. The backend servers of VOD currently have sufficient bandwidth, so the upload quality often depends on the user-side bandwidth.

### Distance between user and storage center
The uploaded files eventually need to be stored in the storage center of VOD. After the user activates VOD, VOD will allocate **Chongqing** as the storage center by default. The distance between the user and the storage center affects the length of the network linkage.

For example, when a file is uploaded from Beijing to Chongqing, the linkage will be longer than that of uploading the same file from Chengdu to Chongqing, and the influencing factors will increase as the distance increases, eventually resulting in slower upload. Due to the long linkage, problems such as network jitter and packet loss during the transfer will also affect the upload success rate. For short linage, such problems may also occur, but their probability of occurrence is much lower than in long linkage. Shortening the distance between the user and the storage center is a key step in improving the upload quality.

### Weak network
Weak network refers to the state of a network with high latency and packet loss rate, which is generally called "slow internet access". This problem is very common in real life, such as in elevators and subway trains. The main cause is poor reception in the affected environment, which results in slow or failing data packet transfer. This scenario is particularly common in uploads from client, especially in the current era of mobile internet. Weak network has been plaguing many developers as the most difficult issue to overcome in improving the upload success rate.

## Solutions

### Concurrent upload
For scenarios where network bandwidth is insufficient, a direct solution is to apply for more bandwidth. However, on a network with limited bandwidth, how to fully utilize the bandwidth for uploads is a problem that needs to be solved. Concurrent upload can be divided into two levels:
- File level, i.e., multiple files are uploaded at the same time.
- Part level, i.e., multiple parts of a single file are uploaded at the same time.

At both levels, the bandwidth utilization can be improved by adjusting the corresponding number of concurrencies.

#### Concurrent file upload
Concurrent file upload refers to using multiple processes or threads to initiate upload operations simultaneously. At present, VOD does not provide related SDK packages for this mode. You can implement this feature by referring to the characteristics of specific programming languages. Below is a simple example based on the [VOD SDK for Java](https://intl.cloud.tencent.com/document/product/266/33914).

```
import com.qcloud.vod.VodUploadClient;
import com.qcloud.vod.model.VodUploadRequest;
import com.qcloud.vod.model.VodUploadResponse;

import java.util.ArrayList;
import java.util.List;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class Main {
    public static void main(String[] args) throws Exception {
        // Number of concurrencies
        Integer threadNumber = 20;
        // List of paths to files to be uploaded
        List<String> filePathList = new ArrayList<String>();

        // Add paths to files to be uploaded
        filePathList.add("/data/path1.mp4");
        filePathList.add("/data/path2.mp4");
        filePathList.add("/data/path3.mp4");

        // Create a thread pool
        ExecutorService pool = Executors.newFixedThreadPool(threadNumber);
        // Create an upload client
        VodUploadClient client = new VodUploadClient("your secretId", "your secretKey");

        // Concurrent upload
        for (String path : filePathList) {
            // Submit an upload task
            pool.submit(new UploadThread(client, path));
        }
    }
}

// Upload thread
class UploadThread implements Runnable {
    // Upload client
    private VodUploadClient uploadClient;
    // File path
    private String filePath;

    public UploadThread(VodUploadClient uploadClient, String filePath) {
        this.uploadClient = uploadClient;
        this.filePath = filePath;
    }

    public void run() {
        VodUploadRequest request = new VodUploadRequest();
        request.setMediaFilePath(filePath);
        try {
            // Execute upload
            VodUploadResponse response = uploadClient.upload("ap-guangzhou", request);
            System.out.println(response.getFileId());
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

#### Concurrent part upload
Concurrent part upload is applicable to uploading a large file in multiple parts simultaneously. The advantage of multipart upload lies in that a large file can be uploaded quickly. The SDK provided by VOD automatically selects simple upload or multipart upload based on the file size, eliminating your need to take care of every step in multipart upload. The number of concurrent parts of the file is specified by the `ConcurrentUploadNumber` parameter. For specific usage examples, please see the corresponding SDK. The SDKs that currently support this parameter include:

- [SDK for Java](https://intl.cloud.tencent.com/document/product/266/33914#.E6.8C.87.E5.AE.9A.E5.88.86.E7.89.87.E5.B9.B6.E5.8F.91.E6.95.B0)
- [SDK for Python](https://intl.cloud.tencent.com/document/product/266/33917#.E6.8C.87.E5.AE.9A.E5.88.86.E7.89.87.E5.B9.B6.E5.8F.91.E6.95.B0)
- [SDK for Go](https://intl.cloud.tencent.com/document/product/266/33919#.E6.8C.87.E5.AE.9A.E5.88.86.E7.89.87.E5.B9.B6.E5.8F.91.E6.95.B0)

### Nearby upload
Nearby upload refers to the ability to sense the location of the uploader and allocate the storage center closest to the uploader for file upload. For example, users in Chengdu will be allocated to the Chongqing rather than Shanghai region for upload.

The biggest benefit of the nearby upload capability is to shorten the transfer distance between the uploader and the server. This feature has the following advantages:
- Shortened transfer distance and improved upload speed.
- Improved stability and guaranteed success rate.

VOD natively supports nearby upload. You just need to simply confirm the following two points:

- **Activate multiple storage regions**
The storage region provided by VOD is **Chongqing** by default. If you want to take full advantage of the nearby upload capability, you need to activate regions desired for nearby upload in the console. For more information, please see [Upload Storage Settings](https://intl.cloud.tencent.com/document/product/266/18874). After multi-region storage is enabled, when a user uploads a file, VOD will identify the user's region by IP and intelligently allocate the region closest to the user out of the activated regions for upload.
- **Check whether the scheduling is proper**
If the storage regions of Chongqing and Shanghai are activated, and the user initiates an upload in Chengdu, the file will theoretically be uploaded to Chongqing through nearby scheduling. To confirm whether the scheduling is reasonable, you can get the `FileId` returned upon upload completion, and confirm it against the basic information (`basicInfo`) returned by the [DescribeMediaInfos API](/document/api/266/31763), which contains a `StorageRegion` field representing the storage region of the uploaded media file.

If the transfer experiences proxy or forwarding, and the region identified by VOD by IP is incorrect, you can forcibly specify a storage region for file uploads. For specific directions, please see:

- [Guide for Upload from Client](https://intl.cloud.tencent.com/document/product/266/33921)
- [Guide for Upload from Server](https://intl.cloud.tencent.com/document/product/266/33912)


### Pre-detection upload
Pre-detection upload is mainly a means to optimize various types of scenarios with network errors, such as network connection failure, timeout, and DNS hijacking. It is an effective mitigation solution offered by VOD for uploads on weak networks. The optimization strategy includes the following points:
- HTTPDNS is used to resolve domain names and get backend addresses to prevent DNS hijacking.
- The connectivity and upload speed in multiple regions are detected to determine the optimal upload target region.
- Tencent Cloud CDN acceleration network is utilized to provide reliable and stable transfer tunnels.

The pre-detection upload capability is currently applied to uploads from client, and the connection method is simple. For specific directions, please see the description of `pre-upload` in the corresponding SDK:

- [Upload SDK for Android](https://intl.cloud.tencent.com/document/product/266/33925)
- [Upload SDK for iOS](https://intl.cloud.tencent.com/document/product/266/33926)
