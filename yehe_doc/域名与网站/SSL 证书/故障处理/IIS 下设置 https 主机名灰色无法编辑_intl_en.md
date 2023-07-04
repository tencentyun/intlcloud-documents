## Symptom

During certificate installation with IIS Manager, **Host name** is grayed out and cannot be edited if you set **Type** to **https** when adding site binding after importing the PFX certificate file.

## Possible causes

Windows Server 2008 does not support the operation, and you need to modify the corresponding file.

## Solutions
1. Open the `applicationHost.config` file in the `C:\Windows\system32\inetsrv\config\applicationHost.config` directory.

2. Modify the file content as follows:
   

   > **Notes**
   > 
   >   - Take the `tencent.com` domain as an example.
   >   - Change `<binding protocol="https" bindingInformation="*:443:" />` to `<binding protocol="https" bindingInformation="*:443:tencent.com" />`.
  
   >   - If you cannot modify the file directly, modify it with the admin permission, or copy the file to the desktop for modification and replace the original file.

   ``` xml
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
3. Add site binding again after saving the file.
