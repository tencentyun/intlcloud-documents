## Overview
Grayscale release (aka canary release) is a release method that can smoothly transition between black and white.

Grayscale release of a serverless application is to configure the traffic rule of the SCF function whose alias is `$default` (default traffic) to configure the traffic of two function versions, where one is the `$latest` version of the function, while the other is the last published version. During the deployment, the `traffic` parameter specifies the traffic percentage on the `$latest` version, while the rest traffic will be switched to the last published version of the current function by default.

Every time a feature is published, you can run `sls deploy` to deploy it onto the `$latest` version. You can switch some traffic to the `$latest` version to check the performance and gradually switch the rest traffic to it. When 100% traffic has been switched to it, it will be fixed, and all traffic will be switched to the fixed version.

![](https://main.qcloudimg.com/raw/d8fc34ba966a562d5f43a2953434286f.svg)

## Command Description
#### Function release version
Publish all function versions under the project during deployment:
```
sls deploy --inputs.publish  
```

Publish the `fun01` and `fun02` function versions under the project during deployment:
```
sls deploy --inputs.publish="fun01,fun02" 
```

#### Setting function traffic
After deployment, switch 20% traffic to the `$latest` version
```
sls deploy --inputs.traffic=0.2
```
- In Serverless Framework, the traffic rule of the SCF function whose alias is `$default` is modified to switch the traffic.
- The objects to be configured are always the `$latest` version and the last published function version.
- The value of `traffic` is configured as the traffic percentage of the `$latest` version. The traffic percentage of the last published SCF function version is 1 minus the traffic percentage of the `$latest` version (for example, if traffic=0.2, the traffic rule of `$default` will be `{$latest:0.2, last published function version: 0.8}`).
- If no fixed versions are published for the function and only the `$latest` version exists, no matter how `traffic` is set, it will always be `$latest:1.0`.

## Directions
You can publish a tested feature through grayscale release in the following steps:
1. Configure the production environment information into the .env file (`STAGE=prod` indicates the production environment):
```
TENCENT_SECRET_ID=xxxxxxxxxx
TENCENT_SECRET_KEY=xxxxxxxx
STAGE=prod 
```
2. Deploy the `$latest` version in the production environment and switch 10% traffic to it (90% traffic will be switched to the last published function version N):
```
sls deploy --inputs.traffic=0.1 
```
3. Monitor the `$latest` version and switch 100% traffic to this version after it becomes stable:
```
sls deploy --inputs.traffic=1.0 
```
4. After all traffic is successfully switched, the stable version needs to be marked, so that you can easily and quickly roll back to this version if a problem occurs in the production environment when a new feature is published. Deploy and publish the function version N+1 and switch 100% traffic to it:
```
sls deploy --inputs.publish --inputs.traffic=0 
```


















