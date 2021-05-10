## Overview
Grayscale release (aka canary release) is a release method that can smoothly transition between black and white.

The grayscale release utilized for a serverless application is to configure traffic rules of the SCF function alias, i.e., configuring traffic rules for the two different versions of the function in the alias. Serverless Framework supports two ways to configure alias: **default alias** and **custom alias**.

## Default Alias

The default alias is to configure the `$default` (default traffic) alias for the function. This alias always contains two function versions: one is the `$latest` version of the function, while the other is the last published version. During the deployment, the `traffic` parameter specifies the traffic percentage on the `$latest` version, while the rest traffic will be switched to the last published version of the current function by default.

Every time a feature is published, you can run `sls deploy` to deploy it onto the `$latest` version. You can switch some traffic to the `$latest` version to check the performance and gradually switch the rest traffic to it. When 100% traffic has been switched to it, it will be fixed, and all traffic will be switched to the fixed version.

![](https://main.qcloudimg.com/raw/8be91bf7dd1c50dc3b17c193f24f428e.svg)

### Command description

>?The legacy command format `sls deploy --inputs.key=value` has been changed to `sls deploy --inputs key=value` since Serverless CLI v3.2.3. Legacy commands cannot be used in new versions of Serverless CLI. If you have upgraded Serverles CLI, please use the new commands.

#### Publishing function version

Publish all function versions under the project during deployment:
```plaintext
sls deploy --inputs publish=true  
```

#### Setting function traffic

After deployment, switch 20% traffic to the `$latest` version
```plaintext
sls deploy --inputs traffic=0.2
```

- In Serverless Framework, the traffic rule of the SCF function whose alias is `$default` is modified to switch the traffic.
- The objects to be configured are always the `$latest` version and the last published function version.
- The value of `traffic` is configured as the traffic percentage of the `$latest` version. The traffic percentage of the last published SCF function version is 1 minus the traffic percentage of the `$latest` version (for example, if traffic=0.2, the traffic rule of `$default` will be `{$latest:0.2, last published function version: 0.8}`).
- If no fixed versions are published for the function and only the `$latest` version exists, no matter how `traffic` is set, it will always be `$latest:1.0`.

### Directions

You can publish a tested feature through grayscale release in the following steps:

1. Configure the production environment information into the .env file (`STAGE=prod` indicates the production environment):
```plaintext
TENCENT_SECRET_ID=xxxxxxxxxx
TENCENT_SECRET_KEY=xxxxxxxx
STAGE=prod 
```

2. Deploy the function to the `$latest` production environment and switch 10% traffic to the `$latest` version (90% traffic will be switched to the last published function version N):
```plaintext
sls deploy --inputs traffic=0.1 
```

3. Monitor the `$latest` version and switch 100% traffic to this version after it becomes stable:
```plaintext
sls deploy --inputs traffic=1.0 
```

4. After all traffic is successfully switched, the stable version needs to be marked, so that you can easily and quickly roll back to this version if a problem occurs in the production environment when a new feature is published. Deploy and publish the function version N+1 and switch 100% traffic to it:
```plaintext
sls deploy --inputs publish=true  traffic=0 
```



## Custom Alias

A custom alias can be created through commands to configure the traffic ratio between two specified function versions.

When using a custom alias for grayscale release, first publish the new feature to a new version, then modify the alias configuration to switch part of the traffic to this version for observation, and finally switch all the traffic to this version gradually.

The custom alias enables flexible version switching. Its configuration method is more complicated than that of the default alias. It is suitable for business scenarios that require higher grayscale release capabilities. **Currently, custom alias is supported only for the SCF component.**

<img src="https://main.qcloudimg.com/raw/777a5b567c06615954e6f3b7fcbcd399.svg">


### Command description

#### Publishing function version

Directly publish the version of the `my-function` function without deployment:
```plaintext
sls  publish-ver --inputs  function=my-function
```

#### Creating alias

Create the `routing-alias` alias for the `my-function` function, with the routing rule of 50% traffic for version 1 and 50% traffic for version 2:
```plaintext
sls  create-alias --inputs name=routing-alias  function=my-function  version=1  
config='{"weights":{"2":0.5}}'
```

#### Updating alias

Update the flow rule of the `routing-alias` alias of the `my-function` function to 10% for version 1 and 90% for version 2:
```plaintext
sls update-alias --inputs name=routing-alias  function=my-function  version=1 config='{"weights":{"2":0.9}}'
```

#### Listing alias

 List the `routing-alias` alias of the `my-function` function:
```plaintext
sls list-alias --inputs function=my-function
```

#### Deleting alias

Delete the `routing-alias` alias of the `my-function` function:
```plaintext
sls delete-alias --inputs name=routing-alias  function=my-function
```

### Directions

You can publish a tested feature through grayscale release in the following steps:

1. Configure the production environment information into the .env file (`STAGE=prod` indicates the production environment):
```plaintext
TENCENT_SECRET_ID=xxxxxxxxxx
TENCENT_SECRET_KEY=xxxxxxxx
STAGE=prod 
```

2. Create the `alias-prod` alias and configure its traffic rule (suppose the current stable production version is N):
```plaintext
sls create-alias --inputs function=my-function name=alias-prod version=n config='{"weights":{"$LATEST":0}}'
```

3. Configure the alias reference corresponding to the trigger in the `serverless.yml` of the `my-function` function:
```
  events: # Trigger
    - timer: # Timer trigger
        name: # Trigger name, which is `timer-${name}-${stage}` by default
        parameters:
          qualifier: alias-prod # Configure the alias as `alias-prod`
          cronExpression: '*/5 * * * *' # Trigger once every 5 seconds
          enable: true
          argument: argument # Additional parameter
```

4. Deploy the function to the `$latest` production environment and publish the new version (suppose the function name is `my-function` and the new version after release is N+1):
```plaintext
sls deploy 
sls publish-ver --inputs function=my-function
```

5. Configure the traffic rule of the function alias to switch 10% traffic to the N+1 version (suppose the original production version is N and the function alias is `alias-prod`):
```plaintext
sls update-alias --inputs function=my-function name=alais-prod version=n config='{"weights":{"n+1":0.1}}'
```

6. Continue to observe the monitor and switch 100% traffic to version N+1 after it becomes stable:
```plaintext
sls update-alias --inputs function=my-function name=alais-prod version=n config='{"weights":{"n+1":1}}'
```




