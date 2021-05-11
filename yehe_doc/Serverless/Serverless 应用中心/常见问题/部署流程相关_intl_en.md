### Why is the error "EnvId is invalid" reported when I deploy a full-stack application through the MongoDB component?
The TCB DB component currently creates one free TCB environment for you by default. If you already have a free environment, creating a new one through Serverless Component will fail and report an error. You can delete the `DB` folder and configure the `MongoId` parameter in `backend -> serverless.yml` in the `Demo` directory and enter the ID of your existing TCB environment to complete the project deployment.

### I created an API Gateway trigger and an SCF function through components, but why isn't the trigger information displayed in the SCF console?
The serverless component creates API Gateway triggers by calling the API Gateway APIs. Currently, the SCF console cannot display triggers created through API Gateway APIs. You can log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway/index) to configure related triggers.

### Why is the error "cdn host no icp" reported?
Tencent Cloud requires that an ICP filing be present when a CDN acceleration domain name or custom domain name is used; otherwise, the domain name won't take effect.

### Why doesn't the configuration in `serverless.yml` take effect?
The configuration information in the `.yml` file should be entered strictly in accordance with the sample format. Please make sure that the content and indentation format of your configuration file are correct.

### Why does parameter verification fail during deployment?
To ensure successful application deployment, Serverless Framework will verify the format of the parameters in the `.yml` file. Please make sure that your parameter format complies with the specifications. If you don't need a parameter, please delete it directly, as verification will fail even if you leave it empty.
