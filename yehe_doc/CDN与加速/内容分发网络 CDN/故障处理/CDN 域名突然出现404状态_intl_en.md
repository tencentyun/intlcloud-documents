## Error Description

 What should I do if a 404 status code is returned by a CDN domain name?



## Cause

1. The origin server is exceptional.
2. The configuration of the origin server information and host header in the console are changed.



## Solution

1. Check whether your origin server works properly.
2. Check whether configuration of the origin server information and host header in the console are correct.



## Troubleshooting Procedure

[](id:step1)

1. Check whether your origin server is exceptional.

   - If it is so, fix the origin server.
   - If it is not, go to [Step 2](#step2).
     [](id:step2)

2. Check the configuration of the origin server information and host header in the console.
   Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management**, find the corresponding domain name, select **Basic Configuration** > **Origin Server Information**, and check whether the settings of **Origin address** and **Host header** are correct.

   - Origin type:

   <table>
   <thead>
   <tr>
   <td><strong>Customer origin server</strong></td>
   <td>If you select customer origin server, you should provide an IP address or domain name of the business server that can be normally accessed.</td>
   </tr>
   </thead>
   <tbody><tr>
   <td><strong>COS origin server</strong></td>
   <td>If you select a bucket in COS as the origin server, select **Default Domain** or **Static Website** based on your bucket configuration. If your bucket is private, authorize CDN and enable origin-pull authentication to turn on private bucket access.</td>
   </tr>
   <tr>
   <td><strong>Third-Party object storage</strong></td>
   <td>If you select a third-party object storage service, enter the valid bucket access address as the origin server. Currently, AWS S3 and Alibaba Cloud OSS are supported. If the bucket is private, enter a valid key and enable origin-pull authentication to turn on private bucket access.</td>
   </tr>
   </tbody></table>

   - Host header:
     It refers to the domain name accessed on the origin server by a CDN node during origin-pull. It defaults to the acceleration domain name. If a wildcard domain name is connected, it will be the actual access subdomain name by default and can be customized. (**Note:** it cannot be modified if the origin server type is COS or a third-party object storage service).

For more information on origin server configuration, see [Origin Server Configuration](https://intl.cloud.tencent.com/document/product/228/6289).
