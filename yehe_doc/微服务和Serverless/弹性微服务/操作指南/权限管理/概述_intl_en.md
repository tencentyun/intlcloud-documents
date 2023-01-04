**TEM** currently allows the **root account** to configure and grant TEM operation and resource permissions to sub-accounts flexibly in the console.

## Overview
A TEM permission policy specifies the **operation scope** and **resource scope**. A complete permission policy can define all operations that can be performed by the policy holder on the specified resources.

|  Resource Type 	|  Resource Scope                	|  Operation Scope  	|
|-----------	|--------------------------	|----------------------|
|  Environment     	|  Specified/All environments       	|  <li>View environment details: This option includes read operations and deployment operations (deploying applications and associate gateways to the environment) of the environment. <li>Manage environment: This option includes the read, deployment, and write operations of the environment.	|
|  Application     	|  Specified/All applications       	|  <li>View application details: This option includes the read operations of the application. <li>**Manage application**: This option includes the read and write operations of the application.                                                         	|
|  CLB gateway  	|  Specified/All CLB gateways 	|  <li>View CLB gateway details: This option includes the read operations of the CLB gateway.<li>Manage CLB gateway: This option includes the read and write operations of the CLB gateway.                                             	|
