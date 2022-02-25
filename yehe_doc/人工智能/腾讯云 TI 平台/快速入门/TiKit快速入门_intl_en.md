
## Overview
TiKit is an open-source SDK for Python provided by TI Platform, which can be used to submit training tasks to TI Platform.

## Directions
### Environment dependencies
Currently, Python 3.4 or later is supported.

### Installing TiKit
On TI Platform, TiKit is built in the containers for notebooks and training tasks, so you don't need to install it separately.

In a non-public cloud TI Platform environment, the installation methods are as follows:

- Install dependencies:

```
# CentOS:

sudo yum -y install cyrus-sasl cyrus-sasl-devel cyrus-sasl-lib

# Ubuntu:

sudo apt-get update
sudo apt-get install -y libsasl2-dev
```


- Method 1. Install through pip (recommended)

```
pip3 install -U tikit
```
- Method 2. Install offline. Download the installation package at https://pypi.org/project/tikit/ and install it with the .whl file or source code:

```
pip3 install tikit-1.0.0-py3-none-any.whl

# Alternatively, after decompressing the source code, run
python3 setup.py install
```

### Getting started

1. Prepare the `secret_id` and `secret_key`.

  Log in to Tencent Cloud to get them on the corresponding page as shown below:

![](https://qcloudimg.tencent-cloud.cn/raw/bc5f93b3272c44b18361ead95afc9cbc.png)

![](https://qcloudimg.tencent-cloud.cn/raw/c20c9a7f320252989e270e9fbc9ef22b.png)





2. Initialize the task and call the function.

```
from tikit.client import Client

# Initialize the client. In a public cloud TI Platform environment (including notebooks and training tasks), you can leave the region information empty, which is already contained in the environment variable.
client = Client("your_secret_id", "your_secret_key", "<region>")

# View the list of algorithm frameworks.
client.describe_training_frameworks()
```

In a notebook environment, the HTML content will be directly displayed as shown below:

![](https://qcloudimg.tencent-cloud.cn/raw/25abffcff87f62aeee534f4c789ff282.png)


In a non-notebook environment, you can print the result as shown below:

![](https://qcloudimg.tencent-cloud.cn/raw/5a482d23c39a929a5ae1a7c1af60d99a.png)

------



3. View the function usage.

```
help(client.create_image_dataset)
```

![](https://qcloudimg.tencent-cloud.cn/raw/85e458c288d595c6cd086ef817f3ccff.png)
