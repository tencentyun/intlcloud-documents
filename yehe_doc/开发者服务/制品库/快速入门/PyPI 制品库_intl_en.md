This document describes how to store PyPI artifacts in CODING-AR for centralized artifact management and version control. The following sections introduce how to create an artifact, configure authentication, and pull and push artifacts.

## Open CODING-AR

1. Log in to the CODING Console and click **Use Now** to go to CODING page.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the project.
3. In the menu on the left, click **Artifact Management**.

## Preparations

>! Before you begin:
> -   Install Python3.
> -   Create an artifact repository (see [Basic Operations](https://intl.cloud.tencent.com/document/product/1136/44804)).
> -   Select PyPI as the repository type.

## Initialize a Local PyPI Project

1.  Create a demo directory for the PyPI project. Run the following command in the terminal to create a demo project folder.
<dx-codeblock>
:::  bash
mkdir -p demo/example_pkg/__init__.py
:::
</dx-codeblock>
2.  Go to the `demo` directory and create a `setup.py` file.
<dx-codeblock>
:::  bash
cd demo && touch setup.py
:::
</dx-codeblock>
3.  Paste the configuration to `setup.py`.
<dx-codeblock>
:::  python
import setuptools

setuptools.setup(
    name="example-pkg-YOUR-USERNAME-HERE", # Replace with your own username
    version="0.0.1",
    author="Example Author",
    author_email="author@example.com",
    description="A small example package",
    url="https://github.com/pypa/sampleproject",
    packages=setuptools.find_packages(),
    classifiers=[
        "Programming Language :: Python :: 3",
        "License :: OSI Approved :: MIT License",
        "Operating System :: OS Independent",
    ],
    python_requires='>=3.6',
)
:::
</dx-codeblock>
4.  Install `setuptools` and `wheel`.
<dx-codeblock>
:::  bash
python3 -m pip install --user --upgrade setuptools wheel
:::
</dx-codeblock>
5.  Package the project.
<dx-codeblock>
:::  bash
python3 setup.py sdist bdist_wheel
:::
</dx-codeblock>
After the project is packaged, the following files will be generated in `/dist` for pushing:
<dx-codeblock>
:::  bash
└─npm
    ├─example_pkg_YOUR_USERNAME_HERE-0.0.1-py3-none-any.whl
    ├─example_pkg_YOUR_USERNAME_HERE-0.0.1.tar.gz
:::
</dx-codeblock>


## Configure Authentication Information

Authentication information must be configured before you can pull artifacts from or push artifacts to CODING-AR. You can select **automatic configuration** or **manual configuration**. Before configuration, run `cd /` to go to the root directory, and then run `ls -a` to check whether `.pypirc` and `pip.conf` files exist.

If such files are not found, run the following command to create these files.
<dx-codeblock>
:::  bash
touch .pypirc && touch pip.conf
:::
</dx-codeblock>


### Automatic configuration

1.  Click **Generate configuration from access token**. An access credential will be generated for you. To view your personal token, go to **Personal Account Settings** > **Access Token**.
![](https://qcloudimg.tencent-cloud.cn/raw/226bbfb0ff3367df8788b6e9016f6d46.png)
2.  Enter your login password to obtain the configuration.
![](https://qcloudimg.tencent-cloud.cn/raw/0a9ca1332f08ee4804876bce6da8856d.png)
Copy the configuration to the `.pypirc` and `pip.conf` files in the root directory.

### Manual configuration

Copy the code in the guide to the specific files.
![](https://qcloudimg.tencent-cloud.cn/raw/8bd2b6f6862f8df28ecd21d34143c4cd.png)

## Push an Artifact

Go to the project directory and copy and run the command in the terminal. For example, go to the `Demo` directory created above and run the command to push all artifacts in `Demo/dist` to CODING-AR.
<dx-codeblock>
:::  bash
twine upload -r coding-pypi dist/*
:::
</dx-codeblock>
<img src = "https://main.qcloudimg.com/raw/b8996f745b0d7d108059c58628743de1.png" style="width: 100%">
After the artifact is pushed successfully, refresh the page to view the latest artifacts.
</dx-codeblock>
<img src = "https://qcloudimg.tencent-cloud.cn/raw/e938b53f3096352840997d7b27366bed.png" style="width: 100%">

## Pull an Artifact

Run the `pip install` command in the PyPI repository guide to pull an artifact.
<dx-codeblock>
:::  bash
pip install <Artifact Name>
:::
</dx-codeblock>


## Configure a Proxy

If you try to pull an artifact that does not exist in the CODING private repository, the system will try to pull from the configured proxy. You can add a third-party artifact source to obtain artifacts from the specific repository. Without the need for configuration, CODING will retrieve artifacts in sequence from top to bottom.
![](https://qcloudimg.tencent-cloud.cn/raw/1b216dfabb90968865047819fc18847a.png)

Replace `<package>` with the package name and run the command generated on the page to pull the package.
![](https://qcloudimg.tencent-cloud.cn/raw/7b88128505e55a250158ffac96e12343.png)

The artifact and its dependencies will be pulled to the local machine and synchronized to CODING-AR. The package source will be shown on the details page.

