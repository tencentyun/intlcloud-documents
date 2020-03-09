## Built-in Dependencies
Some common dependent libraries have been built in various runtimes of SCF, which can be queried in the corresponding runtime development guide:
- [Node.js](<https://intl.cloud.tencent.com/document/product/583/11060#.E5.B7.B2.E5.8C.85.E5.90.AB.E7.9A.84.E5.BA.93.E5.8F.8A.E4.BD.BF.E7.94.A8.E6.96.B9.E6.B3.95>)
- [Python](<https://intl.cloud.tencent.com/document/product/583/11061#python-2-.E6.88.96-3.EF.BC.9F>) 
- [PHP](<https://intl.cloud.tencent.com/document/product/583/17531#.E5.B7.B2.E5.AE.89.E8.A3.85.E6.89.A9.E5.B1.95>)

## Installing Dependent Libraries
You can save the dependent libraries of the SCF code in the code package and upload it to the cloud for use by SCF. SCF supports the following runtimes and usage methods:


### Node.js runtime
**Dependency manager**: In Node.js, dependencies can be managed with the npm package manager.
**Instructions**:
1. Configure dependency information in `package.json`.
2. Install the dependent libraries into the `node_modules` folder with the `npm install` command.
3. When uploading the code library, please package and upload the dependent libraries too.

### Python runtime
**Dependency manager**: In Python, dependencies can be managed with the pip package manager.
**Instructions**:
1. Configure dependency information in `requirements.txt`.
2. Install the dependencies with the `pip install -t .` command.
3. When uploading the code library, please package and upload the dependent libraries too.

### Java runtime
**Dependency manager**: In Java, dependencies can be managed with the Maven package manager.
**Instructions**:
1. Configure dependency information in `pom.xml`.
2. Install the dependencies with the `maven install` command.
3. When uploading the code library, please package and upload the dependent libraries too.

### Go runtime
**Instructions**: upload the final binary file when packaging.


## Upload Methods
SCF provides the following three upload methods for your choice based on your actual needs:

- [Deploy a function](https://intl.cloud.tencent.com/document/product/583/32741): you can create a deployment package in your local environment and upload it to SCF, or write the code directly in the SCF Console, which will create and upload the deployment package for you.
- [Create a function with the VS Code plugin](https://intl.cloud.tencent.com/document/product/583/32744): Tencent Serverless Toolkit for VS Code is a plugin for the Visual Studio (VS) Code IDE of Tencent Cloud serverless products. It enables you to better develop serverless projects, debug their code locally, and then deploy them to the cloud with ease.
- [Create a function with CLI](https://intl.cloud.tencent.com/document/product/583/32743): use the command line tool SCF CLI to create a function and deploy it to the cloud.

