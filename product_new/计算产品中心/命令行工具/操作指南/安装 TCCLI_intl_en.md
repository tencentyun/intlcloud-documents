# Installing TCCLI

## Operation Scenarios

This document describes how to install TCCLI International Version.

## Prerequisites

Before installing CLI, make sure that your system has the Python environment and pip tool installed.

> Note:
>
> Python must be version 2.7 or higher. For more information, please see [Python's official website](https://www.python.org/) and [pip's official website](https://pypi.org/project/pip/).

## Notes

- TCCLI is dependent on the [TencentCloudApi Python SDK](https://github.com/TencentCloud/tencentcloud-sdk-python-intl-en). If the version number of the TencentCloudApi Python SDK is lower than that of TCCLI to be installed, the TencentCloudApi Python SDK will be automatically upgraded when TCCLI is installed.
- If TCCLI Chinese Version has been installed, it will be automatically overwritten by the International Version.

## Directions

1. Install TCCLI by running the following command:

   ```sh
pip install tccli-intl-en
   ```
   
2. After the installation is completed, run the following command to check whether the installation is successful.

   ```
   tccli version
   ```

   > Note:
>
   > If your environment is Linux, you can enable autocomplete feature by running the following command:
   >
   > ```
   >complete -C 'tccli_completer' tccli
   > ```