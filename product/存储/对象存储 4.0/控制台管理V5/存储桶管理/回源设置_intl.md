## Product Introduction

Origin-pull settings are mainly used for such scenarios as live migration of data and redirection of specific requests. For example, when the object requested by a user does not exist in the bucket, or a specific request needs to be redirected, you can set the origin server address.

As of July 2017, the origin servers can be set to IP ranges of China Telecom, China Mobile, China Unicom and Great Wall Broadband. Other ISPs will be supported soon.
![](//mc.qcloudimg.com/static/img/c6e4e6281c47210b8dd97ba3a2a7cb9f/image.png)

## Procedure

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos4/index), and then select the left pane **Bucket List** to go to the Bucket List page. Click the bucket (such as example) for which you want to configure origin-pull to enter the bucket.
   ![](//mc.qcloudimg.com/static/img/b51d5a77d53c3416324ea3eb283c788c/image.png)
2. Click **Basic Configuration** to go to the Basic Configuration page of the bucket, locate the origin-pull settings, and then click **Edit** to go into the editing mode.
   ![](//mc.qcloudimg.com/static/img/5cd4e9d94d871eb4b58714c0d993fe52/image.png)
3. Change the status to **Enabled**, enter the origin server address (such as abc.example.com), and then click **Save**.
   ![](//mc.qcloudimg.com/static/img/31950daad98cbfc7dbbbedf4673ac221/image.png)

> **Notes:**

- **After enabling origin-pull, be sure to enter the origin server's domain name or IP address, otherwise the settings cannot be saved.**
- **In "Origin Server Address", only enter the domain name without "http://" or IP address. You can also add the port number in the format of ":[port]".**

```
For example (the following example is for reference only):
abc.example.com
abc.example.com:8080
10.10.10.10
10.10.10.10:8080
```

- **As of July 2017, the console only supports origin-pull over HTTP. Origin-pull over HTTPS is not supported.**

## Example

**Background**
A user with APPID of 1250000000 created a bucket named "example", and enabled the CDN accelerated domain name:

```
example-1250000000.file.myqcloud.com```
Set the origin server address for the bucket to:
```

abc.example.com

```
Store the image 1.jpg at the origin server (`http://abc.example.com`).

**The first access from the client:**
```

http://example-1250000000.file.myqcloud.com/1.jpg

```
When COS finds that the object cannot be hit, it returns the HTTP status code 302 to the client and is redirected to 
```

http://abc.example.com/1.jpg

```
Then the origin server provides the object to the client to ensure the access, and COS copies 1.jpg from the origin server and saves it to the root directory of the bucket "example".

**The second access**
```

http://example-1250000000.file.myqcloud.com/1.jpg

```
COS directly hits the object 1.jpg in the root directory and returns it to the client.
```
