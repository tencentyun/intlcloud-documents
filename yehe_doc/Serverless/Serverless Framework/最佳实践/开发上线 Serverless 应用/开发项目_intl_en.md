## Overview
This document uses deploying an Express website with the `tencent-express` component as an example to describe how to use Serverless Framework to develop, manage, deploy, and publish a project. You can see the demo [here](https://github.com/June1991/serverless-express).

Project development may involve the following branches:

| Branch Type | Description |
| ------ | ----- |
| master | It is used to deploy a production environment |
| testing | It is used for testing in a testing environment |
| dev      | It is used for daily development |
| feature-xxx | It is used to add a new feature; for example, different developers can pull different feature branches from `dev` for development |
| hotfix-xxx | It is used to fix an urgent bug |


## Directions

### Project initialization

1. Create an Express project as instructed in [Deploying Express.js Application](https://intl.cloud.tencent.com/document/product/1040/37354) and modify the YML file content as follows:

```
#serverless.yml
app: expressDemoApp # Application name, which is the component instance name by default
stage: ${env:STAGE} # Parameter used to isolate the development environment, which is `dev` by default


component: express # Name of the imported component, which is required. The `express-tencent` component is used in this example
name: expressDemo # Name of the instance created by the component, which is required

inputs:
  src:
    src: ./ 
    exclude:
      - .env
  region: ap-guangzhou
  runtime: Nodejs10.15
  funcitonName: ${name}-${stage}-${app} # Function name
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
STAGE=prod # `STAGE` is the `prod` environment. You can also run `sls deploy --stage prod` to pass in the parameter
```

3. After the deployment by running `sls deploy` succeeds, access the generated URL as shown below:
![](https://main.qcloudimg.com/raw/ed180d13d3010d49ec102567c235d461.svg)

4. Create a remote repository ([sample](https://github.com/June1991/serverless-express)), submit the project code to the remote `master` branch, and create `testing` and `dev` branches. In this way, the code of the three branches is on the same version (suppose it is v0).
![](https://main.qcloudimg.com/raw/730575f2662c4a9bc7806f2674f34455.svg)

### Development and testing
#### Background
In this stage, a feature module needs to be developed. Suppose two developers are needed: Tom and Jorge, who create `feature1` and `feature2` feature branches from `dev` (v0) for development, respectively.
![](https://main.qcloudimg.com/raw/0fc0b47077478c25dbb90e9618b0b7bf.svg)
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
![](https://main.qcloudimg.com/raw/0e7bdc2927e6b2cd3cd5672a4a421a20.svg)
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
![](https://main.qcloudimg.com/raw/e494e4bc6a98f0dd722024597ddc6779.svg)
2. Configure the .env file in the testing environment as follows:

```
TENCENT_SECRET_ID=xxxxxxxxxx
TENCENT_SECRET_KEY=xxxxxxxx
STAGE=testing
```
3. After the deployment by running `sls deploy` succeeds, the testing personnel will carry out relevant tests until the features are stable in the testing.


### Release and launch

After the test is passed, merge the testing code into the `master` branch and prepare for release and launch.
![](https://main.qcloudimg.com/raw/3e5d33adeece63065707df9b46e8f839.svg)



Set the .env file in the production environment as follows:

```
TENCENT_SECRET_ID=xxxxxxxxxx
TENCENT_SECRET_KEY=xxxxxxxx
STAGE=prod
```

Run the deployment command:

```
sls deploy 
```

At this point, a `serverless-express` project has been developed and published.














