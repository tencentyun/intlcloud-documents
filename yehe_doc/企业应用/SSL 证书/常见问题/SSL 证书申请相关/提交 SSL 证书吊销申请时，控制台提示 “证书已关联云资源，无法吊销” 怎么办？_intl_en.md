### What should I do if the console prompts that "The certificate is bound to Tencent Cloud resources and cannot be revoked" when I submit an SSL certificate revocation application?

Check whether the target SSL certificate is bound to any Tencent Cloud resources such as CLB and CDN, and if so, unbind them before the revocation.