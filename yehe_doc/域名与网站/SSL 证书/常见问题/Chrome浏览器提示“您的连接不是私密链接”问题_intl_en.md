### What should I do if Chrome prompts "your connection is not a private link"?
Since November 2016, we have received feedback from some Google Chrome users regarding the prompt "your connection is not private" (error **NET::ERR_CERTIFICATE_TRANSPARENCY_REQUIRED**) when accessing HTTPS sites.

This CT error has been confirmed to be a kernel bug with Chrome versions 53 and 54, which causes all SSL certificates issued by Symantec CA to be incompatible. It occurs in all certificates of Symantec CA issued after June 1, 2016. Chrome solved this problem with an immediate release of an automated patch. The problem was fixed with the release of version 55.

Users who can connect to Chrome's servers will not be affected by this issue. However, most users in China do not have access to Chrome's server and are advised to upgrade to version 55 or later to solve this problem.

![](https://mc.qcloudimg.com/static/img/25a818d9e80a02c2b8b7c90f0e1c93df/1.png)

Symantec's official statement: 	https://www.symantec.com/connect/blogs/chrome-53-bug-affecting-symantec-ssltls-certificates

Chrome's official announcement: https://bugs.chromium.org/p/chromium/issues/detail?id=664177

In addition, this problem also exists in earlier versions of QQ browsers using Chromium 53 kernels. However, this problem has been fixed in newer versions. We recommend that users upgrade their QQ browsers to the latest version.
