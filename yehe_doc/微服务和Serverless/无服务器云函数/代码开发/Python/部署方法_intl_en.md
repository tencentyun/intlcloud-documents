## Deployment Methods

Tencent Cloud SCF provides the following function deployment methods. For more information about how to create and update a function, see [Create and Update a Function](https://intl.cloud.tencent.com/document/product/583/19806).
- Uploading and deploying a zip package, as instructed in [Installing and Deploying Dependencies](#install)
- Editing and deploying functions via the console, as instructed in [Deploying Functions](https://intl.cloud.tencent.com/document/product/583/32741).
- Using the command line, as instructed in [Deployment Through Serverless Framework CLI](https://intl.cloud.tencent.com/document/product/583/32741).

[](id:install)

## Installing and Deploying Dependencies

Currently, the SCF standard Python Runtime only supports writing to the `/tmp` directory, and other directories are read-only. Therefore, you need to install, package and upload the local dependent library for use. The Python dependency package can be uploaded with function codes to the cloud, or uploaded to the layer that will be bound to the required function.

### Locally installing dependency packages


#### Dependency manager
In Python, dependencies can be managed with the pip package manager. Replace `pip` with `pip3` or `pip2` according to the environment configurations.

#### Directions
1. Configure dependency information in `requirements.txt`.
2. Run the `pip install -r requirements.txt -t .` command under the code directory to install the dependency package. You can use the `-t` parameter to specify the installation directory, or directly run `-t .` under the project’s code directory to install the dependency package in the current directory.


>!
>
>- Use the `pip freeze > requirements.txt` command to generate a `requirements.txt` file that contains all dependencies of the current environment.
>- Because the function is running on CentOS 7, install the dependency package in the same environment to avoid errors. For detailed directions, see [Using Container Image](https://intl.cloud.tencent.com/document/product/583/39009).
>- If some dependencies require dynamic link library, please manually copy these dependencies to the installation directory, and then package them for uploading. For more information, see [Installing Dependency with Docker](https://intl.cloud.tencent.com/document/product/583/38127).

#### Sample

1. Use the `index.py` code file shown below to install the `requests` dependency locally.
```
# -*- coding: utf8 -*-
import requests

def main_handler(event, context):
        addr = "www.qq.com"
        resp = requests.get(addr)
        print(resp)
        return resp
```
2. Run the `pip3 install requests -t .` command to install the `requests` dependency under the current directory of the project. The code file is as follows:
```
$ pip3 install requests -t .
Collecting requests
      Using cached requests-2.25.1-py2.py3-none-any.whl (61 kB)
Collecting certifi>=2017.4.17
      Using cached certifi-2020.12.5-py2.py3-none-any.whl (147 kB)
Collecting chardet<5,>=3.0.2
      Using cached chardet-4.0.0-py2.py3-none-any.whl (178 kB)
Collecting idna<3,>=2.5
      Using cached idna-2.10-py2.py3-none-any.whl (58 kB)
Collecting urllib3<1.27,>=1.21.1
      Using cached urllib3-1.26.4-py2.py3-none-any.whl (153 kB)
Installing collected packages: urllib3, idna, chardet, certifi, requests
Successfully installed certifi-2020.12.5 chardet-4.0.0 idna-2.10 requests-2.25.1 urllib3-1.26.4

$ ls -l
total 8
drwxr-xr-x   3 xxx  111    96  4 29 16:45 bin
drwxr-xr-x   7 xxx  111   224  4 29 16:45 certifi
drwxr-xr-x   8 xxx  111   256  4 29 16:45 certifi-2020.12.5.dist-info
drwxr-xr-x  44 xxx  111  1408  4 29 16:45 chardet
drwxr-xr-x   9 xxx  111   288  4 29 16:45 chardet-4.0.0.dist-info
drwxr-xr-x  11 xxx  111   352  4 29 16:45 idna
drwxr-xr-x   8 xxx  111   256  4 29 16:45 idna-2.10.dist-info
-rw-r--r--@ 1 xxx 111 177 4 29 16:33 index.py
drwxr-xr-x  21 xxx  111   672  4 29 16:45 requests
drwxr-xr-x   9 xxx  111   288  4 29 16:45 requests-2.25.1.dist-info
drwxr-xr-x  17 xxx  111   544  4 29 16:45 urllib3
drwxr-xr-x  10 xxx  111   320  4 29 16:45 urllib3-1.26.4.dist-info
```


### Packaging and uploading

You can upload dependencies together with the project, and use them through the `import` statement in function codes. You can also package and deploy dependencies to a layer, and bind the layer to a function being created to reuse them.

The zip package for deploying functions or layers can be generated automatically by a local folder via the console or manually. All the packaging should be under the project directory to place codes and dependencies in the root directory of the zip package. For more information, see [Packaging requirements](https://intl.cloud.tencent.com/document/product/583/32741).


### Special dependency packages

Some Python dependencies such as the `pycryptodome` dependency need to be compiled for installation. Because the compilation varies with the operating system, the dependent library, dynamic library, and other programs compiled on Windows or Mac may be unable to run in the SCF environment. The following solutions are recommended.
- Use the dependent library that is ready for FaaS open source implementations.
- Search dependencies or submit requirements in the [SCF public layer](https://github.com/awesome-scf/tencent-scf-public-layer). This layer collects and stores special dependency packages, and provides the deployment support.
- Use the container solution and [SCF container image](https://intl.cloud.tencent.com/document/product/583/39009) to install and extract special dependencies locally, and then package and upload them to the code runtime environment.
