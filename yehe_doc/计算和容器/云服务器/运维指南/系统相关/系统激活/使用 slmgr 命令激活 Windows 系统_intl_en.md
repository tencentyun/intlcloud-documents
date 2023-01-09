## Overview
This document describes how to activate the operating system in a Windows CVM instance.



<dx-alert infotype="explain" title="">
This document is intended only for Windows Server public images provided by Tencent Cloud. It is not applicable for custom images or images imported from external sources.
</dx-alert>




## Directions
1. Log in to the Windows CVM instance. For more information, see [Logging in Using Standard Method (Recommended)](https://intl.cloud.tencent.com/document/product/213/41018).
2. Right-click in the lower left corner of the operating system's desktop, <img src="https://qcloudimg.tencent-cloud.cn/raw/0cfefcbe7474bf6b532a589c53314d5b.png" style="margin:-3px 0px">, and select **Windows PowerShell (Admin)** from the pop-up menu.
3. In the PowerShell window, run the following commands in sequence to activate the operating system.
```
slmgr /upk
```
```
slmgr /ipk <ProductKey>
```
```
slmgr /skms kms.tencentyun.com
```
```
slmgr /ato
```
[](id:ProductKey)`<ProductKey>` in the `slmgr /ipk <ProductKey>` command should be replaced as follows:
   - Windows Server 2008 R2 Enterprise: `489J6-VHDMP-X63PK-3K798-CPX3Y`
   - Windows Server 2012 R2 Datacenter: `W3GGN-FT8W3-Y4M27-J84CP-Q3VJ9`
   - Windows Server 2016: `CB7KF-BWN84-R7R2Y-793K2-8XDDG`
   - Windows Server 2019: `WMDGN-G9PQG-XVVXX-R3X43-63DFG`
   - Windows Server 2022：`WX4NM-KYWYW-QJJR4-XV3QB-6VM33`
For more information, see [Key Management Services (KMS) client activation and product keys](https://docs.microsoft.com/zh-cn/windows-server/get-started/kms-client-activation-keys).
4. Restart the CVM instance to make the settings take effect. For more information, see [Restarting Instances](https://intl.cloud.tencent.com/document/product/213/4928).


## FAQs
In some scenarios where the Windows operating system is not activated, the system memory of a high-end server will be limited to 2 GB, and the rest of the memory will be restricted in the form of "hardware reserved memory". The reason is that the `HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\ProductOptions` registry key is damaged. You can run the following command to determine whether to reactivate the system.
```
(Get-ItemProperty HKLM:\SYSTEM\CurrentControlSet\Control\ProductOptions\).ProductPolicy.count
```
 - If the returned result is above 10,000, such as 56184, there is no need to reactivate the system.
 - If the returned result is "Unactivated value: 1960", refer to the following methods to solve the problem.
<dx-tabs>
::: Method 1
1. Run the following command to activate the operating system.
```
slmgr.vbs /ipk <ProductKey>
```
<dx-alert infotype="explain" title="">
Replace `<ProductKey>` according to the actual operating system version as detailed in [ProductKey](#ProductKey).
</dx-alert>
2. After the command is executed, run the `(Get-ItemProperty...` command again for verification. The returned value is 56184.
3. Restart the CVM instance to make the settings take effect. For more information, see [Restarting Instances](https://intl.cloud.tencent.com/document/product/213/4928).
4. Run the following command to activate the operating system.
```
slmgr.vbs /ato
```

:::
::: Method 2
1. Run the following command to fix it.
```
slmgr.vbs /rilc 
```
2. After the command is executed, run the `(Get-ItemProperty...` command again for verification, and the returned value is still 1960.
3. Run the following command to activate the operating system and restarting CVM.
```
slmgr.vbs /ato
```

:::
::: Method 3
1. Uninstall any MSI program.
2. Run the `(Get-ItemProperty...` command again for verification, and the returned value may change. However, after the system is restarted, the memory limit is still 2 GB.
2. Run the following command to activate the operating system and restarting CVM.
```
slmgr.vbs /ato
``` 
:::
</dx-tabs>

