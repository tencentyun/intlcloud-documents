
### What should I do when the host name field is grayed out and cannot be modified for HTTPS on the IIS manager?
When you install an SSL certificate on an IIS manager, `Host name` is grayed out and cannot be modified if you set `Type` to `https` during site binding after importing the PFX certificate file.

#### Scenario
The problem is shown in the following figure.
![](https://main.qcloudimg.com/raw/7d2f27db6f9677c61b25331486d19c90.png)

#### Solution
1. On Windows Server 2008 (64-bit), open the `applicationHost.config` file at `C:\Windows\system32\inetsrv\config\`.
2. Modify the file content as follows
>
(assume that the domain name is `cloud.com`):
>- Change `<binding protocol="https" bindingInformation="*:443:" />` to the following:
 `<binding protocol="https" bindingInformation="*:443:cloud.com" />`
>- If you cannot modify the file, try the admin permission, or copy the file to the desktop for modification and replace the file in the original directory with the modified one.
>
```
<site name="example.cloud.com" id="8">
                <application path="/">
                    <virtualDirectory path="/" physicalPath="D:\web\cloud" />
                </application>
                <bindings>
                    <binding protocol="http" bindingInformation="*:80:example.cloud.com" />
                    <binding protocol="http" bindingInformation="*:80:www.cloud.com" />
                    <binding protocol="https" bindingInformation="*:443:" />   
                </bindings>
            </site>
```
3. After the file is saved, add the website binding again.

