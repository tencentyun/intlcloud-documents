
### What should I do if the host name field is uneditable in IIS Manager?
When installing a certificate in IIS Manager, after you import a PFX certificate file and set **Type** to **https** during website binding, the **Host name** field becomes uneditable. You can use the following method to address this problem.

#### Scenario
If **Type** is set to **https** during certificate installation in IIS Manager, the **Host name** field becomes uneditable after the SSL certificate is selected, as shown in the following example.
![](https://main.qcloudimg.com/raw/7d2f27db6f9677c61b25331486d19c90.png)

#### Solution
1. Open the `applicationHost.config` file in `C:\Windows\system32\inetsrv\config\applicationHost.config`.
2. Make the following modifications:
>?
>- `tencent.com` is used as the domain name in the following example.
>- Replace `<binding protocol="https" bindingInformation="*:443:" />` in the following sample code with 
 `<binding protocol="https" bindingInformation="*:443:tencent.com" />`.
>- If you cannot modify the file directly, try modifying it as an admin, or copy and paste it to your desktop, modify it, and then replace the original file with the modified one.
>
```
<site name="example.tencent.com" id="8">
                <application path="/">
                    <virtualDirectory path="/" physicalPath="D:\web\tencent" />
                </application>
                <bindings>
                    <binding protocol="http" bindingInformation="*:80:example.tencent.com" />
                    <binding protocol="http" bindingInformation="*:80:www.tencent.com" />
                    <binding protocol="https" bindingInformation="*:443:" />   
                </bindings>
            </site>
```
3. After saving the modified file, bind the website again.

