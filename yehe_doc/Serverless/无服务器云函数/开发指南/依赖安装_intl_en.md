## Built-in Dependencies
Some common dependent libraries have been built in various runtimes of SCF, which can be queried in the corresponding runtime development guide:
- [Node.js](https://intl.cloud.tencent.com/document/product/583/11060)
- [Python](https://intl.cloud.tencent.com/document/product/583/11061) 
- [PHP](https://intl.cloud.tencent.com/document/product/583/17531)

## Installing Dependent Libraries
You can save all the dependent libraries of the SCF code in the code package and upload it to the cloud for use by SCF. SCF supports the following runtimes and usage methods:


### Node.js runtime
**Dependency manager**: in Node.js, dependencies can be managed with the npm package manager.
**Instructions**:
1. Configure dependency information in `package.json`.
2. Install the dependent libraries into the `node_modules` folder by running the `npm install` command.
3. When uploading the code library, please package and upload the dependent libraries too.

### Python runtime
**Dependency manager**: in Python, dependencies can be managed with the pip package manager. For different environment configurations, you can replace `pip` with `pip3` or `pip2` by yourself.
**Instructions**:
1. Configure dependency information in `requirements.txt`.
2. Install the dependencies by running the `pip install -r requirements.txt -t .` command.
3. When uploading the code library, please package and upload the dependent libraries too.

>!
>- You can run `pip freeze > requirements.txt` to generate the `requirements.txt` files for all dependencies in the current environment.
>- The function runtime environment is CentOS 7, and you need to install the dependencies in the same environment. If not, an error where the dependencies cannot be found may occur while running the function after upload. You can install dependencies as instructed in [SCF Container Image](https://intl.cloud.tencent.com/document/product/583/39009).
>- If some dependencies involve a dynamic link library, you need to manually copy the relevant dependency package to the dependency installation directory before packaging and uploading them. For more information, please see [Installing Dependency with Docker](https://intl.cloud.tencent.com/document/product/583/38127).



### Java runtime
**Dependency manager**: in Java, dependencies can be managed with the Maven package manager.
**Instructions**:
1. Configure dependency information in `pom.xml`.
2. Install the dependencies by running the `maven install` command.
3. When uploading the code library, please package and upload the dependent libraries too.

### Go runtime
**Instructions**: upload the final binary file when packaging.


## Upload Methods
SCF provides the following three upload methods for your choice based on your actual needs:

- [Deploy a function](https://intl.cloud.tencent.com/document/product/583/32741): you can create a deployment package in your local environment and upload it to SCF, or write the code directly in the SCF Console, which will create and upload the deployment package for you.
- Create a function with the VS Code plugin: Tencent Serverless Toolkit for VS Code is a plugin for the Visual Studio (VS) Code IDE of Tencent Cloud serverless products. It enables you to better develop serverless projects, debug their code locally, and then deploy them to the cloud with ease.
- [Create a function with CLI](https://intl.cloud.tencent.com/document/product/583/32743): use the command line tool SCF CLI to create a function and deploy it to the cloud.

