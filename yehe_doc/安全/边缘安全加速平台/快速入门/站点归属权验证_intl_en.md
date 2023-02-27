
## When to Verify Your Site
1. If your site is added for the first time and via CNAME, you need to complete site verification.
2. If your site is already added by another account, you can reclaim your site once it’s verified.


## Method 1: DNS Verification
<dx-steps>
- Add the specified TXT record to the DNS settings at your DNS provider.
- Wait until the verification is completed. If the record does not take effect after a long time, you can click **Refresh** to trigger system verification.
- After the record takes effect, click **Verify**.
</dx-steps>

![](https://qcloudimg.tencent-cloud.cn/raw/7fae841267887ab1f89577186e9665a0.png)

## Method 2: File Verification
### For Windows users
<dx-steps>
- Go to the root directory of the server and create the verification directory `.well-known/teo-verification`.
- Click the file URL in step 2 to get the verification file and upload it to the verification directory.
- Copy the URL in step 3 to your browser and make sure that the resource is accessible.
- Click **Verify**.
</dx-steps>

<img src="https://qcloudimg.tencent-cloud.cn/raw/746be9b09061d0453987913720ce091f.png" width=700px>


### For Linux users
<dx-steps>
- Open a command window and get to the web server's root directory.
- Copy the code in step 2 to the command window and run it.
- Copy the URL in step 3 to your browser and make sure that the resource is accessible.
- Click **Verify**.
</dx-steps>

<img src="https://qcloudimg.tencent-cloud.cn/raw/6a6f7b0dfd7b795692358fa9b4b4aa79.png" width=700px>
