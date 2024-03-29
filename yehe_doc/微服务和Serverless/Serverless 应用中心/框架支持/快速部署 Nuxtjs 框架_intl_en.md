The SLS framework deployment scheme has been upgraded. You can use an SCF HTTP-triggered function to quickly deploy your Nuxt.js service to the cloud.

>! **What are the differences between SLS console deployment and direct function deployment?**
Both SLS console deployment and function deployment can be based on HTTP-triggered functions, and quick deployment is usually used for web frameworks.
- If you only need to develop code logic and do not need to create additional resources, you can perform quick deployment through the SCF console.
- If you need to create more capabilities or resources, such as automatic creation of layer hosting dependencies, quick implementation of static resource isolation, and support for direct code repository pulling, in addition to code deployment, you can use the SLS console to create web applications.


## Prerequisites
- Before using Tencent Cloud SCF, you need to sign up for a [Tencent Cloud account](https://intl.cloud.tencent.com/en/account/register) and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).
>! This document introduces the SLS console deployment scheme. You can also complete the deployment in CLI by referring to [Deploying Web Function on Command Line](https://intl.cloud.tencent.com/document/product/583/41376).

## Directions

### Template deployment - deploying Nuxt.js sample code
1. Log in to the [SLS console](https://console.cloud.tencent.com/sls).
2. Choose **Create Application** and select **Web Application** > **Nuxt.js Framework**.
3. Click **Next** and complete basic configuration.
4. Select **Sample Code** as the upload mode and click **Complete**. The application deployment starts.
5. After the application deployment is completed, you can view the basic information of the sample application on the application details page. In addition, you can use access the deployed Nuxt.js project at the access path URL generated by API Gateway.


### Custom deployment - quickly deploying web application
#### Prerequisites

The Node.js runtime environment has been installed locally.

#### Local development

1. Refer to [Installation](https://zh.nuxtjs.org/docs/2.x/get-started/installation) to install and initialize your Nuxt.js project:
```sh
npx create-nuxt-app nuxt-app
```
2. In the root directory, run the following command to directly start the service locally.
```shell
cd nuxt-app && npm run dev
```
3. Visit `http://localhost:3000` in a browser, and you can access the sample Nuxt.js project locally.
![](https://main.qcloudimg.com/raw/ee22e322be32cf1f8237e704ec484215.png)

#### Deployment in cloud

You need to make simple modifications to the initialized project, so that the project can be quickly deployed through an HTTP-triggered function. The project transformation here is usually divided into the following two steps:

- Add the `scf_bootstrap` file.
- Change the listening address and port to `0.0.0.0:9000`.

The detailed steps are as follows:
1. Create the `scf_bootstrap` file in the root directory of the project and add the following content to it (the file is used to start the service and specify the start port):
>? You can also complete the configuration in the console.
>
```sh
#!/var/lang/node12/bin/node
require("@nuxt/cli")
  .run(["start", "--port", "9000", "--hostname", "0.0.0.0"])
  .catch(error => {
    require("consola").fatal(error);
    require("exit")(2);
  });
```

>!  
1. Here is only a sample bootstrap file. Please adjust the configuration according to your actual business scenario.
2. The sample uses the standard node environment path of SCF. When debugging locally, you need to change it to your local path.
>

After the file is created, you need to run the following command to modify the executable permission of the file. By default, the permission `777` or `755` is required for the service to start normally. Below is the sample code: 
```sh
chmod 777 scf_bootstrap
```
2. After the local configuration is completed, run the bootstrap file and make sure that your service can be normally started locally. Then log in to the [SLS console](https://console.cloud.tencent.com/sls), select **Web Application** > **Nuxt.js Framework**, and select **Local Upload** or **Code Repository Pull** as the upload mode.

You can configure the `scf_bootstrap` file in the console. When the configuration is completed, the console automatically generates the `scf_bootstrap` file and packages it and the project code for deployment.
>! The actual `scf_bootstrap` file in your project prevails. If the `scf_bootstrap` file already exists in your project, its content will not be overwritten.
>
When the configuration is completed, click **Complete** to deploy your Nuxt.js project.
