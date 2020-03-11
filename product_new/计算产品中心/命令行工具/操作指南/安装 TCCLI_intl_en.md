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
  
## Please note that a certificate issue may occur in Mac OS
> Note：
>
>While installing Python 3.6 or later versions in Mac OS, you may get an error saying 
`Error: [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed: self signed certificate in certificate chain (_ssl.c:1056).`
This is because that in Mac OS, Python does not use the system default certificate nor provide a certificate.  HTTPS requests require a certificate provided by `certifi`, which cannot be specified by SDK. Therefore you need to install a cerficiate using the command `/Applications/Python 3.6/Install Certificates.command`. "
