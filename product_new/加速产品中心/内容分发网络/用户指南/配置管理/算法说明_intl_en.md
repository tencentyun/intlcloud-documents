## Feature Overview
Contents distributed by CDN are public resources by default. To prevent malicious users from stealing your contents for profits, CDN supports the configuration of URL authentication.

## Algorithm Description
### TypeA
- Access URL format: `http://DomainName/Filename?sign=timestamp-rand-uid-md5hash`
- Algorithm Description:
  - timestamp: A decimal timestamp in UNIX format.
  - rand: A random string consisting of 0 to 100 uppercase or lowercase letters and digits.
  - uid: 0.
  - md5hash: MD5 (file path-timestamp-rand-uid-custom key).

> !If the original request URL is `http://www.test.com/test/1.jpg`, then the file path used for MD5 calculation will be `/test/1.jpg`.

### TypeB
- Access URL format: `http://DomainName/timestamp/md5hash/FileName`
- Algorithm description:
  - timestamp: A timestamp in the format of `YYYYMMDDHHMM`.
  - md5hash: MD5 (custom key+timestamp+file path).

> !If the original request URL is `http://www.test.com/test/1.jpg`, then the file path used for MD5 calculation will be `/test/1.jpg`.

### TypeC
- Access URL format: `http://DomainName/md5hash/timestamp/FileName`
- Algorithm Description:
  - timestamp: A hex timestamp in UNIX format.
  - md5hash: MD5 (custom key + file path + timestamp).

> !If the original request URL is `http://www.test.com/test/1.jpg`, then the file path used for MD5 calculation will be `/test/1.jpg`.

### TypeD
- Access URL format: `http://DomainName/FileName?sign=md5hash&t=timestamp`
- Algorithm Description:
  - timestamp: A decimal or hex timestamp in UNIX format.
  - md5hash: MD5 (custom key + file path + timestamp).

> !If the original request URL is `http://www.test.com/test/1.jpg`, then the file path used for MD5 calculation will be `/test/1.jpg`.

## Configuration Guide
1. Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Domain Management** on the left sidebar to enter the management page. Find the desired domain name and click **Manage** in the "Operation" column.
![img](https://main.qcloudimg.com/raw/dec7f22ef91890a5d39b969d01437361.png)
2. Click **Security Configuration** and you can see the **Authentication Configuration** module, which is disabled by default.
![image](https://main.qcloudimg.com/raw/7704e3f764d2e99ed61504783bb36b42.png)
3. In the **Authentication Configuration** module, click *Configuration** to enable authentication. Currently, three types can be configured:
> !Currently, TypeB cannot be selected due to feature upgrade.
> 
![img](https://main.qcloudimg.com/raw/e011bc76fafa307013956f9b4f1e3b4c.png)
4. After selecting the type, you can configure authentication parameters. The following takes **TypeA** as an example:
   - Authentication Key: Select a specified string as the authentication key based on your business conditions.
   - Signature Parameter: Set a parameter name with a signature string. The value is **sign** by default and can be customized.
   - Effective Time: The server compares the **timestamp** (obtained by parsing the signature) plus the effective time with the current time to determine whether the signature is effective.

<img src="https://main.qcloudimg.com/raw/abf68477508155f85d888668fc6b2b99.png"  style="margin: 0px 0px 0px 30px;">

5. After parameter configuration is completed, specify the authentication range and object.
![img](https://main.qcloudimg.com/raw/4c89dd4fc8aab848a3ada068794c2977.png)

## Authentication Calculator
> ?You can use the authentication calculator to check whether the request path and signature are correct.
> 
In the **Authentication Configuration** module, click *Configuration.** Currently, three types can be configured. Select the type, configure the authentication parameters, and then determine the authentication URL. The following takes **TypeA** as an example:
![img](https://main.qcloudimg.com/raw/8d090ea7b5358120a1e233245e06f885.png)
> !
> - Currently, TypeB cannot be selected due to feature upgrade.
> - If the access path has a URL with Chinese characters, you need to decode the URL first before performing the authentication configuration.

