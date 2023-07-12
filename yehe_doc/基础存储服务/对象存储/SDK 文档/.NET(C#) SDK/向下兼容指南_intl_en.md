## Overview

Starting from V5.4.23, the .NET SDK has been compatible with .NET Framework 4.0 and earlier versions. You can run it by adding the `COSXML-Compatible.dll` library.

>! 
> - Integration with NuGet might not be supported in compatible environments. For more information about the integration, see **Adding Reference**.
> - All advanced APIs (e.g., advanced upload and checkpoint restart download) are not available in `COSXML-Compatible.dll`.
> 

## Adding Reference

Currently, you can only add the .dll file manually as follows:
1. Download `COSXML-Compatible.dll` at [Releases](https://github.com/tencentyun/qcloud-sdk-dotnet/releases).
2. In your Visual Studio project, click **Project** > **Add Reference** > **Browse** > **COSXML-Compatible.dll** to add the .NET SDK.

## How to Use

You can use it in the same way as the general .NET SDK, except that you need to note the following:

1. If you access COS via HTTPS with .NET Framework 4.0 or an earlier version, issues may occur. If a request over HTTPS fails, you can disable it and try again.
2. The compatible .NET does not support the advanced APIs below. You can access COS with other APIs.

| Namespace   | Class          | Description        |
| ----------------- | ---------------------------- | ------------------------------- |
| COSXML.Transfer   | COSXMLCopyTask               | Advanced copy API           |
| COSXML.Transfer   | COSXMLDownloadTask           | Advanced download API   |
| COSXML.Transfer   | COSXMLTask                   | Advanced API abstract class |
| COSXML.Transfer   | COSXMLUploadTask             | Advanced upload API  |
| COSXML.Transfer   | TransferManager              | Transfer task control class    |

## Unknown Issues

The compatible package is still in the prerelease phase. If you encounter any other issues not listed above, please submit an [issue](https://github.com/tencentyun/qcloud-sdk-dotnet/issues) on GitHub.
