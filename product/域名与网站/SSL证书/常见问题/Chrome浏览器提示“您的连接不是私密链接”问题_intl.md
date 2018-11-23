Since November 2016, we have received feedbacks from some Google Chrome users on the prompt "Your connection is not private" (error **NET::ERR_CERTIFICATE_TRANSPARENCY_REQUIRED**) when accessing HTTPS sites.

See the details below:
![](https://mc.qcloudimg.com/static/img/0fdf027303e53946698dcb377431597e/0.png)

This CT error is confirmed to be a kernel bug with Chrome versions 53 and 54, which causes the incompatibility with SSL certificates issued by Symantec CA. CT error occurs in all certificates issued by Symantec CA after June 1, 2016. Chrome has solved this problem with automatic patch immediately, and has fixed this problem in version 55.

Users who can connect to Chrome's server will not be affected by this issue. But most users in China cannot access Chrome's server, it is recommended to upgrade to version 55 or later to solve this problem.

![](https://mc.qcloudimg.com/static/img/25a818d9e80a02c2b8b7c90f0e1c93df/1.png)

Symantec's official announcement: 	https://www.symantec.com/connect/blogs/chrome-53-bug-affecting-symantec-ssltls-certificates

Chrome's official announcement: https://bugs.chromium.org/p/chromium/issues/detail?id=664177

In addition, this problem exists in older QQ browsers using Chromium 53 kernel, but has been fixed in new versions. Users using older QQ browser versions are also recommended to upgrade to the latest version.
Details can be found in QQ Browser's official announcement: http://bbs.browser.qq.com/thread-222732-1-1.html

