## Use Cases

CLS allows you to embed the [CLS console](https://console.cloud.tencent.com/cls) into an external system, so that you can conduct log search and analysis without logging in to the Tencent Cloud console. This feature offers the following benefits:

- Quickly integrate CLS search and analysis capabilities into an external service system (e.g., for business maintenance or operation).
- Easily share your log data with others without needing to manage additional Tencent Cloud sub-accounts.

## Demo Code for Login-Free Implementation

### Directions

1. On the [CAM](https://console.cloud.tencent.com/cam/overview) page, [create a CAM role](https://intl.cloud.tencent.com/document/product/598/19381), set the role entity to **Tencent Cloud Account**, and select **Allow the current role to access console**. Then, configure the target access permission for the CAM role, for example, the read-only policy permission `QcloudCLSReadOnlyAccess`, name it `CLSReadOnly`, and copy its `RoleArn` information.

2. On the [**Policies**](https://console.cloud.tencent.com/cam/policy) page, create a custom policy and select **Create by Policy Generator**. Then, select the JSON tag and enter the following information in **Policy Content**. Note that you need to replace `${YOUR_UIN}` with the account UIN (the resource content is the `RoleArn` of the created role; modify the policy name in case of any inconsistency). Click **Next** and set **Policy Name** to `PlayClsPolicy`.
```json
    {
        "version": "2.0",
        "statement": [
            {
                "effect": "allow",
                "action":[
                    "sts:AssumeRole"
                ],
                "resource": [
                    "qcs::cam::uin/${YOUR_UIN}:roleName/CLSReadOnly"
                ]
            }
        ]
    }
```
3. On the [**Create User**](https://console.cloud.tencent.com/cam/user/userType) page, select **Custom Creation** and set **Type** to **Access Resources and Receive Messages**, **Username** to **PlayClsUser**, **Access Method** to **Programming access**, and **User permissions** to `PlayClsPolicy` created in the previous step. After submitting the user creation operation, copy the generated `SecretId` and `SecretKey`.
4. Clone the **demo code** [cls-iframe-demo](https://github.com/TencentCloud/cls-iframe-demo) for login-free implementation. As instructed in the `ReadMe` content of the demo project, create the `.env` file in the root directory and enter the required parameters `RoleArn`, `SecretId`, and `SecretKey`.<br/>
>!Code leakage may lead to the leakage of `SecretId` and `SecretKey`, thereby affecting your account security. We recommend that you use a key in a more secure manner as instructed in the TencentCloud API key security solution and use a sub-account key with the least privilege.
>
Check the effect after running the project as instructed in the `ReadMe` document of the demo program for login-free implementation.
>! This example does not include the authentication logic of external systems. After deployment, all users (even if they have not logged in to Tencent cloud) can view the data under their accounts with the role permissions configured in the example. To ensure data privacy and security, add the authentication logic of external systems or restrict their access to the private network only to ensure that only authorized users can view the page.
5. Concatenate the destination login-free address `s_url` of CLS (optional). If you enter the obtained address in the configuration file of the login-free project, access to the login-free service will be automatically redirected to this address.
   **The basic address of the CLS search and analysis page:**
```plaintext
https://console.cloud.tencent.com/cls/search?region=<region>&topic_id=<topic_id>
```
**Parameters in the CLS search and analysis page URL**:
<table>
<tr><th>Parameter</th><th>Required</th><th>Type</th><th>Description</th></tr>
<tr><td>region</td><td>Yes</td><td>String</td><td>Region abbreviation, e.g., ap-shanghai for Shanghai region. For other available region abbreviations, see <a href="https://intl.cloud.tencent.com/document/product/614/18940">Available Regions</a></td></tr>
<tr><td>topic_id</td><td>No</td><td>String</td><td>Log topic ID</td></tr>
<tr><td>logset_name</td><td>No</td><td>String</td><td>Logset name</td></tr>
<tr><td>topic_name</td><td>No</td><td>String</td><td>Log topic name</td></tr>
<tr><td>time</td><td>No</td><td>String</td><td>Time range for log search. Format example:
2021-07-15T10:00:00.000,2021-07-15T12:30:00.000</td></tr>
<tr><td>queryBase64</td><td>No</td><td>String</td><td>Search and analysis statement, which is base64Url-encoded</td></tr>
<tr><td>hideWidget</td><td>No</td><td>Boolean</td><td>Indicates whether to hide agent/documentation button in the bottom-right corner. `true`: Yes; `false`: No (default)</td></tr>
<tr><td>hideTopNav</td><td>No</td><td>Boolean</td><td>Indicates whether to hide the top navigation bar in the Tencent Cloud console. `true`: Yes; `false`: No (default)</td></tr>
<tr><td>hideLeftNav</td><td>No</td><td>Boolean</td><td>Indicates whether to hide the left navigation bar in the Tencent Cloud console. `true`: Yes; `false`: No (default)</td></tr>
<tr><td>hideTopicSelect</td><td>No</td><td>Boolean</td><td>Indicates whether to hide the log topic selection controls (including the region, logset, and log topic controls). `true`: Yes; `false`: No (default)</td></tr>
<tr><td>hideHeader</td><td>No</td><td>Boolean</td><td>Indicates whether to hide the log topic selection control and the row where the control resides. `true`: Yes; `false`: No (default). This parameter is valid only when `hideTopicSelect` is `true`.</td></tr>
<tr><td>hideTopTips</td><td>No</td><td>Boolean</td><td>Indicates whether to hide the announcements on the top of the page. `true`: Yes; `false`: No (default)</td></tr>
<tr><td>hideConfigMenu</td><td>No</td><td>Boolean</td><td>Indicates whether to hide the log topic configuration management menu. `true`: Yes; `false`: No (default)</td></tr>
<tr><td>hideLogDownload</td><td>No</td><td>Boolean</td><td>Indicates whether to hide the raw log download button. `true`: Yes; `false`: No (default)</td></tr>
</table>
>! You can specify the log topic to search using URL parameters in either the following modes:
> - topic_id: use the log topic ID to specify the log topic to search.
> - logset_name+topic_name: use the logset name and log topic name to specify the log topic to search. Note that if the logset or log topic name changes, the URL adopting this mode will become invalid.
>
>If `topic_id`, `logset_name`, and `topic_name` exist at the same time, `topic_id` prevails.
>

	<b>Relationship between hidden parameters and page modules</b>:
	<img src="https://qcloudimg.tencent-cloud.cn/raw/d4a78b2948d4018b48d93a7078bbf233.png" style="width: 80%"/>   


​	
## Self-Development for Login-Free Implementation

### Directions

>!Note: Code leakage may lead to the leakage of `SecretId` and `SecretKey`, thereby affecting your account security. We recommend that you use a key in a more secure manner as instructed in the TencentCloud API key security solution and use a sub-account key with the least privilege.

1. Configure the CLS read-only role, custom policy of the target role, and sub-account bound to the custom policy as instructed in **Demo Code for Login-Free Implementation**. Then, save the `RoleArn`, `SecretId`, and `SecretKey` information.
2. Get the destination login-free address `s_url` as needed as instructed in **Demo Code for Login-Free Implementation**. 
3. Repeat the following steps every time you need to open a login-free page.
4. Call the [STS AssumeRole](https://intl.cloud.tencent.com/document/product/1150/49456) API with the obtained key to apply for the temporary key of the target role.
5. Generate the login signature information with the obtained temporary key.
    1. Sort parameters to be signed.
        Sort parameters to be signed listed below in ascending alphabetical or numerical order. That is, sort the parameters by their first letters, then by their second letters if their first letters are the same, and so on. You can do this with the aid of sorting functions in programming languages, such as the ksort function in PHP.
        
        <table>
        <thead>
        <tr>
        <th align="left">Parameter</th>
        <th align="left">Required</th>
        <th align="left">Type</th>
        <th align="left">Description</th>
        </tr>
        </thead>
        <tbody><tr>
        <td align="left">action</td>
        <td align="left">Yes</td>
        <td align="left">String</td>
        <td align="left">Action; fixed as `roleLogin`</td>
        </tr>
        <tr>
        <td align="left">timestamp</td>
        <td align="left">Yes</td>
        <td align="left">Int</td>
        <td align="left">Current timestamp</td>
        </tr>
        <tr>
        <td align="left">nonce</td>
        <td align="left">Yes</td>
        <td align="left">Int</td>
        <td align="left">Random integer. Value range: 10000-100000000</td>
        </tr>
        <tr>
        <td align="left">secretId</td>
        <td align="left">Yes</td>
        <td align="left">String</td>
        <td align="left">Temporary AK returned by STS</td>
        </tr>
        </tbody></table>
        
    2. Combine the parameters.
        Combine the above sorted parameters into the form of "parameter name=parameter value". Example:
        ```plaintext
        action=roleLogin&nonce=67439&secretId=AKI***PLE&timestamp=1484793352
        ```
    3. Concatenate a signature string.
        Construct a signature string in the format of “request method + request CVM + request path + ? + request string”.
        <table>
        <thead>
        <tr>
        <th align="left">Parameter</th>
        <th align="left">Required</th>
        <th align="left">Description</th>
        </tr>
        </thead>
        <tbody><tr>
        <td align="left">Request CVM and path</td>
        <td align="left">Yes</td>
        <td align="left">Fixed as <code>cloud.tencent.com/login/roleAccessCallback</code></td>
        </tr>
        <tr>
        <td align="left">Request method</td>
        <td align="left">Yes</td>
        <td align="left">GET or POST</td>
        </tr>
        </tbody>
        </table>
    
        <h4>Sample signature string</h4>
    
        ```plaintext
            GETcloud.tencent.com/login/roleAccessCallback?action=roleLogin&nonce=67439&secretId=AKI***PLE&timestamp=1484793352
        ```
    
    4. Generate a signature string.
    
        Currently, you can sign a string using HMAC-SHA1 or HMAC-SHA256. The sample code in PHP is as follows:
        ```php
        $secretKey = 'Gu5***1qA';
        $srcStr    = 'GETcloud.tencent.com/login/roleAccessCallback?action=roleLogin&nonce=67439&secretId=&timestamp=1484793352';
        $signStr   = base64_encode(hash_hmac('sha1', $srcStr, $secretKey, true));
        echo $signStr;
        ```
    
         <h4>Sample code for PHP</h4>
    
          ```php
          $secretId  = "AKI***";            //Temporary AK returned by STS
          $secretKey = "Gu5***PLE";         //Temporary SecretKey returned by STS
          $token     = "ADE***fds";         //Security Token returned by STS
          $param["nonce"]     = 11886;      //rand(10000,100000000);
          $param["timestamp"] = 1465185768; //time();
          $param["secretId"]  = $secretId;
          $param["action"]    = "roleLogin";
          ksort($param);
          $signStr = "GETcloud.tencent.com/login/roleAccessCallback?";
          foreach ( $param as $key => $value ) {
              $signStr = $signStr . $key . "=" . $value . "&";
          }
          $signStr   = substr($signStr, 0, -1);
          $signature = base64_encode(hash_hmac("sha1", $signStr, $secretKey, true));
          echo $signature.PHP_EOL;
          ```



6. Combine your login information and destination page URL into a login URL.
**Parameter values need to be URL-encoded.**

    ```plaintext
    https://cloud.tencent.com/login/roleAccessCallback?
    algorithm=<Encryption algorithm for signing. Currently, only `sha1` and `sha256` are supported. `sha1` will be used by default if the parameter is not specified.>
    &secretId=<secretId for signing>
    &token=<Temporary key token>
    &nonce=<nonce for signing>
    &timestamp=<Timestamp for signing>
    &signature=<Signature string>
    &s_url=<Destination URL after login>
    ```

7. Use the final URL to access the embedded CLS page of the Tencent Cloud console. The sample below is a URL to the CLS search analysis page:

    ```plaintext
    https://cloud.tencent.com/login/roleAccessCallback?nonce=52055817&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fcls%2Fsearch%3Fregion%3Dap-guangzhou%26start_time%3D2020-05-26%25252014%25253A01%25253A18%26end_time%3D2020-05-26%25252014%25253A16%25253A18&secretId=AKID-vHJ7WPHcy_RVIOm-QTIktXOf9S9z_k_JackOp3dyQPJwmDrNLQJuiNuw9******&signature=eXeWaDn6iJlcPp1sqqGd6m9%2FQk****&timestamp=1592455018&token=5e4vuBHL7fBQPi1V9fvSINw4Vu7PSr9Ic3de78b86109c171eb4e3ea27c137c1fIWKU8JC-LO01L87sIYlfTSaHHXeHcqim7Jg9hBuN2nbdfgeBUPXhmpyAk4G6e9bHFZ-7yNRig7Y33CQHxh6jOesP4VfhRzQprWGRtC5No1ty******-aoj_WJhA55oyvqaqxw2jtTdh8nx9OjJr3tlbIa9oJe7aZYoPbdpFqrF6ZjlCPPap2yQB_SkUsWwDl_9BrK2Km3U2IocdvQ7QxrW0ts1aiBi7xtTSJRcfkBYPYEV_YoJrtkhYW3E4L47imA1bfVAjM9F5uKWzVzsDGDT0aCUU9mqdb4vjJrY8tm-wJKKEe8eiyY9EbkH3VWnFV2YocYNDJqFyjKOWR******
    ```

## How It Works
The login-free solution is implemented based on [STS](https://intl.cloud.tencent.com/document/product/1150/47143).

The login flowchart is as shown below:<br/>
![img](https://main.qcloudimg.com/raw/c04840e707a3e9aca812d58d9414faea.png)