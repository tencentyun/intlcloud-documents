## Deployment in the console

A deployment package is a zip collection of all the codes and dependencies that SCF runs, which should be specified during function creation. You can create a deployment package in your local environment and upload it to SCF, or write the code directly in the SCF console, which will create and upload the deployment package for you. Please use the following criteria to determine whether you can use the console to create a deployment package:

- Simple scenario: If your custom code only needs to use standard libraries or SDK libraries such as COS and SCF libraries provided by Tencent Cloud, and there is only one code file, you can use the online editor in the SCF console which automatically compresses the code and associated configuration information into an operable deployment package.
- Advanced scenario: If your code requires additional resources (such as a graphics library for image processing, web framework for web programming, or database connection library for executing database commands), you need to first create a function deployment package in your local environment and then upload it to the console.

### Packaging Requirements

#### Zip Format

The code package submitted directly to the SCF platform or submitted by uploading to COS and then imported into SCF must be in [zip format](https://en.wikipedia.org/wiki/Zip_(file_format)). 7-Zip can be used on Windows and zip command line tools can be used on Linux for compression or decompression.

#### Packaging Method

When packaging, you need to package the code files but not the entire directory of the code; after packaging is completed, the entry function file must be in the root directory of the package.

When packaging on Windows, you can enter the function code directory, select all files, right-click and select "Send to > Compressed (zipped) folder" to create the deployment package. If tools such as 7-Zip is used to unzip and browse the package, entry function and other libraries should be included in the package.

When packaging on Linux, you can enter the function code directory, run the `zip` command, and specify the source files as all files in the code directory to generate the deployment package, such as `zip /hoem/scf_code.zip * -r`.

### Sample deployment package

The following sample illustrates the steps to create a deployment package in a local environment.


>
>- Normally, locally installed dependent libraries work well on the SCF platform. In rare cases, the binary files installed may have compatibility problems. If this happens, please [contact us](https://intl.cloud.tencent.com/document/product/583/9712).
>- For the Python programming language in the sample, libraries and dependencies will be installed locally using the pip tool. Please make sure that you have already installed Python and pip locally.

### Python deployment package

#### Creating a Python deployment package on Linux
1. Create a directory:
```
mkdir /data/my-first-scf
```
2. Save all the Python source files (.py files) of the function into this directory.
3. Install all dependencies to this directory using pip:
```
pip install <module-name> -t /data/my-first-scf
```
For example, the following command installs the Pillow library in the `my-first-scf` directory:
```
pip install Pillow -t /data/my-first-scf
```
4. Compress everything in the `my-first-scf` directory. Please note that you need to compress the content of the directory, not the directory itself:
```
cd /data/my-first-scf && zip my_first_scf.zip * -r
```

>
>- For libraries with compilation process, we recommend you perform packaging on CentOS 7 to maintain consistency with the SCF runtime environment.
>- If there are requirements for other software, compilation environment, or development libraries during installation or compilation, please solve the compilation and installation problems as instructed.

#### Creating a Python deployment package on Windows

We recommend you package the dependent packages and codes that have already been successfully executed on Linux into a zip package as the execution code of the function. For details, see [Code practices - obtaining images in COS and creating thumbnails](https://intl.cloud.tencent.com/document/product/583/9736).

In Windows, you can use the `pip install <module-name> -t <code-store-path>` command to install Python libraries. But for packages that need to be compiled or have static or dynamic libraries, libraries compiled and generated on Windows cannot be invoked in SCF runtime environment (CentOS 7), so only libraries completely implemented in Python can be installed on Windows.


