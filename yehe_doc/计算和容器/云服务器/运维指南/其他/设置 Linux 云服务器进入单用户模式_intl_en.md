## Overview
For operations like password management, SSHD fixing and maintenance before disk mounting, Linux users need to enter the single user mode. This document describes how to boot into this mode in mainstream Linux distributions.

## Directions
1. On the CVM console, choose VNC to log in to a CVM. For detailed directions, see [Logging into Linux Instances via VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. In the VNC login window, select **Send CtrlAltDel** in the upper-left corner, press **Ctrl-Alt-Delete**, and click **OK** in the prompt box.
3. When a connection failure message appears, press Up or Down arrow to refresh the page and hovers the cursor over the `grub` menu, as shown below.
![](https://main.qcloudimg.com/raw/350187ce0a771d00e6d54e929291ebae.png)
4. Press **e** to enter the grub rescue mode.
5. Perform the steps that suit your operating system version.
<dx-tabs>
::: CentOS\s6.x
1. Select a kernel in the grub mode, as shown below.
![](https://main.qcloudimg.com/raw/5abc9f57184cc74bba927513fb1c4a88.png)
2. Press **e** to enter the kernel edit page, choose the **kernel** line using Up or Down arrow, and press **e** again, as shown below.
![](https://main.qcloudimg.com/raw/1a596a48df87d1d619e415d8d5b0cb65.png)
3. Enter **single** at the end of line, as shown below.
![](https://main.qcloudimg.com/raw/e1f74a4ce211a34301c4f74ffcc790b8.png)
4. Press **Enter**, and then press **b** to boot the selected command line and enter single user mode, as shown below.
![](https://main.qcloudimg.com/raw/b379937bfc15e93f0823ec50095d1dc6.png)
The following figure indicates that the system boots into single user mode.
![](https://main.qcloudimg.com/raw/517c4d2c24864f3fc8f5002bd1e2c2a1.png)
<dx-alert infotype="explain" title="">
You can run the `exec /sbin/init` command to exit the single user mode.
</dx-alert>
:::
::: CentOS\s7.x
1. Select a kernel in the grub mode, as shown below.
![](https://main.qcloudimg.com/raw/2ddc7d1e4416d9fa763922e23b59d580.png)
2. Press **e** to enter the kernel edit page. Locate the line started with “linux16” using Up or Down arrow and replace `ro` with `rw init=/bin/bash` or `/usr/bin/bash`, as shown below.
![](https://main.qcloudimg.com/raw/1b861ba0ecee1cd82da4364523e8a1c6.png)
3. Press **Ctrl+X** to boot into the single user mode, as shown below:
The following figure indicates that the system boots into the single user mode.
![](https://main.qcloudimg.com/raw/fbe8cfcf43aa4c914882edc4c3ee5faf.png)
<dx-alert infotype="explain" title="">
You can run the `exec /sbin/init` command to exit the single user mode.
</dx-alert>
:::
::: CentOS\s8.0
1. Select a kernel in the grub mode, as shown below.
![](https://main.qcloudimg.com/raw/a6ce701e5845141929d822635bd42b9a.png)
2. Press **e** to enter the kernel edit page. Locate the line started with “linux” using Up or Down arrow and replace `ro` with `rw init=/sysroot/bin/bash`, as shown below.
![](https://main.qcloudimg.com/raw/d06effc3cab12d545fd7bc92f4577b14.png)
3. Press **Ctrl+X** to boot into the single user mode, as shown below:
The following figure indicates that the system boots into the single user mode.
![](https://main.qcloudimg.com/raw/126dcdb5916e57815c3632e9e4b24412.png)
:::
::: Ubuntu\s or \sDebian
1. Select a kernel in the grub mode, as shown below.
![](https://main.qcloudimg.com/raw/c3c0be766481edf3f6521f7764f8d4cb.png)
2. Press **e** to enter the kernel edit page. Locate the line started with “linux” using Up or Down arrow and append `quiet splash rw init=/bin/bash` to the end of the line, as shown below.
![](https://main.qcloudimg.com/raw/40882cf22d755c0338ea9d7c106bc280.png)
3. Press **Ctrl+X** to boot into the single user mode, as shown below:
The following figure indicates that the system boots into single user mode.
![](https://main.qcloudimg.com/raw/df55d20b7eb087744fb6283c5124e7fc.png)
:::
::: SUSE
1. Select a kernel in the grub mode, as shown below.
![](https://main.qcloudimg.com/raw/4da4d0c5c98e4f0dbe4990e920a11daf.png)
2. Press **e** to enter the kernel edit page. Locate the line started with “linux” using Up or Down arrow, add `rw` to the beginning and `1` to the end of the `splash` parameter, as shown below.
![](https://main.qcloudimg.com/raw/013a0099ccb5c19d04441dd60ea7558b.png)
3. Press **Ctrl+X** to boot into the single user mode, as shown below:
:::
::: tlinux
1. Select a kernel in the grub mode, as shown below.
![](https://main.qcloudimg.com/raw/c497e63321b76e5cd1f0eea06f53cdb2.png)
2. Press **e** to enter the kernel edit page, choose the **kernel** line using Up or Down arrow, and press **e** again, as shown below.
![](https://main.qcloudimg.com/raw/06c66e0f30163e9fc7e6aafbf9463645.png)
3. Add a space and **1** to the end of the line (namely after **256M**), as shown below.
![](https://main.qcloudimg.com/raw/06efb32e3a2edb39f32e13be1ab8527f.png)
4. Press **Enter** to enter the single user mode.
:::
</dx-tabs>
