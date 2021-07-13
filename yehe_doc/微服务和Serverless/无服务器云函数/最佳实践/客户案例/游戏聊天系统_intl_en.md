## Customer Overview
Social networking is a basic need of game players, which should be implemented in a mature and stable game chat system. This document shows the successful use of Tencent Cloud SCF by RiverGame and describes how to upgrade the chat system in a game with SCF.

RiverGame used its proprietary chat system in its two games: "Top War: Battle Game" and "Farm Town". However, as the number of online players increased, the system stability and costs were facing more challenges, which called for an upgrade in its technology stack so as to reduce the labor and resource costs while ensuring high performance. In this regard, it chose SCF as its solution for the following reasons:
 - SCF is serverless, which enables the customer to focus on the business logic code while eliminating the need of OPS.
 - SCF is pay-as-you-go, which avoids resource waste during off-peak hours and reduces costs. It is applicable to small and medium-sized businesses with low complexity such as game chat system API.

Accordingly, it is only needed to focus on how to migrate the existing system seamlessly, i.e., how to use SCF to meet all the specific needs.






## Customer Requirements

### Requirement 1. Only few code modifications

With Swoole used as the bottom-layer extension, some legacy APIs were deployed in CVM and used CLB to receive external requests, Composer to manage packages at the code layer, and the open-source framework EasySwoole as the HTTP business framework.


