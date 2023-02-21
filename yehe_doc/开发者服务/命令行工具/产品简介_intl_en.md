
## Overview	
Tencent Cloud Command Line Interface (TCCLI) is a unified tool for managing Tencent Cloud resources. With TCCLI, you can quickly and easily call Tencent Cloud APIs to manage your resources and automate them through scripts for diversified combination and reuse.

<dx-alert infotype="explain" title="">
 
- You can see [tencentcloud-tccli](https://github.com/TencentCloud/tencentcloud-cli) on GitHub to learn more about the tool. If you encounter any issues when you use the tool, please submit them at [GitHub Issues](https://github.com/TencentCloud/tencentcloud-cli/issues/new).

</dx-alert>

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer (recommended)
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn"><i class="rno-icon-explorer"></i>Click to debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                API Explorer automatically generates TCCLI commands, making it easier for you to use TCCLI.
            </div>
        </div>
    </div>
</div>

## Features
### Integrating multiple products

TCCLI integrates all Tencent Cloud products that support TencentCloud API, and allows you to configure and manage the products. For example, you can use TCCLI to create and operate a Cloud Virtual Machine (CVM) instance, create a Cloud Block Storage (CBS) disk and view its usage, and create a Virtual Private Cloud (VPC) and add resources to it. All operations that can be performed on console pages can be performed by running commands in TCCLI.

TCCLI allows you to manage Tencent Cloud resources on a non-graphic interface.

### Supporting multiple accounts
TCCLI allows you to set multiple accounts and rapidly switch between these accounts.

### Supporting multiple platforms
TCCLI supports Windows, macOS, Linux, and Unix to meet the requirements of different developers. Command auto-completion is available for Linux and Unix systems.
To install TCCLI, first install Python on your operating system, and then run the corresponding pip command. TCCLI commands are consistent across all operating systems. Therefore, you can use the commands in the same way on Linux and Windows.

### Supporting multiple output formats
TCCLI supports multiple output formats, including text, JSON, and table.

- text: The output is displayed as text, with each line representing a record. Different records are separated with spaces. This format is suitable for obtaining a list of resources that can be saved as text or converted into a table.
- JSON: The output is in JSON format, which is suitable for secondary development coding. You can parse the output to obtain the information you want.
- table: The output is a table, which is intuitive and suitable for using the command line tool to manage cloud resources.

## Products Supporting TCCLI
All TencentCloud API 3.0 products and their APIs support TCCLI. You can view the products at [APIs](https://www.tencentcloud.com/document/api/213/).
![](https://staticintl.cloudcachetci.com/yehe/backend-news/8zH8964_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221222102318.png)