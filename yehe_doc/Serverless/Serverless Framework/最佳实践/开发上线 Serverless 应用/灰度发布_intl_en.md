## Overview

During update and switch of your business version, to ensure that the business in the production environment is stable, we recommend you use grayscale release:
This document uses a deployed Express project as an example to describe how to perform grayscale release.

## Prerequisites
You have [developed a project](https://intl.cloud.tencent.com/document/product/1040/38253).

## Directions
1. Set the .env file in the production environment:
```
TENCENT_SECRET_ID=xxxxxxxxxx
TENCENT_SECRET_KEY=xxxxxxxx
STAGE=prod
```
2. Deploy the `$latest` version in the production environment and switch 10% traffic to it (90% traffic will be switched to the last published function version N):
```
sls deploy --inputs traffic=0.1 
```
3. Monitor the `$latest` version and switch 100% traffic to this version after it becomes stable:
```
sls deploy --inputs traffic=1.0
```
4. After all traffic is successfully switched, the stable version needs to be marked, so that you can easily and quickly roll back to this version if a problem occurs in the production environment when a new feature is published. Deploy and publish the function version N+1 and switch all traffic to it:
```plaintext
sls deploy --inputs publish=true  traffic=0
```

