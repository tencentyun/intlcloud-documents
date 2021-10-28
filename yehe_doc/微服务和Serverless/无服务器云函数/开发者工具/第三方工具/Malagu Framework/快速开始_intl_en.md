You can use the `@malagu/scf-adapter` component to deploy applications in SCF. Based on the principle of convention over configuration, the component can be used out of the box with zero configuration required.



## Cloud Resource


The adapter component has a default deployment rule, which can be overwritten. When running a deployment task, it will use the SDK provided by the platform to create the required cloud resource according to the deployment rule. If it finds that the cloud resource already exists, it will update the resource differentially. **It always creates or updates cloud resources in the most secure way possible**; for example, if a custom domain name is configured, it will attempt to create or update the custom domain name resource.


The adapter component deploys an application into a function, which means that one application corresponds to one function. If the application is large, it should be split into small microapplications or microservices. Just like the principle of granularity breakdown in the microservice architecture, reasonable granularity breakdown enables better application management. The framework will guarantee the execution performance of one application in one function.


## Environment Isolation


Malagu provides the `stage` configuration attribute to represent the environment. In the deployment rule agreed by the `@malagu/scf-adapter` component, the `mode` attribute is used to map the `stage` attribute. Three environments are provided by default: testing, prerelease, and production. The expression rule is as follows:
```yaml
stage: "${'test' in mode ? 'test' : 'pre' in mode ? 'pre' : 'prod' in mode ? 'prod' : cliContext.prod ? 'prod' : 'test'}" # test, pre, prod
```
The `stage` value rule is as follows:
- **test**: test environment, i.e., when the `mode` attribute contains the `test` mode, or `mode` does not contain `test`, `pre`, and `prod` and the command line parameter `-p,--prod` is not specified.
- **pre**: prerelease environment, i.e., when the `mode` attribute contains the `pre` mode.
- **prod**: production environment, i.e., when the `mode` attribute contains the `prod` mode, or the command line parameter `-p,--prod` is specified.



You can choose different deployment environments by specifying `mode`:
```sh
# Deploy to the test environment
malagu deploy -m test # Or use `malagu deploy`

# Deploy to the prerelease environment. You can also skip deploying to the prerelease environment and deploy directly to the production environment
malagu deploy -m pre

# Deploy to the production environment
malagu deploy -m prod
```


## Isolation Level


**The isolation level of environments can be controlled**. You can use accounts to isolate environments by using different configuration files for different environments and configuring different accounts for different configuration files. Similarly, you can also use regions and service aliases to isolate environments. The framework isolates environments by service alias by default. The isolation methods can be used together.


Association of the `stage` attribute value with the service alias (the following is the default rule and does not need to be configured):
```yaml
malagu:
  faas-adapter:
    alias:
      name: ${stage}
```
Association with the API Gateway environment (the following is the default rule and does not need to be configured):
```yaml
malagu:
  faas-adapter:
    apiGateway:
      release:
        environmentName: "${stage == 'pre' ? 'prepub' : stage == 'prod' ? 'release' : stage}"
```



## Deployment Mode


The adapter component defines the deployment mode through the `mode` attribute. Supported deployment modes include:

- **http**: deployment mode based on API Gateway + HTTP-triggered function. During the deployment process, cloud resources such as API gateways, namespaces, and functions are created or updated.
- **timer**: deployment mode based on timer trigger + event-triggered function. During the deployment process, cloud resources such as timer triggers, namespaces, and functions are created or updated.
- **api-gateway**: deployment mode based on API Gateway + event-triggered function. During the deployment process, cloud resources such as API gateways, namespaces, and functions are created or updated.

```yaml
mode:
	- http
```


## Custom Deployment Rule


You can overwrite the default deployment rule with a custom rule of the same name.


#### Default rule

The default rule is defined in the `malagu-remote.yml` configuration file of the `@malagu/scf-adapter` component.


#### Custom deployment type
```yaml
mode:
	- htpp # Valid values: http, timer, api-gateway. Default value: http
```
#### Custom namespace
```yaml
malagu:
	faas-adapter:
  	namespace:
    	name: xxxx # The default value is `default`
```
>?Other namespace attributes can be configured in a similar way.

#### Custom function name
```yaml
malagu:
	faas-adapter:
    function:
      name: xxxx # The default value is `${pkg.name}`
```
>?Other function attributes can be configured in a similar way.


## Attribute Configuration


```yaml
malagu:
	faas-adapter:
    type:
    namespace:
      description:
    function:
    	name: ''
      namespace:
      handler:
      publish:
      l5Enable:
      type:
      codeSource:
      description:
      memorySize:
      timeout:
      runtime:
      role:
      clsLogsetId:
      ClsTopicId:
      env:
      vpcConfig:
        vpcId:
        subnetId:
      layers:
        name:
        version:
      deadLetterConfig:
        type:
        name:
        filterType:
      publicNetConfig:
        PublicNetStatus:
          eipConfig:
            eipStatus:
    alias:
    	name:
      functionName:
      namespace:
      description:
      routingConfig:
      	additionalVersionWeights:
        	version:
          weight:
        addtionVersionMatchs:
        	version:
          key:
          method:
          expression:
    apiGateway:
    	usagePlan:
      	name:
        environment:
        desc:
        maxRequestNum:
        maxRequestNumPreSec:
      strategy:
      	name:
        environmentName:
        strategy:
      api:
        name:
        serviceTimeout:
        protocol:
        desc:
        authType:
        enableCORS:
        businessType:
        serviceScfFunctionName:
        serviceWebsocketTransportFunctionName:
        serviceScfFunctionNamespace:
        serviceScfFunctionQualifier:
        serviceWebsocketTransportFunctionNamespace:
        serviceWebsocketTransportFunctionQualifier:
        isDebugAfterCharge:
        serviceScfIsIntegratedResponse:
        isDeleteResponseErrorCodes:
        responseSuccessExample:
        responseFailExample:
        authRelationApiId:
        userType:
        oauthConfig:
          publicKey:
          tokenLocation:
          loginRedirectUrl:
        responseErrorCodes:
          code:
          msg:
          desc:
          convertedCode:
          needConvert:
        requestConfig:
          ApiRequestConfig:
          path:
          method:
        requestParameters:
          name:
          desc:
          position:
          type:
          defaultValue:
          required:
        RequestParameter:
      service:
      	exclusiveSetName:
      	name:
        protocol:
        description:
        netTypes:
        ipVersion:
        setServerName:
        appIdType:
      release:
      	environmentName:
        desc:
    customDomain:
    	name: 
      isDefaultMapping:
      certificateId:
      protocol:
      netType:
      pathMappingSet:
      	path:
        Environment:
```
