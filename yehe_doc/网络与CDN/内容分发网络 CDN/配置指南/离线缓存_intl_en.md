## Overview

When your origin fails and resources cannot be pulled from it normally, if offline cache is enabled, the content cached in CDN can be used.
- If there is cached content on nodes, it will be returned. Even if the hit content has expired, it will still be returned until the origin server recovers to resume normal origin-pull.
- If there is no cached content on nodes, an error message indicating that the origin server fails will be returned.

>!
>- Offline cache is supported only for acceleration domain names in the Chinese mainland.
>- This feature may be unavailable in some platforms. We will complete server upgrade as soon as possible.

## Directions

### Viewing the configuration

Offline cache is disabled by default. You can enable it as needed.
![]()







