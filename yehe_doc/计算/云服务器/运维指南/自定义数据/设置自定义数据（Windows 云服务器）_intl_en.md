## Introduction

While you create a CVM instance, you have the option to define a script as **Custom Data** and use it to customize your instance configuration. When the instance starts up for the firs time, that custom data is passed on and executed. If you purchased multiple CVM instances, all instance will execute the script upon first launch.
This article describes how to define a PowerShell script and use it to configure a Windows CVM instance.

## Considerations

- Windows operating systems that support custom data include:
 - Windows Server 2019 Datacenter Edition 64-bit Chinese/English version
 - Windows Server 2016 Datacenter Edition 64-bit Chinese/English version
 - Windows Server 2012 R2 Datacenter Edition 64-bit Chinese/English version
- The script is executed when and only when the instance starts up for the first time.
- Before Base64 encoding, the size of the custom data cannot exceed 16 KB.
- Custom data is Base64 encoded and then passed. If you want a script file in its orginal form, do not select **The entry is Base64-encoded text**.
- The custom configurations you defined in the custom data script take time to execute. We recommend that you wait for the configurations to complete and verify if the results.
- Use the PowerShell tag, such as &lt;powershell&gt;&lt;/powershell&gt; to declare the content of the Windows PowerShell script.

## Directions

### Preparing a script

Prepare a script that suit your needs:

<span id="PowerShellScript"></span>
#### PowerShell script
Use the PowerShell tags to surround script content.
For example, if you want to use the script to create a file called `tencentcloud.txt` with the content of “Hello Tencent Cloud.” in the C: drive, use the following tags:
```
<powershell>
"Hello Tencent Cloud." | Out-File  C:\tencentcloud.txt
</powershell>
```

<span id="Base64Script"></span>
#### Encoding the script with Base64

1. Run the following command to create a PowerShell script named “script_text.ps1”.
```
vi script_text.ps1
```
2. Press **i** to switch to the editing mode, enter the following content, and save.
```
<powershell>
"Hello Tencent Cloud." | Out-File  C:\tencentcloud.txt
</powershell>
```
3. Run the following command to encode **script_text.ps1** with Base64.
```
base64 script_text.ps1
```
The following information is returned:
```
PHBvd2Vyc2hlbGw+CiJIZWxsbyBUZW5jZW50IENsb3VkLiIgfCBPdXQtRmlsZSAgQzpcdGVuY2VudGNsb3VkLnR4dAo8L3Bvd2Vyc2hlbGw+Cg==
```

### Passing the script

We provide multiple methods to launch an instance. The following are the most used methods:
- [Using the official website or the console](#Consoletrans)
- [Using APIs](#APItrans)

<span id="Consoletrans"></span>
#### Using the official website or the console

1. Use [Creating an Instance](https://intl.cloud.tencent.com/document/product/213/4855) as an reference and create a CVM instance. Click **Advanced Configuration** in **4. Configure Security Group and CVM**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/28baf2764488ecfaf5bbac791cec7ea3.png)
2. In **Advanced Configuration**, enter script content in the **Custom Data** text box.
 - PowerShell script: enter the script content you entered in [PowerShell script](#PowerShellScript) in its original form.
 - Base64 encoded script: select **The entry is Base64-encoded text**, and enter the encoded script content you encoded in [Encoding the script with Base64](#Base64Script), as shown in the following figure:
 ![](https://main.qcloudimg.com/raw/0b6b594f174568ca7d3312821c0571ed.png)
4. Follow the instructions and complete the CVM creation.

<span id="APItrans"></span>
#### Using APIs

If you choose to create an CVM instance using Tencent Cloud APIs, you can assign the the encoded result returned in [Encoding the script with Base64](#Base64Script) to the UserData parameter of RunInstances.
The following is an sample CVM creation request with UserData:
```
https://cvm.tencentcloudapi.com/?Action=RunInstances
  &Version=2017-03-12
  &Placement.Zone=ap-guangzhou-2
  &ImageId=img-pmqg1cw7
  &UserData=PHBvd2Vyc2hlbGw+CiJIZWxsbyBUZW5jZW50IENsb3VkLiIgfCBPdXQtRmlsZSAuXHRlbmNlbnRjbG91ZC50eHQKPC9wb3dlcnNoZWxsPgo=
  &<Common request parameter>
```

### Verifying custom data configurations

1. Log in to the CVM instance.
2. Open the C: drive, and check whether `tencentcloud.txt` exists.
If it does, the configuration is successful, as shown in the following figure:
![](https://main.qcloudimg.com/raw/9f94ec922111734a489b9730d66168c3.png)


