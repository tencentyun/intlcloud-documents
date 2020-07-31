## Operation Scenarios
This template can quickly deploy a full-stack Serverless application based on **TCB NoSQL DB + SCF + Website**. It mainly contains the following components:  
- **Serverless Website:** the frontend hosts HTML static pages in COS.
-**Serverless Cloud Function:** the backend function is deployed in the cloud and triggered and invoked over HTTP.
-**TCB environment:** you can create a TCB environment and call NoSQL DB to provide database services for the full-stack website.
   
## Directions
   
### Installation
   
Use npm to install [Serverless CLI](https://github.com/serverless/serverless) globally:
```bash
$ npm install -g serverless
```
   
If you have already installed Serverless Framework, you can run the following command to upgrade it to the latest version:
```bash
$ npm update -g serverless
```
   
After the installation is completed, run the `serverless -v` command to view the version information of Serverless Framework and make sure that the version information is as follows or displays higher versions:
```bash
$ serverless –v
Framework Core: 1.68.0
Plugin: 3.6.6
SDK: 2.3.0
Components: 2.30.1
```
   
### Configuration
   
1. Create a local folder and run the `create --template-url` command to download the relevant template:
```bash
$ mkdir my_tcbdemo && cd my_tcbdemo
$ serverless create --template-url https://github.com/serverless-components/tencent-mongodb/tree/master/example/fullstack-demo
```
   
2. Find the **function->serverless.yaml** file in the project directory and enter your own `SecretId` and `SecretKey`.  
>?
> - If you don't have a Tencent Cloud account yet, please [sign up](https://intl.cloud.tencent.com/register) first.
>- If you already have a Tencent Cloud account, you can get **SecretId** and **SecretKey** in [API Key Management](https://console.cloud.tencent.com/cam/capi).
>- Currently, `sls` supports access to TCB in Mainland China. Please pay attention to the region settings in the `yaml` file during deployment. An error may be reported for other regions.
   
3. In the `function->src` directory, install the required dependencies with the following command:
```bash
$ npm install
```
   
### Deployment
After the configuration is completed, enter the root directory containing the `.env` file, run the following command to create a TCB environment, deploy the backend code to the SCF platform, and deploy the static website with the `website` component:
   
```bash
$ sls deploy --all
   
serverless ⚡ framework

mongoDBDemoMongo:
  Region:    ap-guangzhou
  Name:      Mydemo
  EnvID:     Mydemo-dyxfxv
  FreeQuota: basic

mongoDBDemoSCF: 
  FunctionName: MongoDBDemo
  Description:  
    Namespace:    default
    Runtime:      Nodejs8.9
    Handler:      index.main
    MemorySize:   128
    Triggers: 
      apigw: 
         - https://service-dlq65ccq-1258834142.gz.apigw.tencentcs.com/release/users

mongoDBDemoWebsite: 
   website: http://my-bucket-1258834142.cos-website.ap-guangzhou.myqcloud.com

78s › tcbdemo › Success

```
 You can view your Serverless website by accessing the website URL output on the command line.  
>!
>- Due to the limitation of `sls` executing role, you need to log in to the [Role](https://console.cloud.tencent.com/cam/role) page in the CAM Console and manually associate the **TCBFullAccess** policy with **SLS_QcsRole**; otherwise, the role will not work properly.
>- Currently, the `deploy --all` command only supports Serverless Framework Component v2.30.1 and above; therefore, please make sure that your component has been updated to the latest version.
>- Currently, TCB allows you to create/terminate an environment for up to 4 times per month. Please create an environment with caution, as an error will be reported if the limit is exceeded.
   

   
### Removal
   
Run the following command to remove the project:
   
```bash
$ sls remove --debug
```
   
#### Permission configuration
The TCB component supports quick authorization by scanning code. You can also complete the permission configuration by configuring a `.env` file locally in the following steps:
   
Create a `.env` file in the project root directory and configure the corresponding Tencent Cloud `SecretId` and `SecretKey` information in it:
    
```text
# .env
TENCENT_SECRET_ID=123
TENCENT_SECRET_KEY=123
```
        
#### More components
You can view more component information in the repository of [Serverless Components](https://github.com/serverless/components).
   
#### Q&A
**Why is the error "EnvId is invalid" reported?**
   
The TCB DB component currently creates one free TCB environment for you by default. If you already have a free environment, creating a new one through Serverless Component will fail and report an error. You can delete the `db` folder and configure the **MongoId** parameter in **function->serverless.yaml** in the `demo` directory and enter the ID of your existing TCB environment to complete the project deployment.

