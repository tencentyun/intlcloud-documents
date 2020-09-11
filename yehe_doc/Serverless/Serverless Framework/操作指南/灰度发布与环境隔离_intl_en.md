## Operation Scenarios
This document uses deploying an Express website with the `tencent-express` component as an example to describe how to use Serverless Framework to develop, manage, deploy, and publish a project. You can see the demo [here](https://github.com/June1991/serverless-express).

## Command Description
#### Publishing function version
```plaintext
sls deploy --inputs.publish="fun01,fun02" # Publish the `fun01` and `fun02` function versions under the project during deployment
sls deploy --inputs.publish  # Publish all function versions under the project during deployment
```

#### Setting function traffic
```plaintext
sls deploy --inputs.traffic="0.2" # After deployment, switch 20% traffic to the `$latest` version
```
- In Serverless Framework, the traffic rule of the SCF function whose alias is `$default` is modified to switch the traffic.
- The value of `traffic` is configured as the traffic percentage of the `$latest` version. The traffic percentage of the last published SCF function version is 1 minus the traffic percentage of the `$latest` version.
For example, if `traffic` = "0.2", the traffic rule of `$default` will be configured as `{$latest:0.2, last published SCF function version: 0.8}`.
- If no fixed versions are published for the function and only the `$latest` version exists, no matter how `traffic` is set, it will always be `$latest:1.0`.


## Process Description
The development and launch process of a project is as shown below:
![](https://main.qcloudimg.com/raw/af7fe3252a3607f929ad0c6e1736b6dc.svg)
1. Project initialization: initialize the project; for example, select some development frameworks and templates to complete the basic construction.
2. Development: develop product features. This stage may involve collaboration among multiple developers, who will pull different feature branches for separated development and testing and finally merge them into the `dev` branch for joint testing.
3. Testing: test the product features by testing personnel.
4. Release and launch: publish and launch the tested product features. As a newly published version may be unstable, grayscale release will be used generally, and some rules will be configured to monitor the stability of the new version. After the new version becomes stable, all traffic will be switched to it.

## Basic Concepts
#### Branch concepts
The example involves the following branches:

| Branch Type | Description |
| ------ | ----- |
| master | It is used to deploy a production environment | 
| testing | It is used for testing in a testing environment |
| dev      | It is used for daily development |
| feature-xxx | It is used to add a new feature; for example, different developers can pull different feature branches from `dev` for development |
| hotfix-xxx | It is used to fix an urgent bug | 

#### Serverless Framework parameters
In this example, the `stage` parameter is used to isolate environments. Different `stage` configurations will be deployed into different SCF functions.
```
# serverless.yml

component: express # Name of the imported component, which is required. The `express-tencent` component is used in this example
name: expressDemo # Name of the instance created by this Express component, which is required
org: xxx-department # Organization information, which is optional
app: expressDemoApp # Express application name, which is optional
stage: ${env:stage} # Information for identifying environment, which is optional. The configuration is read from the .env file

inputs:
  src:
    src: ./ 
    exclude:
      - .env
  region: ap-guangzhou
  runtime: Nodejs10.15
  functionName: express-demo-${stage} # SCF function name
  apigatewayConf:
    protocols:
      - http
      - https
    environment: release
```
## Directions
### Project initialization
1. Create an Express project as instructed in [Deploying Express.js Application](https://intl.cloud.tencent.com/document/product/1040/37354) and modify the YML file content as follows:
```
#serverless.yml
component: express # Name of the imported component, which is required. The `express-tencent` component is used in this example
name: expressDemo # Name of the instance created by this Express component, which is required
org: personal # Organization information, which is optional
app: expressDemoApp # Express application name, which is optional
stage: ${env:STAGE} # Information for identifying environment, which is optional. The configuration is read from the .env file

inputs:
  src:
    src: ./ 
    exclude:
      - .env
  region: ap-guangzhou
  runtime: Nodejs10.15
  functionName: express-demo-${stage} # SCF function name
  apigatewayConf:
    protocols:
      - http
      - https
    environment: release
```

2. Configure the following content in the .env file in the project root directory:
```
TENCENT_SECRET_ID=xxxxxxxxxx # `SecretId` of your account
TENCENT_SECRET_KEY=xxxxxxxx # `SecretKey` of your account
STAGE=prod # `STAGE` is the `prod` environment. You can also run `sls deploy --stage=prod` to pass in the parameter
```

3. After the deployment by running `sls deploy` succeeds, access the generated URL as shown below:
![](https://main.qcloudimg.com/raw/ed180d13d3010d49ec102567c235d461.svg)

4. Create a remote repository ([sample](https://github.com/June1991/serverless-express)), submit the project code to the remote `master` branch, and create `testing` and `dev` branches. In this way, the code of the three branches is on the same version (suppose it is v0).
![](https://main.qcloudimg.com/raw/f8ae1d7e0ca59d1b0c49d6878ba4f37d.svg)

### Development and testing
#### Background
In this stage, a feature module needs to be developed. Suppose two developers are needed: Tom and Jorge, who create `feature1` and `feature2` feature branches from `dev` (v0) for development, respectively.
![](https://main.qcloudimg.com/raw/8716ab86706ce857897d81d2538e9253.svg)
Tom starts developing `feature1`. In this example, a `feature.html` file is added, and "This is a new feature 1." is written in it.

#### Development

1. Add router configuration in the `sls.js` file:
```
// Routes
app.get(`/feature`, (req, res) => {
 res.sendFile(path.join(__dirname, 'feature.html'))
})
```

2. Add `feature.html`:
```
<!DOCTYPE html>
<html lang="en">
 <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Serverless Component - Express.js</title>
 </head>
 <body>
  <h1>
   This is a new feature 1.
  </h1>
 </body>
</html>
```

3. Set a stage in the .env file so as to get an independent runtime and debugging environment during the development.
For example, Tom configures the .env file in the project directory of `serverless.yml` as follows:
```
TENCENT_SECRET_ID=xxxxxxxxxx
TENCENT_SECRET_KEY=xxxxxxxx
STAGE=feature1
```

4. After the deployment by running `sls deploy` succeeds, the following content will be returned:
```
region: ap-guangzhou
apigw:
  serviceId:   service-xxxxxx
  subDomain:   service-xxxxxx-123456789.gz.apigw.tencentcs.com
  environment: release
  url:         https://service-xxxxxx-123456789.gz.apigw.tencentcs.com/release/
scf:
  functionName: express-demo-feature1
  runtime:      Nodejs10.15
  namespace:    default
  lastVersion:  $LATEST
  traffic:      1

Full details: https://serverless.cloud.tencent.com/instances/expressDemoApp%3Afeature1%3AexpressDemo

10s » expressDemo » Success
```

5. Access the generated URL (https://service-xxxxxx-123456789.gz.apigw.tencentcs.com/release/feature) as shown below:
![](https://main.qcloudimg.com/raw/ca56e34cbc2f1216871e03bd79d250c9.svg)

At this point, Tom has completed feature development and successfully tested the feature.

Suppose Jorge has also completed feature development and successfully tested the feature. In this example, a `feature.html` file is added, and "This is a new feature 2." is written in it.

#### Joint testing

1. The two developers merge their feature branch code into the `dev` branch (conflicts may occur and need to be solved manually).
![](https://main.qcloudimg.com/raw/fc9297f775bda0eb0bbc7db2b3305285.svg)
2. Carry out joint testing in `dev`. The .env file is configured as follows in the joint testing environment:

```
TENCENT_SECRET_ID=xxxxxxxxxx
TENCENT_SECRET_KEY=xxxxxxxx
STAGE=dev
```

3. After running `sls deploy` to deploy the joint testing environment, access the URL (https://service-xxxxxx-123456789.gz.apigw.tencentcs.com/release/feature) as shown below:
![](https://main.qcloudimg.com/raw/c6a28dff690869c62e0a767944150a87.svg)
At this point, the joint testing is completed, and the development of the entire functionality is also completed.

#### Testing

1. Merge the jointly tested `dev` branch into `testing` code to enter the testing stage.
![](https://main.qcloudimg.com/raw/09d23fc99205b8ac078da6cbf4d7f700.svg)
2. Configure the .env file in the testing environment as follows:
```
TENCENT_SECRET_ID=xxxxxxxxxx
TENCENT_SECRET_KEY=xxxxxxxx
STAGE=testing
```
3. After the deployment by running `sls  deploy` succeeds, the testing personnel will carry out relevant tests until the features are stable in the testing.


### Release and launch

After the test is passed, merge the testing code into the `master` branch and prepare for release and launch.
![](https://main.qcloudimg.com/raw/dcfb979dd18f198b2764d77d0cb7b517.svg)

To ensure that the business in the production environment is stable, we recommend you use grayscale release:
1. Set the .env file in the production environment as follows:
```
TENCENT_SECRET_ID=xxxxxxxxxx
TENCENT_SECRET_KEY=xxxxxxxx
STAGE=prod
```
2. Deploy the `$latest` version in the production environment and switch 10% traffic to it.
```
sls deploy --inputs.traffic=0.1 # Deploy and switch 10% traffic to the `$latest` version
```
3. Monitor the `$latest` version and switch traffic to this version after it becomes stable.
```
sls deploy --inputs.traffic=1.0 # Deploy and switch 100% traffic to the `$latest` version
```
4. After all traffic is successfully switched, the stable version needs to be marked, so that you can easily and quickly roll back to this version if a problem occurs in the production environment when a new feature is published.
```
sls deploy --inputs.publish --inputs.traffic=0 # Deploy and publish function v1 and switch all traffic to it
```

At this point, a `serverless-express` project has been developed and published.
>?
- During the development, you need to set the `stage` value based on the environment and add it to the function name to isolate different environments.
- You can run a custom script to implement grayscale release.


















