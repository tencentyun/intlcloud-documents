This document describes how to configure and use an HTTPS proxy.

## Directions
You can configure an HTTPS proxy in the following ways:

- Run the following command based on the operating system that you use to configure an HTTPS proxy in an environment variable:
<dx-tabs>
::: Linux\Unix and macOS
```
export https_proxy=https://192.168.1.1:1111
export https_proxy=https://myproxy.com:1111
```
:::
::: Windows
```
setx http_proxy=https://192.168.1.1:1111
set  http_proxy=https://myproxy.com:1111
# setx means to set a permanent environment variable. Restart the terminal for the setting to take effect.
```
:::
</dx-tabs>
- Run the following command and use the `--https-proxy` option in the command line to configure an HTTPS proxy:
```bash
# Example:
tccli cvm DescribeRegions --https-proxy https://192.168.1.1:1111
```