With the SCF scheme in place, API Gateway and SCF would be used to provide services at the non-code layer, while Composer would still be used to manage packages at the code layer. The legacy Swoole-based HTTP framework could no longer be used, and the framework was the focus of code modification as shown below:
![](https://main.qcloudimg.com/raw/c66b626f7fdb4ba2c97d8197f31b85d4.png)

The following is the modification principle:
1. Determine the logic entry so as to ensure that only one SCF function is used to process all requests.
An entry is actually a route, and a simple route format needs to be defined to get the required information from the function entry code. Then, the information will be transferred to the legacy class for processing, and specific content will be returned. The following is a simple format example of a `url`:
```
https://url/controller/action?query
```
The `controller` and `action` can be obtained simply by parsing the `path` provided by the SCF function. After the fields are determined, the method of the corresponding class will be called to return relevant content. Based on such an entry, the legacy logic processing classes can be called.
2. Process the parent class of the legacy logic processing classes. After the framework is disused, a parent class for basic features, such as getting `querystring` content, parsing`body`, or returning values in a unified format, needs to be implemented.
PHP is used as an example in the following figure, and the principles for different programming languages are similar. The code requires further modification, such as adding database configuration information (which can be passed through environment variables in the SCF function) and async operations for legacy time-consuming tasks.
```php
date_default_timezone_set('Asia/Shanghai');
require_once__DIR__ . "/vendor/autoload.php";
function run($event, $context)
{
		$path = $event->path;
		// Parse `path`
		list($controller, $action) = parsePath($path);
		$controllerClassName = "\\App\\HttpController\\" . ucwords($controller);
		if(!class_exists($controllerClassName)){
			return return404();
		}
		$controllerClass = new $controllerClassName($event, $context);
		// Do not call classes that should not be called externally in the `HttpController` directory
		if(!controllerClassName instanceof \App\BaseController){
			return return404();
		}
		if(!method_exists($controllerClass, $action)){
			return return404();
		}
		try{
			return $controllerClass->$action();
		}catch(Throwable $e){
			return return500();
		}
}
```


### Requirement 2. Quick release
The quick release capability is indispensable. During the migration, various tests were conducted repeatedly. As the local testing feature of SCF did not support PHP during the migration back then, the release process when API Gateway and SCF were used together was as follows:
1. Develop the code
2. Deploy the `$LATEST` version of the function
3. Generate a new version number based on the `$LATEST` version
4. Switch the version in the corresponding path in API Gateway
5. Publish the test version through API Gateway
6. Switch to the version to be used in the production environment through API Gateway

The release process was relatively complicated. When the migration started, API call as described in step 3 was not supported yet; therefore, automated deployment could not be implemented, which is currently supported though. The scheme where API Gateway was used to directly point to the `$LATEST` version of the function and then the function was deployed can still be used, but it is quite simple and only applicable to testing instead of release in the production environment.
We combined the two methods, i.e., using the release process of stable version for stable features and creating an API path pointing to the `$LATEST` version for new features. In this way, new versions could be released at any time without affecting the features in the production environment.


#### Problem and solution
When API Gateway was published, the resources might exceed the limit, which was found to be caused by the limit on the number of concurrent SCF instances. When a new API version was published, access to a new instance would be requested while the legacy instance had not been released yet. If the total numbers of new and legacy instances exceeded the limit, it would be needed to apply to Tencent Cloud for quota increase.



### Requirement 3. Private network interconnection
The migration was at the system level, but some contents in the legacy system still needed to be used in the future. Therefore, SCF needed to interconnect with the legacy CVM instances over the private network. As SCF supports deployment in the existing private network, it is easy to implement private network interconnection.


#### Problem and solution
As the API service needed to send requests to the public network, but private network SCF could not directly access the public network during the system migration, NAT Gateway was used to enable SCF to access the public network. For more information, please see [Configuring NAT Gateway in VPC](https://intl.cloud.tencent.com/document/product/583/19704).
>!When NAT Gateway is used, it is recommended to assign a separate subnet to SCF, as the egress IP will change if NAT Gateway is bound to an existing subnet. If the server IP of the subnet is in some whitelists, it will result in certain impact.



### Requirement 4. Log query
Originally, logs were directly stored in the disk and compressed and dumped periodically. After the system was migrated to SCF, the SCF log mechanism needed to be used. SCF can directly deliver logs to CLS, and any output information can be directly delivered as logs. It is required to plan the log contents as needed.

The original information, URL paths, client IPs, parameters after parsing, and business logs of the function entry can be output for quick problem locating and query. In addition, there is no need to output the returned values separately, as SCF can print them automatically.
>!After log delivery is enabled, logs can be viewed only after index is enabled. If log content includes index separators, the corresponding keywords need to be deleted from the separators when the index is configured; otherwise, the content will be split.
> 
During the system migration, the SCF log feature had certain shortcomings, such as separate SCF and API Gateway logs. As the original HTTP entry was API Gateway, which might cause some problems hard to be traced. Currently, the `RequestId` fields in SCF and API Gateway have been aligned, which makes it easier to query the logs of the same request through the same ID.



### Requirement 5. Time-consuming task processing
The legacy scheme used `task` of Swoole to process time-consuming tasks. As the PHP environment of SCF supports Swoole, the modification scheme in the following figure was used as an initial attempt:
```php
$p = "1";
$process = new \swoole_process(function (\swoole_process $worker) use ($p){
	echo $p;
	sleep(3);
	echo $p;
});
$pid = $process->start();
```
However, the process implemented through this scheme could not be completely controllable. As discovered from testing, the printed logs belonged to other requests, and the process time and lifecycle could not be determined. Therefore, a more assured "message queue" scheme was used.

CKafka, Tencent Cloud's proprietary message queue service, was used. After a message body with a general structure is encapsulated and sent to CKafka, it will trigger another SCF function (which runs time-consuming task code). If a general structure is used, the CKafka topic can be ignored. If there is any task requiring async operations, it only needs to be written into the SCF function to be triggered by CKafka, and the name and parameters of the function will be sent to CKafka as shown below:
![](https://main.qcloudimg.com/raw/9d436ab286f6f4e48328215d57ddda2c.png)

#### Problem and solution
Only one partition is created for one CKafka topic by default. If the consumption speed is not satisfactory, it can be increased by adding new partitions. After a new partition is added, the trigger needs to be deleted and added again in the SCF function.


### Requirement 6. Configuration file update

Configuration files in the system were large and required frequent updates, such as the list of banned words used in the chat service.

In the legacy scheme, a configuration file had its own Git library, and Jenkins was started after the planner submitted the file, which then uploaded the file to CVM and reloaded it.
After the system was migrated to SCF, configuration files could not be uploaded separately but could only be placed in the code. The scheme was updated as follows: the planner submits a file to Git, Jenkins gets it from Git and uploads it to COS, and SCF pulls it from COS as shown below:
![](https://main.qcloudimg.com/raw/0f095816f3fbd187a62d2f2d683bb241.png)

#### Problem and solution
There was a performance problem where it took some time for an SCF function to pull data from COS; therefore, files could not be pulled every time when a request was initiated. This meant that the content in each pull needed to be retained in the memory; however, the SCF memory could not be managed uniformly, and real-time change could not be guaranteed.
A compromise scheme is adopted where the pull time of file content retained in the memory is compared with last pull time. If the gap between them exceeds 5 minutes, the content will be pulled again to ensure relative real-timeliness and satisfactory performance and meet the current needs as shown below:
```java
private static $fileContent = null;
private static $lastTime = 0;

public static function refresh(){
	self::$fileContent = self::readFromCos("words.txt");
}

public static function getFileContent(){
	if(time() - self::$lastTime > 300 || empty(self::$fileContent)){
		self::refresh();
		self::$lastTime = time();
	}
	return self::$fileContent;
}
```



## Benefits to Customer
At this point, all requirements in the system migration had been satisfied, and the migration was carried out smoothly. After migration to SCF, the customer enjoys the following advantages:
-  The API server does not need to be maintained, and CPU and memory issues can be ignored. Even when the number of requests increases, the customer does not need to consider whether to increase CVM instances.
- The monitoring metrics are specific, which can clearly reflect the overall running efficiency through metrics such as access trends and whether there are slow requests or errors.
- Decoupling is completely achieved after CKafka is used for message division, which also ensures that no messages will be lost. The method of triggering SCF functions by CKafka is applicable to ever-cumulative slow tasks.
- After the version management feature is improved, the versions can be switched at any time, and there is no need to pull code branches for release again.

Tencent Cloud SCF has brought various advantages and benefits to RiverGame, which also plans to use the following features in the future:

-  Stateless HTTP services, such as customer service message receipt and payment callback APIs.
- Async tasks with no returned values needed, such as player ranking reporting in WeChat Mini Game.
- Scheduled tasks, such as periodically pushing relevant event information to players.


