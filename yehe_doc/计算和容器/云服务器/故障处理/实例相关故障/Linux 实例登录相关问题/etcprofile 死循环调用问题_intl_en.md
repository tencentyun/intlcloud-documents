## Issue Description
When you use SSH to log in to a Linux instance, the SSH command gets stuck after outputting the "Last login: " information.


## Common Causes
This problem is probably because the `/etc/profile` file was modified, so `/etc/profile` was called in `/etc/profile`, resulting in an infinite loop call and inability to log in successfully.



## Solution
Check and repair the `/etc/profile` file as instructed in [Steps](#ProcessingSteps).


## Steps[](id:ProcessingSteps)
1. [Log in to the Linux instance via VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Run the following command to view the `/etc/profile` file.
```
vim  /etc/profile
```
3. Check whether the `/etc/profile` file contains commands related to `/etc/profile`.
 - If yes, go to the next step.
 - If no, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for assistance.
4. Press **i** to enter the edit mode and add `#` before the relevant commands in `/etc/profile` to comment them.
5. Press **Esc** to exit the edit mode, and enter **:wq** to save the modification.
6. Log in to the Linux instance again by [using SSH](https://intl.cloud.tencent.com/document/product/213/32501).
